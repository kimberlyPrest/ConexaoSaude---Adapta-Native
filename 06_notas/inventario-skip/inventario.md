# Inventário e classificação — projeto já iniciado no Skip

F1-T008 / SPEC-1-003 / CA-1-011 e CA-1-012. Levantamento em 2026-11-03, somente leitura.

## Qual é o projeto inventariado

O escopo (seção 2) descreve um projeto já iniciado com telas clínicas, prontuário, tumor board, protocolos, exames, documentos, agenda e integrações. Isso corresponde ao projeto **50880 — Oncologista Clínico Virtual** (PocketBase), e **não** ao projeto 64011 — Plataforma Oncológica Multi-Instituição, que é a nova fundação em Supabase.

| Item | 50880 — Oncologista Clínico Virtual | 64011 — Plataforma Oncológica |
|---|---|---|
| Papel | Projeto já iniciado (objeto deste inventário) | Nova fundação (Fase 1) |
| Versão observada | 0.0.42, referência 0645000 | 0.0.6, referência 15b9ef0 |
| Produção | Não publicada (`isPublished: false`) | Publicada (659822f) |
| Pendências | Somente `.skip.config.json` | Nenhuma |
| Backend | PocketBase, 34 coleções | Supabase, 22 tabelas |
| Agente de IA | `oncologista-virtual` (tier reasoning) | Não há |

Correção registrada: o registro da F1-T007 apontava apenas o 64011 como referência. O inventário da seção 2 é sobre o 50880; os dois registros foram separados. Nenhuma versão foi alterada em qualquer um deles.

## Situação por área (18 áreas da seção 2)

Classificação: **aproveitar** (conceito, texto ou componente reutilizável após revisão), **reescrever** (existe, mas a lógica precisa ser refeita), **descartar** (erro comprovado, não pode ser reaproveitado). Dono é o papel que valida o item; nenhum nome pessoal foi presumido.

| # | Área | O que existe no 50880 (evidência) | Objetivo no novo sistema | Dono da validação | Situação |
|---|---|---|---|---|---|
| 1 | Entrada e usuários | Rotas `/login`, `/accept-invite/:token`, `/setup-mfa`, `/verify-mfa`, `/usuarios`, `/perfil`; `AuthContext.tsx`, `totp.ts`, `invitations.ts`, `auditLogs.ts`; coleções `users`, `user_profiles`, `invitations`, `audit_logs` | Autenticar, convidar, atribuir papel e registrar auditoria por instituição | TI + área assistencial | Reescrever (reconstruir em Supabase Auth + RLS) |
| 2 | Pacientes e prontuário | `/pacientes`, `/pacientes/:id`, `/pacientes/:id/timeline`; `patientsService`, `medicalRecords.ts`, `ProntuarioEletronico.tsx`; coleções `patients`, `medical_records` | Cadastro único com vínculo institucional, versões e limites de edição | Área médica + TI | Reescrever; **descartar** a rotina de texto clínico automático (ver erros 1 a 3) |
| 3 | Consulta médica | `MedicalConsultationTab.tsx`, `clinicalConsultations.ts`, `oncologyConsultations.ts`; coleções `medical_consultations`, `oncology_consultations`; hook `generate_consultation_draft.js` | Registrar anamnese, exame e plano com estados de rascunho, revisão e fechamento | Área médica | Reescrever (o hook instrui a não inventar dado; a tela não segue a mesma regra) |
| 4 | Consulta de enfermagem | `NursingConsultationTab.tsx`, `nursing_consultations` | Registrar avaliação de enfermagem e o que exige confirmação médica | Enfermagem | Reescrever |
| 5 | Chat clínico e tumor board | `/chat`, `/tumor-board`; `Chat.tsx`, `TumorBoard.tsx`, `chatSessions.ts`; hooks `ask_stream.js`, `generate_tumor_board.js`; coleção `chat_sessions` | Discussão de caso com fonte, versão e auditoria | Área médica + TI | Reescrever |
| 6 | Protocolos, esquemas, bulário e calculadoras | `/protocolos`, `/esquemas`, `/bulario`, `/calculadoras`; `protocolosData.ts`, `bularioData.ts`, `medications.ts`, `treatmentProtocols.ts`, `regimens.ts` | Catálogo homologado com versão e responsável clínico | Farmácia + corpo clínico | Aproveitar o conceito de catálogo; reescrever conteúdo e regras de dose |
| 7 | Exames | `/exames`; `labExamService.ts`, `ExamComparatorTab.tsx`; hook `analyze_exam.js`; coleção `lab_exams` | Registro, anexo e comparação com unidade, data e origem visíveis | Área médica | Reescrever |
| 8 | Documentos | `/documentos`; `documents.ts`; hooks `generate_document.js`, `prescription_supervision.js`; coleção `documents` | Emitir APAC, laudo, receita e TCLE com pendência por documento e liberação responsável | Regulação + área médica | Parcial, reescrever: faltam formulários homologados e comprovação de envio |
| 9 | Agenda | `/agenda`; `appointmentService.ts`; coleção `appointments` | Mostrar disponibilidade, confirmação, falta e origem da agenda oficial | Recepção + TI | Reescrever |
| 10 | Navegação | `/navegacao-dashboard`, `/navegacao-kanban`, `/notificacoes`; `navigationService.ts`, `NavigationAlerts.tsx`, `barrierService.ts`; coleções `navigation_phases`, `navigation_steps`, `barriers`, `navigation_contacts`, `notifications` | Acompanhar prazos, barreiras, busca ativa e confirmação de execução | Enfermagem navegadora | Parcial, reescrever |
| 11 | Ciclos e toxicidades | `CycleAdminTab.tsx`, `ToxicityCTCAETab.tsx`, `cycleService.ts`, `ctcaeData.ts`; coleções `cycle_administrations`, `toxicity_assessments` | Registro de ciclo, toxicidade e regra de alerta por papel | Enfermagem + farmácia + médico | Reescrever |
| 12 | Cirurgia, radioterapia e paliativos | `SurgeryTab.tsx`, `RadiotherapyTab.tsx`, `PalliativeTools.tsx`, `surgeryService.ts`, `radiotherapyService.ts`; coleções `surgical_procedures`, `radiotherapy_plans` | Integrar esses eventos à linha do tempo do paciente | Cirurgião / radioterapeuta | Aproveitar estrutura de registro; reescrever integração à jornada |
| 13 | Genética, psicossocial, resultados do paciente e sobrevivência | `GeneticCounselingTab.tsx`, `PsychosocialScreening.tsx`, `PROsTab.tsx`, `SurvivorshipTab.tsx`; coleções `genetic_counseling`, `patient_reported_outcomes`, `survivorship_plans` | Definir consentimento, profissional responsável e uso clínico | Área médica + psicologia | Reescrever |
| 14 | Financeiro | `FinanceiroTab.tsx`, `financeService.ts`; coleções `financial_records`, `cost_tracking` | Separar visão gerencial de faturamento efetivo, com permissão própria | Gestão + faturamento | Reescrever |
| 15 | Integrações | `/integracoes`, `IntegracoesTab.tsx`, `integrationService.ts`; coleções `integration_configs`, `integration_logs`; geração de bundle FHIR, SISREG, SISCAN e RHC | Mostrar estado real de envio, com confirmação do destino | TI + regulação | **Descartar** os estados de envio simulados (ver erro 4); reescrever o restante |
| 16 | Painéis | `/dashboard-kpis`, `DashboardKPIs.tsx` | Ligar indicador a evento confiável e à linha de base | Gestão | Reescrever (painéis ficam fora da Fase 1) |
| 17 | Área do paciente | Não existe; a ideia apareceu na reunião | Acesso do paciente e do representante com conteúdo liberado | Direção técnica + jurídico | Novo (nada a reaproveitar) |
| 18 | Operação multi-instituição | Não existe no 50880: as coleções usam `owner_id`, sem instituição | Separar dados, catálogos e equipes por instituição | TI + gestão | Novo (é o objeto do 64011) |

