# SPEC-1-001 — Baseline de métricas do piloto e método de medição

**Fase:** 1
**Status:** planejada (reancorada no escopo integral de 24/09)
**Dono:** Consultor Adapta + Gestão operacional do cliente
**Origem no escopo:** Onda 0; seção 1 (metas do piloto); seção 17 (decisão "Linha de base e método de medição"); seção 13 (indicadores)
**Degrau da solução:** construção mínima — registrar baseline comparável antes de automatizar qualquer documento.

> **Histórico:** SPEC reancorada do plano de 15/09. CAs 1-001..003 preservados; CA-1-004 novo (método de medição da seção 17). Tasks F1-T001/F1-T002 do quadro continuam válidas com os mesmos IDs.

## Resultado observável

Uma fonte de baseline preenchível com os 3 indicadores do piloto (tempo administrativo por consulta, pacientes por oncologista/turno, fila média), cada um com numerador, denominador, fonte, período e status (histórico / medido no piloto / a medir) — e um método de medição aprovado pela gestão, exigido pela decisão institucional da seção 17.

## Limites e dependências

- **Inclui:** modelo de coleta, campos obrigatórios, regra de cálculo, método de medição, evidência mínima.
- **Fora de escopo:** painéis (F20, Fase 5), análise estatística avançada, integração automática com sistema hospitalar.
- **Entradas e pré-condições:** escopo integral publicado; acesso aos dados operacionais do piloto.
- **Saídas/artefatos:** baseline da Fase 1 + método de medição registrado.
- **Dependências e responsáveis:** gestão operacional fornece dados; consultor valida consistência; Leonardo/gestão aprovam o método (seção 17).
- **Risco e plano B:** sem dados históricos, medir amostra inicial antes da automação e marcar "a medir".
- **Rollback ou reversão:** manter versões anteriores da planilha de baseline.

## Fluxo e regras

1. Definir período do baseline e unidade de comparação.
2. Registrar tempo administrativo por consulta, pacientes por oncologista/turno e fila média.
3. Marcar cada indicador como histórico, medido no piloto ou pendente.
4. Registrar método de medição: amostra, período, exclusões e fonte dos três indicadores (seção 17).
5. Validar que cada meta tem numerador, denominador e fonte.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | dados de uma semana disponíveis | baseline calculado por indicador | registrar fonte e período |
| Limite | só existe fila aproximada de 100 dias | fila entra como referência inicial citada | confirmar na Fase 5 |
| Falha | tempo administrativo ausente | indicador fica pendente, nunca estimado | medir amostra antes da Fase 2 |

## Checklist de execução

- [ ] Período e responsável definidos.
- [ ] Três indicadores globais possuem campo próprio.
- [ ] Fonte e status de cada indicador registrados.
- [ ] Método de medição registrado e aprovado pela gestão.
- [ ] Pendências não foram preenchidas por suposição.

## Critérios de aceite

- [ ] **CA-1-001:** baseline contém tempo administrativo por consulta ou pendência explícita de medição inicial.
- [ ] **CA-1-002:** baseline contém pacientes por oncologista/turno ou pendência explícita de medição inicial.
- [ ] **CA-1-003:** baseline contém fila média do piloto, aceitando 100 dias como referência inicial citada até confirmação.
- [ ] **CA-1-004:** método de medição (amostra, período, exclusões, fonte) registrado e aprovado por Leonardo/gestão — decisão da seção 17.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem baseline | tentar validar critérios globais | validação falha por falta de fonte | nota de pendência |
| GREEN | baseline mínimo preenchido | revisar os três indicadores | todos possuem valor ou pendência explícita | baseline salvo |
| REFACTOR/REGRESSÃO | método de medição ausente | remover o método da seção 17 | aceite volta a falhar (CA-1-004) | checklist atualizado |

**Dados/fixtures:** turno piloto, oncologista, amostra de consultas, fila inicial citada.
**Caminhos de erro obrigatórios:** dado ausente, período indefinido, fonte conflitante.
**Evidência exigida:** baseline preenchido ou pendências marcadas + método aprovado.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T001 | Criar estrutura do baseline | Consultor Adapta | SPEC-1-001 | CA-1-001 a CA-1-003 | RED/GREEN baseline | Artefato de baseline com campos | Escopo aprovado | ☐ |
| F1-T002 | Preencher ou marcar pendências dos indicadores | Gestão operacional | SPEC-1-001 | CA-1-001 a CA-1-003 | GREEN baseline | Indicadores com fonte/status | Estrutura criada | ☐ |
| F1-T003 | Registrar método de medição e obter aprovação | Consultor Adapta + Leonardo | SPEC-1-001 | CA-1-004 | REGRESSÃO método | Método registrado com aceite | T1.2 concluída | ☐ |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| 06/10/2026 | Replanejamento escopo integral | CA-1-004 + F1-T003 | Decisão da seção 17 exige método de medição aprovado |
