# Escopo definitivo — Sistema completo de oncologia com Supabase

**Cliente:** Conexão Saúde e Vida LTDA, com aplicação inicial no Hospital Dom Pedro de Alcântara / UNACON  
**Produto:** Oncologista Clínico Virtual, prontuário oncológico, navegação do paciente e Meu Oncologista  
**Versão:** 24/09/2026  
**Finalidade:** definir o sistema completo solicitado após a apresentação do projeto já iniciado no Skip pelo Leonardo  
**Leitura:** documento de produto e operação, escrito para pessoas sem formação em programação

> **Relação com o escopo anterior.** O arquivo `02-Escopo-Definitivo.md`, de 15/09/2026, definiu um recorte para otimizar o atendimento do oncologista e já originou SPECs da Fase 1. Este documento registra a visão completa solicitada agora: os três pilares descritos na reunião, as funcionalidades do projeto já iniciado no Skip e as capacidades que ainda terão de ser construídas. O plano de ação existente precisará ser refeito para representar este escopo integral. As metas do documento anterior continuam como metas do piloto, mas não representam, sozinhas, o aceite de toda a plataforma.

## 1. O que será construído

Será criada uma plataforma única para acompanhar o paciente oncológico desde a entrada no serviço, passando por diagnóstico, discussão clínica, autorização, tratamento, monitoramento, retornos, seguimento e desfecho. Ela atenderá a equipe médica e aos demais profissionais envolvidos, com uma área própria para o paciente chamada **Meu Oncologista**.

A plataforma tem quatro partes que compartilham os mesmos dados:

1. **Oncologista Clínico Virtual:** organiza o caso, apresenta informações relevantes, compara exames, consulta protocolos aprovados, prepara minutas e sugere possibilidades para análise do oncologista. A decisão clínica e a aprovação de qualquer conduta continuam com o médico.
2. **Prontuário oncológico:** reúne a história longitudinal, consultas, exames, diagnósticos, estadiamento, medicamentos, alergias, plano terapêutico, ciclos, toxicidades, documentos e desfechos. Uma informação confirmada pode preencher outros documentos sem nova digitação.
3. **Navegação do paciente:** acompanha o próximo passo de cada pessoa, quem é responsável por realizá-lo, prazos, faltas, barreiras, contatos e pendências entre setores.
4. **Meu Oncologista:** acesso do paciente ou representante autorizado à própria agenda, orientações, documentos liberados, lembretes e canal de comunicação institucional.

O **Supabase** será a base principal de identidade, dados e arquivos da nova plataforma. O projeto já iniciado no Skip será inventariado e aproveitado como referência de telas, fluxos, nomenclaturas e regras candidatas. Cada função reaproveitada passará por revisão funcional, clínica e técnica antes de ser declarada pronta.

### Resultado esperado para o negócio

- Menos tempo do oncologista gasto em busca de informações, repetição de dados e preenchimento de documentos.
- Mais capacidade assistencial por turno sem transferir decisões clínicas a pessoas ou sistemas não habilitados.
- Menos pacientes perdidos entre consulta, exame, autorização, tratamento e retorno.
- Documentos mais consistentes, com pendências detectadas antes da liberação.
- Maior visibilidade de filas, atrasos, devoluções, faltas e segurança assistencial.
- Uma base que possa atender mais de uma instituição, mantendo os dados e acessos de cada uma separados.

As metas já aprovadas para o piloto são **reduzir pelo menos 50% do tempo administrativo por consulta**, **aumentar em pelo menos 50% os pacientes atendidos por oncologista por turno** e **reduzir pelo menos 30% o tempo médio da fila**, partindo da referência verbal de cerca de 100 dias para uma meta inicial de até 70 dias. A medição real exige linha de base, período comparável, volume suficiente e registro de fatores externos que influenciam a fila. Essas metas medem impacto; não substituem os critérios de funcionamento e segurança de cada módulo.

## 2. Fontes, certeza e limites da análise do projeto já iniciado no Skip

Este escopo usa o diagnóstico do cliente, os dois PDFs de contexto, o escopo anterior, o mapeamento dos vídeos do atendimento, a transcrição da reunião técnica posterior e o projeto já iniciado no Skip apresentado pelo Leonardo e disponibilizado para análise.

**Como ler as classificações abaixo:**

- **Identificado no projeto já iniciado no Skip:** há tela, serviço, estrutura de dados ou rotina correspondente. Isso não comprova implantação, desempenho, segurança nem uso real.
- **Parcial:** existe uma aproximação, mas falta parte indispensável do fluxo ou comprovação externa.
- **Novo:** não foi encontrada uma implementação equivalente suficiente para o resultado descrito.

O projeto já iniciado no Skip contém uma aplicação React e estruturas de dados e rotinas de **PocketBase**. A reunião registra que o Leonardo ainda não havia feito testes específicos com pacientes reais. O material analisado do projeto já iniciado no Skip não trouxe uma exportação verificável de dados clínicos de produção, contratos de integração hospitalar ou provas de aceite funcional. Por isso, todos os itens clínicos serão revalidados. **Nenhum dado de paciente deverá ser migrado apenas porque há uma tabela ou uma tela com o mesmo nome.**

### Inventário do que vem do projeto já iniciado no Skip

| Área | O que foi identificado no projeto já iniciado no Skip | Situação para o novo sistema |
|---|---|---|
| Entrada e usuários | Login, perfil, convites, papéis, MFA e trilha de auditoria no projeto já iniciado no Skip | **Identificado no projeto já iniciado no Skip.** Reconstruir autenticação, autorizações e auditoria no Supabase; testar acesso real por instituição e função. |
| Pacientes e prontuário | Cadastro de paciente, detalhe, linha do tempo, registros médicos e de enfermagem | **Identificado no projeto já iniciado no Skip.** Revisar campos, origem, versões, assinaturas e limites de edição. |
| Consulta médica | Tela de consulta, anamnese, exame físico e minuta assistida por IA | **Identificado no projeto já iniciado no Skip.** Definir estados de rascunho, revisão e fechamento; impedir preenchimento clínico inventado. |
| Consulta de enfermagem | Registro de enfermagem e preparação de informações | **Identificado no projeto já iniciado no Skip.** Formalizar o que a navegadora pode registrar e o que exige confirmação médica. |
| Chat clínico e tumor board | Telas e rotinas para perguntas e discussão de casos | **Identificado no projeto já iniciado no Skip.** Reconstruir com fontes verificáveis, versão, limites de uso e auditoria. |
| Protocolos, esquemas, bulário e calculadoras | Catálogos e telas de esquemas, medicamentos e cálculos | **Identificado no projeto já iniciado no Skip.** Homologar conteúdo, versões, fórmulas e responsáveis clínicos; não aceitar doses geradas livremente como prescrição. |
| Exames | Registro, anexos, análise assistida e comparação | **Identificado no projeto já iniciado no Skip.** Revalidar extração, unidades, datas e interpretação clínica. |
| Documentos | Tela com receitas, relatórios, APAC, TCLE, guias e outros modelos; geração textual por IA | **Parcial.** Faltam formulários regulatórios homologados, regras de obrigatoriedade, origem de cada campo, liberação segura e comprovação de envio. |
| Agenda | Agendamentos e visão de consultas | **Identificado no projeto já iniciado no Skip.** Definir fonte oficial da agenda, conflito de horários e sincronização com hospital. |
| Navegação | Fases, passos, Kanban, barreiras, contatos, alertas e notificações | **Parcial.** Completar responsáveis, prazos, busca ativa, confirmação de execução e comunicação ao paciente. |
| Ciclos e toxicidades | Administração de ciclos, eventos adversos e escalas clínicas | **Identificado no projeto já iniciado no Skip.** Homologar protocolos, regras de alerta e papéis de enfermagem/farmácia/médico. |
| Cirurgia, radioterapia e paliativos | Abas e registros específicos | **Identificado no projeto já iniciado no Skip.** Integrar esses eventos à jornada e ao prontuário longitudinal. |
| Genética, aspectos psicossociais, resultados relatados pelo paciente e sobrevivência | Abas, formulários e coleções correspondentes | **Identificado no projeto já iniciado no Skip.** Definir consentimento, profissionais responsáveis e uso clínico dos dados. |
| Financeiro | Registros de custos e dados financeiros | **Identificado no projeto já iniciado no Skip.** Separar visão operacional/gerencial do faturamento efetivo; validar dados e permissões. |
| Integrações | Cadastro de configurações e logs; geração de estruturas FHIR e textos para SISREG, SISCAN e RHC | **Parcial.** A geração local de um arquivo ou texto não demonstra transmissão, aceite ou protocolo emitido pelo órgão/sistema de destino. |
| Painéis | Dashboard de indicadores e KPIs | **Parcial.** Ligar indicadores a eventos confiáveis e às linhas de base do piloto. |
| Área do paciente Meu Oncologista | Ideia apresentada na reunião | **Novo.** Criar acesso, identidade, vínculo com representante, comunicação e documentos autorizados. |
| Operação em várias instituições | Visão futura descrita no briefing | **Novo.** Criar separação de dados, configurações, catálogos e equipes por instituição. |