## Erros comprovados — classificação "descartar" (CA-1-012)

Todos verificados por leitura do código do projeto 50880. Trechos reproduzidos de forma reduzida, sem dado de paciente.

1. **ECOG inventado quando ausente.** `src/pages/PacienteDetalhe.tsx`, modelo de intercorrência: `ECOG: ${patient.ecog ?? '0'}`. Ausência da escala vira "ECOG 0", ou seja, paciente completamente ativo. O hook `generate_consultation_draft.js` manda não inventar campo vazio; a tela faz o contrário. Classificação: descartar a rotina.
2. **ECOG fixo no modelo de alta.** Mesmo arquivo: o texto de alta escreve `ECOG: 0` literalmente, além de afirmar exame físico sem alterações e imagem sem doença ativa, independentemente do caso. Classificação: descartar.
3. **Função renal "Normal" por omissão.** Mesmo arquivo: `Função renal: ${patient.renal_function || 'Normal'}`. Falta de exame vira resultado normal — risco clínico direto. Classificação: descartar.
4. **Envio ao órgão simulado.** `src/services/integrationService.ts`: ao gerar a notificação SISCAN, grava log com `direction: 'Enviado'` e `status: 'Transmitido'`, com protocolo gerado por `SISCAN-BR-${Math.floor(100000 + Math.random() * 900000)}` — número aleatório, sem transmissão real. O mesmo padrão aparece no fluxo SISREG ("Gerado e Protocolado com Sucesso"). Classificação: descartar os estados; nenhum envio será mostrado sem confirmação do destino.
5. **Credenciais de demonstração na tela de login.** `src/pages/Login.tsx` traz e-mail e senha preenchidos por padrão e um bloco "Acesso Rápido de Teste (Admin)" visível na tela. Não é falha clínica, é exposição de acesso: a tela nova não pode repetir esse padrão. Registro sem reproduzir o valor da senha.

CID genérico: `src/lib/cidMapping.ts` só sugere código quando encontra correspondência e devolve vazio quando não encontra; não foi encontrado preenchimento automático de CID genérico nesse arquivo. O item do escopo fica **a confirmar** em outra rotina, não comprovado aqui.

## Regra de não-migração

Nenhum dado de paciente será migrado por existir tabela ou tela com o mesmo nome. O 50880 não tem produção publicada nem exportação verificável apresentada. As 34 coleções foram lidas apenas como estrutura. Nenhum registro clínico foi aberto, copiado ou contabilizado.

## Provas executadas

- CA-1-010: versão do 50880 identificada — 0.0.42 / 0645000, não publicada, pendência apenas `.skip.config.json`. Consulta por `skip_project_get`, `skip_project_status` e `skip_file_list`.
- CA-1-011: as 18 áreas da seção 2 têm dono, objetivo e situação na tabela acima; cada uma aponta arquivo, rota ou coleção que existe no projeto.
- CA-1-012: cinco itens com erro comprovado, com arquivo e trecho de origem.
- Limite: a leitura cobre estrutura e código; não houve execução da aplicação, teste com paciente, validação clínica nem acesso a dados reais.
