# Contexto de Continuidade — Roadmap de Certificação e Ciclo de Vida de Tools para Agentes

> **Documento de handoff completo e deliberadamente não resumido.**
>
> Este arquivo deve permitir que outro agente continue o trabalho sem depender da conversa original. As decisões, distinções, nomenclaturas, racionales, regras, pendências, artefatos e conteúdos oficiais das fases estão registrados abaixo.
>
> **Regra principal:** não tratar este documento como um resumo executivo. Quando houver conteúdo integral de um documento oficial, o conteúdo é reproduzido abaixo. Não substituir os detalhes por interpretações mais curtas. Quando houver dúvida entre uma inferência e uma decisão registrada aqui, preservar a decisão registrada.
---

# 1. Contexto do projeto

Estamos construindo um processo formal de **onboarding, certificação, disponibilização, operação e ciclo de vida de Tools utilizadas por um agente de IA**.

O contexto é um agente consultivo que utiliza múltiplas **Tools / MCP Servers** para consultar informações de clientes e gerar respostas.

O objetivo do processo é controlar a entrada de novas Tools e garantir que elas:

1. sejam corretamente definidas;
2. tenham contrato técnico conhecido;
3. funcionem tecnicamente;
4. funcionem corretamente do ponto de vista funcional e de negócio;
5. sejam utilizadas corretamente pelo agente;
6. tenham observabilidade e capacidade operacional;
7. entrem em produção de forma controlada;
8. permaneçam válidas ao longo do tempo;
9. possam ser revalidadas quando houver mudança ou incidente;
10. tenham evidências suficientes para auditoria, investigação e reprodução.

O processo consolidado possui **7 fases**.
# 2. Roadmap completo

| Fase | Nome | Pergunta principal | Natureza |
|---|---|---|---|
| 1 | Cadastro e Contrato da Nova Tool | Temos tudo definido para iniciar a certificação? | Formulário / entrada |
| 2 | Validação Técnica da Tool | A Tool funciona tecnicamente? | Runbook técnico |
| 3 | Validação Funcional da Tool | A Tool funciona corretamente para o negócio? | Runbook funcional |
| 4 | Avaliação do Uso das Tools pelo Agente | O agente sabe quando e como usar a Tool? | Runbook de agente |
| 5 | Operação, Observabilidade e Monitoramento da Tool | Conseguimos operar e observar a Tool continuamente? | Operacionalização |
| 6 | Rollout da Tool | Conseguimos disponibilizar a Tool em produção com segurança? | Produção / rollout |
| 7 | Revisão, Revalidação e Ciclo de Vida da Tool | A Tool continua válida ao longo do tempo? | Lifecycle / feedback loop |

## Agrupamento

**Certificação:** Fases 1 → 2 → 3 → 4

**Entrada em produção / operacionalização:** Fases 5 → 6

**Ciclo de vida:** Fase 7

## Distinções que não podem ser perdidas

- **F2 e F3 não envolvem o agente.**
- **F4 é a primeira fase que envolve o agente.**
- **F5 não é uma nova rodada de testes das Fases 2–4; é a operacionalização da observabilidade e do monitoramento.**
- **F6 é o rollout efetivo em produção.**
- **F7 é manutenção contínua, revisão e revalidação ao longo do tempo.**
- F7 não deve ser tratado apenas como "mais uma rodada de testes": ele funciona como um ciclo de feedback entre produção, mudanças, incidentes, dataset, regressão e novas versões.
# 3. Papéis, nomenclaturas e ownership

O time anteriormente chamado de "Plataforma" no contexto do agente/MCP foi definido como:

## 🤖 Agentes Satélite

Esse é o time responsável pelo agente e por aspectos da integração MCP.

Escopo conceitual:

- Agente
- MCP Client
- MCP Server
- Integração com Tools
- Tool calling
- Tool selection
- Disponibilização técnica
- Integração da Tool com o agente
- Parte da observabilidade técnica

Papéis que podem aparecer na legenda do one-page:

- 👤 **Owner da Tool**
- 🤖 **Agentes Satélite**
- 📈 **SRE/Operações**
- 🔒 **Segurança**
- 🟣 **Plataforma**

### Importante sobre ownership

**Os owners reais das fases ainda não foram definidos.**

No one-page, cada fase deve possuir uma seção chamada:

> **Responsáveis desta fase**

Essa seção deve ficar **completamente vazia**, sem nomes, símbolos, ícones ou qualquer texto dentro da caixa.

A legenda inferior pode mostrar os papéis/times possíveis.

### Responsabilidades conceituais

**Owner da Tool**
- domínio;
- regras de negócio;
- comportamento funcional;
- dependências de negócio;
- aprovação;
- ciclo de vida da Tool.

**Agentes Satélite**
- agente;
- MCP;
- integração;
- Tool calling;
- Tool selection;
- disponibilização técnica;
- comportamento do agente.

**SRE/Operações**
- observabilidade operacional;
- operação;
- monitoramento;
- capacidade;
- incidentes;
- alertas;
- SLO/SLA.

**Segurança**
- acessos;
- políticas;
- autenticação;
- autorização;
- secrets;
- compliance;
- controles de segurança.

**Plataforma**
- infraestrutura;
- ambientes;
- padrões;
- deployment;
- suporte técnico à certificação;
- participação quando aplicável.

## Racional conceitual de possíveis responsáveis

### Fase 1
Possível principal: Owner da Tool.

Participação de Agentes Satélite porque o contrato precisa ser suficiente para a integração MCP/agente.

### Fase 2
Possível principal: Agentes Satélite.

Participação de Segurança para autenticação, autorização, secrets, permissões e policies.

### Fase 3
Possível principal: Owner da Tool.

Participação de Agentes Satélite como suporte técnico. O Owner determina a correção funcional.

### Fase 4
Possível principal: Agentes Satélite.

Participação de Owner da Tool para domínio e fronteiras funcionais.

### Fase 5
Possível principal: SRE/Operações.

Participação de Agentes Satélite e Owner da Tool.

### Fase 6
Possível principal: Agentes Satélite.

Participação de SRE/Operações e Owner da Tool.

### Fase 7
Multidisciplinar:
- Owner da Tool;
- Agentes Satélite;
- SRE/Operações;
- Segurança;
- Plataforma.
# 4. Princípios de avaliação, evidência e reprodução

## Evidência

Regra fundamental:

> **Um teste sem evidência verificável não pode ser marcado como PASS.**

Os estados de teste definidos são:

- PASS
- FAIL
- BLOCKED
- N/A

## Reprodutibilidade

A validação deve ser reproduzível. Por isso o processo exige:

- cenário;
- input;
- procedimento;
- resultado esperado;
- critério de aceite;
- resultado obtido;
- evidência;
- timestamp;
- ambiente;
- versão;
- status;
- observações.

## Thresholds

Thresholds de qualidade/performance devem ser definidos **antes da execução da avaliação**, e não escolhidos depois de observar os resultados.

Quando existir SLA/SLO da Tool, os testes devem usar os valores definidos no processo de entrada.

Não inventar um threshold universal quando o processo já define que o limite deve vir do contexto/owner.

## Independência do dataset

O dataset fornecido pelo time que criou/possui a Tool pode ser usado como referência e baseline, mas não deve ser a única fonte de avaliação do comportamento do agente.

A avaliação do agente deve contemplar, quando aplicável:

- team-provided;
- independent;
- positive;
- negative;
- hard-negative;
- no-tool;
- boundary;
- ambiguous;
- competing-tool;
- production-incident;
- regression.

A proveniência deve ser preservada.

## Hard negatives

Hard negatives são especialmente importantes porque uma nova Tool pode causar regressões na seleção de Tools já existentes.

Exemplo conceitual:

`getFutureAppointments`

não deve ser selecionada para uma pergunta como:

> "Quais compromissos eu tive na semana passada?"

Esse tipo de caso deve existir explicitamente no dataset.

## Dataset do time versus avaliação independente

O dataset do time pode refletir os casos ideais e conhecidos pelo próprio responsável da Tool. Isso pode deixar de fora:

- ambiguidades;
- casos fora de escopo;
- competição com outras Tools;
- no-tool;
- fronteiras;
- hard negatives;
- casos adversariais;
- comportamento inesperado observado em produção.

Por isso, para F4, recomenda-se combinar a base fornecida pelo time com casos independentes e casos derivados de produção/regressão.
# 5. Fase 1 — decisões e contexto

A Fase 1 é um **formulário**, não um runbook de execução.

Seu objetivo é preparar o pacote de entrada necessário para iniciar a certificação.

O formulário deve contemplar:

## Identificação da Tool

- Nome da Tool
- Descrição
- Owner / responsável técnico
- Time responsável
- Sistema / serviço de origem
- Ambiente disponível para validação
- Data de cadastro
- Versão

## Contrato técnico

### Input

- link para documentação oficial;
- schema;
- field;
- type;
- required;
- description;
- restrictions.

### Output

- link para documentação oficial;
- schema;
- field;
- type;
- required;
- description.

### Error handling

Devem ser definidos, pelo menos:

- invalid input;
- missing required field;
- nonexistent resource;
- unauthorized;
- dependency unavailable.

## Dependências

Tabela com:

