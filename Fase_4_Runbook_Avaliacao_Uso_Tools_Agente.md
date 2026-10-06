# Fase 4 --- Runbook de Avaliação do Uso das Tools pelo Agente

## Objetivo

Validar se o agente sabe **quando e como utilizar a Tool**, desde a
interpretação da intenção até o uso do resultado na resposta final.

> **Esta é a primeira fase em que o agente participa da validação.**

------------------------------------------------------------------------

## 1. Seleção da Tool

### Validar

-   Reconhecimento da intenção
-   Seleção da Tool correta
-   Paraphrases
-   Casos claros
-   Ferramentas semanticamente próximas

### Critério de aceite

O agente seleciona a Tool esperada e não realiza chamadas inadequadas.

### Evidências

-   Input
-   Intenção esperada
-   Tool esperada
-   Tool selecionada
-   Trace/log
-   Versão do agente/modelo

------------------------------------------------------------------------

## 2. No-Tool

### Cenários

-   Perguntas respondíveis sem Tool
-   Fora do domínio
-   Informação insuficiente para uma chamada segura
-   Casos que não devem gerar chamada especulativa

### Critério de aceite

Quando `Expected Tool = NONE`, o agente não realiza chamada indevida e
segue o comportamento definido.

------------------------------------------------------------------------

## 3. Desambiguação entre Tools

### Testar

-   Ferramentas concorrentes
-   Paraphrases
-   Formulações ambíguas
-   Cenários próximos às fronteiras funcionais da Fase 3

### Critério de aceite

A Tool selecionada respeita as fronteiras funcionais estabelecidas na
Fase 3.

------------------------------------------------------------------------

## 4. Construção dos Parâmetros

### Validar

-   Campos obrigatórios
-   Opcionais/defaults
-   Tipos
-   Formatos
-   Datas
-   IDs
-   Filtros
-   Quantidades
-   Combinações

### Critério de aceite

Os argumentos são corretos, completos, necessários e compatíveis com o
contrato.

------------------------------------------------------------------------

## 5. Execução da Tool

### Validar

-   Tool correta
-   Payload correto
-   Quantidade de chamadas
-   Ordem das chamadas
-   Ausência de chamadas duplicadas/especulativas

### Critério de aceite

A sequência de chamadas corresponde ao comportamento esperado.

------------------------------------------------------------------------

## 6. Uso do Resultado

### Cenários

-   Resultado conhecido
-   Múltiplos resultados
-   Resultado vazio
-   Resultado parcial
-   Campos opcionais
-   Erros

### Critério de aceite

A resposta final é consistente com o retorno real da Tool e não contém
dados inventados.

------------------------------------------------------------------------

## 7. Cenários Negativos

Testar:

-   Parâmetro inválido
-   Campo obrigatório ausente
-   Recurso inexistente
-   Resposta vazia
-   Erro da Tool/API
-   Timeout
-   Indisponibilidade, quando aplicável

### Critério de aceite

O agente segue o comportamento definido para cada falha, sem inventar
parâmetros ou resultados.

------------------------------------------------------------------------

## 8. Casos de Fronteira

Reutilizar as fronteiras definidas na Fase 3:

-   Antes do limite
-   No limite
-   Depois do limite

### Critério de aceite

O agente respeita a regra de negócio e não altera silenciosamente o
input, salvo quando isso estiver explicitamente definido.

------------------------------------------------------------------------

## 9. Hard Negatives

Agora avaliamos efetivamente a decisão do agente.

### Critério de aceite

O agente seleciona a Tool correta em cenários plausíveis de confusão e
não chama a Tool concorrente indevidamente.

------------------------------------------------------------------------

## 10. End-to-End

Validar o fluxo completo:

`Intenção → Seleção → Parâmetros → Execução → Resultado → Resposta`

### Critério de aceite

Todos os passos aplicáveis estão corretos. Uma resposta final correta
não compensa seleção ou parâmetros incorretos.

------------------------------------------------------------------------

## 11. Modelo de Cenário

  Campo                                 Valor
  ------------------------------------- -------
  ID                                    
  Categoria                             
  User Input                            
  Intent                                
  Expected Tool                         
  Expected Parameters                   
  Expected Calls                        
  Expected Behavior                     
  Expected Final Response / Critérios   
  Actual Tool                           
  Actual Parameters                     
  Actual Result                         
  Actual Response                       
  Status                                
  Evidence                              
  Observation / Defect                  

------------------------------------------------------------------------

## 12. Métricas

-   Tool Selection Accuracy
-   Parameter Accuracy
-   No-Tool Accuracy
-   Tool Call Accuracy
-   Result Usage Accuracy
-   End-to-End Accuracy

Segmentar por:

-   Happy Path
-   Negative
-   Boundary
-   Hard Negative
-   No-Tool
-   Ambiguous

Os thresholds devem ser definidos antes da execução.

------------------------------------------------------------------------

## 13. Roteamento de Falhas

  Falha                                   Destino
  --------------------------------------- ---------------------------------------
  Erro funcional da Tool                  Fase 3
  Erro técnico/API                        Fase 2
  Tool incorreta                          Fase 4 --- seleção/desambiguação
  Parâmetro incorreto                     Fase 4 --- construção
  Chamada desnecessária                   Fase 4 --- No-Tool/execução
  Resultado interpretado incorretamente   Fase 4 --- uso do resultado
  Dados inventados                        Fase 4 --- uso do resultado/negativos

------------------------------------------------------------------------

## 14. Gate da Fase 4

-   Cenários obrigatórios executados
-   Thresholds atingidos
-   Hard negatives tratados
-   No-Tool tratado
-   Fronteiras da Fase 3 preservadas
-   Resultados utilizados corretamente
-   Falhas críticas resolvidas ou formalmente aceitas
-   Evidências completas

### Saída

**AGENTE VALIDADO PARA USO DA TOOL**
