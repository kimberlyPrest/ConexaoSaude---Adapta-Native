# SPEC-1-003 — Inventário e congelamento do projeto já iniciado no Skip

**Fase:** 1
**Status:** planejada
**Dono:** Consultor Adapta + TI do cliente
**Origem no escopo:** Onda 0 (inventário do projeto já iniciado no Skip); seção 2 (inventário e classificação); seção 11 (etapas 1–2)
**Degrau da solução:** construção mínima — catalogação e congelamento de referência, sem alterar o projeto existente.

## Resultado observável

O projeto já iniciado no Skip congelado em versão identificada (data + lista de módulos) e inventariado: cada tela, serviço, coleção PocketBase, prompt, catálogo e fluxo com dono, objetivo, origem e situação (**aproveitar / reescrever / descartar por erro comprovado**). A equipe consegue comparar qualquer tela nova com essa referência.

## Limites e dependências

- **Inclui:** congelamento de referência, inventário completo, classificação por item, registro de erros comprovados (ex.: preenchimento automático de ECOG 0, função renal "normal", CID genérico).
- **Fora de escopo:** validação clínica de conteúdo (etapa 3 da seção 11, Fase 2), migração de dados, alteração no projeto Skip.
- **Entradas e pré-condições:** acesso de leitura ao projeto Skip do Leonardo; lista de módulos da seção 2.
- **Saídas/artefatos:** versão congelada identificada + planilha/documento de inventário.
- **Dependências e responsáveis:** Leonardo fornece acesso e contexto; TI confirma onde vivem dados e coleções.
- **Risco e plano B:** sem acesso a alguma área, inventariar pelo código-fonte e marcar "a confirmar com o dono".
- **Rollback ou reversão:** o projeto Skip não é alterado; congelamento é apenas registro.

## Fluxo e regras

1. Registrar a versão congelada: data, URL, lista de módulos e responsável pela preservação.
2. Inventariar telas, serviços, coleções, prompts, catálogos e fluxos reais.
3. Classificar cada item: aproveitar / reescrever / descartar por erro comprovado.
4. Registrar explicitamente os erros comprovados citados na seção 2 (exemplos de preenchimento automático de informação ausente).
5. Confirmar que NENHUM dado de paciente será migrado apenas por haver tabela/tela com o mesmo nome.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | acesso completo ao projeto | inventário 100% classificado | registro por módulo |
| Limite | módulo sem dono identificado | item fica "a confirmar" com responsável | escalado ao Leonardo |
| Falha | erro comprovado em função candidata | item classificado "descartar" com evidência do erro | não entra no reaproveitamento |

## Checklist de execução

- [ ] Versão congelada registrada (data, URL, módulos).
- [ ] Inventário cobre telas, serviços, coleções, prompts e catálogos.
- [ ] Cada item tem dono, objetivo, origem e situação.
- [ ] Erros comprovados registrados com evidência.
- [ ] Regra de não-migração automática confirmada no documento.

## Critérios de aceite

- [ ] **CA-1-010:** versão congelada do projeto Skip identificada com data e lista de módulos.
- [ ] **CA-1-011:** inventário cobre todas as áreas da tabela da seção 2, cada item com dono, objetivo e situação.
- [ ] **CA-1-012:** itens com erro comprovado classificados como "descartar" com evidência registrada.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem inventário | tentar decidir reaproveitamento de uma função | decisão falha por falta de classificação | nota de bloqueio |
| GREEN | inventário preenchido | revisar áreas da seção 2 | todas classificadas | inventário salvo |
| REFACTOR/REGRESSÃO | item sem classificação | remover a situação de um item | aceite volta a falhar (CA-1-011) | checklist atualizado |

**Dados/fixtures:** tabela de inventário da seção 2 (18 áreas), código do projeto Skip.
**Caminhos de erro obrigatórios:** área sem acesso, item sem dono, erro sem evidência.
**Evidência exigida:** documento de inventário + registro da versão congelada.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T007 | Congelar versão de referência do projeto Skip | TI + Consultor | SPEC-1-003 | CA-1-010 | GREEN inventário | Registro da versão congelada | Acesso ao projeto | ☐ |
| F1-T008 | Inventariar e classificar todas as áreas | Consultor Adapta | SPEC-1-003 | CA-1-011, CA-1-012 | GREEN inventário | Inventário completo classificado | T1.7 concluída | ☐ |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