- dependency;
- purpose;
- environment;
- owner.

## Pré-condições

- ambiente de teste disponível;
- credenciais de teste;
- dados de teste;
- dependências acessíveis;
- responsável técnico disponível;
- documentação atualizada.

## Critérios de aceite

Tabela com:

- ID;
- criterion;
- mandatory;
- expected evidence.

## Critérios de aceite das APIs downstream

Foi explicitamente decidido que não basta cadastrar as APIs usadas pelo MCP como dependências.

Devem existir também **critérios de aceite para as APIs utilizadas pelo MCP**, de modo que as condições downstream relevantes sejam verificáveis.

## Referências obrigatórias

- documentação da Tool;
- dataset de treinamento, quando aplicável;
- dataset de avaliação;
- dashboard principal do Datadog;
- outros links operacionais necessários.

## Validation Collection

A Collection é obrigatória na Fase 1 e será usada na Fase 2.

Deve conter chamadas ao MCP Server/Tool e seus resultados esperados.

Campos:

- ID;
- endpoint/tool;
- scenario;
- input;
- expected result.

Requisitos:

- executável em ambiente de teste;
- variáveis documentadas;
- nenhuma credencial exposta;
- resultado esperado para cada chamada;
- casos positivos;
- casos negativos;
- erros relevantes;
- versão;
- owner;
- atualização atual.

## Dataset

Estrutura:

| Caso | Tool esperada | Valores esperados | Justificativa |
|---|---|---|---|

Não criar um campo separado chamado "Parâmetros esperados".

Os valores esperados devem ficar em objeto chave/valor.

Exemplo:

```json
{
  "customer_id": "12345"
}
```

Categorias:

- positivos;
- negativos;
- hard negatives/confusão;
- contextuais;
- parametrização;
- no-tool.

## Gate da Fase 1

O pacote deve estar completo e pronto para iniciar a Fase 2.

Saída conceitual:

> **Pacote completo e pronto para iniciar a validação técnica.**
# 6. Fase 2 — decisões e contexto

A Fase 2 é exclusivamente técnica.

**O agente não participa da Fase 2.**

A pergunta é:

> **A Tool funciona tecnicamente conforme o contrato?**

A validação deve contemplar:

1. Pré-requisitos
2. Contrato técnico
3. Integração MCP
4. Segurança
5. Resiliência e tratamento de erros
6. Performance e capacidade
7. Observabilidade
8. Evidências e registro
9. Gate
10. Modelo de caso de teste
11. Automação futura

## Contrato técnico

Validar:

- required fields;
- tipos;
- restrições;
- invalid values;
- output;
- no-data;
- erros.

## Integração MCP

Validar:

- `tools/list`;
- discovery;
- schema;
- chamada MCP;
- argumentos;
- erros;
- consistência entre chamada direta e chamada via MCP.

Diferenças inexplicadas entre chamada direta e MCP são falhas.

## Segurança

Validar:

- autenticação;
- autorização;
- dados sensíveis;
- secrets;
- permissões;
- policies;
- OPA.

Fluxo conceitual de OPA:

1. avaliar policy;
2. registrar policy input;
3. registrar decisão;
4. registrar evidência.

Violação crítica de policy impede aprovação.

## Resiliência

Validar:

- timeout;
- dependência indisponível;
- resposta inválida;
- retry;
- idempotência para operações mutáveis;
- erros de autenticação/autorização quando aplicável.

## Performance

Medir:

- média;
- mediana;
- P95;
- P99;
- máximo;
- error rate;
- concorrência;
- throughput;
- degradação.

Os limites devem vir do SLA/SLO definido anteriormente.

## Observabilidade

Trace conceitual:

`MCP Client → MCP Server → Tool → Dependency`

## Gate

A Fase 2 só é aprovada quando:

- todas as seções aplicáveis foram executadas;
- critérios foram atendidos;
- evidências foram registradas;
- não existem falhas críticas/bloqueantes sem tratamento.

Saída:

> **APROVADO PARA FASE 3**
# 7. Fase 3 — decisões e contexto

A Fase 3 também **não envolve o agente**.

Pergunta:

> **A Tool funciona corretamente do ponto de vista funcional e de negócio?**

Seções:

1. Objetivo
2. Escopo
3. Pré-condições
4. Preparação dos cenários
5. Casos positivos / happy path
6. Casos negativos
7. Casos de fronteira
8. Hard negatives / fronteiras funcionais
9. Validação de parâmetros
10. Validação do resultado funcional
11. Consistência
12. Cobertura do dataset
13. Registro dos testes
14. Classificação
15. Gate

## Hard negative na Fase 3

Na Fase 3, hard negative não é usado para medir a decisão do agente.

Ele é usado para definir objetivamente a **fronteira funcional da Tool**.

Exemplo conceitual:

- caso plausível;
- parece pertencer à Tool;
- porém pertence a outra Tool ou está fora do escopo.

A F3 registra essa fronteira.

A F4 posteriormente usa essa fronteira para avaliar a decisão do agente.

## Resultado funcional

Validar:

- conteúdo;
- quantidades;
- filtros;
- ordenação;
- cálculos;
- datas;
- valores;
- relações entre campos;
- ausência de dados.

O fato de a API responder HTTP 200 não significa que o teste funcional passou.

A resposta deve estar correta segundo as regras de negócio.

## Gate

Aprovar somente quando:

- casos obrigatórios executados ou formalmente bloqueados;
- positivos corretos;
- negativos corretos;
- fronteiras corretas;
- hard negatives definem claramente as fronteiras;
- parâmetros corretos;
- resultados corretos;
- evidências completas;
- nenhum erro funcional crítico não tratado.

Saída:

> **Contrato funcional da Tool validado, incluindo a fronteira funcional.**
# 8. Fase 4 — decisões e contexto

A Fase 4 é a **primeira fase que envolve o agente**.

Pergunta:

> **O agente sabe quando e como usar a Tool?**

Validações:

1. Seleção da Tool
2. No-Tool
3. Desambiguação
4. Construção dos parâmetros
5. Execução da Tool
6. Uso do resultado
7. Cenários negativos
8. Casos de fronteira
9. Hard negatives
10. End-to-End

## Seleção

Validar se o agente reconhece a intenção e escolhe a Tool correta.

Testar:

- casos claros;
- paraphrases;
- variações semânticas.

Evidências:

- input;
- intenção esperada;
- Tool esperada;
- Tool real;
- trace/log;
- versão do agente/modelo.

## No-Tool

Validar que o agente não chama Tools desnecessariamente.

Casos:

- pergunta que pode ser respondida sem Tool;
- fora do domínio;
- informação insuficiente para uma chamada segura;
- cenários nos quais uma chamada seria especulativa.

Se `Expected Tool = NONE`, não deve haver chamada inadequada.

## Desambiguação

Usar Tools semanticamente próximas e as fronteiras funcionais definidas na F3.

## Parâmetros

Validar:

- required;
- optional;
- defaults;
- tipos;
- formatos;
- datas;
- IDs;
- filtros;
- quantidades;
- combinações.

Os parâmetros precisam ser corretos, completos, necessários e compatíveis com o contrato.

## Execução

Validar:

- Tool correta;
- payload correto;
- número de chamadas;
- ordem/sequence;
- ausência de chamadas duplicadas ou especulativas.

## Uso do resultado

Testar:

- resultado conhecido;
- múltiplos resultados;
- resultado vazio;
- resultado parcial;
- campos opcionais.

O agente não pode inventar dados.

## Negativos

Exemplos:

- parâmetro inválido;
- required ausente;
- recurso inexistente;
- resposta vazia;
- erro da Tool/API;
- timeout/unavailability quando aplicável.

O agente deve seguir o comportamento definido e não inventar parâmetros ou resultados.

## Fronteiras

Reutilizar fronteiras da F3.

Testar:

- abaixo;
- exatamente no limite;
- acima.

O agente não deve ajustar silenciosamente o input, salvo se isso estiver explicitamente definido.

## Hard negatives

Na F4, finalmente se avalia a **decisão do agente** em casos plausíveis de confusão.

## End-to-End

Fluxo:

`Intent → Tool Selection → Parameters → Execution → Result → Final Response`

A resposta final correta não compensa uma Tool ou parâmetro incorreto.

## Métricas

- Tool Selection Accuracy
- Parameter Accuracy
- No-Tool Accuracy
- Tool Call Accuracy
- Result Usage Accuracy
- End-to-End Accuracy

Segmentar por:

- Happy Path;
- Negative;
- Boundary;
- Hard Negative;
- No-Tool;
- Ambiguous.

Thresholds devem existir antes da execução.

## Falhas e roteamento

- erro funcional da Tool → voltar à F3;
- erro técnico/API → voltar à F2;
- Tool errada → F4 seleção/desambiguação;
- parâmetro errado → F4 parameter construction;
- chamada desnecessária → F4 No-Tool/execution;
- resultado correto, resposta final errada → F4 result usage;
- dado inventado → F4 result usage/negative.

Saída:

> **Agente demonstrou capacidade de utilizar a Tool corretamente.**
# 9. Fase 5 — decisões e contexto

A Fase 5 é de **operacionalização**, não de repetição das validações anteriores.

Pergunta:

