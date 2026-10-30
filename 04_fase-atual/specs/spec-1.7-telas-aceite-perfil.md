# SPEC-1-007 — Telas essenciais e demonstração de aceite por perfil

**Fase:** 1
**Status:** planejada
**Dono:** Consultor Adapta (implementação) + Leonardo e equipe (aceite)
**Origem no escopo:** Onda 1 (aceite: "cada perfil executa sua tarefa; acesso indevido entre instituições é negado; recuperação é ensaiada"); seção 10 (telas próprias sobre base Supabase); seção 11 (etapa 7 — comparar fluxos)
**Degrau da solução:** reuso — componentes de interface e conceitos de fluxo do projeto Skip reaproveitados após avaliação (seção 2), reconstruídos sobre a base Supabase.

## Resultado observável

Telas essenciais da fundação operando sobre o Supabase: login com MFA, seleção de instituição/unidade, cadastro de usuários e vínculos, cadastro de paciente com alerta de duplicidade, e visão mínima por perfil. Demonstração de aceite em que **cada perfil executa sua tarefa**, acesso cruzado é negado e a recuperação ensaiada é apresentada — comparada com o projeto congelado do Skip (etapa 7 da seção 11).

## Limites e dependências

- **Inclui:** telas de login/MFA, administração de usuários, cadastro de paciente, navegação mínima por perfil, sessão de demonstração com aceite.
- **Fora de escopo:** prontuário, consulta, documentos, agenda, IA, Meu Oncologista (fases 2–4).
- **Entradas e pré-condições:** SPEC-1-004/005/006 concluídas; inventário do Skip disponível (SPEC-1-003).
- **Saídas/artefatos:** build publicada em ambiente de homologação + registro de aceite por perfil.
- **Dependências e responsáveis:** Leonardo e equipe participam da demonstração; consultor conduz.
- **Risco e plano B:** perfil sem representante na demonstração → aceite registrado por escrito com vídeo.
- **Rollback ou reversão:** versões do frontend versionadas; demonstração repetível.

## Fluxo e regras

1. Construir telas essenciais reusando componentes avaliados do projeto Skip.
2. Preparar roteiro de demonstração: um caso por perfil (recepção, navegação, médico, farmácia, regulação, gestão, TI).
3. Executar a demonstração: cada perfil executa sua tarefa; tentativa de acesso cruzado é negada ao vivo; recuperação ensaiada é apresentada.
4. Comparar com o projeto congelado do Skip e documentar melhorias/diferenças (etapa 7, seção 11).
5. Registrar aceite por perfil.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | perfil executa sua tarefa na demonstração | aceite registrado | ata da demonstração |
| Limite | acesso cruzado tentado ao vivo | negação no servidor exibida | log de auditoria |
| Falha | tela falha na demonstração | item registrado como pendência; aceite parcial documentado | nova demonstração agendada |

## Checklist de execução

- [ ] Telas essenciais publicadas em homologação.
- [ ] Roteiro de demonstração por perfil preparado.
- [ ] Demonstração executada com negação de acesso cruzado ao vivo.
- [ ] Comparação com o projeto Skip documentada.
- [ ] Aceite por perfil registrado.

## Critérios de aceite

- [ ] **CA-1-023:** cada perfil executa sua tarefa na demonstração, com aceite registrado.
- [ ] **CA-1-024:** acesso indevido entre instituições é negado ao vivo durante a demonstração (prova pública do CA-1-016).
- [ ] **CA-1-025:** recuperação ensaiada apresentada; aceite da fundação registrado por Leonardo e TI.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem telas | executar roteiro de demonstração | passos falham por ausência de tela | roteiro marcado |
| GREEN | telas publicadas | executar roteiro completo | todos os perfis executam suas tarefas | ata + vídeo |
| REFACTOR/REGRESSÃO | regressão de RLS na UI | repetir tentativa de acesso cruzado após ajustes de tela | negação mantida no servidor | log de auditoria |

**Dados/fixtures:** usuários fictícios dos 11 perfis, 2 instituições, pacientes fictícios, anexos de teste.
**Caminhos de erro obrigatórios:** MFA pendente, perfil sem vínculo, instituição errada, anexo sem permissão.
**Evidência exigida:** ata de demonstração + vídeo + registro de aceite por perfil.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T016 | Construir telas essenciais e executar demonstração de aceite | Consultor Adapta + Leonardo | SPEC-1-007 | CA-1-023 a CA-1-025 | GREEN demonstração | Ata + vídeo + aceites | T1.13 e T1.15 concluídas | ☐ |

## Teste humano do cliente

- **Ritmo:** construir as tasks vinculadas em sequência, sem pedir autorização nem teste a cada task.
- **Quando:** quando F1-T012 a F1-T016 estiverem no ar. É o teste desta SPEC e o aceite da Fase 1 (F1-T016, CA-1-023 a CA-1-025).
- **Quem testa:** Leonardo, as áreas assistenciais, a TI, a regulação e a gestão.
- **Passos:** 1) entrar com o segundo fator e escolher instituição e unidade; 2) cada perfil executar a própria tarefa: recepção cadastra paciente com alerta de duplicidade, navegação abre a jornada, médico e farmácia veem a tarefa do perfil, regulação e gestão consultam o que lhes cabe; 3) tentar, com um perfil de outra instituição, abrir a mesma ficha pelo link direto e conferir a negativa registrada; 4) cadastrar o mesmo paciente duas vezes e conferir o encaminhamento para conferência, sem fusão automática; 5) abrir o relatório do ensaio de restauração e comparar a tela nova com o projeto congelado do Skip.
- **Resultado esperado:** cada perfil executa a sua tarefa; o acesso cruzado entre instituições é negado ao vivo; a recuperação ensaiada é apresentada; o aceite da fundação é registrado (CA-1-023 a CA-1-025).
- **Evidência do aceite:** mensagem do Leonardo confirmando a demonstração e o aceite da fundação, registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| 30/10/2026 | Teste por SPEC | SPEC-1-007 / F1-T016 | Seção `## Teste humano do cliente`: teste único da SPEC, que é o aceite da Fase 1 (CA-1-023 a CA-1-025). |