**Decisão sobre reaproveitamento:** identidade visual, componentes de interface, textos úteis, catálogo candidato e conceitos de fluxo podem ser aproveitados após avaliação. A lógica de segurança, regras clínicas, integrações e dados não serão copiados sem revisão. Foram observados exemplos de preenchimento automático de informações ausentes com valores como ECOG 0, função renal “normal”, CID genérico ou texto clínico padrão. O novo sistema deverá exibir **“não informado”** e solicitar confirmação; nunca transformar ausência de dado em achado normal. Também foram vistos registros de integração marcados como “enviado” ou “transmitido” após apenas gerar um documento local. O novo sistema só mostrará esses estados quando receber confirmação verificável do destino.

## 3. Pessoas que usarão o sistema e suas responsabilidades

| Pessoa ou equipe | O que precisa fazer | O que não pode aprovar em nome de outra pessoa |
|---|---|---|
| Oncologista clínico | Rever caso, decidir conduta, prescrever, aprovar documentos, definir próximos passos e encerrar atendimento | Não pode delegar aprovação clínica a um clique executado por outro perfil. |
| Médico residente | Registrar avaliações e preparar propostas conforme regras institucionais | Prescrição ou decisão sujeita a preceptor deve aguardar revisão quando exigida. |
| Enfermeira navegadora | Coletar e qualificar dados, orientar fluxo, acompanhar prazos, contatar pacientes e sinalizar barreiras | Não aprova diagnóstico, dose, prescrição ou documento médico final. |
| Enfermagem assistencial | Registrar avaliação, administração, intercorrência, toxicidade e continuidade do ciclo | Não altera prescrição médica por conta própria. |
| Farmácia clínica/hospitalar | Conferir prescrições, conciliar medicamentos, verificar preparo/dispensação e registrar intervenções | Não transforma intervenção em alteração médica sem decisão do prescritor. |
| Cirurgião e radioterapeuta | Registrar seus planos, procedimentos, datas e resultados quando participarem | Não altera conduta de outra especialidade sem processo assistencial apropriado. |
| Regulação e faturamento | Conferir APAC, autorizações, guias, devoluções e status de envio | Não substitui justificativa clínica ou assinatura médica. |
| Recepção e agendamento | Cadastrar, confirmar horários, anexar documentos recebidos e orientar pendências administrativas | Não vê dados clínicos além do necessário para a tarefa. |
| Gestão assistencial/operacional | Ver capacidade, tempos, pendências, qualidade e desempenho por instituição | Acesso analítico não significa acesso irrestrito ao prontuário individual. |
| TI/administrador institucional | Gerir usuários, integrações, disponibilidade, suporte e segurança | Acesso técnico a conteúdo clínico será excepcional, justificado e auditado. |
| Paciente ou representante autorizado | Consultar informações liberadas, responder formulários, confirmar compromissos e comunicar barreiras | Não altera documento profissional, conduta ou resultado validado. |

Uma pessoa pode ter mais de um papel apenas quando a instituição autorizar. O sistema deve registrar **quem fez a ação, em qual instituição, quando, em qual paciente, a versão anterior, a nova versão e o motivo**, quando se tratar de decisão ou correção relevante.

## 4. Jornada completa do paciente

1. **Entrada e identificação.** A recepção ou integração recebe o encaminhamento, verifica identidade, vínculo institucional, contatos e documentos iniciais. Possíveis duplicidades são sinalizadas antes de criar outro prontuário.
2. **Triagem operacional.** A navegadora confere urgência, pendências, exames existentes, possibilidade de contato e barreiras de acesso. Critérios clínicos de prioridade dependem de protocolo aprovado.
3. **Agenda da primeira avaliação.** O sistema mostra disponibilidade, prazo, confirmação e falta. Se a agenda oficial estiver em outro sistema, a origem e o estado da sincronização ficam visíveis.
4. **Preparação pré-consulta.** Exames e documentos são anexados; dados extraídos automaticamente aparecem como sugestão até validação humana. A navegadora organiza as informações e marca lacunas.
5. **Consulta oncológica.** O médico vê um resumo cronológico, registra história, exame físico, diagnóstico/hipótese, estadiamento, capacidade funcional e plano. Dados antigos e novos são diferenciados.
6. **Apoio clínico.** O médico pode solicitar comparação de exames, leitura de protocolos e alternativas de conduta. Cada sugestão explicita fonte, data, dados usados e incertezas. Nada vira prescrição sem ação do médico.
7. **Discussão multidisciplinar.** Quando necessária, a equipe registra pergunta, participantes, materiais vistos, opções discutidas, conclusão e profissional responsável pela execução.
8. **Plano terapêutico.** O médico escolhe finalidade, protocolo, via, ciclos, avaliações de resposta e critérios de suspensão. Farmácia clínica e enfermagem recebem apenas itens liberados para suas etapas.
9. **Documentos.** A plataforma prepara APAC, laudo, receita, relatório, solicitação, TCLE e orientações aplicáveis. Pendências aparecem por documento. O médico revisa, ajusta e libera o que for de sua responsabilidade.
10. **Autorização e handoffs.** Cada item enviado a regulação, farmácia, enfermagem ou recepção ganha destinatário, prazo, estado e confirmação de recebimento. Devoluções retornam à pessoa certa com motivo e ação necessária.
11. **Tratamento.** O sistema acompanha ciclo previsto, preparo, administração, adiamento, dose aprovada, toxicidade, intercorrências e cuidados de suporte. A execução é registrada pelo profissional responsável.
12. **Navegação contínua.** Exames, retorno, cirurgia, radioterapia, aconselhamento genético, paliativos e demais passos aparecem numa linha do tempo com datas e responsáveis. Faltas geram tarefa de busca ativa segundo política institucional.
13. **Participação do paciente.** O Meu Oncologista apresenta somente conteúdo liberado, compromissos, orientações, questionários e um canal para comunicar dúvidas ou barreiras. Respostas urgentes seguem fluxo de triagem e não dependem de uma IA responder sozinha.
14. **Reavaliação e seguimento.** O médico registra resposta, mudança de tratamento, remissão, progressão, sobrevivência, transferência ou cuidado paliativo, com plano de acompanhamento e próximos marcos.
15. **Desfecho e continuidade.** Alta, transferência ou óbito recebem registro e documentos pertinentes. Pendências abertas têm destino e responsável antes do encerramento operacional.
16. **Gestão e melhoria.** Indicadores agregados mostram atrasos, causas, retrabalho, capacidade, segurança e resultados, respeitando o acesso de cada perfil.

## 5. Regras que valem para todo o produto

1. Uma **minuta** é um rascunho; **revisado**, **aprovado**, **assinado**, **enviado**, **recebido** e **executado** são estados diferentes. O sistema nunca apresenta um como sinônimo de outro.
2. O prontuário conserva versões e histórico de correções. Corrigir um registro não apaga quem registrou o conteúdo anterior.
3. Informação ausente, vencida, contraditória ou sem origem confiável aparece como pendência. O sistema não presume normalidade nem inventa diagnóstico, exame físico, alergia, dose, data ou autorização.
4. Uma sugestão de IA é visível como sugestão. Ela não edita dado confirmado, não libera documento, não envia ordem e não altera agenda sem o fluxo humano autorizado.
5. A fonte de cada campo reutilizado fica visível: quem registrou, data, documento/atendimento de origem, confirmação e validade clínica quando aplicável.
6. Alergias, interações, função renal/hepática, resultados laboratoriais, peso, altura, superfície corporal, dose acumulada e contraindicações devem ser conferidos segundo regras aprovadas para o medicamento e o contexto. Alerta crítico impede liberação até avaliação e tratamento formal da exceção.
7. Cálculo de dose mostra dados de entrada, fórmula/versão, valor calculado, ajuste e valor final aprovado. Redução ou suspensão exige motivo e responsável.
8. Paciente, equipe, documentos e integrações pertencem a uma instituição definida. Compartilhamento entre instituições requer base operacional/jurídica, autorização e registro próprios.
9. Nenhuma “integração configurada” é considerada “integração funcionando” sem teste de ida, confirmação do destino, tratamento de falha e reconciliação.
10. O sistema deve continuar oferecendo uma rota de trabalho assistida quando um serviço externo estiver indisponível, identificando o que ficou pendente de transmissão ou reconciliação.

