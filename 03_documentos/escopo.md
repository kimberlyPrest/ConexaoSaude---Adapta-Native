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

**Decisão sobre reaproveitamento:** identidade visual, componentes de interface, textos úteis, catálogo candidato e conceitos de fluxo podem ser aproveitados após avaliação. A lógica de segurança, regras clínicas, integrações e dados não serão copiados sem revisão. Foram observados exemplos de preenchimento automático de informações ausentes com valores como ECOG 0, função renal “normal”, CID genérico ou