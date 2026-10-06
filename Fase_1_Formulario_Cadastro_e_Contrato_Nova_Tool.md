# Fase 1 --- Cadastro e Contrato da Nova Tool

## Objetivo

Preparar o pacote de entrada da Tool, garantindo que todas as
informações necessárias para sua certificação estejam definidas,
documentadas e reproduzíveis.

------------------------------------------------------------------------

## 1. Identificação da Tool

-   **Nome da Tool:**
-   **Descrição:**
-   **Owner / Responsável técnico:**
-   **Time responsável:**
-   **Sistema / Serviço de origem:**
-   **Ambiente disponível para validação:**
-   **Data de cadastro:**
-   **Versão:**

------------------------------------------------------------------------

## 2. Contrato Técnico

### Input

-   **Link da documentação oficial:**
-   **Schema / definição:**

  Campo   Tipo   Obrigatório   Descrição   Restrições
  ------- ------ ------------- ----------- ------------
                                           

### Output

-   **Link da documentação oficial:**
-   **Schema / definição:**

  Campo   Tipo   Obrigatório   Descrição
  ------- ------ ------------- -----------
                               

### Tratamento de erros

  Cenário                     Erro/status esperado   Observações
  --------------------------- ---------------------- -------------
  Input inválido                                     
  Campo obrigatório ausente                          
  Recurso inexistente                                
  Não autorizado                                     
  Dependência indisponível                           

------------------------------------------------------------------------

## 3. Dependências, Pré-condições e Critérios de Aceite

### Dependências

  Dependência   Finalidade   Ambiente   Owner
  ------------- ------------ ---------- -------
                                        

### Pré-condições

-   [ ] Ambiente de teste disponível
-   [ ] Credenciais de teste disponíveis
-   [ ] Dados de teste disponíveis
-   [ ] Dependências acessíveis
-   [ ] Responsável técnico disponível
-   [ ] Documentação atualizada

### Critérios de aceite

  ID   Critério   Obrigatório   Evidência esperada
  ---- ---------- ------------- --------------------
                                

### Critérios de aceite das APIs utilizadas pelo MCP

Registrar os critérios que as APIs downstream utilizadas pela Tool/MCP
devem satisfazer.

  API   Critério   Obrigatório   Evidência
  ----- ---------- ------------- -----------
                                 

------------------------------------------------------------------------

## 4. Referências e Links Operacionais

-   **Documentação da Tool:**
-   **Dataset de treinamento, quando aplicável:**
-   **Dataset de avaliação:**
-   **Dashboard principal Datadog:**
-   **Outros links operacionais:**

------------------------------------------------------------------------

## 5. Dataset de Avaliação

O dataset deve representar cenários reais e relevantes para avaliar a
Tool e, posteriormente, preservar o comportamento de seleção do agente.

### Estrutura

  -------------------------------------------------------------------------
  Caso                Tool esperada     Valores esperados Justificativa
  ------------------- ----------------- ----------------- -----------------
  Pergunta/contexto   `nome_da_tool` ou `{}` ou objeto    Motivo da decisão
  do cliente          `None`            com valores       
                                        esperados         

  -------------------------------------------------------------------------

### Categorias obrigatórias

-   **Positivos:** a Tool deve ser utilizada.
-   **Negativos:** a Tool não deve ser utilizada.
-   **Hard negatives / confusão:** casos plausíveis que pertencem a
    outra Tool.
-   **Contextuais:** a Tool depende do contexto disponível.
-   **Parametrização:** cenários que verificam construção dos
    argumentos.
-   **No-tool:** casos em que nenhuma Tool deve ser chamada.

### Exemplo

``` json
{
  "caso": "Quais são meus próximos compromissos?",
  "tool_esperada": "getFutureAppointments",
  "valores_esperados": {
    "customer_id": "12345"
  },
  "justificativa": "A pergunta solicita compromissos futuros do cliente."
}
```

------------------------------------------------------------------------

## 6. Collection de Validação --- Obrigatória

A collection deve conter as chamadas necessárias ao MCP Server/Tool e
seus resultados esperados. Ela será utilizada na Fase 2.

-   **Link da Collection:**
-   **Formato:** Postman / Insomnia / outro
-   **Versão:**
-   **Responsável:**
-   **Data da última atualização:**
-   **Local compartilhado:**
-   **Ambiente / variáveis:**

### Requisitos

-   [ ] Executável no ambiente de teste
-   [ ] Variáveis documentadas
-   [ ] Sem credenciais expostas
-   [ ] Cada chamada possui resultado esperado
-   [ ] Casos positivos incluídos
-   [ ] Casos negativos incluídos
-   [ ] Casos de erro relevantes incluídos
-   [ ] Versão registrada
-   [ ] Owner definido
-   [ ] Collection atualizada

### Estrutura mínima

  ID   Endpoint / Tool   Cenário   Input   Resultado esperado
  ---- ----------------- --------- ------- --------------------
                                           

------------------------------------------------------------------------

## 7. Checklist de Completude

-   [ ] Identificação completa
-   [ ] Owner definido
-   [ ] Contrato de input
-   [ ] Contrato de output
-   [ ] Tratamento de erros
-   [ ] Dependências
-   [ ] Pré-condições
-   [ ] Critérios de aceite
-   [ ] Documentação
-   [ ] Dataset de treinamento, quando aplicável
-   [ ] Dashboard Datadog
-   [ ] Dataset de avaliação
-   [ ] Collection executável
-   [ ] Resultados esperados
-   [ ] Reprodutibilidade
-   [ ] Informações suficientes para iniciar a Fase 2

### Gate

-   **\[ \] APROVADO --- pronto para Fase 2**
-   **\[ \] PENDENTE --- necessita correções/informações**

------------------------------------------------------------------------

## 8. Aprovação

-   **Responsável técnico:**
-   **Validador:**
-   **Aprovador:**
-   **Data:**
-   **Status:**
