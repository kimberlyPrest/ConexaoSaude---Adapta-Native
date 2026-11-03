# Baseline — Fase 1

Fonte preenchível: `indicadores.csv` (UTF-8, separador ponto e vírgula). SPEC-1-001.

Campos por indicador: ID, indicador, unidade, numerador, denominador, valor, fonte, período inicial/final, status, responsável pela coleta e pendência.

Indicadores: tempo administrativo por consulta (minutos ativos / consultas observadas), pacientes por oncologista/turno (atendimentos concluídos / turnos equivalentes) e fila média (soma dos dias entre entrada elegível e primeiro atendimento / pacientes observados).

Status: histórico, medido no piloto, a medir. Denominador zero ou ausente: não calculável, nunca zero automático. Período indefinido: datas vazias com pendência explícita. Fontes conflitantes: gestão/TI decidem, sem inferência automática. A referência verbal da fila (≈100 dias) é documental e não é medição validada.

Somente totais agregados; sem pacientes identificados, credenciais ou dados clínicos individuais. Nenhuma alteração no Skip ou no banco. A aprovação humana do método permanece pendente na F1-T003.
