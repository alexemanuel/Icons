                                           Runbook — Fase 3

                               Validação Funcional da Tool
 Documento operacional para execução, registro e aprovação da validação funcional de uma nova tool antes de sua
 avaliação dentro do agente.



 1. Objetivo
 Comprovar que a tool atende corretamente à sua responsabilidade funcional e às regras de negócio definidas. A
 tool é avaliada isoladamente nesta fase; não são avaliadas a escolha da tool pelo agente nem a geração de
 parâmetros pelo agente.

 Pergunta principal: quando a tool recebe uma entrada que pertence à sua responsabilidade, ela produz o
 comportamento e o resultado funcionalmente esperado?


 2. Escopo da validação
 1. Preparação dos cenários de teste

 2. Casos positivos (happy path)

 3. Casos negativos

 4. Casos de fronteira

 5. Hard negatives e fronteiras funcionais

 6. Validação de parâmetros

 7. Validação do resultado funcional

 8. Consistência dos resultados

 9. Cobertura do dataset

 10. Registro das evidências

 11. Gate de aprovação da Fase 3


 3. Pré-requisitos
 • Tool aprovada na Fase 2.

 • Documentação funcional da tool.

 • Descrição clara da responsabilidade da tool.

 • Regras de negócio aplicáveis.

 • Collection de validação da Fase 1.

 • Dataset de avaliação e casos de teste.

 • Resultado esperado para cada cenário.

 • Dados necessários para execução.

 • Owner funcional ou de negócio disponível para esclarecer ambiguidades.
 Critério de aceite: a execução só deve começar quando houver informação suficiente para determinar
 objetivamente o comportamento esperado. Se o resultado esperado não puder ser definido, o cenário deve ser
 marcado como BLOCKED, e não como PASS.



Runbook — Fase 3: Validação Funcional da Tool                                                              Página 1

 4. Preparação dos cenários de teste
 O que será validado: Identificar os principais casos de uso da tool e transformá-los em cenários testáveis. Cada
 cenário deve ser classificado como positivo, negativo, fronteira ou hard negative.

 Como validar: Para cada cenário, registrar contexto, entrada, tool sob teste, parâmetros esperados, resultado
 esperado e regra de negócio relacionada. Não usar o resultado observado da primeira execução como definição do
 resultado esperado.

 Por que validar: Garantir uma base objetiva para avaliar a tool e evitar que o resultado do teste seja definido após
 a execução.

 Critério de aceite: Todos os comportamentos funcionais relevantes possuem cenário, entrada, resultado esperado
 e regra de negócio claramente definidos.


 5. Casos positivos — Happy Path
 O que será validado: Validar os cenários em que a solicitação é válida, os parâmetros são suportados e a
 informação solicitada pertence à responsabilidade da tool.

 Como validar: Preparar os dados, executar a tool diretamente, capturar request e response, comparar com o
 resultado esperado e verificar as regras de negócio. O status HTTP não é suficiente.

 Por que validar: Comprovar que a principal responsabilidade funcional da tool funciona corretamente em
 condições normais.

 Critério de aceite: O resultado corresponde ao esperado, com dados corretos, filtros e regras respeitados e sem
 divergências funcionais relevantes.


 6. Casos negativos
 O que será validado: Validar o comportamento quando a condição necessária para uma resposta válida não existe
 ou quando a entrada não é suportada.

 Como validar: Executar cenários como recurso inexistente, parâmetro inválido, dados ausentes, período inválido
 ou combinação não permitida. Comparar o comportamento com a regra definida.

 Por que validar: Garantir que a tool não produza resultados incorretos, enganosos ou indevidamente positivos.

 Critério de aceite: A tool apresenta o comportamento negativo previsto, não retorna informação incorreta e trata
 ausência ou invalidade conforme a regra de negócio.


 7. Casos de fronteira
 O que será validado: Validar os limites das regras funcionais.

 Como validar: Quando aplicável, testar antes do limite, exatamente no limite e depois do limite. Exemplos: datas,
 quantidades, períodos, paginação e valores mínimos ou máximos.

 Por que validar: Erros de regra frequentemente aparecem na transição entre comportamentos válidos e inválidos.

 Critério de aceite: O comportamento em cada limite corresponde exatamente à regra de negócio documentada.


 8. Hard Negatives e fronteiras funcionais
 O que será validado: Definir os limites funcionais entre esta tool e outras tools semanticamente próximas.

 Como validar: Identificar tools potencialmente confundíveis, documentar a responsabilidade de cada uma, criar
 cenários próximos semanticamente e executar a tool sob certificação. Não avaliar a decisão do agente.
 Por que validar: Criar uma referência funcional objetiva para a futura avaliação do agente.

 Critério de aceite: É possível determinar claramente quais cenários pertencem à tool e quais estão fora de sua
 responsabilidade, com evidências e regras documentadas.