> **Conseguimos operar e observar a Tool continuamente?**

Ela transforma os requisitos e sinais definidos anteriormente em:

- logs;
- métricas;
- traces;
- dashboards;
- alertas;
- SLO/SLA;
- runbook;
- ownership;
- escalonamento;
- retenção;
- monitoramento do uso pelo agente;
- testes de incidente.

## Pré-requisitos

- Fases 1–4 aprovadas;
- owner definido;
- SLA/SLO quando aplicável;
- dependências conhecidas;
- ferramentas de observabilidade;
- acesso ao Datadog;
- ambiente de produção/equivalente;
- estratégia de logs/métricas/tracing.

## Logs

Devem permitir reconstruir uma ocorrência sem exposição indevida de dados.

## Métricas

- volume;
- sucesso/erro;
- latência;
- p95;
- p99;
- disponibilidade;
- timeout;
- retry;
- frequência de seleção;
- falhas após seleção.

## Tracing

Fluxo:

`Agente → Tool → API/Dependência → Resposta → Agente`

## Dashboard

O dashboard principal deve permitir visualizar:

- volume;
- sucesso/erro;
- latência;
- p95/p99;
- timeout;
- retry;
- disponibilidade;
- uso pelo agente.

O Datadog foi definido como referência principal de observabilidade no formulário.

## Alertas

- picos de erro;
- degradação de latência;
- downtime;
- timeout;
- anomalias de volume.

O alerta deve chegar ao responsável correto e apontar para o procedimento de resposta.

## SLO/SLA

Indicadores críticos devem possuir medição e, quando necessário, alertamento.

## Runbook operacional

Deve permitir que alguém que não implementou a Tool consiga iniciar a investigação.

## Ownership e escalonamento

Devem existir:

- owner;
- time;
- canal;
- responsável pelo monitoramento;
- caminho de escalonamento.

## Retenção e acesso

Definir:

- retenção;
- permissões;
- acesso a logs;
- acesso a métricas;
- acesso a traces.

## Monitoramento do agente

Monitorar:

- frequência de seleção;
- operações;
- sucesso/erro;
- latência;
- mudanças/anomalias no uso.

## Qualidade operacional

Monitorar:

- fallbacks;
- no-result;
- mudança na distribuição de seleção;
- outras alterações relevantes.

Mudanças relevantes devem gerar investigação e, se necessário, reexecução de avaliações.

## Incident Test

Fluxo:

`Falha → Métrica → Dashboard → Alerta → Owner → Investigação → Escalonamento`

O fluxo deve ser testado antes de depender dele em produção.

Saída:

> **Capacidade operacional e observabilidade implementadas.**
# 10. Fase 6 — decisões e contexto

A Fase 6 foi adicionada entre F5 e F7.

Sua finalidade é o **rollout efetivo da Tool em produção**.

Descrição consolidada:

> A Fase 6, Rollout da Tool, tem o objetivo de introduzir a ferramenta em produção de forma controlada, gradual e reversível. Aqui definimos estratégia de exposição, aumento gradual, critérios de GO/HOLD/ROLLBACK, monitoramento de erros, latência, volume, falhas de parâmetros e comportamento do agente, além de um plano de rollback, com responsáveis e evidências. Quando concluído e aprovado, o rollout termina e a Tool avança para a Fase 7, de revisão e ciclo de vida.

## Distinção F5 x F6

**F5:** prepara e operacionaliza a observabilidade.

**F6:** utiliza essa capacidade para disponibilizar a Tool em produção e controlar sua exposição.

## Estrutura conceitual atual

1. Preparação para o Rollout
2. Estratégia de Rollout
3. Configuração e Disponibilização
4. Validação do Canary / Primeira Exposição
5. Expansão Gradual da Exposição
6. Monitoramento do Comportamento do Agente
7. Avaliação de Performance e Capacidade
8. Gestão de Incidentes durante o Rollout
9. Rollback
10. Conclusão do Rollout
11. Transição para a Fase 7

### Estado importante dos artefatos

O **Markdown atual e o PDF atualmente gerado da Fase 6 possuem 10 seções**, não 11.

O conteúdo oficial atualmente utilizado para o PDF é o arquivo:

`/mnt/data/Fase_6_Runbook_Rollout_Tool.md`

Ele possui a seção 10 "Conclusão do Rollout" e não possui uma seção separada 11 "Transição para a Fase 7".

A estrutura de 11 seções acima é uma decisão conceitual registrada durante a evolução do processo, mas ainda não foi aplicada ao documento atual.

## Critérios de rollout

A estratégia deve definir:

- público inicial;
- percentual inicial;
- etapas;
- duração;
- critérios de GO;
- critérios de HOLD;
- critérios de ROLLBACK;
- responsáveis.

Exemplo:

`Certificação → Deploy → 0% → Canary → 10% → 25% → 50% → 100%`

Os percentuais dependem do risco/contexto.

## GO / HOLD / ROLLBACK

**GO:** métricas dentro dos limites.

**HOLD:** sinal de degradação que exige investigação, mas ainda não caracteriza rollback.

**ROLLBACK:** condição crítica predefinida.

Não avançar sem GO explícito conforme os critérios definidos.

## Comportamento do agente durante rollout

Monitorar:

- frequência de seleção;
- chamadas inadequadas;
- chamadas esperadas ausentes;
- falhas de parâmetros;
- erros;
- uso incorreto dos resultados;
- interação com outras Tools;
- chamadas desnecessárias.

## Performance

Monitorar:

- latência;
- P50;
- P95;
- P99;
- throughput;
- timeout;
- retry;
- recursos;
- limites de dependências;
- capacidade do MCP Server;
- capacidade das APIs.

## Rollback

Deve existir mecanismo para:

- desabilitar;
- restaurar configuração;
- restaurar versão anterior quando aplicável;
- remover exposição;
- verificar comportamento do agente;
- verificar recuperação de dependências;
- comunicar;
- registrar a operação.

## Conclusão

A conclusão exige:

- nível planejado atingido;
- métricas dentro dos limites;
- ausência de incidentes críticos abertos;
- observabilidade ativa;
- rollback disponível;
- evidências registradas;
- aprovação formal.

Saída:

> **Tool em produção no nível planejado, com rollout concluído e aprovado.**
# 11. Fase 7 — decisões e contexto

A pergunta central é:

> **A Tool continua válida ao longo do tempo?**

A Fase 7 ocorre:

- periodicamente;
- após mudanças relevantes;
- após incidentes relevantes.

Ela é um ciclo de lifecycle e feedback.

## Triggers

- mudança de contrato;
- mudança de API;
- mudança de schema;
- mudança de regra de negócio;
- mudança de segurança;
- mudança de roles;
- rotação de secrets;
- expiração de secrets;
- revogação de secrets;
- mudança de dependências;
- mudança no MCP;
- mudança no agente/modelo;
- degradação de performance;
- incidente relevante;
- mudança de observabilidade;
- evolução do dataset.

## Verificação de mudanças

Comparar a situação atual com a última versão validada usando:

- histórico;
- releases;
- documentação;
- PRs;
- infraestrutura;
- configurações;
- políticas;
- secrets.

Toda mudança relevante deve ser identificada, registrada e classificada.

## Análise de impacto

Classificar:

- Sem impacto;
- Parcial;
- Amplo;
- Crítico.

Dimensões:

- Técnico;
- Segurança;
- Funcional;
- Agente;
- Performance;
- Observabilidade;
- Dados;
- Dependências.

Deve existir registro do impacto e das fases potencialmente afetadas.

## Revalidação técnica

Impacto técnico → executar testes afetados da F2.

Exemplos:

- contrato;
- MCP;
- segurança;
- resiliência;
- performance;
- observabilidade.

## Revalidação funcional

Impacto funcional → executar testes afetados da F3.

Exemplos:

- regras de negócio;
- fronteiras;
- parâmetros;
- resultados;
- hard negatives funcionais.

## Revalidação do agente

Impacto no uso pelo agente → executar testes afetados da F4.

Exemplos:

- seleção;
- No-Tool;
- desambiguação;
- parâmetros;
- execução;
- uso do resultado;
- regressão.

## Regressão

Executar cenários críticos e representativos.

Nenhuma regressão crítica pode permanecer sem:

- correção;
- rollback;
- bloqueio;
- exceção formalmente aceita.

## Segurança, Secrets e Permissões

Verificar:

- autenticação;
- autorização;
- roles;
- policies;
- secrets;
- tokens;
- certificados;
- permissões MCP;
- princípio do menor privilégio.

### Secret Breaking

O termo foi explicitamente incluído como ponto de atenção no contexto da Tool.

Avaliar eventos que possam interromper ou alterar a integração:

- expiração;
- rotação;
- revogação;
- alteração;
- credencial inválida;
- quebra de acesso.

## Produção

Usar os sinais definidos na F5:

- volume;
- sucesso/erro;
- latência;
- P95/P99;
- timeouts;
- retries;
- disponibilidade;
- erros de dependência;
- uso pelo agente;
- distribuição de seleção;
- incidentes.

## Análise de incidentes

Para cada incidente perguntar:

- estava coberto pelo dataset?
- qual foi a causa?
- foi técnico, funcional ou relacionado ao agente?
- precisa de novo caso de teste?
- alguma fase precisa ser reexecutada?

