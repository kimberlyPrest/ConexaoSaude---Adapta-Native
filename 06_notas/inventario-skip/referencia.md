# Referência congelada — F1-T007

Registro documental em 2026-11-03, BRT. SPEC-1-003, CA-1-010.
Projeto confirmado pelo conector: 64011 — Plataforma Oncológica Multi-Instituição, publicado. O candidato 64009 tem o mesmo nome, mas não é o alvo publicado já identificado.
- Produção: https://plataforma-oncologica-multi-instituicao-44213.goskip.app
- Preview: https://plataforma-oncologica-multi-instituicao-44213--preview.goskip.app
- Versão atual: 0.0.6, referência 15b9ef0.
- Referência publicada: 659822f.
- Referência indicada para desenvolvimento: e918fe5.
- Árvore limpa: pendingChanges vazio.
- Divergência preservada: atual, desenvolvimento e produção não são a mesma referência; não houve publicação para igualá-las. O registro é referência histórica, não backup restaurável nem bloqueio de edições futuras.
- Custódia: TI + Consultor, conforme task; pessoa responsável pela preservação a confirmar com Leonardo/TI.

## Módulos identificados
Rotas conferidas por project_get e leitura de src/App.tsx; menu em src/components/Sidebar.tsx.
- Entrada/autenticação: /login; AuthProvider, AuthGuard e MfaChallengeOverlay nos arquivos.
- Contexto instituição/unidade: TenantProvider e seletor no menu.
- Visão geral: /.
- Pacientes: /pacientes, /pacientes/novo, /pacientes/:id, /pacientes/:id/editar.
- Equipes: /equipes, /equipes/:id.
- Convites: /convites.
- Configurações: /configuracoes.
- Perfil: /perfil.
- Página não encontrada: *.
- Camada de serviço: src/services/oncology.ts, tipos em src/types/oncology.ts.
- Integração Supabase: src/lib/supabase/client.ts, typed-client.ts, types.ts; diretório supabase/migrations com sete arquivos listado pelo conector. Só presença estrutural: não comprova execução, segurança ou migração aplicada.

## Preservação e limites
Nenhum arquivo, configuração, dado, segredo ou versão do Skip foi alterado. Não foi executado apply, QA nem publish. Não se acessou .env. Nenhum paciente será migrado por coincidência de nomes de tabelas/telas. Classificação completa e erros comprovados pertencem à F1-T008.
Para comparar telas futuras, usar a referência publicada 659822f para o que estava no ar e 15b9ef0 para o código atual no momento deste registro. Dados do banco só pelo conector Supabase, quando uma task exigir.

## Correção — 2026-11-03 (F1-T008)
Este registro cobre o projeto 64011 (fundação em Supabase). O inventário da seção 2 do escopo trata do projeto 50880 — Oncologista Clínico Virtual (PocketBase, 0.0.42 / 0645000, não publicado), cuja referência está em 06_notas/inventario-skip/inventario.md. Nenhuma versão de qualquer projeto foi alterada por esta correção.
