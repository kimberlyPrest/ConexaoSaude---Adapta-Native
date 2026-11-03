# Método de medição — proposta para aprovação

F1-T003 / SPEC-1-001 / CA-1-004. **NÃO APROVADO.** Elaborado em 03/11/2026; não comprova coleta ou aceite da gestão.

## Proposta recomendada
- Unidade: mesmo serviço/equipe do piloto, a confirmar por Leonardo e gestão. A SPEC cita Dom Pedro de Alcântara / UNACON; isso não é confirmação institucional.
- Período: uma semana operacional completa antes da automação; datas de início/fim a definir pela gestão. Repetir janela comparável depois, com mesma duração, perfil de consultas, equipe e carga horária.
- Amostra: todas as consultas oncológicas concluídas nos turnos selecionados dessa semana; registrar total e perdas. Se inviável, gestão define amostra viável antes da coleta; não selecionar retrospectivamente apenas casos rápidos. Não há tamanho de amostra já aprovado.
- Tempo administrativo: observar minutos ativos de preparação, correção, emissão e liberação de documentos por atendimento; separar tempo médico dos demais profissionais. Não contar intervalo/espera como tempo ativo. Fonte proposta: registro manual de observação por coletor designado; fonte ainda não confirmada.
- Pacientes por oncologista/turno: atendimentos concluídos divididos por turnos equivalentes; definir duração de referência do turno antes de calcular. Fonte proposta: agenda/registro oficial de atendimentos confirmado pela TI/gestão. Não contar agendamento, cancelamento ou falta como atendimento concluído.
- Fila média: somar dias corridos entre entrada elegível na fila e primeiro atendimento oncológico, dividir pelos pacientes que tiveram primeiro atendimento na janela. Fonte proposta: registros oficiais de entrada e atendimento; TI/gestão devem identificá-los. Não misturar retorno com primeira consulta.
- Cancelamentos, faltas, transferências e registros sem datas: não entram no denominador de atendimentos concluídos; registrar contagem e motivo separadamente. A gestão precisa validar a regra de elegibilidade e o tratamento de reagendamentos antes da medição da fila.
- Controles: documentar mudança de carga horária, composição da equipe, perfil dos pacientes e fatores externos; não atribuir melhoria ao sistema sem comparabilidade.

## Dados disponíveis e lacunas
- Tempo administrativo: a medir; não foi fornecido histórico.
- Capacidade por turno: a medir; não foi fornecido histórico.
- Fila: aproximadamente 100 dias, somente referência verbal citada no escopo (seções 1 e 13), permitida por CA-1-003. Sem numerador/denominador/período confirmados; não é média calculada ou medição atual.
- Sem fonte confirmada, período, duração equivalente de turno ou coletor: não calcular. Manter lacuna explícita em indicadores.csv.
- Fonte conflitante: gestão/TI resolvem qual registro é oficial; conservar divergência, não escolher automaticamente.
- Denominador zero: não calculável; nunca zero por substituição.

## Privacidade
Somente totais agregados no repositório. Registros individuais permanecem em ambiente institucional autorizado. Não enviar prontuários ou identificadores no chat/GitHub.

## Aceite a recolher
Leonardo/gestão devem revisar período, amostra, exclusões e fontes; confirmar ou corrigir a proposta e indicar unidade/equipe, datas, coletor e fontes oficiais. Aprovação do desenho não transforma dados pendentes em dados medidos.

- Decisão do cliente: pendente.
- Confirmação institucional/gestão: pendente.
- Evidência, data e referência do aceite: pendentes.
- CA-1-004: não satisfeito enquanto não houver aprovação humana registrada e detalhes operacionais suficientes.
