# Changelog

## 2026-10-30
- [CONSULTORIA] · 2026-10-30 · **Teste do cliente por SPEC, não por task.** As sete SPECs da Fase 1 receberam a seção `## Teste humano do cliente`: a SPEC-1-007 com o roteiro de 5 passos da demonstração por perfil, que é o aceite da fase (CA-1-023 a CA-1-025), e as SPECs 1-001 a 1-006 declaradas internas, com a prova automática que substitui o teste e onde o cliente vê o resultado (painel e demonstração da 1-007). `AGENTS.md` e `CLAUDE.md` passam a dizer que as tasks são construídas em sequência, sem pedir autorização nem teste entre elas; `fase.md` e `STATUS.md` registram o teste da fase. Nenhuma task foi criada, fundida ou apagada; nenhum critério, escopo, aceite ou status mudou. Continuam paradas as decisões da seção 17 (F1-T003/F1-T006), o acesso ao Skip e à instância do cliente e o aceite final da fase.

- 2026-10-06: replanejamento da Fase 1 sobre o escopo integral (24/09) aprovado: 7 SPECs, 25 critérios de aceite, 16 tasks em 9 levas. Handoff da Fase 1 publicado.

- 30/10/2026 · [CONSULTORIA] · Correção de auditoria do commit dadeeee: as seções novas tratavam aprovação do método, aceites por área e assinatura da TI como fechamento automático. Corrigida somente a orientação de teste/fechamento nas SPEC-1-001/002/006, AGENTS, fase e STATUS. Mantidos os critérios originais, TDD, regras, responsáveis, pré-condições, status e histórico; a demonstração final da SPEC-1-007 continua obrigatória. Nenhuma decisão humana foi tomada pelo agente, nenhum teste foi executado nem task fechada por esta correção documental.

## 2026-11-03 — Execução autorizada pelo cliente
- [Tesla] F1-T001 concluída: estrutura dos três indicadores em 06_notas/baseline/indicadores.csv; 12 campos, RED de ausência e GREEN de completude executados.
- [Tesla] F1-T002 concluída: indicadores a medir com pendências explícitas e fonte; fila ≈100 dias apenas como referência verbal do escopo. Sem inventar medição, datas ou aceite.
- [Tesla] F1-T007 concluída no recorte CA-1-010: data, URLs e módulos registrados em 06_notas/inventario-skip/referencia.md. Atual 15b9ef0, produção 659822f, campo dev e918fe5; nenhuma alteração, QA ou publicação no Skip. Registro não é backup restaurável.
- [Tesla] F1-T004 em espera: rascunho de 16 passos em 06_notas/jornada/mapa.md; faltam fontes oficiais e contexto real por etapa, não declarado como mapa aprovado.
- [Tesla] F1-T003 em andamento: método proposto em 06_notas/baseline/metodo-medicao.md; aguardando Leonardo/gestão para aprovação e parâmetros operacionais. CA-1-004 e SPEC-1-001 não concluídos. Pedido de implementação não é aprovação do método.
- [Tesla] Associação operacional registrada em 07-sistemas/plataforma-oncologica/plataforma.md, sem espelho ou mudança do executável.

- Envio pendente: tentativas pelo conector GitHub retornaram 404 ao criar tree e arquivo. Diagnóstico: conta leonardofq-alt sem permissão de escrita (403 ao consultar colaboradores). Corrigido depois por convite; commits d5a30cb e 0a1c8b9 em main.
- Pedido do cliente em 03/11: “implementar no Skip a primeira tarefa”. F1-T001 é artefato documental; painel no app está fora do escopo da SPEC-1-001 (painéis são F20/Fase 5). Nada foi alterado no Skip; decisão registrada abaixo.

## 2026-11-03 — Decisão do cliente sobre a F1-T001 no Skip
- DECISÃO DO CLIENTE (Leonardo, 03/11/2026 16:48 BRT): **opção A — manter a F1-T001 como documento e seguir a fase.** A estrutura do baseline permanece em 06_notas/baseline (indicadores.csv + README), fora do aplicativo. Não será criada tela de baseline no Skip nesta fase; painéis seguem fora do escopo da Fase 1 conforme a SPEC-1-001 (F20/Fase 5).
- DECISÃO DO CLIENTE (Leonardo, 03/11/2026 16:48 BRT): convidar a conta `leonardofq-alt` com permissão de escrita no repositório kimberlyPrest/ConexaoSaude---Adapta-Native. Envio ao GitHub permanece pendente até a permissão existir; conferência será feita pelo próprio conector.
- Efeito: nenhuma mudança de escopo, SPEC ou critério de aceite. F1-T001/T002/T007 seguem concluídas por prova documental; F1-T003 e F1-T004 seguem em espera por aprovação/confirmação humana.

- Envio ao GitHub concluído após o convite da conta leonardofq-alt: commits d5a30cb e 0a1c8b9 em main. Pendência de escrita resolvida; leitura e gravação conferidas pelo conector.

## 2026-11-03 — F1-T008 concluída
- [Tesla] F1-T008 concluída (CA-1-011, CA-1-012): inventário em 06_notas/inventario-skip/inventario.md. 18 áreas classificadas com dono, objetivo e situação; cinco erros comprovados com arquivo e trecho.
- Descoberta: o inventário da seção 2 do escopo refere-se ao projeto 50880 Oncologista Clínico Virtual (PocketBase, 0.0.42/0645000, não publicado), e não ao 64011. Os dois foram separados no registro; nenhum foi alterado.
- CID genérico não comprovado em cidMapping.ts; mantido como "a confirmar". Nenhum dado de paciente foi lido, copiado ou migrado.
- Correção de regressão própria (03/11): ao reescrever 04_fase-atual/fase.md para atualizar status, o critério da F1-T013 perdeu o CA-1-017. Comparação com o arquivo original (99bcde9) mostrou a perda; o valor foi restaurado para "CA-1-017, 018". Nenhum outro campo, task ou critério foi alterado.

## 2026-11-03 — F1-T003 concluída: método de medição aprovado
- **DECISÃO DO CLIENTE (Leonardo, 03/11/2026 17:17 BRT):** “Aprovo o método como proposto.” Aprovação do desenho de medição exigida pelo CA-1-004 e pela decisão “Linha de base e método de medição” da seção 17 do escopo.
- [Tesla] F1-T003 concluída (CA-1-004): registro em 06_notas/baseline/metodo-medicao.md, com a aprovação datada e a evidência da resposta. **SPEC-1-001 fechada** — F1-T001, F1-T002 e F1-T003 concluídas.
- A aprovação cobre o desenho: uma semana operacional comparável, amostra de todas as consultas concluídas nos turnos, exclusão de cancelamentos/faltas/transferências/sem data e fontes registradas. Não foi inferida de pedido anterior, silêncio ou “ok” solto.
- Pendências de execução mantidas como lacuna explícita, não estimadas: unidade/equipe do piloto, datas de início e fim, duração de referência do turno, coletor do tempo administrativo e fontes oficiais de atendimento e fila. A decisão 2 da seção 17 continua com TI e donos de processo.
- Correção de registro (03/11, 17:25 BRT): o commit 3b6ceb1 salvou a aprovação no método, na análise e no estado, mas não incluiu este changelog, o quadro da fase e o STATUS. Os três foram atualizados em seguida; nada de conteúdo do cliente mudou.
