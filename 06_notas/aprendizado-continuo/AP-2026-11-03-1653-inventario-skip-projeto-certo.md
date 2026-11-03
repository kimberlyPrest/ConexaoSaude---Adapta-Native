# AP — inventariar o projeto certo antes de classificar áreas

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T008 / SPEC-1-003
- Sinal: o escopo descreve "o projeto já iniciado no Skip" com telas clínicas e PocketBase; o projeto apontado inicialmente (64011) era a nova fundação em Supabase e não continha nenhuma dessas telas. A classificação só ficou correta ao localizar o projeto 50880 pela lista da organização e confrontar rotas e coleções.
- Evidência: skip_project_get/50880 com 24 rotas clínicas e 34 coleções PocketBase; skip_project_get/64011 com 12 rotas de fundação e 22 tabelas Supabase. Registro em 06_notas/inventario-skip/inventario.md.
- Regra reutilizável: antes de inventariar ou classificar um "projeto já iniciado", confirmar qual projeto físico contém as telas citadas, comparando rotas e backend; nunca assumir que o projeto de mesmo assunto é o inventariado.
- Quando aplicar: qualquer SPEC que peça inventário, congelamento ou comparação com sistema anterior, especialmente quando a organização tem projetos homônimos ou uma fundação nova do mesmo produto.
- Quando não aplicar: quando a SPEC já cita o id do projeto de forma inequívoca.
- Confiança: alta — evidência direta de rotas e coleções divergentes.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
