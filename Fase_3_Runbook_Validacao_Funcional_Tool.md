# Fase 3 --- Runbook de Validação Funcional da Tool

## Objetivo

Validar se a Tool entrega o comportamento correto do ponto de vista
funcional e de negócio.

> **Importante:** a Fase 3 não envolve o agente.

------------------------------------------------------------------------

## 1. Preparação dos Cenários

Cada cenário deve possuir:

-   Contexto
-   Input
-   Tool sob teste
-   Valores/parâmetros esperados
-   Resultado esperado
-   Regra de negócio
-   Categoria

### Regra

O resultado esperado deve ser definido antes da execução e não pode ser
construído a partir da primeira resposta observada da Tool.

------------------------------------------------------------------------

## 2. Happy Path / Casos Positivos

### Validar

-   Condições válidas
-   Parâmetros suportados
-   Casos de uso dentro do escopo
-   Regras de negócio esperadas

### Critério de aceite

A Tool retorna exatamente o comportamento funcional esperado, não apenas
HTTP 200 ou schema válido.

------------------------------------------------------------------------

## 3. Casos Negativos

### Cenários

-   Dados inexistentes
-   Parâmetro inválido
-   Campo obrigatório ausente
-   Período inválido
-   Valor não suportado
-   Recurso sem permissão
-   Solicitação fora do escopo

### Critério de aceite

A Tool apresenta o comportamento negativo definido e não retorna dados
incorretos ou falsos positivos.

------------------------------------------------------------------------

## 4. Casos de Fronteira

Testar:

-   Antes do limite
-   Exatamente no limite
-   Depois do limite

Aplicável a:

-   Datas
-   Quantidades
-   Valores mínimo/máximo
-   Paginação
-   Limites de negócio

### Critério de aceite

O comportamento corresponde exatamente à regra de negócio definida.

------------------------------------------------------------------------

## 5. Hard Negatives / Fronteiras Funcionais

Um hard negative é um cenário plausível que parece pertencer à Tool, mas
funcionalmente pertence a outra Tool ou está fora de escopo.

### Objetivo

Definir claramente os limites funcionais da Tool.

> Na Fase 3 não avaliamos se o agente escolheu a Tool. Avaliamos se o
> cenário pertence ou não ao escopo funcional da Tool.

### Critério de aceite

As fronteiras funcionais são objetivas e documentadas.

------------------------------------------------------------------------

## 6. Validação de Parâmetros

### Verificar

-   Obrigatórios
-   Opcionais
-   Defaults
-   Tipos
-   Formatos
-   Datas
-   IDs
-   Filtros
-   Quantidades
-   Combinações

### Critério de aceite

Todas as combinações suportadas funcionam corretamente e as não
suportadas seguem o comportamento definido.

------------------------------------------------------------------------

## 7. Validação do Resultado Funcional

Validar:

-   Conteúdo
-   Quantidades
-   Filtros
-   Ordenação
-   Cálculos
-   Datas
-   Valores
-   Relacionamentos entre campos
-   Ausência de dados

### Critério de aceite

O resultado representa corretamente a regra de negócio.

------------------------------------------------------------------------

## 8. Cobertura do Dataset

O dataset deve cobrir:

-   Positivos
-   Negativos
-   Fronteiras
-   Hard negatives
-   Regras de negócio relevantes

------------------------------------------------------------------------

## 9. Registro dos Testes

Cada caso deve conter:

-   ID
-   Cenário
-   Input
-   Resultado esperado
-   Resultado obtido
-   Critério de aceite
-   Evidência
-   Status
-   Observações

------------------------------------------------------------------------

## 10. Gate da Fase 3

### Aprovar quando

-   Cenários obrigatórios executados ou formalmente bloqueados
-   Positivos corretos
-   Negativos corretos
-   Fronteiras corretas
-   Hard negatives definem limites funcionais
-   Parâmetros corretos
-   Resultados corretos
-   Evidências completas
-   Nenhuma falha funcional crítica

### Saída

**APROVADO PARA FASE 4**

------------------------------------------------------------------------

## Princípio

A Fase 3 responde:

> **"A Tool funciona corretamente para o negócio?"**

Não responde:

> "O agente escolhe essa Tool corretamente?"
