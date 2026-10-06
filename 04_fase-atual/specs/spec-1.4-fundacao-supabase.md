# SPEC-1-004 — Fundação Supabase: instituições, usuários, perfis e MFA

**Fase:** 1
**Status:** planejada
**Dono:** Consultor Adapta (implementação) + TI do cliente (política institucional)
**Origem no escopo:** Onda 1; F01; seção 10.1; CAs globais 1 e 2; seção 3 (11 perfis); seção 17 (decisões 4 e 10)
**Degrau da solução:** nativo da plataforma — Supabase Auth + RLS para identidade, papéis e segundo fator; construção mínima nas tabelas de vínculo.

> **Substitui** a SPEC-1-002 antiga (perfis e permissões, 15/09), que não cobria multi-instituição, MFA nem os 11 perfis da seção 3.

## Resultado observável

No Supabase: cadastro de instituições e unidades, equipes, especialidades, vínculos profissionais, convites, os 11 perfis da seção 3, substitutos temporários, bloqueio/desativação de usuário e segundo fator exigido para perfis com acesso clínico/administrativo. Recepção, navegação, médico, farmácia, regulação, gestão, TI e paciente veem apenas suas tarefas e dados autorizados; tentativa de acesso indevido é **negada no servidor** (RLS) e registrada.

## Limites e dependências

- **Inclui:** Auth, MFA, RLS por instituição/unidade/papel/vínculo, matriz de permissões, auditoria de acesso negado.
- **Fora de escopo:** cadastro clínico do paciente (SPEC-1-005), Storage (SPEC-1-006), telas completas (SPEC-1-007), IA.
- **Entradas e pré-condições:** mapa aprovado (SPEC-1-002); matriz de permissões e fluxo de assinatura decididos (seção 17, decisões 4 e 10); projeto Supabase criado com região registrada.
- **Saídas/artefatos:** migrações versionadas + matriz de permissões implementada + evidências de teste.
- **Dependências e responsáveis:** TI define política de MFA e revisão periódica; consultor implementa; Leonardo valida papéis clínicos.
- **Risco e plano B:** se a matriz de permissões não estiver decidida, implementar apenas instituição/unidade/vínculo e bloquear as tasks dependentes (Leva C).
- **Rollback ou reversão:** migrações reversíveis; ambiente de desenvolvimento usa dados fictícios.

## Fluxo e regras

1. Criar projeto Supabase (região registrada com responsáveis — seção 10.3) e ambientes separados (dev fictício).
2. Modelar instituição, unidade, equipe, especialidade, vínculo profissional e substituição temporária.
3. Implementar Auth com convites, bloqueio/desativação e MFA para perfis clínicos/administrativos.
4. Implementar RLS: toda leitura/alteração verifica instituição, unidade, papel, vínculo com paciente e estado do registro.
5. Registrar auditoria de acessos e de tentativas negadas.
6. Testar os cenários do CA global 1: dois vínculos, desligado, substituto temporário, representante de paciente, acesso direto por link e chamada direta ao servidor.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | profissional com vínculo válido executa sua tarefa | operação permitida e auditada | registro de evento |
| Limite | mesma pessoa em duas unidades | contextos separados, sem mistura de pacientes | troca de contexto explícita |
| Falha | perfil sem autorização chama o servidor diretamente | operação negada pelo RLS e registrada | auditoria de acesso negado |

## Checklist de execução

- [ ] Projeto Supabase criado com região registrada.
- [ ] Migrações versionadas aplicadas em dev (dados fictícios).
- [ ] MFA exigido conforme política institucional.
- [ ] RLS testado por papel e por instituição (prova negativa).
- [ ] Auditoria de acessos e negações funcionando.

## Critérios de aceite

- [ ] **CA-1-013:** um usuário só lê e altera registros autorizados, inclusive por link direto ou chamada ao servidor (CA global 1).
- [ ] **CA-1-014:** perfis definidos na política não acessam dados clínicos sem segundo fator; recuperação de conta não contorna (CA global 2).
- [ ] **CA-1-015:** os 11 perfis da seção 3 existem com permissões da matriz aprovada; acesso excepcional de TI exige motivo e auditoria.
- [ ] **CA-1-016:** cada ficha, arquivo, tarefa, log e configuração tem instituição proprietária; acesso cruzado é negado e testado.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem RLS | consultar tabela clínica com token de perfil não autorizado | consulta retorna dados (falha de segurança) | log do teste |
| GREEN | RLS aplicado | repetir a consulta | zero linhas + evento de auditoria | log do teste |
| REFACTOR/REGRESSÃO | acesso cruzado entre instituições | token da instituição A lê registro da instituição B | negado no servidor | log do teste |

**Dados/fixtures:** usuários fictícios dos 11 perfis, 2 instituições, 2 unidades, vínculo duplo, usuário desligado, substituto temporário.
**Caminhos de erro obrigatórios:** token inválido, perfil desligado, MFA pendente, vínculo inexistente, instituição errada.
**Evidência exigida:** logs de teste RLS + captura do fluxo de MFA + migrações versionadas.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T009 | Criar projeto Supabase e migrações de instituição/unidade/vínculo | Consultor Adapta | SPEC-1-004 | CA-1-016 | GREEN fundação | Migrações aplicadas em dev | T1.6 (decisões 17) concluída | ☐ |
| F1-T010 | Implementar Auth, convites, bloqueio e MFA | Consultor Adapta | SPEC-1-004 | CA-1-014 | GREEN MFA | Fluxo de MFA demonstrado | T1.9 concluída | ☐ |
| F1-T011 | Implementar RLS por papel/instituição + auditoria de negações | Consultor Adapta | SPEC-1-004 | CA-1-013, CA-1-015, CA-1-016 | RED/GREEN RLS | Logs de teste com prova negativa | T1.9 e T1.10 concluídas | ☐ |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
