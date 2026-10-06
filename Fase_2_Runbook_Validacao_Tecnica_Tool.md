# Fase 2 --- Runbook de Validação Técnica da Tool

## Objetivo

Comprovar que a Tool funciona tecnicamente conforme o contrato definido,
incluindo integração MCP, segurança, resiliência, performance e
observabilidade.

> **Importante:** a Fase 2 não envolve o agente. A validação é executada
> diretamente na Tool/MCP e por meio do MCP Client.

------------------------------------------------------------------------

## 1. Pré-requisitos

Devem estar disponíveis:

-   Schema de input
-   Schema de output
-   Exemplos válidos e inválidos
-   Collection da Fase 1
-   Resultado esperado para cada chamada
-   Método de autenticação
-   Timeout esperado
-   SLA/SLO, quando aplicável
-   Ambiente de teste
-   Credenciais de teste
-   Responsável técnico
-   Documentação da Tool
-   Dataset de treinamento, quando aplicável
-   Dashboard principal Datadog

### Critério de aceite

Todos os artefatos obrigatórios estão disponíveis, acessíveis,
executáveis e suficientemente claros para permitir a execução
reproduzível dos testes.

------------------------------------------------------------------------

## 2. Validação do Contrato Técnico

### Objetivo

Validar o comportamento da Tool diretamente, sem o agente.

### Verificações

-   Campos obrigatórios
-   Tipos de dados
-   Restrições
-   Valores inválidos
-   Output
-   Ausência de dados
-   Erros

### Como validar

1.  Executar os casos da Collection.
2.  Registrar input e output.
3.  Comparar o resultado com o schema e resultado esperado.
4.  Registrar evidências.
5.  Classificar o teste.

### Critério de aceite

O comportamento observado está de acordo com o contrato técnico e os
resultados esperados.

### Evidências

-   Request
-   Response
-   Caso da Collection
-   Resultado esperado
-   Resultado obtido
-   Schema
-   Logs/traces, quando necessários
-   Status PASS/FAIL

------------------------------------------------------------------------

## 3. Validação da Integração MCP

### Objetivo

Comprovar que a Tool funciona corretamente quando acessada através do
protocolo MCP.

### Verificações

-   Descoberta da Tool (`tools/list`)
-   Schema disponibilizado pelo MCP
-   Chamada MCP
-   Passagem dos argumentos
-   Erros MCP
-   Consistência entre chamada direta e chamada via MCP

### Critério de aceite

-   Tool corretamente descoberta
-   Schema suficiente
-   Tool correta executada
-   Argumentos preservados
-   Erros controlados
-   Nenhuma diferença inexplicada entre chamada direta e MCP

------------------------------------------------------------------------

## 4. Validação de Segurança

### Verificações

-   Autenticação
-   Autorização
-   Dados sensíveis
-   Secrets
-   Permissões
-   Políticas de segurança
-   OPA, quando aplicável

### OPA

1.  Avaliar a política.
2.  Registrar o input da política.
3.  Registrar a decisão.
4.  Armazenar evidência.

### Critério de aceite

Nenhuma violação de política crítica ou de controle de acesso permanece
aberta.

------------------------------------------------------------------------

## 5. Resiliência e Tratamento de Erros

### Cenários

-   Timeout
-   Dependência indisponível
-   Resposta inválida
-   Retry
-   Idempotência para operações mutáveis
-   Erros de autenticação/autorização
-   Falhas de infraestrutura

### Critério de aceite

A Tool apresenta o comportamento definido para cada cenário e não produz
estado inconsistente ou resultado incorreto.

------------------------------------------------------------------------

## 6. Performance e Capacidade

### Métricas

-   Média
-   Mediana
-   P95
-   P99
-   Máximo
-   Taxa de erro
-   Concorrência
-   Throughput
-   Degradação

### Fórmula

`Taxa de erro = chamadas com falha / total de chamadas`

### Critério de aceite

Os resultados atendem aos SLA/SLO definidos na Fase 1. Não devem ser
inventados thresholds universais após a execução.

------------------------------------------------------------------------

## 7. Observabilidade

### Verificar

-   Logs
-   Métricas
-   Tracing
-   Dashboard Datadog

### Trace esperado

`MCP Client → MCP Server → Tool → Dependência`

### Critério de aceite

É possível localizar, correlacionar e investigar uma chamada ponta a
ponta.

------------------------------------------------------------------------

## 8. Registro de Evidências

Cada teste deve registrar:

-   ID
-   Seção
-   Cenário
-   Pré-condições
-   Input
-   Procedimento
-   Resultado esperado
-   Critério de aceite
-   Resultado obtido
-   Evidência
-   Timestamp
-   Ambiente
-   Status
-   Observações

### Status

-   PASS
-   FAIL
-   BLOCKED
-   N/A

> **Regra:** um teste sem evidência verificável não pode ser marcado
> como PASS.

------------------------------------------------------------------------

## 9. Gate da Fase 2

### Aprovar quando

-   Todos os testes aplicáveis foram executados.
-   Critérios foram atendidos.
-   Evidências foram registradas.
-   Não existem falhas críticas/bloqueantes.

### Saídas

**APROVADO PARA FASE 3** ou **RETORNAR PARA CORREÇÃO**

------------------------------------------------------------------------

## 10. Modelo de Caso de Teste

``` text
ID:
Seção:
Cenário:
Pré-condições:

Input:

Procedimento:
1.
2.
3.

Resultado esperado:

Critério de aceite:

Resultado obtido:

Evidência:

Status:
PASS / FAIL / BLOCKED / N/A

Observações:
```

------------------------------------------------------------------------

## 11. Automação Futura

Podem ser automatizados:

-   Validação de schema
-   Execução da Collection
-   Comparação de outputs
-   Descoberta MCP
-   Validação de argumentos
-   Casos negativos
-   Métricas
-   Consultas de observabilidade
-   Consolidação de evidências
-   Geração do relatório

``` text
Artefatos da Fase 1
        ↓
Contrato + Collection + Critérios
        ↓
Executor de testes
        ↓
Resultados
        ↓
Comparação
        ↓
Evidências
        ↓
Relatório da Fase 2
```
