# Fase 1 — Fundação e definições (Ondas 0 e 1 do escopo integral)

**Data:** 06/10/2026 · **Substitui:** fase_1.md de 15/09 (recorte antigo)
**Fonte:** `03-Projeto/03-Escopo-Definitivo-Sistema-Completo-Supabase.md` (24/09)
**Resolve:** GATE-REPLANEJAMENTO-ESCOPO-INTEGRAL

## Resultado de fechamento da fase (aceite do escopo)

Mapa de fluxos e campos aprovado por Leonardo, áreas assistenciais, TI, regulação e gestão; cada perfil executa sua tarefa; acesso indevido entre instituições é negado no servidor; recuperação é ensaiada.

## Fora desta fase

- Prontuário clínico, consulta, exames, protocolos, ciclos, toxicidades (F03–F09) — Fase 2, Ondas 2–3.
- APAC/regulação, kit documental, filas, agenda/busca ativa, comunicação (F12–F17) — Fases 2–3.
- IA clínica, tumor board, minutas (F10/F11) — Fase 4, Onda 5. **Nenhuma chamada de IA nesta fase.**
- Meu Oncologista e app do paciente (F18) — Fase 4, Onda 6.
- Integrações reais (F22) — Fase 5, Onda 7; nesta fase apenas se IDENTIFICA o contrato.
- Migração de pacientes reais — bloqueada até base exportável + autorização + plano de conciliação (seção 11, etapa 6).

## Tasks

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|
| F1-T001 | Criar estrutura do baseline | Consultor Adapta | SPEC-1-001 | CA-1-001..003 | RED/GREEN baseline | Artefato de baseline com campos | Escopo aprovado | A | ☐ |
| F1-T002 | Preencher ou marcar pendências dos indicadores | Gestão operacional | SPEC-1-001 | CA-1-001..003 | GREEN baseline | Indicadores com fonte/status | T1.1 | A | ☐ |
| F1-T004 | Mapear a jornada de 16 passos no contexto do piloto | Consultor Adapta | SPEC-1-002 | CA-1-005 | GREEN mapa | Mapa com 16 passos preenchidos | Escopo aprovado | A | ☐ |
| F1-T007 | Congelar versão de referência do projeto Skip | TI + Consultor | SPEC-1-003 | CA-1-010 | GREEN inventário | Registro da versão congelada | Acesso ao projeto | A | ☐ |
| F1-T003 | Registrar método de medição e obter aprovação | Consultor + Leonardo | SPEC-1-001 | CA-1-004 | REGRESSÃO método | Método registrado com aceite | T1.2 | B | ☐ |
| F1-T005 | Consolidar grupos de dados e inventário de integrações | Consultor + TI | SPEC-1-002 | CA-1-006, 007 | GREEN mapa | Grupos com dono + integrações | T1.4 | B | ☐ |
| F1-T008 | Inventariar e classificar todas as áreas do Skip | Consultor Adapta | SPEC-1-003 | CA-1-011, 012 | GREEN inventário | Inventário classificado | T1.7 | B | ☐ |
| F1-T006 | Registrar decisões 1 e 2 da seção 17 e coletar aceites | Leonardo + TI + Consultor | SPEC-1-002 | CA-1-008, 009 | REGRESSÃO aceite | Aceites das 5 áreas | T1.4, T1.5 | C | ☐ |
| F1-T009 | Criar projeto Supabase e migrações de instituição/unidade/vínculo | Consultor Adapta | SPEC-1-004 | CA-1-016 | GREEN fundação | Migrações aplicadas em dev | T1.6 | D | ☐ |
| F1-T010 | Implementar Auth, convites, bloqueio e MFA | Consultor Adapta | SPEC-1-004 | CA-1-014 | GREEN MFA | Fluxo de MFA demonstrado | T1.9 | E | ☐ |
| F1-T011 | Implementar RLS por papel/instituição + auditoria de negações | Consultor Adapta | SPEC-1-004 | CA-1-013, 015, 016 | RED/GREEN RLS | Logs com prova negativa | T1.9, T1.10 | F | ☐ |
| F1-T012 | Modelar e implementar cadastro de pacientes | Consultor Adapta | SPEC-1-005 | CA-1-019 | GREEN cadastro | Migrações + RLS testado | T1.11 | G | ☐ |
| F1-T014 | Implementar auditoria append-only e políticas de Storage | Consultor Adapta | SPEC-1-006 | CA-1-020, 021 | RED/GREEN auditoria | Logs + políticas testadas | T1.11 | G | ☐ |
| F1-T013 | Implementar duplicidade, conferência e fusão | Consultor Adapta | SPEC-1-005 | CA-1-017, 018 | RED/GREEN duplicidade | Logs dos 3 cenários | T1.12 | H | ☐ |
| F1-T015 | Registrar decisão de região/retenção/backup e ensaiar restauração | TI + Consultor | SPEC-1-006 | CA-1-022 | REGRESSÃO restauração | Relatório do ensaio | T1.14 | H | ☐ |
| F1-T016 | Construir telas essenciais e executar demonstração de aceite | Consultor + Leonardo | SPEC-1-007 | CA-1-023..025 | GREEN demonstração | Ata + vídeo + aceites | T1.13, T1.15 | I | ☐ |

## Notas de execução

- **Tasks do quadro antigo:** F1-T001 e F1-T002 mantêm os mesmos IDs (trabalho em andamento continua válido). As antigas tasks 3–4 (ficha do paciente, teste de atendimento) movem para a Fase 2.
- **Regra de execução:** nenhuma task da Leva D em diante começa sem as decisões 1, 2, 4 e 5 da seção 17 registradas (T1.3/T1.6 concluídas).
- **Ambientes:** desenvolvimento usa dados fictícios; homologação usa dados fictícios/anonimizados; produção só após controles e contratos (seção 10.2).
- **Fases 2–5:** SPECs chegam na onda (D21) — Fase 2 (Ondas 2–3) será detalhada durante a Fase 1 via `liberar-fase`.
