# Fase 7 --- Runbook de Revisão, Revalidação e Ciclo de Vida da Tool

## Objetivo

Garantir que a Tool continue válida ao longo do tempo, identificando
mudanças, avaliando impacto, executando revalidações quando necessárias
e tomando decisões de ciclo de vida.

A fase ocorre:

-   Periodicamente
-   Extraordinariamente após mudanças ou incidentes relevantes

------------------------------------------------------------------------

## 1. Quando Executar

Triggers:

-   Revisão periódica
-   Mudança de contrato
-   Mudança de API
-   Mudança de schema
-   Mudança de regra de negócio
-   Mudança de segurança
-   Mudança de roles
-   Rotação/expiração/revogação de secrets
-   Mudança de dependências
-   Mudança no MCP
-   Mudança no agente/modelo
-   Degradação de performance
-   Incidente relevante
-   Mudança de observabilidade
-   Evolução do dataset

------------------------------------------------------------------------

## 2. Verificação de Mudanças

Comparar a situação atual com a última versão validada.

### Fontes

-   Histórico
-   Releases
-   Documentação
-   PRs
-   Infraestrutura
-   Configurações
-   Políticas
-   Secrets

### Critério de aceite

Toda mudança relevante foi identificada, registrada e classificada.

------------------------------------------------------------------------

## 3. Análise de Impacto

Classificar:

-   Sem impacto
-   Parcial
-   Amplo
-   Crítico

### Dimensões

-   Técnico
-   Segurança
-   Funcional
-   Agente
-   Performance
-   Observabilidade
-   Dados
-   Dependências

### Critério de aceite

Existe registro do impacto e das fases potencialmente afetadas.

------------------------------------------------------------------------

## 4. Revalidação Técnica

Se houver impacto técnico, executar os testes afetados da **Fase 2**.

Exemplos:

-   Contrato
-   MCP
-   Segurança
-   Resiliência
-   Performance
-   Observabilidade

------------------------------------------------------------------------

## 5. Revalidação Funcional

Se houver impacto funcional, executar os testes afetados da **Fase 3**.

Exemplos:

-   Regras de negócio
-   Fronteiras
-   Parâmetros
-   Resultados
-   Hard negatives funcionais

------------------------------------------------------------------------

## 6. Revalidação do Agente

Se houver impacto no uso pelo agente, executar os testes afetados da
**Fase 4**.

Exemplos:

-   Seleção
-   No-Tool
-   Desambiguação
-   Parâmetros
-   Execução
-   Uso do resultado
-   Regressão

------------------------------------------------------------------------

## 7. Regressão

Executar cenários críticos e representativos.

### Critério de aceite

Nenhuma regressão crítica permanece sem:

-   Correção
-   Rollback
-   Bloqueio
-   Exceção formalmente aceita

------------------------------------------------------------------------

## 8. Segurança, Secrets e Permissões

Verificar:

-   Autenticação
-   Autorização
-   Roles
-   Policies
-   Secrets
-   Tokens
-   Certificados
-   Permissões MCP
-   Princípio do menor privilégio

### Secret Breaking

Avaliar eventos que possam interromper ou alterar a integração:

-   Expiração
-   Rotação
-   Revogação
-   Alteração
-   Falha de acesso
-   Credencial inválida

### Critério de aceite

Somente acessos necessários são mantidos, secrets não são expostos e
políticas são respeitadas.

------------------------------------------------------------------------

## 9. Monitoramento em Produção

Utilizar os sinais definidos na Fase 5:

-   Volume
-   Sucesso/erro
-   Latência
-   P95/P99
-   Timeouts
-   Retries
-   Disponibilidade
-   Erros de dependência
-   Uso pelo agente
-   Distribuição de seleção
-   Incidentes

------------------------------------------------------------------------

## 10. Análise de Incidentes

Para cada incidente:

-   Estava coberto pelo dataset?
-   Qual foi a causa?
-   Foi técnico, funcional ou relacionado ao agente?
-   Precisa de novo caso de teste?
-   Alguma fase precisa ser reexecutada?

------------------------------------------------------------------------

## 11. Evolução do Dataset

Adicionar casos originados de:

-   Novos comportamentos
-   Novas regras
-   Novas fronteiras
-   Hard negatives
-   Incidentes de produção
-   Confusão entre Tools
-   Regressões

### Proveniência

Usar classificações como:

-   `team-provided`
-   `independent`
-   `production-incident`
-   `regression`
-   `hard-negative`

------------------------------------------------------------------------

## 12. Ações Conforme a Mudança

  -----------------------------------------------------------------------
  Detecção                            Ação
  ----------------------------------- -----------------------------------
  Nenhuma mudança relevante           Registrar revisão e continuar

  Apenas documentação                 Atualizar documentação

  Mudança técnica isolada             Reexecutar testes afetados da F2

  Mudança de regra de negócio         Reexecutar F3

  Mudança na interface do agente      Reexecutar F4

  Mudança de segurança                Revalidar segurança/permissões

  Mudança de secret                   Validar
                                      credenciais/acesso/integração

  Degradação de performance           Investigar/revalidar

  Novo incidente                      Analisar e adicionar regressão
                                      quando aplicável

  Mudança ampla                       Reexecutar múltiplas fases

  Regressão crítica                   Bloquear/rollback

  Tool não atende mais à necessidade  Avaliar substituição/depreciação
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 13. Decisão de Ciclo de Vida

Possíveis decisões:

-   **KEEP** --- manter em operação
-   **UPDATE** --- atualizar
-   **REVALIDATE** --- executar novamente as fases necessárias
-   **DEPRECATE** --- descontinuar
-   **REPLACE** --- substituir por outra solução

------------------------------------------------------------------------

## 14. Critérios de Aceite

-   Revisão executada
-   Mudanças identificadas
-   Análise de impacto registrada
-   Fases afetadas revalidadas
-   Regressão executada
-   Segurança/permissões/secrets avaliados
-   Métricas de produção analisadas
-   Incidentes analisados
-   Dataset atualizado quando necessário
-   Evidências registradas
-   Decisão de ciclo de vida registrada
-   Ações possuem responsáveis e prazos

------------------------------------------------------------------------

## 15. Registro da Revisão

-   **Data:**
-   **Versão avaliada:**
-   **Motivo da revisão:**
-   **Mudanças identificadas:**
-   **Impacto:**
-   **Fases reexecutadas:**
-   **Resultado da regressão:**
-   **Incidentes relacionados:**
-   **Dataset atualizado?**
-   **Decisão:**
-   **Ações:**
-   **Responsáveis:**
-   **Prazo:**
-   **Evidências:**

------------------------------------------------------------------------

## Princípio do Ciclo de Vida

``` text
Produção
   ↓
Monitoramento
   ↓
Mudança / Incidente
   ↓
Análise de Impacto
   ↓
Revalidação
   ↓
Dataset / Regressão
   ↓
Nova versão
   ↓
Produção
```

### Saída

**TOOL MANTIDA, ATUALIZADA, REVALIDADA OU DESCONTINUADA CONFORME A
NECESSIDADE.**