## Evolução do dataset

Adicionar casos originados de:

- novos comportamentos;
- novas regras;
- novas fronteiras;
- hard negatives;
- incidentes de produção;
- confusão entre Tools;
- regressões.

Preservar proveniência:

- `team-provided`
- `independent`
- `production-incident`
- `regression`
- `hard-negative`

## Ações conforme mudança

| Detecção | Ação |
|---|---|
| Nenhuma mudança relevante | Registrar revisão e continuar |
| Apenas documentação | Atualizar documentação |
| Mudança técnica isolada | Reexecutar testes afetados da F2 |
| Mudança de regra de negócio | Reexecutar F3 |
| Mudança na interface do agente | Reexecutar F4 |
| Mudança de segurança | Revalidar segurança/permissões |
| Mudança de secret | Validar credenciais/acesso/integração |
| Degradação de performance | Investigar/revalidar |
| Novo incidente | Analisar e adicionar regressão quando aplicável |
| Mudança ampla | Reexecutar múltiplas fases |
| Regressão crítica | Bloquear/rollback |
| Tool não atende mais à necessidade | Avaliar substituição/depreciação |

## Decisão de ciclo de vida

Decisões possíveis:

- **KEEP** — manter em operação
- **UPDATE** — atualizar
- **REVALIDATE** — executar novamente as fases necessárias
- **DEPRECATE** — descontinuar
- **REPLACE** — substituir por outra solução

## Critérios de aceite

- revisão executada;
- mudanças identificadas;
- análise de impacto registrada;
- fases afetadas revalidadas;
- regressão executada;
- segurança/permissões/secrets avaliados;
- métricas de produção analisadas;
- incidentes analisados;
- dataset atualizado quando necessário;
- evidências registradas;
- decisão de ciclo de vida registrada;
- ações possuem responsáveis e prazos.

## Registro da revisão

Campos:

- Data;
- Versão avaliada;
- Motivo da revisão;
- Mudanças identificadas;
- Impacto;
- Fases reexecutadas;
- Resultado da regressão;
- Incidentes relacionados;
- Dataset atualizado?;
- Decisão;
- Ações;
- Responsáveis;
- Prazo;
- Evidências.

## Princípio do ciclo

```text
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

Saída:

> **TOOL MANTIDA, ATUALIZADA, REVALIDADA OU DESCONTINUADA CONFORME A NECESSIDADE.**
# 12. One-page — especificação completa atual

Título:

**Roadmap de Certificação e Ciclo de Vida de Tools para o Agente**

Subtítulo:

> Da definição à operação contínua, com validação técnica, funcional e do uso pelo agente, observabilidade, rollout e revisão ao longo do tempo.

Cada fase deve apresentar:

- número;
- título;
- objetivo;
- principais atividades;
- **Saída**;
- **Responsáveis desta fase**.

A seção **Responsáveis desta fase** deve estar vazia.

Não colocar nomes, símbolos ou ícones dentro dela.

A legenda inferior pode conter:

- 👤 Owner da Tool
- 🤖 Agentes Satélite
- 📈 SRE/Operações
- 🔒 Segurança
- 🟣 Plataforma

Fluxo:

`1 → 2 → 3 → 4 → 5 → 6 → 7`

Agrupamento:

- Certificação: F1–F4
- Entrada em produção: F5–F6
- Ciclo de vida: F7

Decisões do lifecycle:

- KEEP
- UPDATE
- REVALIDATE
- DEPRECATE
- REPLACE

## Saídas

**F1:** Pacote completo e pronto para iniciar a validação técnica.

**F2:** Tool tecnicamente aprovada.

**F3:** Contrato funcional da Tool validado, incluindo fronteira funcional.

**F4:** Agente demonstrou capacidade de utilizar a Tool corretamente.

**F5:** Capacidade operacional e observabilidade implementadas.

**F6:** Tool em produção no nível planejado, com rollout concluído e aprovado.

**F7:** Tool mantida, atualizada, revalidada ou descontinuada conforme necessidade.
# 13. Notas pessoais / backlog — não misturar automaticamente aos documentos oficiais

Estas são pendências/ideias pessoais e devem continuar separadas dos documentos oficiais até que haja decisão explícita de incorporá-las.

1. Revisar a documentação MCP existente para identificar o que já está disponível e quais campos/lacunas precisam ser adicionados ao formulário.
2. Abrir um ticket/chamado formal para o onboarding, controlando SLA entre criação/submissão do formulário, revisão, correção, aprovação e início da fase.
3. Levar o roadmap/processo já construído pelo time para uma revisão conjunta antes da formalização, decidindo o que adicionar, remover ou alterar.
4. Criar um run recorrente dos tickets de onboarding, possivelmente diário, com os estágios e checks que as pessoas precisam executar.
5. Garantir que o dataset tenha positivos, negativos, hard negatives/confusão e no-tool, especialmente para evitar regressões na seleção de Tools existentes quando uma nova Tool for adicionada.
6. Adicionar na Fase 1 os links para dataset de treinamento, documentação da Tool e dashboard principal do Datadog.
7. Estudar e utilizar OPA para verificação das políticas de segurança das APIs utilizadas pelo MCP.
8. Estudar a criação de uma Skill no Devin para automatizar partes da validação, incluindo Fase 1 e posteriormente outras fases.
9. Tornar obrigatória a Validation Collection contendo chamadas às APIs/MCP Server/Tool e resultados esperados para uso na Fase 2.
10. Documentar o processo de geração do dataset, tanto qualitativamente quanto quantitativamente.
11. Incluir "Secret Breaking" no contexto da role da Tool, cobrindo expiração, rotação, revogação, alteração, credencial inválida e quebra de acesso.
# 14. Automação futura

O processo foi pensado desde o início para permitir automação posterior.

## Fase 1 → Fase 2

Artefatos:

- contrato;
- collection;
- critérios de aceite;
- documentação.

Fluxo:

```text
Phase 1 artifacts
  ↓
Contract + Collection + Acceptance Criteria + Documentation
  ↓
Test executor
  ↓
Results
  ↓
Comparison with criteria
  ↓
Evidence
  ↓
