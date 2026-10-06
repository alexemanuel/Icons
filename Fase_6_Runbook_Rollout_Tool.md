# Fase 6 --- Runbook de Rollout da Tool

## Objetivo

Introduzir a Tool em produção de forma controlada, gradual e reversível,
utilizando os mecanismos de observabilidade da Fase 5 para tomar
decisões de GO, HOLD ou ROLLBACK.

------------------------------------------------------------------------

## 1. Preparação para o Rollout

### Verificar

-   Fases anteriores aprovadas
-   Versão identificada
-   Ambiente de produção preparado
-   Configuração definida
-   MCP disponível
-   Autenticação/autorização
-   Secrets
-   Dashboards
-   Alertas
-   Owners
-   Rollback documentado

### Critério de aceite

Não existem pré-requisitos críticos pendentes, a versão está
identificada e o mecanismo de rollback está preparado.

------------------------------------------------------------------------

## 2. Estratégia de Rollout

### Definir

-   Estratégia de exposição
-   Público inicial
-   Percentual inicial
-   Etapas de expansão
-   Duração por etapa
-   Critérios de avanço
-   Critérios de pausa
-   Critérios de rollback
-   Responsáveis

### Exemplo

`Certificação → Deploy → 0% → Canary → 10% → 25% → 50% → 100%`

Os percentuais devem ser definidos conforme o risco e contexto.

### Critério de aceite

Todos os estágios, critérios GO/HOLD/ROLLBACK e responsáveis estão
documentados.

------------------------------------------------------------------------

## 3. Configuração e Disponibilização

### Verificar

-   Deploy da versão certificada
-   Configuração de produção
-   Registro/habilitação da Tool
-   MCP
-   Integração com o agente
-   Permissões
-   Secrets
-   Feature flags
-   Conectividade com dependências

### Critério de aceite

A Tool está disponível somente para o público planejado e na versão
aprovada.

------------------------------------------------------------------------

## 4. Canary / Primeira Exposição

### Monitorar

-   Chamadas
-   Sucesso
-   Erros
-   Latência
-   Timeouts
-   Falhas de parâmetros
-   Disponibilidade
-   Comportamento do agente
-   Erros MCP
-   Dependências

### Decisões

-   **GO:** métricas dentro dos limites.
-   **HOLD:** sinal de degradação exige investigação, mas não
    caracteriza rollback.
-   **ROLLBACK:** condição crítica predefinida.

### Critério de aceite

Não avançar sem GO explícito segundo os critérios definidos.

------------------------------------------------------------------------

## 5. Expansão Gradual

### Verificar

-   Percentual atual
-   Volume
-   Erros
-   Latência
-   Disponibilidade
-   Capacidade
-   Comportamento do agente
-   Incidentes
-   Impacto em outras Tools
-   Comparação com baseline

### Critério de aceite

-   GO → avançar
-   HOLD → manter exposição e investigar
-   ROLLBACK → retornar ao estado anterior

------------------------------------------------------------------------

## 6. Monitoramento do Comportamento do Agente

### Verificar

-   Frequência de seleção
-   Chamadas inadequadas
-   Chamadas esperadas ausentes
-   Falhas de parâmetros
-   Erros de execução
-   Uso incorreto do resultado
-   Interação com outras Tools
-   Chamadas desnecessárias

### Critério de aceite

Não existem regressões críticas ou padrões relevantes e inexplicados de
mudança de comportamento.

------------------------------------------------------------------------

## 7. Performance e Capacidade

### Monitorar

-   Latência
-   P50
-   P95
-   P99
-   Throughput
-   Timeouts
-   Retries
-   Utilização de recursos
-   Limites de dependências
-   Capacidade do MCP Server
-   Capacidade das APIs

### Critério de aceite

A expansão não provoca degradação além dos limites definidos.

------------------------------------------------------------------------

## 8. Gestão de Incidentes

### Fluxo

1.  Identificar impacto
2.  Definir severidade
3.  Relacionar ao rollout
4.  Decidir GO/HOLD/ROLLBACK
5.  Executar ação
6.  Registrar evidências
7.  Comunicar
8.  Recuperar

### Critério de aceite

Incidentes são tratados antes que o rollout avance.

------------------------------------------------------------------------

## 9. Rollback

### Verificar

-   Mecanismo de desabilitação
-   Restauração de configuração
-   Restauração de versão, quando aplicável
-   Remoção de exposição
-   Comportamento do agente após rollback
-   Recuperação das dependências
-   Comunicação
-   Registro da operação

### Critério de aceite

A Tool pode ser removida/revertida sem gerar estado inconsistente ou
impacto residual crítico.

------------------------------------------------------------------------

## 10. Conclusão do Rollout

### Verificar

-   Exposição final
-   Métricas
-   Erros
-   Latência
-   Disponibilidade
-   Comportamento do agente
-   Incidentes
-   Capacidade
-   Observabilidade
-   Rollback
-   Evidências
-   Aprovação

### Critério de aceite

-   Nível planejado atingido
-   Métricas dentro dos limites
-   Sem incidentes críticos abertos
-   Observabilidade ativa
-   Rollback disponível
-   Evidências registradas
-   Aprovação formal

------------------------------------------------------------------------

## 11. Transição para a Fase 7

Registrar:

-   Documentação atualizada
-   Versão
-   Configuração final
-   Baseline de produção
-   Owners
-   Incidentes
-   Decisão de conclusão

### Saída

**A TOOL FOI DISPONIBILIZADA EM PRODUÇÃO NO NÍVEL PLANEJADO, COM ROLLOUT
CONCLUÍDO E APROVADO.**

### Fluxo

`Preparação → Estratégia → Disponibilização → Canary → Avaliação → GO/HOLD/ROLLBACK → Expansão → Conclusão → Fase 7`
