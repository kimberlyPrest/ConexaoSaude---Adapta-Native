# Referência congelada — F1-T007

Registro documental em 2026-11-03, BRT. SPEC-1-003, CA-1-010.
Projeto confirmado pelos conectores de listagem, detalhes, arquivos e status: 64011 — Plataforma Oncológica Multi-Instituição, publicado. Projeto homônimo 64009 não é o alvo ativo identificado.
- Produção: https://plataforma-oncologica-multi-instituicao-44213.goskip.app
- Preview: https://plataforma-oncologica-multi-instituicao-44213--preview.goskip.app
- Versão atual: 0.0.6, referência 15b9ef0.
- Referência publicada: 659822f.
- Referência indicada para desenvolvimento: e918fe5.
- Árvore limpa: pendingChanges vazio.
- Divergência preservada: atual, desenvolvimento e produção diferem; não houve publicação para igualá-las. Registro histórico, não backup restaurável nem bloqueio de futuras edições.
- Custódia: TI + Consultor, conforme task; pessoa responsável pela preservação a confirmar com Leonardo/TI.

## Módulos identificados
Rotas conferidas por project_get e leitura de src/App.tsx; menu em src/components/Sidebar.tsx.
- Entrada/autenticação: /login; AuthProvider, AuthGuard e MfaChallengeOverlay presentes nos arquivos.
- Instituição/unidade: TenantProvider e seletor no menu.
- Visão geral: /.
- Pacientes: /pacientes, /pacientes/novo, /pacientes/:id, /pacientes/:id/editar.
- Equipes: /equipes, /equipes/:id.
- Convites: /convites.
- Configurações: /configuracoes.
- Perfil: /perfil.
- Página não encontrada: *.
- Serviço: src/services/oncology.ts; tipos: src/types/oncology.ts.
- Integração Supabase: src/lib/supabase/client.ts, typed-client.ts e types.ts; sete arquivos em supabase/migrations listados pelo conector. Presença estrutural não comprova execução, segurança ou migração aplicada.

## Preservação e limites
Nenhum arquivo, configuração, dado, segredo ou versão do Skip foi alterado. Sem apply, QA ou publish. .env não acessado. Nenhum paciente será migrado por coincidência de nomes de tabelas/telas. Classificação completa e erros comprovados pertencem à F1-T008, não declarados verificados aqui.
Comparação futura: 659822f é a referência do que estava publicado; 15b9ef0 é a referência do código atual observado. Banco somente pelo conector Supabase quando a task exigir.