## 6. Funcionalidades detalhadas — fundação e prontuário

### F01 — Instituições, unidades, usuários e acesso

**Origem:** perfis, convites e MFA presentes no projeto já iniciado no Skip; separação institucional e autorização completa são novas.  
**Entregas:** cadastro de instituições e unidades, equipes, especialidades, vínculos profissionais, convites, perfis, substitutos temporários, bloqueio/desativação de usuário, segundo fator de acesso e revisão periódica de permissões. A mesma pessoa pode trabalhar em duas unidades sem misturar pacientes. Um suporte técnico pode diagnosticar falha usando dados mínimos; acesso excepcional a conteúdo clínico exige motivo e auditoria.  
**Pronto quando:** recepção, navegação, médico, farmácia, regulação, gestão, TI e paciente veem apenas suas tarefas e dados autorizados; uma tentativa de acesso indevido é negada no servidor e registrada.

### F02 — Identidade e cadastro do paciente

**Origem:** cadastro e tela de pacientes presentes no projeto já iniciado no Skip; prevenção de duplicidade e governança de identidade são novas.  
**Entregas:** identificação, contatos, responsáveis, preferências de comunicação, vínculo institucional, convênio/SUS, documentos, alertas de identidade e histórico de fusão de cadastros. Campos clínicos sensíveis ficam separados dos administrativos.  
**Pronto quando:** dois registros candidatos a representar a mesma pessoa são encaminhados para conferência; nenhuma fusão elimina histórico ou mistura dados por semelhança de nome.

### F03 — Prontuário oncológico longitudinal

**Origem:** prontuário, linha do tempo e coleções clínicas presentes no projeto já iniciado no Skip; consistência longitudinal e versões são novas.  
**Entregas:** problema/diagnóstico, histologia, topografia, morfologia, CID, TNM/estadiamento, biomarcadores, performance, comorbidades, alergias, medicamentos, histórico familiar, procedimentos, terapias, exames, toxicidades, resposta, status da doença e plano de seguimento. Cada dado tem data de referência e autor.  
**Pronto quando:** o profissional consegue reconstruir a trajetória do paciente, identificar o dado mais recente e saber de onde veio cada informação usada em documento ou decisão.

### F04 — Consulta médica e de enfermagem

**Origem:** módulos presentes no projeto já iniciado no Skip.  
**Entregas:** anamnese, exame físico, avaliação de desempenho, avaliação de sintomas, hipótese/diagnóstico, conduta, plano e orientações. A enfermagem prepara e registra suas próprias avaliações; a validação médica fica explícita. Rascunhos podem ser retomados, sem aparecer como atendimento concluído.  
**Pronto quando:** cada profissional conclui somente a sua parte, pendências obrigatórias são mostradas antes da liberação e o atendimento encerrado conserva a versão final.

### F05 — Exames, imagens e documentos de origem

**Origem:** exames, anexos, análise e comparação presentes no projeto já iniciado no Skip; conferência de dados extraídos e reconciliação são novas.  
**Entregas:** pedido, agendamento, realização, resultado, arquivo original, interpretação, comparação temporal e indicação de resultado crítico. A leitura de arquivo por IA produz campos sugeridos com referência visual ao original. Unidade, intervalo de referência, data e laboratório não podem ser descartados.  
**Pronto quando:** o usuário distingue exame solicitado, exame realizado e laudo validado; uma extração errada pode ser corrigida sem adulterar o documento original.

### F06 — Medicações, alergias, reconciliação e bulário

**Origem:** medicações, bulário e reconciliação presentes no projeto já iniciado no Skip; bloqueios clínicos homologados são novos.  
**Entregas:** lista de uso atual, histórico, alergias com tipo de reação, itens de catálogo, protocolos de instituição e intervenções de farmácia clínica. Itens descontinuados permanecem no histórico. Catálogos externos ou locais exigem revisão de versão e responsável.  
**Pronto quando:** prescrições utilizam itens estruturados, conflitos relevantes são sinalizados antes de liberar e uma exceção exige justificativa e aprovação adequada.

### F07 — Protocolos, esquemas, calculadoras e ciclos

**Origem:** protocolos, esquemas, calculadoras e administração de ciclos presentes no projeto já iniciado no Skip; homologação, controle de versão e vínculo operacional completo são novos.  
**Entregas:** indicação, linha e finalidade terapêutica, drogas, via, calendário, pré-medicação, parâmetros de dose, critérios de redução/suspensão, exames prévios, consentimento, ciclos previstos e realizados. Cada alteração de protocolo registra motivo e profissional.  
**Pronto quando:** é possível mostrar a versão do protocolo vigente no momento da decisão e comparar dose calculada, dose prescrita, dose preparada e dose administrada.

### F08 — Segurança do tratamento e toxicidades

**Origem:** toxicidades, checklist, administração e ferramentas paliativas presentes no projeto já iniciado no Skip; regras e escalonamento homologados são novos.  
**Entregas:** checagens antes do ciclo, alergias, resultados necessários, toxicidade, intercorrência, adiamento, suspensão, alerta e encaminhamento. Escalas e recomendações clínicas só entram em produção com aprovação institucional.  
**Pronto quando:** um item crítico pendente não desaparece ao mudar de tela; o profissional autorizado registra decisão, ação e motivo.

### F09 — Outras linhas da jornada oncológica

**Origem:** abas de cirurgia, radioterapia, genética, cuidados paliativos, aspectos psicossociais, resultados informados pelo paciente e sobrevivência presentes no projeto já iniciado no Skip.  
**Entregas:** planejamento, execução e resultado de cirurgia/radioterapia; aconselhamento genético e documentos associados; sintomas e qualidade de vida relatados pelo paciente; apoio psicossocial; cuidados paliativos; plano de sobrevivência e seguimento. Esses registros se conectam ao mesmo paciente, sem tentar converter toda especialidade em uma única consulta médica.  
**Pronto quando:** o oncologista e a navegadora veem os marcos pertinentes, com data, fonte, responsável e próximo passo; dados restritos aparecem apenas para perfis autorizados.

## 7. Funcionalidades detalhadas — decisão, documentos e operação

### F10 — Oncologista Clínico Virtual e chat sobre o caso

**Origem:** chat e agente clínico presentes no projeto já iniciado no Skip; governança de evidências, segurança e avaliação são novas.  
**Entregas:** pergunta sobre paciente ou tema, resumo do caso com fatos confirmados, lacunas de informação, opções de investigação/tratamento, justificativas e referências verificáveis. O profissional escolhe se deseja incorporar uma informação ao prontuário. Uma resposta deve distinguir fatos do paciente, conteúdo de protocolo institucional, literatura consultada e inferência da IA. A versão da fonte, a data e o modelo usado ficam registradas.  
**Pronto quando:** respostas sem fonte, com informação insuficiente ou com conflito de dados são identificadas como tal; o médico consegue rejeitar ou corrigir a sugestão e isso não altera a conduta por si só.

### F11 — Apoio à discussão multidisciplinar

**Origem:** tumor board presente no projeto já iniciado no Skip.  
**Entregas:** indicação da reunião, pergunta clínica, resumo preparado, exames necessários, participantes, opiniões, conclusão, divergências e plano de ação. A IA pode preparar uma síntese e organizar materiais, sem registrar consenso que a equipe não tenha aprovado.  
**Pronto quando:** a ata corresponde às decisões efetivamente validadas pelos participantes e cada ação tem responsável e prazo.

### F12 — Checklist preventivo do atendimento

**Origem:** proposto no escopo anterior; precisa ser implementado de modo transversal.  
**Entregas:** pendências por atendimento, protocolo, receita, APAC, relatório, solicitação, TCLE, encaminhamento e encerramento. Cada pendência informa o dado faltante, o motivo, a fonte necessária e quem pode resolvê-la.  
**Pronto quando:** o usuário identifica o problema antes de tentar liberar o documento e o bloqueio é específico, explicável e testado.

