# Grupos de dados — dono da confirmação

F1-T005 / SPEC-1-002 / CA-1-006. Fonte: `03_documentos/escopo.md` seção 9 (escopo integral aprovado em 24/09 e revalidado na ata de 06/10/2026).

Os 12 grupos abaixo são os da seção 9, na mesma ordem e com o mesmo responsável de confirmação indicado pelo escopo. O escopo já define **quem confirma** cada grupo; o que ainda falta é a confirmação nominal e a validação do conteúdo por essa pessoa ou área, que pertence à F1-T006.

| # | Grupo | Informações principais | Quem confirma | Confirmação nominal |
|---|---|---|---|---|
| 1 | Instituição e unidade | Identidade, locais, equipes, configurações, catálogos e sistemas conectados | Administração/TI | a confirmar |
| 2 | Pessoa usuária | Identidade, papéis, vínculo, situação do acesso e fator adicional de autenticação | Administração da instituição | a confirmar |
| 3 | Paciente | Identificadores, contato, representante, preferência de comunicação e vínculo | Recepção/navegação, com conferência de identidade | a confirmar |
| 4 | Jornada | Encaminhamento, fase, próximo passo, prazo, compromisso, falta, barreira, contato e desfecho | Navegação e equipe responsável | a confirmar |
| 5 | Atendimento | Data, profissional, motivo, registros, estado e documentos produzidos | Profissional autor | a confirmar |
| 6 | Histórico clínico | Diagnóstico, estadiamento, alergias, comorbidades, medicamentos e dados de performance | Profissional habilitado | a confirmar |
| 7 | Exames e arquivos | Pedido, laudo, valores, unidades, datas, original e interpretação | Profissional responsável pelo dado | a confirmar |
| 8 | Tratamento | Protocolo, versão, doses, ciclos, administrações, toxicidades e resposta | Médico, farmácia e enfermagem em suas etapas | a confirmar |
| 9 | Documentos | Tipo, modelo, dados de origem, versões, aprovações, assinatura, destinatário e estado | Autor/revisor autorizado | a confirmar |
| 10 | Integração | Origem, destino, identificador externo, pedido, resposta, protocolo e falha | Sistema com conciliação humana quando necessária | a confirmar |
| 11 | IA | Pergunta, contexto selecionado, fontes, modelo, resposta, versão e decisão humana | Profissional usuário e governança clínica | a confirmar |
| 12 | Auditoria e indicadores | Eventos, acessos, tempos, correções, responsáveis e métricas | Sistema registra; gestão revisa definições | a confirmar |

## Regras de qualidade que acompanham o dicionário

Transcritas da seção 9 e válidas para qualquer desenho de banco nas próximas tasks:

- Cada campo importante tem definição única; a mesma informação não recebe dois nomes.
- Data clínica e data de registro são campos distintos e nunca se confundem.
- Unidade de medida é explícita em todo valor laboratorial ou de dose.
- A mesma pessoa pode ter múltiplos episódios e múltiplos vínculos institucionais.
- Dado histórico não é sobrescrito só porque um valor novo chegou.
- O identificador de origem acompanha importações e exportações.
- Campo livre é aceito para contexto clínico, mas não substitui campo estruturado exigido para cálculo, prescrição, autorização ou indicador.

## Limite deste documento

Listar o responsável definido no escopo **não** é obter a confirmação dele. Nenhuma pessoa foi nomeada por suposição e nenhuma informação foi validada com a área. A confirmação nominal e o aceite dos cinco grupos de áreas são da F1-T006, com Leonardo, áreas assistenciais, TI, regulação e gestão.
