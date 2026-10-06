# SPEC-1-006 — Auditoria, anexos privados e ensaio de recuperação

**Fase:** 1
**Status:** planejada
**Dono:** Consultor Adapta (implementação) + TI (política de retenção/backup)
**Origem no escopo:** Onda 1; F23; seção 10.2 (Storage) e 10.3 (recuperação); CAs globais 4, 28 e 29; seção 17 (decisão "Região, retenção, backup e metas de recuperação")
**Degrau da solução:** nativo da plataforma — Supabase Storage com políticas privadas + trilha de auditoria em tabelas próprias.

## Resultado observável

Trilha de auditoria completa (autor, data, conteúdo anterior, novo conteúdo e motivo quando exigido; aprovação médica não reproduzível por outro perfil), Storage privado para anexos com acesso só de quem pode vê-lo pelo tempo necessário, e um ensaio de restauração executado cobrindo banco **e** arquivos — com responsáveis, tempo de recuperação e procedimento registrados.

## Limites e dependências

- **Inclui:** tabelas de auditoria, gatilhos de versionamento, políticas de Storage, ensaio de restauração documentado, decisão de retenção/região registrada.
- **Fora de escopo:** monitoramento de produção contínuo (Fase 5), integrações, IA.
- **Entradas e pré-condições:** SPEC-1-004 concluída; política de retenção e metas de recuperação decididas com TI (seção 17).
- **Saídas/artefatos:** migrações + políticas de Storage + relatório do ensaio de restauração.
- **Dependências e responsáveis:** TI define retenção, região e metas (RPO/RTO); consultor implementa e executa o ensaio.
- **Risco e plano B:** sem decisão de retenção, implementar auditoria append-only com retenção provisória registrada como pendência.
- **Rollback ou reversão:** políticas de Storage versionadas; ensaio é repetível.

## Fluxo e regras

1. Implementar trilha de auditoria append-only: quem, instituição, quando, paciente, versão anterior, nova versão e motivo.
2. Garantir que aprovação médica não pode ser reproduzida por outro perfil (prova negativa).
3. Configurar Storage privado com políticas por papel/vínculo e expiração de acesso.
4. Registrar decisão de região, retenção, backup e metas de recuperação (seção 17).
5. Executar ensaio de restauração incluindo registros, versões, anexos e vínculos; documentar tempo e procedimento.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | alteração clínica autorizada | trilha completa com motivo | registro append-only |
| Limite | anexo solicitado por perfil sem vínculo | acesso negado pelo Storage | auditoria de negação |
| Falha | restauração parcial (só banco) | ensaio detecta incoerência com anexos | repetir incluindo Storage |

## Checklist de execução

- [ ] Auditoria append-only ativa nas tabelas da fundação.
- [ ] Prova negativa de reprodução de aprovação médica.
- [ ] Políticas privadas de Storage aplicadas e testadas.
- [ ] Decisão de região/retenção/backup registrada.
- [ ] Ensaio de restauração executado e documentado (banco + arquivos).

## Critérios de aceite

- [ ] **CA-1-020:** uma alteração clínica mostra autor, data, conteúdo anterior, novo conteúdo e motivo quando exigido; aprovação médica não é reproduzível por outro perfil (CA global 4).
- [ ] **CA-1-021:** anexos ficam em área privada; acesso concedido só a quem pode vê-lo, pelo tempo necessário (CA global 28, parte Storage).
- [ ] **CA-1-022:** restauração ensaiada inclui registros, versões, anexos e vínculos; responsáveis conhecem tempo de recuperação e procedimento (CA global 29).

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | sem auditoria | alterar registro clínico | nenhuma trilha gerada (falha) | log do teste |
| GREEN | auditoria ativa | repetir a alteração | trilha completa gerada | log do teste |
| REFACTOR/REGRESSÃO | restauração sem Storage | ensaiar restauração só do banco | incoerência detectada e documentada | relatório do ensaio |

**Dados/fixtures:** registros fictícios com alterações, anexos de teste, 2 perfis com permissões distintas.
**Caminhos de erro obrigatórios:** alteração sem motivo quando exigido, acesso a anexo sem vínculo, restauração incompleta.
**Evidência exigida:** logs de auditoria + relatório do ensaio de restauração assinado pelo TI.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T014 | Implementar auditoria append-only e políticas de Storage | Consultor Adapta | SPEC-1-006 | CA-1-020, CA-1-021 | RED/GREEN auditoria | Logs + políticas testadas | T1.11 concluída | ☐ |
| F1-T015 | Registrar decisão de região/retenção/backup e executar ensaio de restauração | TI + Consultor | SPEC-1-006 | CA-1-022 | REGRESSÃO restauração | Relatório do ensaio | T1.14 concluída | ☐ |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
