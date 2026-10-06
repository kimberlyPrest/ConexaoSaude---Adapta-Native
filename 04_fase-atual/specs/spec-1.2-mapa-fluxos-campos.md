# SPEC-1-002 — Mapa de fluxos e campos aprovado + contratos de integração identificados

**Fase:** 1
**Status:** planejada
**Dono:** Consultor Adapta + Leonardo (validação clínica) + TI (fontes e integrações)
**Origem no escopo:** Onda 0 (aceite: "mapa de fluxos e campos aprovado por Leonardo, áreas assistenciais, TI, regulação e gestão"); seções 4, 9, 12 e 17
**Degrau da solução:** construção mínima — documento de definição, sem código.

## Resultado observável

Um mapa aprovado da jornada de 16 passos (seção 4) com, para cada passo: responsável, dados usados/produzidos, fonte oficial e estado atual; mais o inventário de integrações (seção 12) com nome/versão do sistema, função real, condição de acesso e dono — sem implementar nenhuma integração.

## Limites e dependências

- **Inclui:** mapa da jornada, dicionário de grupos de dados (seção 9), inventário de integrações, decisões 1 e 2 da seção 17 registradas.
- **Fora de escopo:** implementação de conectores (F22, Fase 5), desenho de tabelas Supabase (SPEC-1-004/005), migração de dados.
- **Entradas e pré-condições:** escopo integral publicado; participação de Leonardo, áreas assistenciais, TI, regulação e gestão.
- **Saídas/artefatos:** mapa de fluxos e campos + inventário de integrações, ambos com aceite registrado.
- **Dependências e responsáveis:** TI confirma nome/versão dos sistemas (TASY/MV, Mednews, Wellon, laboratório, regulação); donos de processo confirmam função.
- **Risco e plano B:** se TI não confirmar um sistema, registrar "a confirmar" com responsável e prazo — o mapa não fica bloqueado.
- **Rollback ou reversão:** versionamento do documento; aceite pode ser revisado por emenda.

## Fluxo e regras

1. Transcrever a jornada de 16 passos (seção 4) para o contexto real do piloto (Dom Pedro de Alcântara / UNACON).
2. Para cada passo: registrar responsável, dados de entrada/saída, fonte oficial e como é feito hoje.
3. Consolidar os 12 grupos de dados (seção 9) com quem confirma cada um.
4. Inventariar integrações da seção 12: sistema, uso pretendido, condição para "concluído", acesso real disponível.
5. Registrar as decisões 1 e 2 da seção 17 (unidade do piloto; fonte oficial de paciente/agenda/exames/prescrição/APAC).
6. Obter aceite de Leonardo, áreas assistenciais, TI, regulação e gestão.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | todas as áreas participam | mapa completo com aceite | registrar aceite por área |
| Limite | agenda oficial em outro sistema | origem e estado da sincronização ficam visíveis no mapa | marcar integração como "a confirmar" |
| Falha | fonte oficial indefinida para um dado | passo fica com pendência nomeada e responsável | decisão da seção 17 escalada |

## Checklist de execução

- [ ] Jornada de 16 passos mapeada no contexto do piloto.
- [ ] 12 grupos de dados com quem confirma cada um.
- [ ] Inventário de integrações preenchido (nome, versão, acesso, dono).
- [ ] Decisões 1 e 2 da seção 17 registradas.
- [ ] Aceite de Leonardo, áreas, TI, regulação e gestão anexado.

## Critérios de aceite

- [ ] **CA-1-005:** mapa da jornada de 16 passos existe com responsável, dados e fonte oficial por passo.
- [ ] **CA-1-006:** cada um dos 12 grupos de dados (seção 9) tem dono de confirmação registrado.
- [ ] **CA-1-007:** inventário de integrações lista cada destino/origem da seção 12 com condição de conclusão e situação de acesso real.
- [ ] **CA-1-008:** decisões 1 e 2 da seção 17 (unidade do piloto; fontes oficiais) registradas com responsável e evidência.
- [ ] **CA-1-009:** aceite do mapa registrado por Leonardo, áreas assistenciais, TI, regulação e gestão.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem mapa | tentar desenhar tabelas da Onda 1 | desenho falha por falta de fonte oficial | nota de bloqueio |
| GREEN | mapa preenchido | revisar 16 passos + 12 grupos + integrações | todos com dono e fonte | mapa salvo |
| REFACTOR/REGRESSÃO | passo sem fonte oficial | remover a fonte de um passo | aceite volta a falhar (CA-1-005) | checklist atualizado |

**Dados/fixtures:** jornada da seção 4, grupos de dados da seção 9, tabela de integrações da seção 12.
**Caminhos de erro obrigatórios:** sistema sem acesso confirmado, dono de dado ausente, aceite faltante de uma área.
**Evidência exigida:** documento do mapa + registro de aceite por área.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T004 | Mapear a jornada de 16 passos no contexto do piloto | Consultor Adapta | SPEC-1-002 | CA-1-005 | GREEN mapa | Mapa com 16 passos preenchidos | Escopo aprovado | ☐ |
| F1-T005 | Consolidar grupos de dados e inventário de integrações | Consultor Adapta + TI | SPEC-1-002 | CA-1-006, CA-1-007 | GREEN mapa | Grupos com dono + integrações com situação | T1.4 em andamento | ☐ |
| F1-T006 | Registrar decisões 1 e 2 da seção 17 e coletar aceites | Leonardo + TI + Consultor | SPEC-1-002 | CA-1-008, CA-1-009 | REGRESSÃO aceite | Aceites das 5 áreas registrados | T1.4 e T1.5 concluídas | ☐ |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