Phase 2 report
```

Itens candidatos à automação:

- schema validation;
- execução da Collection;
- comparação de output;
- MCP discovery;
- validação de argumentos;
- negative cases;
- métricas;
- consultas de observabilidade;
- consolidação de evidências;
- geração de relatório.

A aprovação final continua subordinada às regras de governança definidas pela equipe.

## Automação de avaliação do agente

A F4 pode futuramente usar:

- dataset versionado;
- execução automatizada;
- traces;
- métricas;
- judge/evaluator;
- análise de Tool selection;
- análise de parâmetros;
- análise de resultado;
- regressão automática.

O processo não deve depender exclusivamente de um único modelo/judge sem validação da qualidade do próprio evaluator.

## Devin / Skills

É uma linha de investigação registrada no backlog pessoal para automatizar partes do onboarding e validação.
# 15. Histórico de decisões e mudanças de estrutura

## Adição da Fase 6 — Rollout

Inicialmente existiam 6 fases, e a última era "Revisão, Revalidação e Ciclo de Vida".

Foi adicionada uma nova fase entre Operação/Observabilidade e Lifecycle:

**Fase 6 — Rollout da Tool**

Consequentemente:

- a antiga Fase 6 de lifecycle tornou-se Fase 7;
- o lifecycle passou a ser explicitamente posterior ao rollout;
- o rollout passou a ter seu próprio gate, estratégia de exposição e rollback.

## F5 versus F6

Foi discutido se F5 seria apenas uma preparação para monitoramento.

A decisão foi:

- F5 é **operacionalização** de observabilidade e monitoramento;
- F6 é **entrada/rollout efetivo em produção**.

F5 não deve ser descrita apenas como "preparação para F6", porque ela entrega capacidade operacional real.

## F7 versus teste

A F7 não é apenas uma nova execução das Fases 2–4.

Ela:

- identifica mudanças;
- classifica impacto;
- determina quais fases precisam ser reexecutadas;
- incorpora incidentes ao dataset;
- cria regressões;
- revisa segurança;
- revisa secrets;
- revisa produção;
- decide o lifecycle.

## Hard negatives

Foi estabelecido que hard negatives têm dois papéis diferentes:

### F3
Definem a fronteira funcional da Tool.

### F4
Avaliam se o agente respeita essa fronteira e escolhe a Tool correta.

Essa distinção deve ser preservada.

## Dataset do time

Foi decidido que o dataset fornecido pelo time da Tool não deve ser considerado suficiente para avaliar o agente.

Ele é uma fonte de referência/base, mas deve ser complementado com casos independentes e casos derivados de fronteiras, ambiguidades, no-tool, competição e produção.

## Ownership

Foi decidido não preencher owners no one-page.

A seção "Responsáveis desta fase" permanece vazia.

A legenda de possíveis papéis permanece permitida.

## Nomenclatura

O time do agente/MCP deve ser chamado:

> **Agentes Satélite**

"Plataforma" permanece como papel separado na legenda inferior quando fizer sentido.

## "Saída" versus "Entregas da fase"

Foi definido que a seção do one-page deve ser chamada:

> **Saída**

e não "Entregas da fase".
# 16. Estado dos artefatos e arquivos

## Markdown oficial/corrente

### Fase 1
`/mnt/data/md_fielmente_pdf/Formulario_Fase_1_Cadastro_e_Contrato_Nova_Tool_Com_Collection.md`

Esse Markdown foi criado para preservar fielmente o conteúdo textual do PDF correspondente à Fase 1 com Collection.

### Fase 2
`/mnt/data/md_fielmente_pdf/Runbook_Fase_2_Validacao_Tecnica_Tool.md`

### Fase 3
`/mnt/data/md_fielmente_pdf/Runbook_Fase_3_Validacao_Funcional_Tool.md`

### Fase 4
`/mnt/data/md_fielmente_pdf/Runbook_Fase_4_Avaliacao_Uso_Tools_Agente.md`

### Fase 5
`/mnt/data/md_fielmente_pdf/Runbook_Fase_5_Operacao_Observabilidade_Monitoramento_Tool.md`

### Fase 6
`/mnt/data/Fase_6_Runbook_Rollout_Tool.md`

### Fase 7
`/mnt/data/Fase_7_Runbook_Revisao_Revalidacao_Ciclo_de_Vida_Tool.md`

Também existe uma cópia gerada com nome final:

`/mnt/data/Runbook_Fase_7_Revisao_Revalidacao_Ciclo_de_Vida_Tool.md`

## PDFs

### Fase 1
`/mnt/data/Formulario_Fase_1_Cadastro_e_Contrato_Nova_Tool_Com_Collection.pdf`

Também existem versões anteriores:

- `/mnt/data/Formulario_Fase_1_Cadastro_e_Contrato_Nova_Tool.pdf`
- `/mnt/data/Formulario_Fase_1_Cadastro_e_Contrato_Nova_Tool_Atualizado.pdf`

A versão com Collection é a versão mais relevante para o estado atual.

### Fase 2
`/mnt/data/Runbook_Fase_2_Validacao_Tecnica_Tool.pdf`

### Fase 3
`/mnt/data/Runbook_Fase_3_Validacao_Funcional_Tool.pdf`

### Fase 4
`/mnt/data/Runbook_Fase_4_Avaliacao_Uso_Tools_Agente.pdf`

### Fase 5
`/mnt/data/Runbook_Fase_5_Operacao_Observabilidade_Monitoramento_Tool.pdf`

### Fase 6
`/mnt/data/Runbook_Fase_6_Rollout_Tool.pdf`

Esse PDF foi gerado a partir do Markdown atual da Fase 6.

### Fase 7
`/mnt/data/Runbook_Fase_7_Revisao_Revalidacao_Ciclo_de_Vida_Tool.pdf`

Esse PDF foi gerado a partir do Markdown atual da Fase 7.

## ZIP

Existe:

`/mnt/data/PDFs_Originais_e_Fase_6_Rollout.zip`

Ele contém os PDFs F1–F5 e o PDF F6 Rollout.

Como o F7 foi gerado posteriormente, esse ZIP ainda não contém o F7.

## Artefato histórico

Existe um PDF antigo da lifecycle:

`Runbook_Fase_6_Revisao_Revalidacao_Ciclo_de_Vida_Tool.pdf`

Ele foi criado quando lifecycle ainda era Fase 6.

O arquivo existe no histórico/Library e não deve ser confundido com a numeração atual.

O conteúdo atual do lifecycle corresponde à **Fase 7**.
# 17. Regras para continuar este trabalho

Um agente que assumir este documento deve preservar estas regras:

1. Não misturar F2/F3 com F4.
2. F2 e F3 não usam o agente.
3. F4 é a primeira fase que avalia o agente.
4. F5 operacionaliza observabilidade e monitoramento.
5. F6 executa rollout.
6. F7 mantém a Tool válida ao longo do tempo.
7. Não transformar F7 em simples repetição integral das Fases 2–4.
8. Reexecutar apenas as fases afetadas pelo impacto, salvo mudança ampla/crítica.
9. Evidência é obrigatória para PASS.
10. Thresholds devem ser definidos antes da avaliação.
11. Dataset do time da Tool não é fonte única da avaliação do agente.
12. Hard negatives são essenciais para prevenir regressões de Tool selection.
13. Na F3, hard negative define fronteira funcional.
14. Na F4, hard negative avalia decisão do agente.
15. No-tool precisa ser explicitamente avaliado.
16. Os valores esperados do dataset ficam em objeto chave/valor; não criar campo separado "Parâmetros esperados".
17. Validation Collection é obrigatória.
18. Critérios de aceite das APIs downstream usadas pelo MCP também fazem parte do contrato de entrada.
19. OPA faz parte da linha de validação de segurança.
20. Secret Breaking deve ser tratado como risco de lifecycle/integridade da integração.
21. Owners reais ainda não foram definidos.
22. No one-page, "Responsáveis desta fase" fica vazio.
23. A legenda pode conter Owner da Tool, Agentes Satélite, SRE/Operações, Segurança e Plataforma.
24. Usar "Agentes Satélite" para o time de agente/MCP.
25. Usar "Saída" no one-page.
26. Não inventar informações de domínio, SLA, owners, thresholds ou contratos que não estejam definidos.
27. Não considerar uma resposta HTTP 200 como evidência suficiente de correção funcional.
28. Uma resposta final correta do agente não compensa Tool selection ou parâmetros incorretos.
29. Alterações relevantes devem passar por análise de impacto antes de decidir quais fases reexecutar.
30. Incidentes relevantes devem alimentar o processo de regressão/dataset quando aplicável.
31. O processo deve manter rastreabilidade entre versão, teste, evidência, resultado e decisão.
32. Não apagar decisões históricas só porque uma estrutura posterior foi adotada; quando uma decisão antiga ainda explica o estado atual, registrá-la como histórico.
# 18. Conteúdo integral dos documentos oficiais

A partir deste ponto, os documentos abaixo são incorporados **sem sumarização** para que o handoff contenha o conteúdo necessário para continuidade.

Eles são tratados como os conteúdos documentais de referência das respectivas fases.

---

# Fase 1 — Formulário de Cadastro e Contrato — CONTEÚDO INTEGRAL

```markdown
                   Fase 1 — Cadastro e Contrato da Nova Tool
Formulário de onboarding — versão atualizada com Collection de Validação


1. Identificação da Tool
Campo                      Orientação                                                Exemplo / resposta

Nome da Tool               Nome oficial da ferramenta.                               Ex.: getFutureAppointments

Tool ID                    Identificador único no MCP/catálogo.                      Ex.: appointments.get_future

MCP responsável            MCP que disponibiliza a tool.                             Nome/ID oficial.

Equipe responsável         Time responsável pela manutenção.                         Nome do time/squad.

Owner técnico              Responsável técnico e contato.                            Nome + canal.

Versão                     Versão proposta para disponibilização.                    Ex.: v1.0.0



2. Descrição Funcional
Campo                      Orientação                                                Exemplo / resposta

O que a Tool faz           Descreva objetivamente a função e o resultado entregue.   Evite descrições genéricas.

Objetivo / caso de uso     Principal cenário de negócio.                             Inclua exemplos de solicitações.



3. Escopo e Não Escopo
Campo                      Orientação                                                Exemplo / resposta

Quando usar                Solicitações que devem utilizar a tool.                   Inclua exemplos positivos.

Quando não usar            Solicitações em que não deve ser chamada.                 Inclua casos fora do escopo e hard
                                                                                     negatives.

Tools relacionadas         Tools que podem competir ou ser confundidas.              Explique a fronteira entre elas.



4. Contrato de Entrada
Campo                      Orientação                                                Exemplo / resposta

Parâmetros                 Nome, tipo, formato, restrições e descrição.              Conforme schema oficial.

Obrigatoriedade            Obrigatórios e opcionais.                                 Não deixe implícito.

Exemplo válido             Payload completo válido.                                  Inclua valores representativos.

Exemplo inválido           Entrada que deve ser rejeitada/tratada.                   Descreva o comportamento
                                                                                     esperado.



5. Contrato de Saída
Campo                      Orientação                                                Exemplo / resposta

Estrutura                  Campos, tipos, obrigatoriedade e significado.             Inclua schema da resposta.

Exemplo de sucesso         Resposta completa representativa.                         Use dados fictícios quando
                                                                                     necessário.

Ausência de dados          Comportamento quando não há informação.                   Diferencie ausência de dados de
                                                                                     erro.

Erros                      Erros possíveis e estrutura.                              Inclua códigos/mensagens.

6. Dependências, Pré-condições e Critérios de Aceite
Campo                         Orientação                                                           Exemplo / resposta

APIs / dependências           APIs, serviços, bancos e componentes usados.                         Informe finalidade.

Pré-condições                 Condições necessárias antes da chamada.                              Ex.: autenticação, identificação,
                                                                                                   permissão.

Critérios de aceite das       Condições mínimas para cada dependência.                             Ex.: disponibilidade, latência,
dependências                                                                                       timeout, códigos e autenticação.

Indisponibilidade             Comportamento quando dependência falhar.                             Timeout, erro estruturado e retry
                                                                                                   quando aplicável.



