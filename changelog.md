# Changelog

## 2026-10-30
- [CONSULTORIA] · 2026-10-30 · **Teste do cliente por SPEC, não por task.** As sete SPECs da Fase 1 receberam a seção `## Teste humano do cliente`: a SPEC-1-007 com o roteiro de 5 passos da demonstração por perfil, que é o aceite da fase (CA-1-023 a CA-1-025), e as SPECs 1-001 a 1-006 declaradas internas, com a prova automática que substitui o teste e onde o cliente vê o resultado (painel e demonstração da 1-007). `AGENTS.md` e `CLAUDE.md` passam a dizer que as tasks são construídas em sequência, sem pedir autorização nem teste entre elas; `fase.md` e `STATUS.md` registram o teste da fase. Nenhuma task foi criada, fundida ou apagada; nenhum critério, escopo, aceite ou status mudou. Continuam paradas as decisões da seção 17 (F1-T003/F1-T006), o acesso ao Skip e à instância do cliente e o aceite final da fase.

- 2026-10-06: replanejamento da Fase 1 sobre o escopo integral (24/09) aprovado: 7 SPECs, 25 critérios de aceite, 16 tasks em 9 levas. Handoff da Fase 1 publicado.

- 30/10/2026 · [CONSULTORIA] · Correção de auditoria do commit dadeeee: as seções novas tratavam aprovação do método, aceites por área e assinatura da TI como fechamento automático. Corrigida somente a orientação de teste/fechamento nas SPEC-1-001/002/006, AGENTS, fase e STATUS. Mantidos os critérios originais, TDD, regras, responsáveis, pré-condições, status e histórico; a demonstração final da SPEC-1-007 continua obrigatória. Nenhuma decisão humana foi tomada pelo agente, nenhum teste foi executado nem task fechada por esta correção documental.
