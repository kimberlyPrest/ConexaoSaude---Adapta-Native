# SPEC-1-005 — Pacientes: identidade, cadastro, duplicidade e fusão

**Fase:** 1
**Status:** planejada
**Dono:** Consultor Adapta (implementação) + Recepção/navegação (operação)
**Origem no escopo:** Onda 1; F02; CA global 3; seção 9 (grupo Paciente); seção 4 (passo 1)
**Degrau da solução:** construção mínima — tabelas e regras de identidade próprias no Supabase; conceitos de tela reaproveitados do projeto Skip após revisão.

> **Substitui** a SPEC-1-003 antiga (cadastro clínico essencial, 15/09): o cadastro administrativo/identidade entra na Fase 1 (Onda 1); o prontuário clínico (F03) vai para a Fase 2.

## Resultado observável

Cadastro de paciente com identificação, contatos, responsáveis, preferências de comunicação, vínculo institucional, convênio/SUS e documentos — campos clínicos sensíveis separados dos administrativos. Dois registros candidatos a representar a mesma pessoa são encaminhados para conferência; nenhuma fusão elimina histórico ou mistura dados por semelhança de nome.

## Limites e dependências

- **Inclui:** tabela de pacientes, alerta de duplicidade, fluxo de conferência, fusão com preservação de histórico, RLS herdado da SPEC-1-004.
- **Fora de escopo:** dados clínicos (F03, Fase 2), integração com sistema hospitalar (Fase 5), migração de pacientes reais (bloqueada — seção 11, etapa 6).
- **Entradas e pré-condições:** SPEC-1-004 concluída (Auth + RLS); mapa aprovado com fonte oficial de paciente (decisão 2 da seção 17).
- **Saídas/artefatos:** migrações versionadas + fluxo de duplicidade/fusão testado.
- **Dependências e responsáveis:** recepção/navegação confirma campos e regra de conferência; consultor implementa.
- **Risco e plano B:** sem definição da fonte oficial, cadastro funciona com pendência nomeada e alerta de identidade manual.
- **Rollback ou reversão:** migrações reversíveis; fusão registra histórico reversível por trilha.

## Fluxo e regras

1. Modelar paciente com campos administrativos separados dos clínicos sensíveis.
2. Implementar detecção de possível duplicidade na criação (encaminhar para conferência, não bloquear atendimento).
3. Implementar conferência responsável com registro de decisão e autor.
4. Implementar fusão que preserva a história de fusão/correção — nunca sobrescrever histórico.
5. Testar: duplicidade detectada, conferência, fusão correta, tentativa de fusão por semelhança de nome rejeitada.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | cadastro novo sem duplicidade | paciente criado com vínculo institucional | registro de criação |
| Limite | dois registros com nome parecido | alerta de conferência, sem fusão automática | fila de conferência |
| Falha | fusão solicitada sem autorização do perfil | negada pelo RLS e registrada | auditoria |

## Checklist de execução

- [ ] Campos administrativos e clínicos separados no modelo.
- [ ] Detecção de duplicidade ativa na criação.
- [ ] Fluxo de conferência com registro de decisão.
- [ ] Fusão preserva histórico (prova).
- [ ] RLS herdado testado no novo conjunto de tabelas.

## Critérios de aceite

- [ ] **CA-1-017:** dois registros candidatos à mesma pessoa são encaminhados para conferência responsável (CA global 3).
- [ ] **CA-1-018:** nenhuma fusão elimina histórico ou mistura dados por semelhança de nome; história de fusão fica registrada.
- [ ] **CA-1-019:** campos clínicos sensíveis ficam separados dos administrativos e herdam o RLS da fundação.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem alerta de duplicidade | cadastrar paciente com dados idênticos a um existente | segundo cadastro criado sem alerta (falha) | log do teste |
| GREEN | alerta ativo | repetir o cadastro | conferência proposta, sem criação automática | log do teste |
| REFACTOR/REGRESSÃO | fusão destrutiva | tentar fusão que apaga histórico | negada; histórico preservado | log do teste |

**Dados/fixtures:** pacientes fictícios com nomes parecidos, documento divergente, representante autorizado.
**Caminhos de erro obrigatórios:** documento ausente, contato inválido, fusão sem permissão, duplicidade não detectada.
**Evidência exigida:** logs de teste + captura do fluxo de conferência e fusão.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T012 | Modelar e implementar cadastro de pacientes com separação admin/clínico | Consultor Adapta | SPEC-1-005 | CA-1-019 | GREEN cadastro | Migrações + RLS testado | T1.11 concluída | ☐ |
| F1-T013 | Implementar duplicidade, conferência e fusão com histórico | Consultor Adapta | SPEC-1-005 | CA-1-017, CA-1-018 | RED/GREEN duplicidade | Logs dos 3 cenários | T1.12 concluída | ☐ |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