### F13 — APAC, regulação SUS e autorizações privadas

**Origem:** categorias documentais e textos de APAC existem no projeto já iniciado no Skip; fluxo regulatório completo é novo.  
**Entregas:** preparação de APAC de tratamento e de exames de alta complexidade; seleção de procedimento e justificativa; vínculo com diagnóstico, estadiamento, protocolo e período; validação de campos; revisão médica; conferência regulatória; envio ou exportação controlada; protocolo do destino; devolução, correção e reenvio. Para convênios, há guias e solicitações próprias, com regras e modelos por operadora/instituição quando fornecidos.  
**Pronto quando:** cada solicitação distingue **gerada**, **aprovada**, **enviada**, **recebida**, **autorizada**, **devolvida** ou **negada**, com evidência de cada transição. Texto genérico não satisfaz campo clínico obrigatório.

### F14 — Prescrições, receitas, relatórios, TCLE e kit documental

**Origem:** tela de documentos e geração textual presentes no projeto já iniciado no Skip; controles de liberação são novos.  
**Entregas:** modelos institucionais, preenchimento com dados confirmados, versões, revisão, bloqueios, assinatura quando juridicamente/institucionalmente aceita, entrega e registro de destinatário. O kit por conduta reúne, em uma mesma tarefa, todos os itens aplicáveis: receita oral, ordem de uso imediato, ciclo infusional, exames, APAC, relatório, orientações e consentimento. Receitas sujeitas a forma especial só serão emitidas no formato homologado pela instituição e responsáveis jurídicos.  
**Pronto quando:** o médico vê exatamente o que será liberado, pode editar cada item, identifica de onde veio cada campo e o sistema não entrega ao paciente um rascunho.

### F15 — Filas entre setores e encerramento assistido

**Origem:** ideia de handoffs no escopo anterior; navegação e status parciais no projeto já iniciado no Skip.  
**Entregas:** caixas de trabalho por regulação, farmácia, enfermagem, recepção e médico; confirmação de recebimento; devolução com motivo; prazo; responsável; substituição em ausência; escalonamento. No encerramento da consulta, o médico vê itens liberados, ainda pendentes e encaminhados.  
**Pronto quando:** não existe item liberado sem destino e é possível responder quem está com a próxima ação.

### F16 — Agenda, navegação e busca ativa

**Origem:** agenda, Kanban, fases, passos, barreiras, contatos e alertas presentes no projeto já iniciado no Skip; fechamento do ciclo operacional é novo.  
**Entregas:** próximo passo por paciente; data prevista e realizada; confirmação; atraso; falta; tarefa de contato; motivo da barreira; tentativa, resultado e novo plano. Regras diferentes podem ser configuradas para exame, consulta, ciclo, cirurgia, radioterapia e seguimento. Alertas que indiquem risco clínico são encaminhados a um profissional competente.  
**Pronto quando:** um paciente que faltou ou passou do prazo aparece na fila de busca ativa, com responsável, histórico de contato e resultado.

### F17 — Comunicação institucional

**Origem:** notificações presentes no projeto já iniciado no Skip; ligação efetiva a canais externos e preferências de comunicação são novas.  
**Entregas:** confirmação de consulta, lembretes, orientação de preparo, aviso de documento disponível, pedidos de agendamento e respostas do paciente. O conteúdo enviado por WhatsApp, SMS, e-mail ou outro canal é limitado ao necessário e depende de canal institucional autorizado, configuração e preferência registrada. Mensagens não substituem orientação de urgência nem revelam informação sensível em notificações abertas.  
**Pronto quando:** o sistema sabe o que foi preparado, enviado, entregue e respondido; falha de envio retorna à fila humana.

### F18 — Meu Oncologista, área do paciente

**Origem:** produto solicitado pelo Leonardo na reunião; novo.  
**Entregas:** acesso seguro por celular e computador; aplicativo instalável para Android e iOS; próximos compromissos; confirmação ou pedido de remarcação; documentos liberados; orientações; lista de preparos e próximos passos; questionários de sintomas e qualidade de vida; comunicação de barreiras; contatos úteis; autorização de representante quando aplicável. A instituição decide quais informações o paciente verá e quando. A forma técnica de produzir e distribuir o aplicativo será escolhida na implementação, com as contas, políticas e aprovações das lojas identificadas antes da publicação; a entrega não depende de um artifício específico do Skip.  
**Pronto quando:** o aplicativo pode ser instalado nos dispositivos suportados, um paciente acessa apenas seus próprios dados, o representante vê somente o vínculo autorizado e uma resposta de sintoma relevante cria tarefa para a equipe, com confirmação de recebimento.

### F19 — Regulação, farmácia, enfermagem e gestão financeira

**Origem:** financeiro, ciclos e parte dos documentos presentes no projeto já iniciado no Skip; filas, conciliação e fechamento institucional são novos.  
**Entregas:** regulação acompanha autorização e glosa/devolução; farmácia acompanha análise, preparo, dispensação e intervenções; enfermagem registra administração e intercorrência; gestão acompanha custos, utilização e motivos de atraso. Estoque, cobrança e faturamento efetivos dependem de integração e regras do sistema oficial da instituição.  
**Pronto quando:** cada área usa dados liberados e consegue devolver uma pendência sem criar uma segunda verdade clínica.

### F20 — Painéis e indicadores

**Origem:** dashboards presentes no projeto já iniciado no Skip; fontes verificáveis e medição de impacto são novas.  
**Entregas:** tempo de consulta e de documentação, pacientes por turno, fila, faltas, prazo até diagnóstico/tratamento, tempo de autorização, devoluções, pendências, ciclos realizados/adiados, ações de navegação, uso e qualidade das sugestões de IA. Indicadores terão definição, população, origem, periodicidade e responsável.  
**Pronto quando:** um gestor consegue reproduzir o número a partir de eventos registrados e visualizar separadamente dados ausentes, cancelados e corrigidos.

### F21 — Administração, catálogos e parâmetros

**Origem:** cadastro de configurações e catálogos no projeto já iniciado no Skip; controle institucional de versões e publicação são novos.  
**Entregas:** gestão de modelos documentais, protocolos, medicamentos, exames, unidades, prazos, alertas, formulários, destinatários, modelos de IA e políticas de retenção. Mudanças são preparadas em rascunho, revisadas e publicadas por responsáveis designados. A data de vigência evita aplicar uma regra nova retroativamente ao tratamento antigo.  
**Pronto quando:** o administrador identifica o que mudou, quem aprovou e quais unidades usam cada versão.

### F22 — Integrações e interoperabilidade

**Origem:** tela de integração, configurações, logs e geradores de estruturas no projeto já iniciado no Skip; conectores operacionais são novos.  
**Entregas:** conectar, conforme acesso real da instituição, prontuário hospitalar, agenda, laboratório, imagem, regulação, farmácia, canais de comunicação e sistemas públicos/privados pertinentes. Cada conector tem contrato de dados, autenticação, autorização, testes, monitoramento, tratamento de duplicidades e reconciliação. Padrões como FHIR podem ser usados quando o destino de fato os aceitar; gerar um arquivo nesse formato não comprova interoperabilidade.  
**Pronto quando:** uma transação completa é confirmada pelo destino, falhas são recuperáveis e o usuário consegue distinguir operação automática de exportação para lançamento assistido.

### F23 — Auditoria, segurança e recuperação

**Origem:** logs de auditoria e controles de acesso presentes no projeto já iniciado no Skip; governança de segurança, privacidade e continuidade é nova.  
**Entregas:** trilha de auditoria de dados clínicos e administrativos, gestão de acessos privilegiados, políticas de retenção e descarte, plano de cópias e restauração, monitoramento de incidentes e resposta prevista.  
**Pronto quando:** cada acesso e alteração relevante é rastreável; a instituição consegue demonstrar conformidade e recuperar o serviço dentro das metas acordadas.

### F24 — Evolução governada da IA

