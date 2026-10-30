# Instruções do projeto — Conexão Saúde e Vida

Execute somente a fase atual e siga a fase, as SPECs e as tasks publicadas. Não altere critérios de aceite sem aprovação da consultora Kimberly Prestes.

## Ritmo e teste do cliente
Vale desde 30/10/2026 e substitui o ritmo antigo, em que cada task pedia autorização e teste.

- Construa as tasks em sequência, uma por vez, sem pedir autorização nem teste entre elas. Cada task fecha pelas provas automáticas da SPEC (RED, GREEN, REGRESSÃO) e pelas evidências que ela já exige.
- O teste do cliente é por SPEC e segue `## Teste humano do cliente` de cada uma. Além da demonstração/aceite da fase na SPEC-1-007, permanecem a aprovação do método pela gestão na SPEC-1-001, os aceites por área na SPEC-1-002 e a decisão de política e assinatura do relatório pela TI na SPEC-1-006. Não são substituídos por prova automática nem adiados para o fim. As SPEC-1-003/004/005 fecham por suas provas técnicas, respeitando decisões e acessos que sejam pré-condições.
- Continuam paradas: pergunta que muda implementação, acesso que só o cliente tem, divergência que a SPEC manda revisar com o cliente e aprovação expressamente exigida nos critérios. Também continuam as aprovações críticas para mudança de dados, permissões ou fluxo em uso e primeira escrita externa não comprovável pelo agente da qual as próximas tasks dependam. Preservar segurança, autorização de integrações e dados reais, e aceite final da fase.
