# Fase 5 --- Runbook de Operação, Observabilidade e Monitoramento da Tool

## Objetivo

Operacionalizar a Tool no contexto do agente, garantindo mecanismos
suficientes para observar, detectar, investigar e responder a problemas
continuamente.

> A Fase 5 não repete as validações das Fases 2--4. Ela transforma os
> requisitos validados em mecanismos operacionais contínuos.

------------------------------------------------------------------------

## 1. Pré-requisitos

-   Fases 1--4 aprovadas
-   Owner definido
-   SLA/SLO definido, quando aplicável
-   Dependências conhecidas
-   Ferramentas de observabilidade disponíveis
-   Acesso ao Datadog
-   Ambiente de produção/equivalente
-   Estratégia de logs, métricas e tracing

### Critério de aceite

Todos os mecanismos necessários para operar e observar a Tool estão
disponíveis.

------------------------------------------------------------------------

## 2. Logs

### Monitorar

-   Timestamp
-   Operação/Tool
-   Resultado
-   Erro
-   Dependências
-   Correlation/Trace ID
-   Contexto necessário para investigação
-   Ausência de exposição indevida de dados sensíveis

### Critério de aceite

Os logs permitem reconstruir uma ocorrência sem exposição indevida de
informações sensíveis.

------------------------------------------------------------------------

## 3. Métricas

### Monitorar

-   Volume
-   Sucesso/erro
-   Latência
-   P95
-   P99
-   Disponibilidade
-   Timeout
-   Retry
-   Frequência de seleção pelo agente
-   Falhas após seleção

### Critério de aceite

As métricas existem, são atualizadas e representam o comportamento
observado.

------------------------------------------------------------------------

## 4. Tracing

### Fluxo esperado

`Agente → Tool → API/Dependência → Resposta → Agente`

### Critério de aceite

É possível acompanhar o fluxo ponta a ponta sem perda de correlação.

------------------------------------------------------------------------

## 5. Dashboard Operacional

### Deve permitir observar

-   Volume
-   Sucesso/erro
-   Latência
-   P95/P99
-   Timeout
-   Retry
-   Disponibilidade
-   Uso pelo agente

### Critério de aceite

Dashboard disponível, atualizado e suficiente para identificar problemas
relevantes.

------------------------------------------------------------------------

## 6. Alertas

### Monitorar

-   Aumento de erros
-   Degradação de latência
-   Indisponibilidade
-   Timeouts
-   Anomalias de volume

### Critério de aceite

O alerta dispara segundo o threshold definido, chega ao responsável
correto e aponta para o procedimento de resposta.

------------------------------------------------------------------------

## 7. SLO/SLA

### Indicadores

-   Disponibilidade
-   Latência
-   Erro máximo
-   Capacidade
-   Outros indicadores relevantes

### Critério de aceite

Indicadores críticos possuem medição e alertamento quando necessário.

------------------------------------------------------------------------

## 8. Runbook Operacional

Deve cobrir:

1.  Identificação
2.  Investigação
3.  Mitigação
4.  Escalonamento
5.  Encerramento

### Critério de aceite

Uma pessoa que não participou da implementação consegue iniciar a
investigação seguindo o runbook.

------------------------------------------------------------------------

## 9. Ownership e Escalonamento

Registrar:

-   Owner
-   Time
-   Canal de suporte
-   Responsável pelo monitoramento
-   Caminho de escalonamento

### Critério de aceite

Existe responsável e caminho de escalonamento para incidentes
relevantes.

------------------------------------------------------------------------

## 10. Retenção e Acesso

Verificar:

-   Retenção
-   Permissões
-   Acesso a logs
-   Acesso a métricas
-   Acesso a traces

### Critério de aceite

As evidências necessárias permanecem disponíveis pelo período requerido
e somente para perfis autorizados.

------------------------------------------------------------------------

## 11. Monitoramento do Uso pelo Agente

Monitorar:

-   Frequência de seleção
-   Operações
-   Sucesso/erro
-   Latência
-   Uso anômalo
-   Mudanças relevantes na distribuição de chamadas

### Critério de aceite

É possível identificar volume, saúde e mudanças relevantes no uso da
Tool pelo agente.

------------------------------------------------------------------------

## 12. Qualidade Operacional

Monitorar:

-   Fallbacks
-   Respostas sem resultado
-   Mudanças na distribuição de seleção
-   Indicadores específicos da Tool

### Critério de aceite

Desvios relevantes podem ser detectados e existe processo para
investigação/reavaliação.

------------------------------------------------------------------------

## 13. Teste de Incidente

### Fluxo

`Falha → Métrica → Dashboard → Alerta → Owner → Investigação → Escalonamento`

### Critério de aceite

O fluxo é reproduzível, o problema é detectado e a investigação pode ser
iniciada com evidências suficientes.

------------------------------------------------------------------------

## Gate da Fase 5

Devem estar implementados e evidenciados:

-   Logs
-   Métricas
-   Tracing
-   Dashboard
-   Alertas
-   SLO/SLA
-   Runbook operacional
-   Ownership/escalonamento
-   Retenção/acesso
-   Monitoramento do uso pelo agente
-   Teste de incidente

### Saída

**TOOL OPERACIONALIZADA E OBSERVÁVEL**