7. Referências e Links Operacionais
Campo                         Orientação                                                           Exemplo / resposta

Link para documentação        URL da documentação oficial e atualizada.                            URL: _______________________
                                                                                                   ___________

Link para dataset de          URL/localização do dataset de treinamento ou ajuste, quando          URL: _______________________
treinamento                   aplicável.                                                           ___________

Link para observabilidade —   URL do dashboard principal do Datadog.                               URL: _______________________
Datadog                                                                                            ___________



8. Collection de Validação — Obrigatória
Campo                         Orientação                                                           Exemplo / resposta

Collection                    Entregar uma collection executável contendo chamadas                 Preferencialmente
                              representativas das APIs/tools do servidor MCP.                      Postman/Insomnia ou formato
                                                                                                   equivalente.

Link da Collection            Informe um link compartilhado para acesso à collection. Pode ser     URL: _______________________
                              Drive ou repositório corporativo, desde que acessível à equipe       ___________
                              certificadora.

Formato                       Informe o formato e ferramenta utilizada.                            Ex.: Postman Collection v2.1 /
                                                                                                   Insomnia.

Versão                        Versão da collection utilizada na entrega.                           Ex.: v1.2.

Responsável                   Pessoa/time responsável por manter a collection atualizada.          Nome + contato.

Última atualização            Data da última atualização da collection.                            Data: ____/____/______

Chamadas incluídas            A collection deve conter chamadas suficientes para cobrir os         Incluir inputs válidos, inválidos e
                              principais contratos e cenários da tool.                             casos relevantes.

Resultado esperado            Cada chamada deve possuir o resultado esperado claramente            Documentar response esperada,
                              definido, permitindo comparação objetiva durante a Fase 2.           status/código e comportamento.

Reprodutibilidade             As chamadas devem poder ser executadas pela equipe                   Não utilizar credenciais pessoais
                              certificadora em ambiente de teste, com variáveis e credenciais de   ou dados reais desnecessários.
                              teste documentadas.



9. Versionamento e Ciclo de Vida
Campo                         Orientação                                                           Exemplo / resposta

Estratégia de versionamento   Como versões serão identificadas e mantidas.                         Ex.: versionamento semântico.

Breaking changes              O que é breaking change e como será tratado.                         Inclua revalidação.

Depreciação                   Como versões serão descontinuadas.                                   Prazo, comunicação e
                                                                                                   substituição.

10. Governança e Suporte
Campo                       Orientação                                                           Exemplo / resposta

Owner de negócio            Responsável pelo domínio de negócio.                                 Nome/time.

Canal de suporte            Onde incidentes e dúvidas serão tratados.                            Canal ou sistema de chamados.

Aprovação de mudanças       Responsáveis por aprovar alterações relevantes.                      Defina critérios.

Revalidação                 Quando uma alteração exige nova certificação.                        Ex.: contrato, dependência ou
                                                                                                 comportamento.



11. Dataset de Avaliação da Tool
Campo                       Orientação                                                           Exemplo / resposta

Caso                        Interação avaliada: pergunta do cliente + contexto necessário.       Ex.: Cliente 12345 pergunta:
                                                                                                 “Quais são meus próximos
                                                                                                 compromissos?”

Tool esperada               Tool que deveria ser chamada; use “None” se nenhuma deve ser         Ex.: getFutureAppointments ou
                            chamada.                                                             None.

Valores esperados           Objeto chave-valor com os valores que devem ser enviados na          Ex.: {"customer_id":"12345"}
                            chamada.

Justificativa               Por que a tool deve/não deve ser chamada e por que esses valores     Explique de forma determinística.
                            são esperados.

Tipos de casos              Cubra positivos, negativos, hard negatives, competição e contexto.   Ex.: compromissos passados →
                                                                                                 None se a tool só consulta futuros.



12. Checklist de Completude — Gate para Fase 2
Campo                       Orientação                                                           Exemplo / resposta

Contrato completo           Campos obrigatórios preenchidos e consistentes.                      ■ Sim ■ Não

Documentação                Link válido e atualizado.                                            ■ Sim ■ Não

Collection disponível       Collection executável, com chamadas e resultados esperados.          ■ Sim ■ Não

Dependências                APIs e critérios de aceite definidos.                                ■ Sim ■ Não

Observabilidade             Dashboard principal do Datadog informado.                            ■ Sim ■ Não

Dataset de avaliação        Casos positivos, negativos e confusão, com valores esperados.        ■ Sim ■ Não

Governança                  Owners, suporte e mudanças definidos.                                ■ Sim ■ Não

Aprovação para Fase 2       Formulário revisado e apto para validação técnica.                   ■ Aprovado ■ Reprovado


Regra de passagem: a Fase 2 só inicia quando o contrato estiver completo, revisado e aprovado. A Collection de Validação
deve estar acessível, executável e conter resultados esperados.
```

---

# Fase 2 — Runbook de Validação Técnica — CONTEÚDO INTEGRAL

```markdown
         Runbook — Fase 2: Validação Técnica da Tool
Processo operacional para validação manual e futura automação por agente de IA
Versão: 1.0 | Data: 27/09/2026

Fluxo: Collection + contrato → Tool direta → MCP Client → Segurança → Resiliência → Performance → Observabilidade → Gate →
Fase 3


1. Objetivo e Escopo
Objetivo: Certificar tecnicamente uma tool antes de sua avaliação pelo agente. A Fase 2 verifica se a tool é previsível, segura,
resiliente, observável e tecnicamente aderente ao contrato.

Escopo: A validação é executada sem o agente. A Seção 1 chama a tool diretamente. A Seção 2 usa um MCP Client. As Seções 3 a 6
avaliam segurança, resiliência, performance e observabilidade. A avaliação de seleção da tool pelo agente fica para a Fase 4.

Princípio: Todo teste deve possuir: cenário, pré-condições, entrada, procedimento, resultado esperado, critério de aceite, resultado
obtido, evidência e status.


2. Pré-requisitos
2.1 Artefatos obrigatórios: Disponibilizar documentação do schema de input/output; exemplos válidos e inválidos; Collection de
Validação da Fase 1; resultados esperados por chamada; método de autenticação; timeouts; SLAs/SLOs; acesso ao ambiente de teste;
owner técnico; link da documentação; link do dataset de treinamento; dashboard principal do Datadog.

2.2 Collection de Validação: A Collection deve conter chamadas reproduzíveis para o servidor/tool, parâmetros necessários e
resultado esperado de cada cenário. Pode ser Postman, Insomnia ou formato equivalente compartilhado. Deve possuir versão,
responsável e data de atualização.

2.3 Critério de entrada: Não iniciar a execução quando faltar um artefato obrigatório, quando os resultados esperados forem ambíguos
ou quando o ambiente de teste não estiver acessível. Registrar o bloqueio.


3. Seção 1 — Validação do Contrato Técnico
Objetivo: Comprovar, em chamada direta à tool, que inputs, outputs e erros seguem o contrato definido, sem envolver MCP Client ou
agente.

3.1 Campos obrigatórios: Validar uma chamada válida e repetir removendo cada campo obrigatório individualmente. Verificar rejeição
controlada e aderência ao erro esperado.

Aceite: Todos os campos obrigatórios funcionam quando presentes; chamadas sem campos obrigatórios são rejeitadas conforme
contrato; nenhum campo obrigatório é ignorado silenciosamente.

3.2 Tipos de dados: Executar valores válidos e alterar individualmente tipos de string, número, boolean, array e objeto, conforme
aplicável.

Aceite: Tipos válidos são aceitos; tipos incompatíveis são rejeitados ou tratados exatamente como definido no contrato.

3.3 Restrições e valores: Testar limites, enums, formatos, strings vazias, nulos, valores fora do intervalo e combinações incompatíveis.

Aceite: Restrições documentadas são efetivamente aplicadas e o comportamento para valores inválidos é determinístico.

3.4 Output: Comparar campos, tipos e estrutura do response real com o schema e com os resultados esperados da Collection.

Aceite: Output aderente ao schema; campos obrigatórios presentes; tipos e estrutura corretos.

3.5 Ausência de dados: Executar cenário sem dados e validar status, estrutura, mensagem e campos opcionais.

Aceite: Ausência de dados não produz resposta ambígua nem quebra o contrato.

3.6 Erros: Executar cenários inválidos e verificar formato, consistência e segurança das mensagens de erro.

Aceite: Erro previsível, estruturado quando aplicável, sem exposição de secrets ou dados sensíveis.

Evidências: Request, response, comparação com esperado, schema validado, logs/traces quando necessários e identificação do caso
da Collection.


4. Seção 2 — Validação da Integração MCP
Objetivo: Comprovar que o comportamento validado diretamente na Seção 1 é preservado quando a tool é acessada pelo protocolo
MCP.

4.1 Descoberta: Conectar com MCP Client e listar as tools. Comparar nome, descrição, schema e parâmetros publicados com a
definição aprovada.

Aceite: Tool é descoberta; identidade e schema publicados são corretos e suficientes para execução.

4.2 Chamada via MCP: Executar os mesmos cenários relevantes da Collection usando MCP Client e comparar o resultado com a
chamada direta.

