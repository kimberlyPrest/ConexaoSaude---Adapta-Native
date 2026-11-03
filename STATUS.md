# Status — Conexão Saúde e Vida

**Fase:** 1 — Fundação e definições (Ondas 0 e 1)
**Status:** execução iniciada; 4/16 tasks concluídas (25%). F1-T001, F1-T002, F1-T007 e F1-T008 têm prova documental. F1-T003 aguarda aprovação; F1-T004 aguarda confirmação operacional. Demais 10 tasks não concluídas.

## Próximas ações

1. Leva A: baseline (F1-T001/T002), mapa da jornada (F1-T004), congelamento do projeto Skip (F1-T007).
2. Registrar as decisões 1, 2, 4 e 5 da seção 17 do escopo (T1.3/T1.6) antes da Leva D.
3. Criar o projeto Supabase com região registrada (T1.9).
- **Teste do cliente:** por SPEC, não por task. A demonstração/aceite da fase é na SPEC-1-007 (F1-T016). Permanecem a aprovação do método na SPEC-1-001, aceites das áreas na SPEC-1-002 e decisão/assinatura da TI na SPEC-1-006; essas validações humanas não são provas automáticas (`AGENTS.md`).

## Execução — 03/11/2026
- Entregas: 06_notas/baseline/indicadores.csv e README.md; 06_notas/inventario-skip/referencia.md e inventario.md.
- Método proposto: 06_notas/baseline/metodo-medicao.md — sem aprovação; decisão humana não substituída por conferência automática.
- Impedimento F1-T003: aprovação e parâmetros operacionais ausentes — gestão deve revisar método, unidade/equipe, datas, duração do turno, coletor e fontes.
- Impedimento F1-T004: contexto real e fontes oficiais por etapa não confirmados — gestão/TI devem revisar 06_notas/jornada/mapa.md. Rascunho não satisfaz CA-1-005.
- Skip sem mudanças, sem publicação; divergência entre referência atual e publicada preservada. Supabase existente não foi recriado nem alterado; a F1-T009 precisa reconciliar o projeto real pelo conector antes de qualquer migração.
- As aprovações institucionais continuam pré-condições para Leva D em diante.

## Decisão do cliente — 03/11/2026 16:48
- **DECISÃO DO CLIENTE:** F1-T001 permanece como documento em `06_notas/baseline/` (opção A); nenhuma tela de baseline será criada no Skip nesta fase. Painéis seguem fora do escopo da Fase 1 (SPEC-1-001).
- **DECISÃO DO CLIENTE:** convidar `leonardofq-alt` com permissão de escrita no GitHub — feito; envio concluído.

- F1-T008 (03/11): inventário classificado em 06_notas/inventario-skip/inventario.md. Inventário da seção 2 refere-se ao projeto 50880, não ao 64011. Cinco erros comprovados; CID genérico a confirmar.