**Origem:** a reunião propõe aprender com correções dos médicos; mecanismo governado é novo.  
**Entregas:** coleta de aceites/rejeições com motivo, revisão amostral por especialistas, avaliação em casos clínicos aprovados, comparação entre versões, atualização controlada de conteúdo/modelos e possibilidade de voltar à versão anterior. Correções dos médicos **alimentam uma fila de avaliação**; não alteram automaticamente o comportamento clínico do agente.  
**Pronto quando:** qualquer mudança de modelo, prompt, protocolo ou base de conhecimento tem responsável, evidência de melhoria e aprovação antes de chegar aos usuários.

## 8. Inteligência artificial: onde atua e como será controlada

| Uso | O que pode produzir | Revisão necessária |
|---|---|---|
| Resumo de prontuário | Linha do tempo, fatos, lacunas e perguntas para a consulta | Profissional confirma antes de usar em documento. |
| Leitura de arquivo/exame | Campos sugeridos e comparação com resultados anteriores | Conferência com o original, unidades e datas. |
| Discussão de caso | Possibilidades clínicas, justificativas, perguntas e fontes | Médico decide; fonte e incerteza ficam visíveis. |
| Minuta de consulta/documento | Texto inicial a partir de dados confirmados | Autor responsável edita, aprova e assina conforme regra. |
| Apoio a protocolos | Localização e comparação de protocolos homologados | Médico e farmácia clínica validam aplicação ao paciente. |
| Navegação | Sugestão de próximo passo, alerta de atraso e priorização operacional | Navegadora ou responsável valida ação; alerta clínico escala para profissional habilitado. |
| Gestão | Agrupamento de causas de devolução, atrasos e retrabalho | Gestor valida interpretação antes de alterar processo. |

Cada uso terá finalidade própria, dados mínimos necessários, regra de acesso, provedor/modelo aprovado, limite de custo, formato de resposta, qualidade mínima e procedimento para falha. Modelos podem ser distintos por tarefa, como discutido na reunião, mas a escolha fica registrada e gerida pelo sistema. Informação do prontuário ou de anexos é **dado a analisar**, não uma instrução capaz de mudar as regras do assistente. Não haverá envio indiscriminado de prontuário completo a um provedor de IA. Contratos, retenção, localização do processamento e uso dos dados pelo provedor serão avaliados antes do uso clínico.

**Regras especiais:** a IA não inventa dado ausente; não preenche exame físico não realizado; não calcula dose apenas por texto livre; não diagnostica ou prescreve de modo autônomo; não responde a mensagem urgente do paciente como único mecanismo de cuidado; não confirma transmissão a outro sistema; não se reprograma automaticamente a partir das correções. Quando não houver dados ou fonte suficientes, informa a limitação e encaminha para avaliação humana.

## 9. Dados que o sistema precisa conhecer

Para uma pessoa sem formação técnica, o banco do Supabase pode ser entendido como conjuntos de fichas ligadas pelo paciente e pelo atendimento. Os conjuntos abaixo descrevem **o que precisa existir**, sem fixar ainda os nomes das tabelas:

| Grupo | Informações principais | Quem confirma |
|---|---|---|
| Instituição e unidade | Identidade, locais, equipes, configurações, catálogos e sistemas conectados | Administração/TI. |
| Pessoa usuária | Identidade, papéis, vínculo, situação do acesso e fator adicional de autenticação | Administração da instituição. |
| Paciente | Identificadores, contato, representante, preferência de comunicação e vínculo | Recepção/navegação, com conferência de identidade. |
| Jornada | Encaminhamento, fase, próximo passo, prazo, compromisso, falta, barreira, contato e desfecho | Navegação e equipe responsável. |
| Atendimento | Data, profissional, motivo, registros, estado e documentos produzidos | Profissional autor. |
| Histórico clínico | Diagnóstico, estadiamento, alergias, comorbidades, medicamentos e dados de performance | Profissional habilitado. |
| Exames e arquivos | Pedido, laudo, valores, unidades, datas, original e interpretação | Profissional responsável pelo dado. |
| Tratamento | Protocolo, versão, doses, ciclos, administrações, toxicidades e resposta | Médico, farmácia e enfermagem em suas etapas. |
| Documentos | Tipo, modelo, dados de origem, versões, aprovações, assinatura, destinatário e estado | Autor/revisor autorizado. |
| Integração | Origem, destino, identificador externo, pedido, resposta, protocolo e falha | Sistema com conciliação humana quando necessária. |
| IA | Pergunta, contexto selecionado, fontes, modelo, resposta, versão e decisão humana | Profissional usuário e governança clínica. |
| Auditoria e indicadores | Eventos, acessos, tempos, correções, responsáveis e métricas | Sistema registra; gestão revisa definições. |

Regras de qualidade: cada campo importante deve ter definição única; datas clínicas e datas de registro não são confundidas; unidades de medida são explícitas; a mesma pessoa pode ter múltiplos episódios e instituições; dados históricos não são sobrescritos apenas porque um valor novo chegou; o identificador de origem acompanha importações e exportações. Campos livres são aceitos para contexto clínico, mas não substituem campos estruturados necessários para cálculo, prescrição, autorização ou indicador.

## 10. Como o Supabase será usado

O Supabase reúne um banco de dados PostgreSQL, serviço de contas de usuários, armazenamento de arquivos e funções que executam ações protegidas no servidor. Na prática, ele guardará as fichas do paciente, controlará quem pode acessá-las e executará processos como gerar uma minuta ou falar com um sistema externo. O aplicativo e as telas continuarão sendo construídos como produto próprio; Supabase é a base operacional, não uma interface clínica pronta.

O projeto já iniciado no Skip traz telas construídas em React. Skip e Maestro podem ser usados pela equipe para construir ou adaptar essas telas, como conversado na reunião. O produto entregue deverá continuar funcionando sobre a base Supabase e com código e documentação que a equipe de TI do cliente consiga manter, independentemente da ferramenta usada durante a criação.

### 10.1 Conta, acesso e separação entre instituições

