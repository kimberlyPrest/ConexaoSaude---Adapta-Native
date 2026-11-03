# Inventário de integrações

F1-T005 / SPEC-1-002 / CA-1-007. Fonte: `03_documentos/escopo.md` seção 12.

Cada destino/origem recebe a condição de conclusão que o escopo já exige. A coluna **situação de acesso real** é o ponto crítico: nada aqui foi testado com o sistema de destino, e nenhuma conexão é presumida por existir uma tela de configuração no sistema anterior.

| # | Destino/origem | Uso pretendido | Condição para considerar concluído | Situação de acesso real | Responsável pela confirmação | Prazo |
|---|---|---|---|---|---|---|
| 1 | TASI/TASY e MV | Ler cadastro, agenda e dados clínicos permitidos; devolver documentos, status ou resultados conforme viabilidade | Instituição confirma nome/versão, acesso, contrato de dados, direção, identificação do paciente, teste e confirmação de recebimento | Não verificado. Grafia do produto divergente no próprio escopo ("TASI/TASY"); versão, contrato e acesso pendentes | TI + fornecedor do sistema | até a F1-T006 |
| 2 | Mednews e Wellon | Dados operacionais, mensagens ou fluxos existentes, conforme função real em cada hospital | Função e permissão confirmadas por TI e dono do processo; sem presumir API disponível | Não verificado. Função real em cada hospital não confirmada | TI + dono do processo em cada hospital | até a F1-T006 |
| 3 | Laboratório, imagem e farmácia | Pedidos, resultados, disponibilidade, preparo, dispensação e administração | Cada transação com identificador, estado, data, origem e reconciliação | Não verificado. Sem contrato nem ambiente de homologação confirmados | TI + chefias de laboratório, imagem e farmácia | até a F1-T006 |
| 4 | Regulação SUS, APAC, SISREG, SISCAN, RHC e outros | Exportar ou transmitir documentos e dados exigidos | Formato e canal homologados; protocolo verdadeiro ou comprovante; devolução tratada. Geração de texto local nunca aparece como transmissão | Não verificado. O sistema anterior exibia envio simulado como "Transmitido" (erro 4 do inventário); nenhum protocolo real conferido | Regulação + TI | até a F1-T006 |
| 5 | Operadoras e faturamento privado | Guias, solicitações, autorizações e glosas | Regras por operadora e retorno efetivo do destino, quando houver acesso | Não verificado. Regras por operadora não recebidas | Faturamento + TI | até a F1-T006 |
| 6 | WhatsApp/SMS/e-mail | Confirmações, lembretes e busca ativa | Canal institucional autorizado, conteúdo aprovado, estado de entrega e preferência do paciente | Não verificado. Canal institucional e política de conteúdo pendentes | Gestão + TI (canal institucional) | até a F1-T006 |
| 7 | Google/Microsoft | Agenda, identidade ou documentos, se a instituição optar | Permissões, contratos, controle de acesso e prevenção de cópias clínicas desgovernadas | Não verificado. Depende de decisão institucional de adoção | TI + gestão (decisão de adoção) | até a F1-T006 |
| 8 | Provedores de IA | Resumo, extração, consulta a fontes e minutas | Contrato e política de dados aprovados, modelo identificado, custo monitorado e avaliação clínica | Não verificado. Nesta fase nenhuma chamada de IA é feita (fora da Fase 1) | Direção técnica + privacidade/jurídico | antes da Fase 4 |

## Rota de operação por integração

O escopo exige que cada integração declare uma rota: **conexão direta**, **troca de arquivo**, **importação/exportação assistida** ou **registro manual controlado**. A tela deve mostrar qual rota está ativa, e conexão direta só pode ser prometida após validação técnica e institucional.

Nenhuma rota foi escolhida nesta task: a escolha depende da validação com TI e com o dono do processo, que é a F1-T006.

## Como ler a coluna de situação

O plano B da SPEC-1-002 vale aqui: quando a TI ainda não confirmou um sistema, o item é registrado como "não verificado / a confirmar", com responsável e prazo, e o mapa não fica bloqueado. Nenhuma integração foi testada, contratada ou implementada, e nenhuma credencial existe neste documento.

## Limite

- Nenhuma integração foi implementada, testada ou contratada. Esta é a identificação do contrato que o escopo permite nesta fase (integrações reais são F22, Fase 5).
- Não há credencial, chave ou endereço de serviço neste documento, por regra de segurança.
- A coluna de situação real registra ausência de verificação, não uma falha do fornecedor: simplesmente nada foi confirmado ainda.