Runbook — Fase 3: Validação Funcional da Tool                                                                  Página 2

 9. Validação dos parâmetros
 O que será validado: Validar o comportamento funcional produzido por parâmetros obrigatórios, opcionais,
 defaults, valores válidos, inválidos e combinações suportadas ou não suportadas.

 Como validar: Construir uma matriz de testes para parâmetros e combinações relevantes. Executar cada
 combinação e comparar com o comportamento esperado.

 Por que validar: Garantir que diferentes formas de entrada não alterem indevidamente a regra funcional.

 Critério de aceite: Cada combinação suportada produz o comportamento especificado; combinações não
 suportadas são tratadas conforme a regra definida.


 10. Validação do resultado funcional
 O que será validado: Verificar se o conteúdo retornado está correto do ponto de vista do negócio, além do
 contrato técnico.

 Como validar: Comparar resultado esperado e obtido, verificando conteúdo, quantidade, filtros, ordenação,
 cálculos, datas, valores, relacionamentos entre campos e ausência de dados.

 Por que validar: Uma resposta tecnicamente bem-sucedida pode estar funcionalmente errada.

 Critério de aceite: O resultado obtido satisfaz integralmente as regras funcionais do cenário.


 11. Validação de consistência
 O que será validado: Verificar se cenários equivalentes produzem resultados funcionalmente consistentes.

 Como validar: Executar novamente cenários equivalentes quando os dados permitirem e comparar resultados.
 Diferenciações legítimas por dados dinâmicos devem ser identificadas.

 Por que validar: Garantir estabilidade do comportamento funcional.

 Critério de aceite: Entradas e condições equivalentes produzem resultados funcionalmente consistentes, salvo
 variação justificável e documentada.


 12. Cobertura do dataset
 O que será validado: Verificar se o dataset representa adequadamente o espaço funcional da tool.

 Como validar: Mapear regras de negócio para cenários e categorias: positivos, negativos, fronteiras, hard
 negatives e variações de entrada. Identificar regras relevantes sem cobertura.

 Por que validar: Evitar certificar a tool com uma amostra que não represente seus principais comportamentos.

 Critério de aceite: Toda regra relevante possui pelo menos um cenário; regras críticas devem ter cobertura
 adicional quando necessário.


 13. Registro dos testes
 O que será validado: Garantir rastreabilidade completa da execução.

 Como validar: Para cada cenário, registrar ID, categoria, cenário, input, tool, parâmetros, resultado esperado,
 resultado obtido, status, evidência e observações.

 Por que validar: Permitir auditoria, reprodução, análise de falhas e futura automação.

 Critério de aceite: Todos os cenários executados possuem evidência suficiente para reproduzir e entender o
 resultado.


 14. Classificação dos resultados
 O que será validado: Padronizar o resultado de cada cenário.


Runbook — Fase 3: Validação Funcional da Tool                                                                  Página 3

 Como validar: Usar três estados: PASS, FAIL e BLOCKED. PASS significa comportamento conforme esperado;
 FAIL significa divergência; BLOCKED significa impossibilidade de executar ou avaliar por dependência ou falta de
 definição.

 Por que validar: Evitar que testes não executados ou inconclusivos sejam tratados como aprovados.

 Critério de aceite: Nenhum cenário BLOCKED pode ser contabilizado como PASS; falhas impeditivas devem ser
 corrigidas ou formalmente tratadas.


 15. Modelo de registro de teste
      Campo                           Descrição

      ID                              Identificador único do cenário

      Categoria                       Positivo / Negativo / Fronteira / Hard Negative

      Cenário                         Descrição da situação avaliada

      Input                           Dados de entrada utilizados

      Tool                            Tool executada

      Parâmetros                      Parâmetros enviados

      Resultado esperado              Comportamento previamente definido

      Resultado obtido                Comportamento observado

      Status                          PASS / FAIL / BLOCKED

      Evidência                       Request, response, logs, screenshots etc.

      Observações                     Divergências, justificativas e comentários



 16. Critérios de aceite da Fase 3
 • Todos os cenários obrigatórios foram executados ou possuem tratamento formal para BLOCKED.

 • Casos positivos apresentam comportamento correto.

 • Casos negativos apresentam o comportamento esperado.

 • Casos de fronteira respeitam as regras de negócio.

 • Hard negatives possuem fronteiras funcionais claramente documentadas.

 • Parâmetros apresentam comportamento funcional correto.

 • Resultados atendem às regras de negócio.

 • Não existem falhas funcionais críticas abertas.

 • Todas as evidências estão registradas.

 • Exceções foram formalmente aceitas pelo owner responsável, quando aplicável.


 17. Gate para a Fase 4
 A Fase 3 deve terminar com uma referência funcional certificada: deve estar documentado quando a tool é
 aplicável, qual comportamento ela deve produzir e quais cenários estão fora de sua responsabilidade.
 Fase 2: a tool funciona tecnicamente?
 Fase 3: a tool funciona corretamente do ponto de vista funcional e de negócio?
 Fase 4: o agente sabe quando e como utilizar a tool?



Runbook — Fase 3: Validação Funcional da Tool                                                                Página 4

 Somente após a certificação funcional a tool deve ser utilizada como referência na avaliação do agente, incluindo
 seleção da tool, geração de parâmetros e tratamento do resultado.




Runbook — Fase 3: Validação Funcional da Tool                                                                 Página 5