Aceite: A chamada é encaminhada à tool correta e o resultado é equivalente ao comportamento esperado da Seção 1.

4.3 Argumentos: Testar strings, números, booleanos, arrays, objetos, opcionais e nulos conforme aplicável.

Aceite: Nenhum argumento é perdido, convertido indevidamente ou alterado de forma incompatível durante o transporte MCP.

4.4 Erros MCP: Executar chamadas inválidas e cenários de falha para observar como o MCP Client recebe e interpreta erros.

Aceite: Erros são propagados de forma controlada, identificável e sem exposição de informação sensível.

4.5 Consistência: Comparar: chamada direta → resultado e MCP Client → resultado.

Aceite: Diferenças não justificadas pelo protocolo ou pelo contrato são falhas.


5. Seção 3 — Validação de Segurança
Objetivo: Verificar autenticação, autorização, proteção de dados e políticas de segurança.

5.1 Autenticação: Testar credencial válida, inválida, ausente e expirada quando aplicável.

Aceite: Apenas credenciais válidas e vigentes obtêm acesso conforme a política.

5.2 Autorização: Executar com identidade autorizada e não autorizada, incluindo tentativa de acesso a recurso não permitido.

Aceite: A autorização é aplicada no ponto correto e acesso indevido é bloqueado.

5.3 Dados sensíveis: Inspecionar responses, erros, logs e traces em cenários normais e de falha.

Aceite: Não há exposição indevida de secrets, tokens, credenciais ou dados sensíveis.

5.4 Secrets: Verificar configuração, logs e respostas para garantir que secrets não estejam hardcoded ou retornados.

Aceite: Nenhum secret aparece em código/configuração indevida, response, log ou trace.

5.5 OPA: Quando houver policy OPA aplicável, executar a avaliação da policy contra a API/tool e registrar input, decisão e evidência.

Aceite: A API atende às policies obrigatórias; violações são identificadas e impedem aprovação quando classificadas como
bloqueantes.


6. Seção 4 — Resiliência e Tratamento de Erros
Objetivo: Verificar comportamento controlado diante de falhas, indisponibilidade e respostas inesperadas.

6.1 Timeout: Provocar ou simular dependência lenta e verificar timeout, tempo até falha e tipo de erro.

Aceite: Não há espera indefinida; timeout respeita configuração ou SLO definido.

6.2 Dependência indisponível: Simular API, banco ou serviço downstream indisponível.

Aceite: Falha é tratada de forma previsível, sem crash ou comportamento indefinido.

6.3 Resposta inválida: Simular JSON inválido, campo ausente, schema inesperado e tipo inesperado.

Aceite: Tool rejeita ou trata resposta inválida de forma controlada e observável.

6.4 Retry: Verificar existência, quantidade, backoff e condições de retry.

Aceite: Retry ocorre somente quando apropriado, respeita limites e não amplifica falhas ou efeitos colaterais.

6.5 Idempotência: Para operações mutáveis, repetir a mesma chamada ou simular retry.

Aceite: Retries não geram duplicidade ou efeitos colaterais indevidos quando a operação exige idempotência.


7. Seção 5 — Performance e Capacidade
Objetivo: Medir o comportamento quantitativo da tool e compará-lo com os SLAs/SLOs definidos na Fase 1.

7.1 Latência: Executar conjunto representativo de chamadas e calcular média, mediana, P95, P99 e máximo.

Aceite: Métricas ficam dentro dos limites acordados; desvios devem ser classificados e justificados.

7.2 Taxa de erro: Executar volume definido de chamadas e calcular erros/total.

Aceite: Taxa de erro atende ao limite estabelecido para o ambiente.

7.3 Concorrência: Executar chamadas simultâneas em níveis progressivos.

Aceite: Tool mantém comportamento correto e métricas dentro dos limites sob concorrência esperada.

7.4 Carga: Aumentar gradualmente o volume até o limite esperado ou até identificar degradação.

Aceite: Capacidade observada atende à demanda de referência ou o limite é documentado.

7.5 Degradação: Registrar o ponto em que latência/erro/throughput começam a degradar.

Aceite: Ponto de degradação conhecido e compatível com a capacidade esperada; ausência de comportamento catastrófico.


8. Seção 6 — Observabilidade
Objetivo: Comprovar que uma falha pode ser detectada, correlacionada e diagnosticada.

8.1 Logs: Executar chamadas de sucesso e falha e localizar registros correspondentes.

Aceite: Logs possuem contexto suficiente, como timestamp, operação, correlation/request ID e resultado, sem dados sensíveis.

8.2 Métricas: Verificar chamadas, erros, latência, throughput, timeout e retry quando aplicável.

Aceite: Métricas existem, são atualizadas e permitem identificar degradação.

8.3 Tracing: Executar chamada e acompanhar o fluxo MCP Server → Tool → dependência.

Aceite: Trace permite localizar o componente responsável por uma falha.

8.4 Datadog: Abrir o dashboard principal informado na Fase 1 e executar cenários conhecidos para localizar os sinais correspondentes.

Aceite: Dashboard apresenta sinais relevantes e permite correlacionar uma execução com logs/métricas/traces.


9. Evidências e Registro
Registro mínimo: Cada teste deve registrar ID, seção, cenário, pré-condições, input, procedimento, resultado esperado, resultado
obtido, status, evidência, timestamp, ambiente e observações.

Status: PASS: todos os critérios do teste atendidos. FAIL: pelo menos um critério não atendido. BLOCKED: execução não foi possível
por pré-condição/infraestrutura. NOT APPLICABLE: item não se aplica, com justificativa.

Regra: Não marcar PASS por ausência de evidência. Um teste executado sem evidência verificável deve permanecer como FAIL ou
BLOCKED, conforme a causa.


10. Gate de Aprovação da Fase 2
Critério geral: A Fase 2 é aprovada quando todas as seções aplicáveis possuem critérios de aceite atendidos, evidências registradas e
nenhuma falha crítica ou bloqueante permanece aberta.

FAIL: Qualquer falha crítica de contrato, segurança, integração MCP, resiliência ou outro requisito obrigatório impede o avanço até
correção ou exceção formal.

BLOCKED: Bloqueios devem ser resolvidos antes da aprovação, salvo exceção formal definida pelo processo.

Saída: APROVADO PARA FASE 3 ou RETORNAR PARA CORREÇÃO. O resultado deve incluir resumo das falhas, evidências e
pendências.


11. Modelo de Caso de Teste
Template: ID: F2-Sx-Tyy | Cenário: ... | Pré-condições: ... | Input: ... | Procedimento: ... | Resultado esperado: ... | Critério de aceite: ... |
Resultado obtido: ... | Evidência: ... | Status: PASS/FAIL/BLOCKED/N/A.

Exemplo: Cenário: chamada sem customer_id. Input: payload sem customer_id. Resultado esperado: rejeição conforme contrato.
Critério de aceite: chamada rejeitada e erro correspondente ao contrato. Evidência: request/response + log. Status: PASS se todos os
critérios forem atendidos.


12. Automação Futura
Princípio: O Runbook deve ser executável manualmente hoje e estruturado para automação amanhã.

Automatizável: Validação de schema, execução da Collection, comparação de outputs, descoberta MCP, testes de argumentos,
chamadas negativas, coleta de métricas, consulta de observabilidade e consolidação de evidências.

Agente de IA: Um futuro agente pode receber os artefatos da Fase 1, executar os testes permitidos, interpretar resultados contra
critérios explícitos e gerar o relatório. A aprovação final deve permanecer sujeita às regras de governança definidas pela equipe.

Checklist Executivo
      Seção   Objetivo             Critério de aceite                              Status

      1       Contrato técnico     Input/output/erros aderentes ao contrato

      2       Integração MCP       Descoberta, chamadas e erros MCP corretos

      3       Segurança            Acesso e proteção de dados conforme políticas

      4       Resiliência          Falhas tratadas sem comportamento indefinido

      5       Performance          SLA/SLO e capacidade atendidos

      6       Observabilidade      Logs, métricas, traces e Datadog utilizáveis