- **Supabase Auth:** entrada de profissionais e pacientes, recuperação de conta, bloqueio e segundo fator de autenticação. Segundo fator deve ser exigido para perfis com acesso clínico ou administrativo conforme política institucional. A documentação oficial do Supabase descreve o suporte a MFA e sua aplicação também nas regras de acesso: [Supabase Auth MFA](https://supabase.com/docs/guides/auth/auth-mfa).
- **Permissões no próprio banco:** uma regra de segurança verifica instituição, unidade, papel, vínculo com paciente e estado do registro em toda leitura ou alteração. Esconder um botão na tela não basta. O mecanismo do Supabase para isso é chamado *Row Level Security* (RLS): [documentação oficial](https://supabase.com/docs/guides/database/postgres/row-level-security).
- **Separação institucional:** cada ficha, arquivo, tarefa, log e configuração tem instituição proprietária. Acesso entre instituições requer vínculo e política específicos. Mudança de unidade não troca automaticamente o contexto clínico do paciente.
- **Acesso do paciente:** o Meu Oncologista consulta somente os dados liberados daquele paciente ou de representante autorizado. Um profissional que também é paciente não obtém acesso ampliado por ter duas funções.

### 10.2 Dados, arquivos e ações protegidas

- **Banco PostgreSQL:** dados estruturados do prontuário, agenda, documentos, fluxo, auditoria, integrações e indicadores. Mudanças na estrutura serão versionadas, para que ambientes de desenvolvimento, homologação e produção possam ser reproduzidos.
- **Supabase Storage:** laudos, PDFs, imagens documentais e anexos em áreas privadas. O sistema libera um arquivo apenas a quem pode vê-lo, pelo tempo necessário. A documentação oficial descreve controle de acesso para arquivos por políticas: [Storage Access Control](https://supabase.com/docs/guides/storage/security/access-control).
- **Edge Functions:** ações que não devem acontecer diretamente no navegador, como chamar modelos de IA, gerar documento final, enviar mensagem, receber resposta de integração e aplicar uma decisão privilegiada. A chave secreta de provedor nunca aparece no aplicativo do usuário: [Supabase Edge Functions](https://supabase.com/docs/guides/functions).
- **Eventos e tarefas agendadas:** avisos de prazo, fila de busca ativa, tentativa de reenvio e atualização de indicadores terão processamento controlado, com registro de execução e proteção contra duplicidade. O desenho exato do agendador será definido na implementação.
- **Ambientes separados:** desenvolvimento usa dados fictícios; homologação usa dados fictícios ou anonimizados conforme autorização; produção guarda dados reais somente após os controles e contratos necessários.

### 10.3 Segurança, região e recuperação

A região escolhida para o projeto será registrada com os responsáveis pelo tratamento dos dados. O Supabase lista a região de São Paulo, mas **escolher uma região não comprova conformidade legal**; contratos, fluxo dos dados, provedores de IA, cópias de segurança e acesso por terceiros também serão analisados. Consulte [regiões disponíveis](https://supabase.com/docs/guides/platform/regions) e a [orientação da ANPD sobre dados pessoais sensíveis de saúde](https://www.gov.br/anpd/pt-br/perguntas-frequentes.pdf/%40%40display-file/file). Este escopo exige avaliação jurídica e de privacidade institucional, sem presumir qual hipótese legal se aplica a todos os usos.

O plano de recuperação terá cópia e ensaio de restauração do banco **e** dos arquivos. A própria documentação do Supabase informa que a cópia do banco não inclui os objetos guardados pelo Storage: [Supabase Database Backups](https://supabase.com/docs/guides/platform/backups). Serão definidos frequência, responsável, prazo máximo aceitável de perda de dados e tempo máximo para retomar o serviço. Logs clínicos e arquivos necessários à rastreabilidade precisam permanecer coerentes depois de uma restauração.

**Custos:** não se adotam como compromisso os valores de planos citados informalmente na reunião. A estimativa deverá considerar usuários, tamanho e crescimento de exames/arquivos, tráfego, cópias, processamento de IA, canais de mensagem, suporte e ambientes. Custos de Supabase, modelos de IA, canais e eventuais sistemas parceiros serão apresentados separadamente.

## 11. Evolução do projeto já iniciado no Skip para a nova base

“Recomeçar” significa reconstruir a base e as regras em Supabase, preservando o conhecimento e os componentes úteis do projeto já iniciado no Skip. Não significa importar automaticamente todos os comportamentos atuais.

| Etapa | Trabalho | Evidência de conclusão |
|---|---|---|
| 1. Congelar referência | Preservar uma versão identificada do projeto já iniciado no Skip, sua data e lista de módulos. | Equipe consegue comparar qualquer tela nova com o projeto já iniciado no Skip. |
| 2. Inventariar | Catalogar telas, serviços, coleções PocketBase, dados, prompts, catálogos e fluxos reais. | Cada função tem dono, objetivo, origem e situação: aproveitar, reescrever ou descartar por erro comprovado. |
| 3. Validar clinicamente | Revisar modelos, protocolos, doses, texto de IA, campos obrigatórios, critérios de risco e informações de origem. | Especialistas registram o que foi aprovado e versão aplicada. |
| 4. Desenhar os dados novos | Mapear campo antigo para campo novo, com unidade, significado, dono, obrigatoriedade e regras de acesso. | Não há dado clínico sem destino claro ou regra de tratamento. |
| 5. Reconstruir no Supabase | Criar identidade, banco, arquivos, permissões, funções e trilha de eventos. | Operações são negadas a papéis sem autorização, inclusive por chamadas diretas ao servidor. |
| 6. Migrar referências aprovadas | Levar apenas catálogos e conteúdos revisados; migrar pacientes reais somente se houver base de origem exportável, autorização e plano de conciliação. | Contagens, amostras e divergências são reconciliadas por responsáveis. |
| 7. Comparar fluxos | Executar os mesmos casos clínicos fictícios no projeto já iniciado no Skip e na nova versão com Supabase, documentando melhorias e diferenças. | Fluxos importantes não perdem informação ou etapa sem decisão registrada. |
| 8. Piloto controlado | Usar a plataforma com a equipe definida, suporte próximo e rota assistida para sistemas ainda não conectados. | Incidentes, tempos e qualidade são medidos; responsáveis autorizam expansão. |

O material analisado do projeto já iniciado no Skip mostra a estrutura da aplicação e dados de exemplo/semente, não uma exportação confirmada do banco ativo. Antes de falar em “migração de pacientes”, a TI deverá confirmar se há dados reais no ambiente atual, quem os controla, como podem ser exportados e quais são suas autorizações de uso. A versão já iniciada no Skip só será desativada depois de preservar dados, trilhas e acesso exigidos pela instituição.

## 12. Integrações previstas e o que cada uma deve provar

| Destino/origem | Uso pretendido | Condição para considerar concluído |
|---|---|---|
| TASI/TASY e MV | Ler cadastro, agenda e dados clínicos permitidos; devolver documentos, status ou resultados conforme viabilidade | A instituição confirma nome/versão do sistema, acesso, contrato de dados, direção, identificação de paciente, teste e confirmação de recebimento. |
| Mednews e Wellon | Dados operacionais, mensagens ou fluxos existentes, conforme função real em cada hospital | Função e permissão confirmadas por TI e dono do processo; sem presumir API disponível. |
| Laboratório, imagem e farmácia | Pedidos, resultados, disponibilidade, preparo, dispensação e administração | Cada transação tem identificador, estado, data, origem e reconciliação. |
| Regulação SUS, APAC, SISREG, SISCAN, RHC e outros destinos aplicáveis | Exportar ou transmitir documentos/dados exigidos | Formato e canal homologados; protocolo verdadeiro ou comprovante; devolução tratada. Geração de texto local nunca aparece como transmissão. |
| Operadoras e faturamento privado | Guias, solicitações, autorizações e glosas | Regras por operadora e retorno efetivo do destino, quando houver acesso. |
| WhatsApp/SMS/e-mail | Confirmações, lembretes e busca ativa | Canal institucional autorizado, conteúdo aprovado, estado de entrega e preferência do paciente. |
| Google/Microsoft | Agenda, identidade ou documentos, se a instituição optar por usar esses serviços | Permissões, contratos, controle de acesso e prevenção de cópias clínicas desgovernadas. |
| Provedores de IA | Resumo, extração, consulta a fontes e minutas | Contrato e política de dados aprovados, modelo identificado, custo monitorado e avaliação clínica. |

Para cada integração, a equipe definirá uma das rotas: **conexão direta**, **troca de arquivo**, **importação/exportação assistida** ou **registro manual controlado**. Todas fazem parte do sistema completo como formas de operação possíveis; a tela deve mostrar qual rota está ativa. Conexão direta só será prometida para um destino após a validação técnica e institucional. Se o hospital usa mais de um sistema, a direção de cada dado e a “fonte oficial” serão documentadas para evitar duplicidade de agenda e prontuário.

## 13. Indicadores e como medir sucesso

| Indicador | Definição operacional proposta | Fonte e cuidado |
|---|---|---|
| Tempo administrativo por consulta | Soma do tempo ativo de preparação, correção, emissão e liberação de documentos por atendimento | Medir antes e depois no mesmo tipo de consulta; distinguir tempo médico de tempo de outros profissionais. Meta do piloto: redução ≥ 50%. |
| Pacientes por oncologista/turno | Atendimentos efetivamente concluídos divididos por turnos equivalentes | Comparar mesma carga horária, perfil de pacientes e equipe. Meta do piloto: razão pós/pré ≥ 1,5. |
| Espera da fila | Dias entre entrada elegível e primeiro atendimento oncológico, com regras para cancelamentos | Confirmar baseline real; referência verbal atual ≈ 100 dias e alvo inicial ≤ 70 dias. |
| Retrabalho documental | Documentos devolvidos ou corrigidos após preparação por total emitido | Separar erro clínico, regulatório, cadastro e falha de integração. |
| Segurança de prescrição | Alertas relevantes detectados, exceções justificadas e incidentes | Meta inicial é rastreabilidade e prevenção; não transformar “menos alertas” automaticamente em segurança maior. |
| Continuidade da navegação | Percentual de passos no prazo, faltas contatadas, barreiras resolvidas | Contato feito não equivale a tratamento realizado. |
| Prazo de autorização | Tempo de liberação médica até resposta da regulação/operadora | Separar tempo dentro do hospital e tempo do órgão externo. |
| Adoção | Uso real por perfil e proporção de atendimentos com fluxo completo | Avaliar se o sistema está economizando trabalho ou criando uma tela adicional. |
| Qualidade da IA | Respostas aceitáveis, rejeitadas e motivos, em amostra clínica revisada | Separar fluência textual de correção factual e segurança clínica. |

Antes do piloto, gestão e equipe clínica registrarão: período de medição, inclusão/exclusão de atendimentos, tamanho da amostra, método de cronometragem, fontes atuais e responsáveis por conferir números. Relatórios poderão mostrar resultado por unidade, período, tipo de consulta e profissional apenas dentro das regras de acesso. A meta de fila depende também de oferta de vagas, equipe, demanda, regulação e tratamento; a análise de impacto documentará esses fatores.

## 14. Entrega por ondas, cobrindo todo o sistema

As ondas organizam a construção e a validação; **nenhuma delas elimina os módulos descritos neste escopo**. A passagem para dados reais depende de segurança e aceites correspondentes.

| Onda | Resultado completo da onda | Demonstração de aceite |
|---|---|---|
| 0 — Definições e linha de base | Jornada real, regras institucionais, métricas, arquitetura de dados, inventário do projeto já iniciado no Skip e contratos de integração identificados | Mapa de fluxos e campos aprovado por Leonardo, áreas assistenciais, TI, regulação e gestão. |
| 1 — Fundação Supabase | Instituições, usuários, perfis, MFA, pacientes, anexos privados, auditoria, primeiras migrações e telas essenciais | Cada perfil executa sua tarefa; acesso indevido entre instituições é negado; recuperação é ensaiada. |
| 2 — Prontuário e atendimento | Consulta médica/enfermagem, linha do tempo, exames, dados oncológicos, origem de dados e checklist | Atendimento fictício completo é registrado e revisado sem perda ou duplicação de informação. |
| 3 — Terapia e documentos | Protocolos, catálogo, cálculos, prescrição, ciclos, segurança, APAC, relatórios, TCLE, kit documental e liberação | Médico e farmácia revisam casos de rotina e exceção; bloqueios e trilha funcionam. |
| 4 — Navegação e equipes | Agenda, busca ativa, handoffs, regulação, farmácia, enfermagem, notificações e painéis operacionais | Paciente com falta, pendência de autorização ou ciclo adiado é acompanhado até resolução ou justificativa. |
| 5 — IA clínica governada | Chat de caso, comparação de exames, tumor board, minutas, avaliação de qualidade e controle de versões | Casos clínicos de referência são avaliados por oncologistas; respostas inseguras são bloqueadas ou encaminhadas. |
| 6 — Jornada ampliada e Meu Oncologista | Cirurgia, radioterapia, genética, psicossocial, paliativos, resultados relatados pelo paciente, sobrevivência e acesso do paciente | Paciente e equipe acompanham a mesma jornada, com visões e permissões diferentes. |
| 7 — Integrações e gestão | Conectores homologados por instituição, exportações controladas, custos/financeiro, reconciliação e indicadores gerenciais | Cada integração exibe prova real de sucesso/falha; dados operacionais batem com a fonte oficial. |
| 8 — Piloto e expansão | Operação assistida, segurança, treinamento, comparação de metas, correção de falhas e preparação de outras unidades | Critérios ponta a ponta, privacidade, recuperação, desempenho e decisão de expansão documentados. |

O calendário, investimento e equipe por onda só poderão ser estimados depois da Onda 0, porque disponibilidade de integrações, modelos oficiais, dados do projeto já iniciado no Skip e validação clínica ainda são variáveis não confirmadas. O produto completo permanece definido aqui para evitar que a estimativa de uma primeira entrega seja confundida com o escopo total.

## 15. Critérios de aceite do sistema completo

Cada critério abaixo será demonstrado com um caso de rotina, um caso incompleto e, quando houver risco, um caso de exceção. “A tela existe” não é prova de que o fluxo funciona.

### A. Pessoas, instituições e prontuário

1. **Acesso por papel e instituição:** um usuário só lê e altera os registros autorizados, inclusive quando tenta acesso direto por link ou chamada ao servidor. O teste cobre profissional com dois vínculos, profissional desligado, substituto temporário e representante de paciente.
2. **Segundo fator:** profissionais definidos na política institucional não acessam dados clínicos protegidos sem completar o segundo fator; recuperação de conta não contorna essa regra.
3. **Identidade do paciente:** o sistema detecta possível duplicidade, permite conferência responsável e preserva a história de fusão/correção.
4. **Rastreabilidade:** uma alteração clínica mostra autor, data, conteúdo anterior, novo conteúdo e motivo quando exigido. Aprovação médica não pode ser reproduzida por outro perfil.
5. **Origem dos dados:** um campo de APAC, receita ou relatório mostra sua origem e se foi confirmado. Campo ausente não se converte silenciosamente em normal.
6. **Linha do tempo:** consulta, exame, procedimento, tratamento, intercorrência e desfecho aparecem com data clínica e data de registro separadas.

### B. Atendimento e tratamento

7. **Consulta:** a enfermeira prepara dados; o médico revisa, registra avaliação/conduta e encerra a consulta com pendências visíveis.
8. **Prescrição:** seleção de medicamento, via, dose, intervalo e duração é estruturada; alergia ou dado obrigatório ausente aciona bloqueio ou exceção formal definida pela instituição.
9. **Dose:** valor calculado, fonte dos dados, ajuste, valor aprovado, preparado e administrado são distinguíveis. Mudança de peso, altura ou creatinina não altera prescrição liberada sem revisão.
10. **Ciclo:** ciclo previsto, autorizado, preparado, administrado, adiado ou cancelado apresenta datas, responsáveis e motivo das diferenças.
11. **Toxicidade e intercorrência:** evento relevante chega à equipe competente, permanece pendente até tratamento e não é resolvido apenas por leitura da mensagem.
12. **Outras linhas da jornada:** cirurgia, radioterapia, genética, paliativos, aspectos psicossociais, resultados do paciente e sobrevivência podem ser registrados e consultados conforme permissões, com próximo passo definido.

### C. Documentos e setores

13. **Kit documental:** a conduta selecionada prepara os itens aplicáveis; o médico consegue revisar cada um separadamente e nenhum rascunho aparece como documento final.
14. **APAC e regulação:** campos obrigatórios são validados; status de envio só muda mediante ação e evidência reais; devoluções retornam com motivo e responsável.
15. **Receitas e relatórios:** modelos institucionais usam dados confirmados, registram versão e exigem liberação do responsável.
16. **Consentimento:** o sistema registra modelo, versão, entrega, assinatura/aceite quando aplicável e vínculo com o tratamento; termo preparado não é termo obtido.
17. **Handoff:** cada documento, ordem ou tarefa liberada tem destinatário, prazo, estado e confirmação ou devolução; o encerramento do atendimento aponta o que falta.
18. **Agenda:** a fonte oficial é conhecida; criação, remarcação, falta e cancelamento não geram duas agendas divergentes sem alerta.

### D. Navegação, paciente e IA

19. **Busca ativa:** falta e prazo vencido criam tarefa; contatos, resultado, barreira e novo plano ficam registrados.
20. **Meu Oncologista:** aplicativo instalável em Android e iOS e acesso por navegador; paciente acessa apenas o próprio conteúdo liberado; representante precisa de vínculo válido; confirmação de consulta e resposta de questionário aparecem à equipe correta.
21. **Sintoma relevante:** relato do paciente segue classificação e escalonamento institucionais; a plataforma não promete atendimento emergencial automático.
22. **IA com fontes:** resposta clínica mostra dados considerados, fontes, data/versão, incertezas e profissional que aceitou ou rejeitou a sugestão.
23. **IA sem dados suficientes:** ausência ou conflito de informação é apontado; o sistema não gera dado clínico fictício para completar a resposta.
24. **Evolução da IA:** uma correção feita por médico entra na fila de avaliação e não muda automaticamente respostas futuras.

### E. Integração, gestão e operação

25. **Integração real:** cada conector apresenta teste de envio/recebimento, identificador externo, tratamento de erro e conciliação. Exportação local é mostrada como exportação local.
26. **Fallback:** falha de sistema externo cria tarefa de operação assistida; após restabelecimento há reconciliação, sem duplicar documento ou pedido.
27. **Indicadores:** gestão consegue reproduzir tempo administrativo, pacientes por turno e fila a partir de eventos e visualizar as exclusões usadas no cálculo.
28. **Segurança e privacidade:** políticas do banco e de arquivos passam por revisão; segredos não ficam expostos ao navegador; acessos privilegiados são auditados.
29. **Recuperação:** restauração ensaiada inclui registros, versões, anexos e vínculos; responsáveis conhecem tempo de recuperação e procedimento de contingência.
30. **Implantação:** equipe recebe treinamento por papel, material de operação, canal de suporte e critérios documentados para avançar do piloto a outras unidades.

## 16. Requisitos de operação, qualidade e continuidade

- **Usabilidade:** médico encontra resumo, pendências, documentos e próximo paciente sem procurar informação em múltiplas áreas desconectadas. A equipe participará de demonstrações com tarefas reais antes do aceite.
- **Acessibilidade:** telas principais, inclusive Meu Oncologista, devem funcionar por teclado, ter textos legíveis, contraste adequado e mensagens compreensíveis. O paciente pode ter baixa familiaridade digital; comunicações essenciais continuam com alternativa humana.
- **Desempenho:** a aplicação deve abrir prontuário, agenda e filas no tempo acordado para o volume real do piloto. O alvo numérico e a carga de referência serão registrados após medir volume de usuários, pacientes e anexos; testes incluirão horário de pico.
- **Disponibilidade:** monitoramento de falhas e atrasos, rotina de contingência, responsável de plantão/suporte e aviso claro de indisponibilidade. Função de IA indisponível não impede o profissional de registrar o atendimento sem IA.
- **Privacidade:** coleta limitada à finalidade, acesso mínimo por função, retenção e descarte definidos com a instituição, registro de compartilhamentos e atendimento às solicitações cabíveis dos titulares. Dados de saúde são dados sensíveis; o tratamento exige base legal específica e avaliação institucional, sem presumir uma hipótese única para todos os usos.
- **Portabilidade:** instituição consegue exportar seus dados e documentos em formato acordado, preservando identificadores e histórico necessários à continuidade do cuidado.
- **Capacidade de expansão:** dados e configurações de hospitais diferentes são separados; processos comuns são reaproveitados sem obrigar todas as instituições a usar o mesmo protocolo local.
- **Treinamento e adoção:** materiais distintos para médico, enfermagem, farmácia, regulação, recepção, gestor, TI e paciente. Medir onde o usuário abandona ou contorna o fluxo para corrigir o processo.

## 17. Decisões institucionais necessárias para executar o escopo

Estas decisões **não reduzem o produto**. Elas definem a forma correta de implementar cada parte e quem assume a responsabilidade:

| Decisão | Responsável principal | Evidência necessária |
|---|---|---|
| Hospital/unidade do piloto, número de equipes e tipos de atendimento | Leonardo e gestão assistencial | Lista de unidades, papéis, volume e fluxo real. |
| Fonte oficial de paciente, agenda, exames, prescrição, APAC e faturamento | TI e donos dos processos | Mapa dos sistemas e quem pode criar/alterar cada dado. |
| Integrações acessíveis e formato de cada uma | TI, fornecedores e instituição | APIs/documentação, credenciais de teste, contratos e ambiente de homologação. |
| Protocolos, bulário, calculadoras, modelos documentais e critérios de alerta | Corpo clínico, farmácia, regulação | Versões aprovadas e responsáveis por atualização. |
| Casos em que residente, enfermagem e farmácia precisam de revisão superior | Direção técnica e áreas assistenciais | Matriz de permissões e fluxo de assinatura/aprovação. |
| Política de compartilhamento com IA e canais de mensagem | Responsáveis por privacidade, jurídico e gestão clínica | Avaliação de dados, provedores, textos, finalidade e contratos. |
| Identidade, representante e conteúdo liberado no Meu Oncologista | Direção técnica, jurídico, recepção e pacientes consultados | Regras de acesso, autorização e teste com usuários. |
| Política de assinatura e validade de documentos | Direção técnica, jurídico e regulação | Modelos, meios aceitos e destino de cada documento. |
| Linha de base e método de medição | Gestão operacional e consultoria | Amostra, período, exclusões e fonte dos três indicadores principais. |
| Região, retenção, backup e metas de recuperação | TI, privacidade e gestão | Registro de decisão, contratos e teste de restauração. |

## 18. Riscos concretos e resposta prevista

| Risco | Consequência | Resposta neste escopo |
|---|---|---|
| Projeto já iniciado no Skip ser interpretado como produto pronto | Lançamento sem prova de segurança e funcionamento | Inventário, revisão clínica, testes por cenário e aceite por módulo. |
| Supabase ser tratado como simples troca de banco | Repetir falhas de regras e acesso do projeto já iniciado no Skip | Reconstruir identidade, permissões, origem dos dados, funções e auditoria. |
| Dados ausentes virarem valores padrão | Documento ou sugestão clinicamente falsa | Mostrar ausência; bloquear conclusão que dependa do dado; registrar confirmação humana. |
| “Enviado” sem confirmação externa | Perda de autorização ou continuidade do cuidado | Estados separados e protocolo real do destino; reconciliação. |
| IA apresentar conduta convincente e incorreta | Risco assistencial | Fontes, avaliação clínica, limites de autonomia, supervisão e revisão de versão. |
| Nova tela aumentar o tempo médico | Fracasso da meta de capacidade | Reutilização de dados, preparação pela equipe, medição por etapa e ajuste de fluxo. |
| Instituições compartilharem dados indevidamente | Incidente de privacidade | Isolamento por instituição em banco, arquivos, funções e relatórios; teste de acesso cruzado. |
| Falta de acesso a sistemas hospitalares | Digitação dupla e atrasos | Rota assistida explícita, avaliação de custo operacional e priorização de conectores viáveis. |
| Crescimento de arquivos, mensagens e IA elevar custos | Operação economicamente inviável | Orçamento por módulo, limites, monitoramento e revisão de uso, sem reduzir controles de segurança. |
| Muitos módulos sem responsáveis operacionais | Informação desatualizada e alertas ignorados | Dono, fila, prazo, treinamento e indicador para cada processo. |

## 19. Glossário rápido

- **APAC:** autorização de procedimento de alta complexidade; neste projeto, inclui preparação, revisão, acompanhamento e retorno da solicitação aplicável.
- **Prontuário longitudinal:** histórico organizado ao longo de vários atendimentos, tratamentos e serviços.
- **Navegação:** trabalho de acompanhar próximos passos e impedir que o paciente se perca entre serviços.
- **Handoff:** passagem de uma tarefa ou documento de uma equipe para outra, com dono e estado.
- **Minuta:** texto preparado que ainda depende de revisão e liberação.
- **Protocolo clínico:** conjunto de regras terapêuticas aprovado para uso pela instituição, com versão e indicação.
- **Supabase:** plataforma escolhida para guardar dados, controlar usuários, armazenar arquivos e executar ações protegidas da nova aplicação.
- **RLS:** regra aplicada no banco para decidir quais fichas cada pessoa pode acessar.
- **Integração:** troca de dados comprovada entre sistemas; gerar arquivo ou registrar uma configuração não significa que o destinatário recebeu algo.
- **Fonte oficial:** sistema ou profissional responsável pelo dado que deve prevalecer quando duas cópias divergem.
- **Meu Oncologista:** área do paciente vinculada ao mesmo sistema, com acesso restrito ao conteúdo liberado.

## 20. Rastreabilidade da definição

| Fonte | O que sustenta neste documento |
|---|---|
| `00-DMO.md` e PDFs `Conexão Saúde` | Objetivo de capacidade, fila, futuro produto para outras instituições e três tarefas a mapear. |
| Sales Call de 05/08/2026 e mapeamento dos vídeos de 29/08/2026 | Gargalo do oncologista, sequência do atendimento, APAC, receitas, relatórios, protocolos e falhas observadas. |
| `02-Escopo-Definitivo.md` de 15/09/2026 | Metas do piloto, papéis, revisão médica, pendências, documentos e handoffs. |
| Reunião técnica posterior fornecida em `Texto colado.txt` | Três pilares, prontuário alimentado pela equipe, navegação, farmácia clínica, agenda, Supabase, IA com modelos distintos e ideia do Meu Oncologista. |
| Projeto já iniciado no Skip | Existência de telas e estruturas PocketBase para os módulos inventariados; também mostra a necessidade de revisar valores padrão clínicos e estados de integração. |
| Documentação oficial Supabase e ANPD, citada nas seções 10 e 16 | Capacidades da plataforma e cuidados de segurança/privacidade que informam a arquitetura proposta. |

**Interpretação das fontes:** falas da reunião e textos presentes no projeto já iniciado no Skip expressam visão, hipótese ou comportamento da versão existente. Eles não autorizam publicação de conduta, transmissão regulatória, uso de dados reais ou dispensa de revisão clínica. Quando uma fonte descreve o que “deveria fazer”, este escopo o transforma em requisito verificável, mantendo explícitas as validações institucionais necessárias.
