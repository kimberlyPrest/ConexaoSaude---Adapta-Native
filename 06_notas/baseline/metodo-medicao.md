# Método de medição — aprovado

F1-T003 / SPEC-1-001 / CA-1-004. **APROVADO por Leonardo em 03/11/2026, 17:17 BRT** — resposta “Aprovo o método como proposto”, registrada em `changelog.md` e na análise da task. A aprovação cobre o desenho: período, amostra, exclusões e fontes. Os parâmetros operacionais de execução continuam listados abaixo como pendentes; aprovar o método não transforma lacuna em dado medido.

## Desenho aprovado
- Unidade: serviço/equipe do piloto — a indicar pela gestão antes da coleta. A SPEC cita Dom Pedro de Alcântara / UNACON; isso não é confirmação institucional.
- Período: uma semana operacional completa antes da automação; datas de início/fim a definir pela gestão. Repetir janela comparável depois, com mesma duração, perfil de consultas, equipe e carga horária.
- Amostra: todas as consultas oncológicas concluídas nos turnos selecionados dessa semana; registrar total e perdas. Se inviável, gestão define amostra viável antes da coleta; não selecionar retrospectivamente apenas casos rápidos.
- Tempo administrativo: observar minutos ativos de preparação, correção, emissão e liberação de documentos por atendimento; separar tempo médico dos demais profissionais. Não contar intervalo/espera como tempo ativo. Registro manual por coletor designado.
- Pacientes por oncologista/turno: atendimentos concluídos divididos por turnos equivalentes; duração de referência do turno definida antes de calcular. Não contar agendamento, cancelamento ou falta como atendimento concluído.
- Fila média: somar dias corridos entre entrada elegível na fila e primeiro atendimento oncológico, dividir pelos pacientes que tiveram primeiro atendimento na janela. Não misturar retorno com primeira consulta.
- Cancelamentos, faltas, transferências e registros sem datas: não entram no denominador de atendimentos concluídos; registrar contagem e motivo separadamente. Elegibilidade e reagendamentos precisam de regra da gestão antes da medição da fila.
- Controles: documentar mudança de carga horária, composição da equipe, perfil dos pacientes e fatores externos; não atribuir melhoria ao sistema sem comparabilidade.

## Dados disponíveis e lacunas
- Tempo administrativo: a medir; não foi fornecido histórico.
- Capacidade por turno: a medir; não foi fornecido histórico.
- Fila: aproximadamente 100 dias, somente referência verbal citada no escopo (seções 1 e 13), permitida por CA-1-003. Não é média calculada ou medição atual.
- Fonte conflitante: gestão/TI resolvem qual registro é oficial; conservar divergência, não escolher automaticamente.
- Denominador zero: não calculável; nunca zero por substituição.

## Privacidade
Somente totais agregados no repositório. Registros individuais permanecem em ambiente institucional autorizado. Não enviar prontuários ou identificadores no chat/GitHub.

## Aceite registrado
- **DECISÃO DO CLIENTE (Leonardo, 03/11/2026 17:17 BRT):** “Aprovo o método como proposto.” Aprovação do desenho de medição prevista na seção 17 do escopo e exigida pelo CA-1-004.
- **Evidência:** resposta ao formulário de aprovação desta conversa, transcrita na íntegra; referência no `changelog.md` e em `.adapta-cliente/analises/F1-T003.md`.
- **CA-1-004:** satisfeito — método com amostra, período, exclusões e fontes registrado e aprovado por Leonardo.
- Versão aprovada: este documento na data acima. Alteração posterior de período, amostra, exclusões ou fonte exige nova aprovação e novo registro.

## Pendências para executar a medição (não bloqueiam o método)
Estes itens faltam para rodar a coleta. Permanecem como “a medir” na planilha; não são estimados nem substituídos por padrão.
- Unidade e equipe exatas do piloto.
- Datas de início e fim da semana operacional.
- Duração de referência do turno.
- Nome ou função do coletor do tempo administrativo.
- Identificação das fontes oficiais de atendimento e de entrada na fila. A decisão 2 da seção 17 (fonte oficial de paciente, agenda, exames, prescrição, APAC e faturamento) continua com TI e donos dos processos.