Resultado final: ■ APROVADO PARA FASE 3 ■ RETORNAR PARA CORREÇÃO
```

---

# Fase 3 — Runbook de Validação Funcional — CONTEÚDO INTEGRAL

```markdown
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
```

---

# Fase 4 — Runbook de Avaliação do Uso das Tools pelo Agente — CONTEÚDO INTEGRAL

```markdown
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
```

---

# Fase 5 — Runbook de Operação, Observabilidade e Monitoramento — CONTEÚDO INTEGRAL

```markdown
         Runbook — Fase 5: Operação, Observabilidade e
                   Monitoramento da Tool
 Objetivo: garantir que, após a aprovação das Fases 1–4, a tool esteja preparada para operação dentro do
 agente e possua mecanismos para acompanhar seu comportamento, detectar degradações, investigar falhas e
 acionar os responsáveis.

 Escopo: esta fase não revalida a funcionalidade da tool nem a capacidade de seleção do agente. Ela
 operacionaliza o monitoramento contínuo dos comportamentos já avaliados.


 1. Pré-requisitos
 Antes de iniciar, confirmar: Fases 1–4 aprovadas; owner definido; SLA/SLO definido quando aplicável;
 dependências conhecidas; ferramentas de observabilidade disponíveis; acesso ao Datadog; ambiente de
 produção ou equivalente; estratégia de logs, métricas e tracing definida.

 Critério de aceite: todos os pré-requisitos obrigatórios estão disponíveis e documentados. Evidências:
 checklist, links para dashboards, documentação e responsáveis.


 2. Logs
  Por que existe             Garantir que cada execução gere informações suficientes para investigação e auditoria.

  O que acompanhar           Acompanhar timestamp, operação/tool, resultado, erro, dependências, correlation/trace ID e
                             informações necessárias à investigação, sem registrar dados sensíveis indevidamente.

  Como implementar/validar   Executar chamadas representativas, localizar os logs e verificar correlação e conteúdo. Validar
                             também mascaramento de dados sensíveis.

  Critério de aceite         Os logs permitem reconstruir a execução sem exposição indevida de dados.

  Evidências                 Exemplos de logs, timestamps, correlation ID, trace ID e evidência de mascaramento.




 3. Métricas
  Por que existe             Garantir visibilidade quantitativa sobre saúde, volume e desempenho.

  O que acompanhar           Volume, sucesso, erro, latência, p95, p99, disponibilidade, timeout e retry. No contexto do
                             agente, frequência de seleção e falhas após a seleção.

  Como implementar/validar   Executar chamadas conhecidas e comparar o volume real com o volume registrado. Verificar
                             atualização e granularidade das métricas.

  Critério de aceite         As métricas existem, são atualizadas e representam corretamente o comportamento observado.

  Evidências                 Dashboard/export do Datadog e valores observados no período.




 4. Tracing
  Por que existe             Permitir acompanhar o fluxo completo e localizar gargalos ou falhas.

  O que acompanhar           Fluxo agente → tool → API/dependência → resposta → agente, com duração, erro e IDs de
                             correlação.

  Como implementar/validar   Executar uma chamada pelo agente e localizar o trace correspondente.

  Critério de aceite         É possível acompanhar a execução ponta a ponta sem perda de correlação.




Runbook — Fase 5                                                                                                           Página 1

  Evidências                 Trace completo, IDs e timestamps.




 5. Dashboard operacional
  Por que existe             Centralizar os principais sinais para permitir diagnóstico rápido.

  O que acompanhar           Volume, sucesso/erro, latência, p95/p99, timeout, retry, disponibilidade e uso pelo agente.

  Como implementar/validar   Abrir o dashboard e verificar se uma pessoa responsável consegue identificar rapidamente o
                             estado da tool.

  Critério de aceite         Dashboard disponível, atualizado e suficiente para identificar problemas relevantes.

  Evidências                 Link e evidência visual/configuração do dashboard.




 6. Alertas
  Por que existe             Detectar automaticamente condições que exigem investigação ou ação.

  O que acompanhar           Aumento de erro, degradação de latência, indisponibilidade, timeout e anomalias de volume,
                             conforme thresholds definidos.

  Como implementar/validar   Provocar ou simular uma condição controlada e verificar o disparo e roteamento do alerta.

  Critério de aceite         O alerta dispara no threshold definido, chega ao responsável correto e aponta para
                             procedimento de resposta.

  Evidências                 Configuração do monitor, evento, notificação e timestamp.




 7. SLO/SLA
  Por que existe             Garantir que compromissos operacionais sejam mensuráveis.

  O que acompanhar           Disponibilidade, latência, taxa máxima de erro, capacidade e outros indicadores definidos pelo
                             owner.

  Como implementar/validar   Comparar SLO/SLA documentado com métricas, dashboard e alertas.

  Critério de aceite         Todo indicador crítico possui mecanismo de medição e alerta quando necessário.

  Evidências                 Documento de SLO/SLA, métrica e monitor correspondente.




 8. Runbook operacional
  Por que existe             Permitir resposta consistente a incidentes sem depender de conhecimento individual.

  O que acompanhar           Procedimentos para identificar, investigar, mitigar, escalar e encerrar problemas.

  Como implementar/validar   Executar ou revisar um cenário de incidente seguindo o runbook.

  Critério de aceite         Uma pessoa que não participou da implementação consegue iniciar a investigação seguindo o
                             procedimento.

  Evidências                 Link do runbook e registro da execução.




 9. Ownership e escalonamento

Runbook — Fase 5                                                                                                           Página 2

  Por que existe             Garantir que incidentes tenham responsáveis claros.

  O que acompanhar           Owner, time, canal de suporte, responsável por monitoramento e caminho de escalonamento.

  Como implementar/validar   Verificar documentação e realizar teste de acionamento quando aplicável.

  Critério de aceite         Cada incidente relevante possui responsável e caminho de escalonamento definidos.

  Evidências                 Registro de owners, canais e evidência de acionamento.




 10. Retenção e acesso
  Por que existe             Garantir disponibilidade das evidências pelo período necessário.

  O que acompanhar           Retenção, permissões e acessibilidade de logs, métricas e traces.

  Como implementar/validar   Consultar evidências com perfis de acesso apropriados e verificar período de retenção definido.

  Critério de aceite         As evidências necessárias estão disponíveis pelo período estabelecido e apenas para perfis
                             autorizados.

  Evidências                 Política/configuração de retenção e teste de acesso.




 11. Uso pelo agente
  Por que existe             Monitorar como a tool se comporta quando efetivamente utilizada pelo agente.

  O que acompanhar           Frequência de seleção, operações utilizadas, sucesso/erro, latência e alterações anormais de
                             utilização.

  Como implementar/validar   Observar execuções reais ou controladas do agente e comparar com o baseline.

  Critério de aceite         É possível identificar volume, saúde e alterações relevantes no uso da tool pelo agente.

  Evidências                 Métricas e traces correlacionados agente→tool.




 12. Qualidade operacional
  Por que existe             Detectar sinais de degradação que possam exigir nova avaliação funcional ou do agente.

  O que acompanhar           Fallbacks, respostas sem resultado, mudanças na distribuição de seleção e outros indicadores
                             disponíveis.

  Como implementar/validar   Definir baseline e acompanhar desvios significativos; estabelecer gatilhos para investigação.

  Critério de aceite         Desvios relevantes são detectáveis e existe processo documentado para investigar e, se
                             necessário, reexecutar avaliações.

  Evidências                 Baseline, métricas e registros de investigação.




 13. Teste de incidente
  Por que existe             Validar o fluxo completo de detecção e resposta antes de depender dele em produção.

  O que acompanhar           Falha → métrica → dashboard → alerta → responsável → investigação → escalonamento.

  Como implementar/validar   Simular uma falha controlada e executar o fluxo definido no runbook.




Runbook — Fase 5                                                                                                        Página 3

  Critério de aceite       O fluxo é reproduzível e permite detectar o problema, localizar evidências e iniciar a
                           investigação.

  Evidências               Incidente simulado, alerta, dashboard, logs, trace, ações e tempos de detecção/início da
                           investigação.




 14. Gate de Aprovação da Fase 5
 A tool pode ser aprovada para operação contínua quando logs, métricas, tracing, dashboard, alertas,
 SLO/SLA, runbook operacional, ownership, escalonamento, retenção, monitoramento do uso pelo agente e
 teste de incidente estiverem implementados e evidenciados.

 Checklist: ■ Logs adequados ■ Métricas essenciais ■ P95/P99 ■ Tracing ponta a ponta ■ Dashboard
 ■ Alertas ■ SLO/SLA ■ Runbook operacional ■ Owner/escalonamento ■ Retenção/acesso ■ Uso pelo
 agente ■ Teste de incidente.


 15. Resultado da fase
 O resultado esperado é: “A tool está operacionalizada dentro do agente e possui mecanismos
 suficientes para observar seu comportamento, detectar problemas, investigá-los e acionar os
 responsáveis.”




Runbook — Fase 5                                                                                                      Página 4
```

---

# Fase 6 — Runbook de Rollout — CONTEÚDO INTEGRAL

```markdown
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
```

---

# Fase 7 — Runbook de Revisão, Revalidação e Ciclo de Vida — CONTEÚDO INTEGRAL

```markdown
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
```

---

# 19. Estado de continuidade

O próximo trabalho deve partir do estado descrito neste arquivo e dos documentos integrais acima.

Não assumir que uma decisão conceitual já foi aplicada ao artefato se a seção "Estado dos artefatos" disser o contrário.

Em particular:

- F1–F5 possuem PDFs formais e versões Markdown fiéis ao conteúdo dos PDFs;
- F6 possui Markdown e PDF atuais, mas o documento atual possui 10 seções;
- existe uma estrutura conceitual de F6 com uma 11ª seção de transição para F7, ainda não incorporada ao documento atual;
- F7 possui Markdown e PDF atuais sob a numeração nova;
- existe um PDF histórico de lifecycle com o nome antigo "Fase 6";
- o one-page ainda é um artefato visual separado e os owners das fases ainda não devem ser preenchidos;
- as notas pessoais permanecem separadas dos documentos oficiais.

Este arquivo deve ser atualizado quando houver uma nova decisão estrutural, mudança de nomenclatura, alteração de fase, novo artefato oficial, definição de ownership, mudança de dataset, mudança de critérios de aceite ou nova regra de governança.
