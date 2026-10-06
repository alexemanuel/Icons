                                                        RUNBOOK



   Fase 4 — Avaliação do Uso das Tools pelo
                   Agente
     Documento operacional para validação reproduzível do comportamento do agente ao
                           selecionar, executar e utilizar tools.




  Campo                         Valor

  Fase                          4 — Avaliação do Uso das Tools pelo Agente

  Objetivo                      Validar se o agente sabe utilizar corretamente uma tool no contexto em que ela foi
                                disponibilizada.

  Entrada                       Tool aprovada nas Fases 2 e 3 + dataset de avaliação + ambiente do agente.

  Saída                         Relatório reproduzível com resultados, métricas, evidências, falhas e decisão de gate.

  Status possíveis              PASS / FAIL / BLOCKED / WAIVED




    Princípio central: a Fase 3 comprova que a tool é funcionalmente correta; a Fase 4 comprova que o
    agente sabe quando e como utilizá-la.




Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                                                Página 1

 1. Objetivo e escopo
 A Fase 4 avalia o comportamento do agente diante de solicitações reais ou representativas. O foco não é
 testar novamente a implementação da tool, mas verificar se o agente toma a decisão correta e executa
 o fluxo corretamente.

 Fluxo avaliado
  Etapa                        O que deve ser validado

  1. Solicitação               Interpretação da intenção do usuário.

  2. Seleção                   Tool correta, outra tool ou nenhuma tool.

  3. Parâmetros                Argumentos corretos, completos e coerentes.

  4. Execução                  Chamada correta, quantidade e ordem de chamadas.

  5. Resultado                 Interpretação fiel do retorno.

  6. Resposta                  Resposta final consistente com o resultado e o contexto.

 A fase contempla dez validações: seleção da tool; no-tool; desambiguação; construção dos parâmetros;
 execução; uso do resultado; cenários negativos; casos de fronteira; hard negatives; e end-to-end.


 2. Pré-requisitos
 • Tool aprovada na Fase 2 — Validação Técnica.

 • Tool aprovada na Fase 3 — Validação Funcional.

 • Contrato e documentação funcional atualizados.

 • Dataset de avaliação versionado.

 • Cenários esperados de uso e fronteiras funcionais conhecidos.

 • Tools concorrentes ou semanticamente próximas identificadas.

 • Ambiente de teste do agente disponível.

 • Logs/traces capazes de registrar as decisões e tool calls.

 • Mecanismo de captura da resposta da tool e da resposta final do agente.


 3. Regras de execução
 • Executar os cenários usando uma versão identificada do agente/modelo.

 • Não alterar o cenário durante a execução sem registrar a alteração.

 • Comparar o comportamento observado com o resultado esperado definido antes do teste.

 • Registrar evidência suficiente para reproduzir o resultado.

 • Não considerar somente a resposta final: tool, parâmetros, chamadas e resultado também fazem parte
 da avaliação.

 • Problemas funcionais da própria tool devem ser encaminhados para as fases anteriores, quando
 aplicável.




Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                         Página 2

 4. Modelo de cenário de teste
 Cada cenário deve ser identificável e conter expectativa explícita antes da execução.

  Campo                        Descrição

  ID                           Identificador único do cenário.

  Categoria                    Happy Path, Negative, Boundary, Hard Negative, No-Tool, Ambiguous ou variação de
                               linguagem.

  User Input                   Solicitação enviada ao agente.

  Intent                       Intenção esperada.

  Expected Tool                Tool esperada; pode ser NONE.

  Expected Parameters          Parâmetros e valores esperados.

  Expected Calls               Quantidade e ordem esperadas de chamadas.

  Expected Behavior            Comportamento esperado do agente.

  Expected Final Response      Resposta esperada ou critérios para avaliá-la.

  Actual Tool                  Tool efetivamente selecionada.

  Actual Parameters            Parâmetros enviados.

  Actual Result                Resultado efetivamente retornado.

  Actual Response              Resposta final produzida.

  Status                       PASS / FAIL / BLOCKED / WAIVED.

  Evidence                     Trace, log, payload, screenshot, request/response ou referência.

  Observation / Defect         Observações e referência de incidente, quando houver.



 5. Validações
 5.1 Seleção da Tool
 O que validar: Validar se o agente identifica a intenção do usuário e seleciona a tool correspondente.

 Como validar:

 • Executar solicitações claras que tenham uma única tool esperada.

 • Repetir a intenção com diferentes formulações de linguagem natural.

 • Comparar a tool efetivamente selecionada com Expected Tool.

 • Incluir casos em que outra tool é semanticamente próxima.

 Critério de aceite: A tool correta é selecionada em todos os cenários aplicáveis; nenhuma tool
 inadequada é chamada.

 Evidências: Input, intent esperada, tool esperada, tool efetiva, trace/log, versão do agente e status.

 5.2 No-Tool
 O que validar: Validar se o agente reconhece situações em que nenhuma tool é necessária.

 Como validar:

 • Executar perguntas que podem ser respondidas sem tool.

 • Executar solicitações fora do domínio das tools.

 • Executar casos em que faltam informações para uma chamada segura.

 • Verificar se não ocorre chamada especulativa.




Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                                         Página 3

 Critério de aceite: Quando Expected Tool = NONE, o agente não realiza chamada indevida e responde,
 esclarece ou recusa conforme comportamento definido.

 Evidências: Input, lista de tool calls, trace, resposta final e status.

 5.3 Desambiguação entre Tools
 O que validar: Validar a diferenciação entre tools com funções semanticamente próximas.

 Como validar:

 • Criar pares/trincas de tools concorrentes.

 • Executar uma solicitação para cada intenção.

 • Executar variações de linguagem que removam termos óbvios.

 • Registrar a característica que diferencia cada tool.

 Critério de aceite: A tool escolhida corresponde à intenção funcional e respeita a fronteira definida para
 cada tool.

 Evidências: Tool esperada, tools concorrentes, tool efetiva, input, motivo da distinção, trace e status.

 5.4 Construção dos Parâmetros
 O que validar: Validar se o agente extrai e monta corretamente os argumentos da chamada.

 Como validar:

 • Testar parâmetros obrigatórios.

 • Testar opcionais e defaults.

 • Testar tipos e formatos.

 • Testar datas, filtros, IDs, quantidades e combinações.

 • Comparar payload observado com Expected Parameters.

 Critério de aceite: Todos os parâmetros enviados são corretos, necessários e compatíveis com o contrato
 da tool.

 Evidências: Payload esperado e observado, contrato, trace/request, resposta e status.

 5.5 Execução da Tool
 O que validar: Validar se a chamada ocorre corretamente, sem chamadas desnecessárias.

 Como validar:

 • Comparar tool e payload executados com o esperado.

 • Verificar quantidade de chamadas.

 • Verificar ordem quando houver múltiplas chamadas.

 • Identificar duplicidades ou chamadas especulativas.

 Critério de aceite: A sequência de chamadas corresponde ao comportamento esperado para o cenário.

 Evidências: Trace completo, lista de chamadas, timestamps, payloads, resultados e status.

 5.6 Uso do Resultado
 O que validar: Validar se o agente interpreta e utiliza corretamente o retorno da tool.

 Como validar:

 • Fornecer resultados conhecidos e verificáveis.

 • Testar resultados únicos, múltiplos, vazios e parciais.



Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                              Página 4

 • Testar campos opcionais.

 • Comparar a resposta final com o resultado efetivamente retornado.

 Critério de aceite: A resposta é consistente com o retorno da tool, sem alteração indevida ou invenção de
 dados.

 Evidências: Tool response, resposta final, trace e comparação expected/actual.

 5.7 Cenários Negativos
 O que validar: Validar o comportamento do agente diante de parâmetros inválidos, ausência de dados e
 erros.

 Como validar:

 • Parâmetro inválido.

 • Parâmetro obrigatório ausente.

 • Recurso inexistente.

 • Resposta vazia.

 • Erro da tool/API.

 • Timeout ou indisponibilidade, quando suportado pelo ambiente.

 Critério de aceite: O agente segue o comportamento definido: solicita informação, comunica
 impossibilidade ou trata o erro; não inventa parâmetros nem resultados.

 Evidências: Input, erro/retorno da tool, comportamento observado, resposta final, trace e status.

 5.8 Casos de Fronteira
 O que validar: Validar se o agente preserva os limites funcionais estabelecidos na Fase 3.

 Como validar:

 • Reutilizar limites mínimo e máximo da Fase 3.

 • Testar imediatamente abaixo do limite.

 • Testar exatamente no limite.

 • Testar imediatamente acima do limite.

 • Testar limites de datas e valores, quando aplicável.

 Critério de aceite: O agente respeita exatamente a regra funcional. Não ajusta, arredonda ou altera o
 input para contornar uma restrição, salvo comportamento explicitamente definido.

 Evidências: Regra da Fase 3, input, parâmetros, chamada, resultado, resposta e status.

 5.9 Hard Negatives
 O que validar: Validar se o agente evita selecionar uma tool incorreta quando outra tool é
 funcionalmente adequada.

 Como validar:

 • Selecionar cenários plausíveis que se aproximem semanticamente da tool avaliada.

 • Identificar a tool correta e a concorrente.

 • Executar variações de linguagem.

 • Verificar a fronteira funcional definida na Fase 3.

 Critério de aceite: A tool correta é selecionada e a concorrente não é chamada indevidamente.

 Evidências: Cenário, tool correta, tool concorrente, critério de diferenciação, tool efetiva, trace e status.


Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                                Página 5

 5.10 End-to-End
 O que validar: Validar o fluxo completo desde a intenção até a resposta final.

 Como validar:

 • Executar o cenário como uma solicitação real.

 • Validar intenção, seleção, parâmetros, execução, resultado e resposta.

 • Considerar o cenário PASS somente quando todas as etapas aplicáveis estiverem corretas.

 Critério de aceite: Todo o fluxo atende ao comportamento esperado. Uma resposta final correta não
 compensa uma execução incorreta.

 Evidências: Trace completo, tool calls, payloads, resultados, resposta final e status.




Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                        Página 6

 6. Cenários de teste — exemplos
  ID           Categoria      Input                         Expected Tool        Expected            Aceite
                                                                                 Parameters

  TC-001       Happy Path     Qual é o saldo do cliente     get_customer_bala    customer_id=123     Tool e parâmetro
                              123?                          nce                                      corretos.

  TC-002       Happy Path     Quais foram as transações     get_customer_trans   customer_id=123     Não selecionar
                              do cliente 123?               actions                                  balance.

  TC-003       No-Tool        O que significa saldo         NONE                 —                   Nenhuma tool.
                              disponível?

  TC-004       Negative       Consulte o saldo.             get_customer_bala    customer_id         Não inventar ID.
                                                            nce ou               ausente
                                                            esclarecimento

  TC-005       Boundary       Transações dos últimos 90     get_customer_trans   period=90           Aceitar se 90 for
                              dias                          actions                                  limite.

  TC-006       Boundary       Transações dos últimos 91     Definido pela F3     period=91           Respeitar limite; não
                              dias                                                                   truncar.

  TC-007       Hard           Quais foram as transações     get_customer_trans   customer_id         Não selecionar
               Negative       do cliente?                   actions              conforme contexto   balance.

  TC-008       Result Usage   Qual é o saldo do cliente     get_customer_bala    customer_id=123     Resposta igual ao
                              123?                          nce                                      retorno da tool.



 7. Formulário de execução
 A tabela abaixo pode ser usada como registro operacional para cada cenário executado.

  Campo                                Preenchimento

  Scenario ID                          ____________________________

  Data/Hora                            ____________________________

  Executor                             ____________________________

  Dataset / versão                     ____________________________

  Agente / versão                      ____________________________

  Modelo                               ____________________________

  User Input                           ____________________________

  Intent esperada                      ____________________________

  Tool esperada                        ____________________________

  Tool executada                       ____________________________

  Parâmetros esperados                 ____________________________

  Parâmetros executados                ____________________________

  Resultado da tool                    ____________________________

  Resposta final                       ____________________________

  Status                               PASS / FAIL / BLOCKED / WAIVED

  Evidência / link                     ____________________________

  Observações                          ____________________________

  Defect / ticket                      ____________________________



 8. Métricas
 As métricas devem ser calculadas por dimensão e também segmentadas por categoria de cenário. Evite
 depender de uma única nota global.


Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                                                Página 7

  Métrica                                    Definição

  Tool Selection Accuracy                    Seleções corretas / cenários que exigem tool.

  Parameter Accuracy                         Chamadas com parâmetros corretos / chamadas avaliadas.

  No-Tool Accuracy                           Decisões corretas de não chamar / cenários No-Tool.

  Tool Call Accuracy                         Execuções cuja tool, quantidade e sequência correspondem ao esperado.

  Result Usage Accuracy                      Respostas que utilizam corretamente o resultado da tool.

  End-to-End Accuracy                        Cenários em que todas as etapas aplicáveis estão corretas.

 Segmentar pelo menos por: Happy Path, Negative, Boundary, Hard Negative, No-Tool e Ambiguous.




Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                                            Página 8

 9. Evidências obrigatórias
  Evidência                             Obrigatoriedade      Objetivo

  Input original                        Obrigatória          Reproduzir o cenário.

  Tool esperada                         Obrigatória          Comparar decisão.

  Tool efetiva                          Obrigatória          Verificar seleção.

  Parâmetros esperados/efetivos         Obrigatória          Verificar construção do payload.

  Trace/log da execução                 Obrigatória          Reconstituir o fluxo.

  Tool response                         Obrigatória quando   Verificar uso do resultado.
                                        houver chamada

  Resposta final                        Obrigatória          Verificar comportamento apresentado ao usuário.

  Versão do agente/modelo               Obrigatória          Reprodutibilidade.

  Status                                Obrigatória          Consolidar resultado.

  Ticket/defect                         Quando houver        Rastreabilidade da correção.
                                        FAIL



 10. Tratamento de falhas
  Falha observada                                            Direcionamento inicial

  Tool retorna resultado funcionalmente incorreto            Reavaliar Fase 3.

  Tool/API indisponível ou comportamento técnico             Reavaliar Fase 2.
  incorreto

  Agente seleciona tool incorreta                            Fase 4 — seleção/desambiguação.

  Parâmetro incorreto                                        Fase 4 — construção de parâmetros.

  Chamada desnecessária                                      Fase 4 — No-Tool/execução.

  Resultado correto, resposta final incorreta                Fase 4 — uso do resultado.

  Agente inventa dados                                       Fase 4 — uso do resultado/negativos.

 Para cada FAIL, registrar causa provável, evidência, severidade, ticket/defect e decisão sobre reteste.


 11. Gate de aprovação
 A aprovação deve considerar os resultados por dimensão, e não apenas uma média geral.

 • Todos os cenários obrigatórios executados.

 • Thresholds de acerto definidos pelo owner antes da execução.

 • Seleção de tools dentro do threshold estabelecido.

 • Parâmetros dentro do threshold estabelecido.

 • No-Tool e hard negatives tratados corretamente.

 • Limites funcionais da Fase 3 preservados.

 • Uso dos resultados consistente com os retornos reais.

 • Falhas críticas corrigidas ou formalmente aceitas pelo responsável.

 • Evidências completas e reproduzíveis.


 12. Resultado e entrega da Fase 4
 Ao final da execução, gerar um relatório contendo:



Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                                      Página 9

 • Identificação da versão do agente, modelo e dataset.

 • Quantidade de cenários executados por categoria.

 • Resultados por dimensão.

 • Métricas de seleção, parâmetros, chamadas, No-Tool, resultado e End-to-End.

 • Lista de FAILs e respectivos tickets.

 • Hard negatives com maior taxa de erro.

 • Casos de fronteira que apresentaram desvio.

 • Decisão final: APPROVED / REJECTED / APPROVED WITH EXCEPTIONS.

 • Exceções formalmente aprovadas, quando existirem.


 13. Separação entre as fases
  Fase                         Pergunta principal                                  Envolve agente?

  Fase 2 — Técnica             A tool funciona tecnicamente?                       Não

  Fase 3 — Funcional           A tool atende corretamente às regras do negócio?    Não

  Fase 4 — Agente              O agente sabe quando e como usar a tool?            Sim



    Saída final: um relatório reproduzível que demonstra, com evidências, se o agente utiliza corretamente
    a tool no contexto para o qual ela foi disponibilizada.




Runbook — Fase 4 | Avaliação do Uso das Tools pelo Agente                                            Página 10

