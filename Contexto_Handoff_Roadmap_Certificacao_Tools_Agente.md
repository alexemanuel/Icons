# Contexto de Continuidade — Roadmap de Certificação e Ciclo de Vida de Tools para Agentes

> Documento de handoff para outro agente continuar esta conversa sem perder contexto, decisões, nomenclaturas, estruturas e pendências.

## 1. Contexto Geral

Estamos construindo um processo formal de **onboarding, certificação, disponibilização, operação e ciclo de vida de Tools utilizadas por um agente de IA**.

O contexto é um agente consultivo que utiliza múltiplas Tools/MCP Servers para consultar informações e gerar respostas.

Objetivo do processo:

1. definir corretamente a Tool;
2. validar funcionamento técnico;
3. validar comportamento funcional/de negócio;
4. validar o uso da Tool pelo agente;
5. operacionalizar observabilidade e monitoramento;
6. fazer rollout seguro, gradual e reversível;
7. manter a Tool válida ao longo do tempo.

O processo foi consolidado em **7 fases**.

---

## 2. Roadmap Consolidado

| Fase | Nome | Pergunta principal |
|---|---|---|
| 1 | Cadastro e Contrato da Tool | Temos tudo definido para iniciar a certificação? |
| 2 | Validação Técnica | A Tool funciona tecnicamente? |
| 3 | Validação Funcional | A Tool funciona corretamente para o negócio? |
| 4 | Avaliação do Uso pelo Agente | O agente sabe quando e como usar a Tool? |
| 5 | Operação, Observabilidade e Monitoramento | Conseguimos operar e observar a Tool continuamente? |
| 6 | Rollout da Tool | Conseguimos disponibilizar a Tool em produção com segurança? |
| 7 | Revisão, Revalidação e Ciclo de Vida | A Tool continua válida ao longo do tempo? |

### Agrupamento

**Certificação:** Fases 1 → 2 → 3 → 4

**Entrada em produção / operacionalização:** Fases 5 → 6

**Ciclo de vida:** Fase 7

### Distinções fundamentais

- F2 e F3 **não envolvem o agente**.
- F4 é a **primeira fase que envolve o agente**.
- F5 não é uma nova rodada de testes; é a **operacionalização da observabilidade e monitoramento**.
- F6 é o **rollout efetivo em produção**.
- F7 é a **manutenção contínua e revalidação ao longo do tempo**.

---

## 3. Papéis / Possíveis Owners

O time anteriormente chamado de “Plataforma” foi identificado como:

### 🤖 Agentes Satélite

É o time responsável pelo agente e também por aspectos de MCP/integração.

Escopo:

- Agente
- MCP Client
- MCP Server
- Integração com Tools
- Tool calling
- Tool selection
- Disponibilização técnica
- Integração da Tool com o agente
- Parte da observabilidade técnica

Papéis que devem aparecer na legenda do one-page:

- 👤 **Owner da Tool**
- 🤖 **Agentes Satélite**
- 📈 **SRE/Operações**
- 🔒 **Segurança**
- 🟣 **Plataforma**

### Responsabilidades conceituais

**Owner da Tool:** domínio, regras de negócio, comportamento funcional e ciclo de vida da Tool.

**Agentes Satélite:** agente, MCP, integração, Tool calling, seleção de Tools e disponibilização técnica.

**SRE/Operações:** observabilidade operacional, operação, monitoramento, capacidade e incidentes.

**Segurança:** acessos, políticas, autenticação/autorização, secrets e controles de segurança.

**Plataforma:** possível participante para infraestrutura, ambientes, padrões, deployment e suporte técnico à certificação, quando aplicável.

### Atenção

**Os owners reais das fases ainda não foram definidos.**

No one-page, cada fase deve possuir a seção:

> **Responsáveis desta fase**

mas a caixa abaixo deve ficar **completamente vazia**, sem nomes, símbolos ou ícones.

---

## 4. Racional dos possíveis responsáveis por fase

### Fase 1 — Cadastro e Contrato

Possível principal: **Owner da Tool**

Participação: **Agentes Satélite**

O Owner conhece finalidade, domínio, regras, dependências, critérios de aceite e documentação. Agentes Satélite pode garantir que o contrato seja suficientemente definido para integração.

### Fase 2 — Validação Técnica

Possível principal: **Agentes Satélite**

Participação: **Segurança**

Valida MCP, schemas, integração, conectividade, erros, timeout, performance, tracing, logs e métricas. Segurança valida autenticação, autorização, secrets, permissões e políticas.

### Fase 3 — Validação Funcional

Possível principal: **Owner da Tool**

Participação: **Agentes Satélite**

A pergunta é se o resultado está correto para o negócio. Agentes Satélite apoia tecnicamente, mas o Owner determina a correção funcional.

### Fase 4 — Avaliação no Agente

Possível principal: **Agentes Satélite**

Participação: **Owner da Tool**

Agentes Satélite avalia seleção, no-tool, desambiguação, parâmetros, execução, uso do resultado e resposta final. Owner ajuda a confirmar domínio e fronteiras funcionais.

### Fase 5 — Operação e Observabilidade

Possível principal: **SRE/Operações**

Participação: **Agentes Satélite + Owner da Tool**

SRE cuida de incidentes, alertas, SLO, disponibilidade e capacidade. Agentes Satélite fornece mecanismos técnicos. Owner é referência do serviço.

### Fase 6 — Rollout

Possível principal: **Agentes Satélite**

Participação: **SRE/Operações + Owner da Tool**

Agentes Satélite disponibiliza tecnicamente. SRE acompanha risco operacional. Owner acompanha a entrada da Tool em produção.

### Fase 7 — Ciclo de Vida

É multidisciplinar:

- Owner da Tool
- Agentes Satélite
- SRE/Operações
- Segurança
- Plataforma

Mudanças podem afetar negócio, agente, MCP, infraestrutura, segurança, performance, operação e dependências.

---

# 5. Fase 1 — Cadastro e Contrato da Nova Tool

A Fase 1 é um **formulário**.

## Objetivo

Preparar o pacote de entrada da Tool para certificação.

## Conteúdo

### Identificação

- Nome
- Descrição
- Owner / responsável técnico
- Time
- Sistema/serviço de origem
- Ambiente
- Data
- Versão

### Contrato técnico

Input:

- link da documentação;
- schema;
- field;
- type;
- required;
- description;
- restrictions.

Output:

- link;
- schema;
- field;
- type;
- required;
- description.

Error handling:

- invalid input;
- missing required field;
- nonexistent resource;
- unauthorized;
- dependency unavailable.

### Dependências

Tabela:

- dependency;
- purpose;
- environment;
- owner.

### Pré-condições

- ambiente de teste;
- credenciais;
- dados;
- dependências;
- responsável técnico;
- documentação atualizada.

### Critérios de aceite

Tabela:

- ID;
- criterion;
- mandatory;
- expected evidence.

### Critérios de aceite das APIs utilizadas pelo MCP

Foi solicitado explicitamente que as APIs downstream utilizadas pelo MCP também tenham critérios de aceite formais.

### Referências

- documentação da Tool;
- dataset de treinamento, quando aplicável;
- dataset de avaliação;
- dashboard principal Datadog;
- outros links operacionais.

---

## 6. Dataset de Avaliação

Estrutura desejada:

| Caso | Tool esperada | Valores esperados | Justificativa |
|---|---|---|---|

Não criar um campo separado chamado “Parâmetros esperados”.

Os valores esperados ficam em objeto chave/valor.

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

### Importância

Uma nova Tool pode causar regressões na seleção de Tools existentes.

Exemplo:

`getFutureAppointments`

não deveria ser selecionada para:

> “Quais compromissos eu tive na semana passada?”

Por isso são essenciais os casos negativos e hard negatives.

---

## 7. Dataset fornecido pelo time da Tool

Pode ser usado como **referência/base**, mas não deve ser a única fonte de avaliação do agente.

Motivo: pode não conter:

- ambiguidades;
- hard negatives;
- no-tool;
- fronteiras;
- competição com outras Tools;
- cenários adversariais;
- casos fora de escopo.

Manter proveniência:

- `team-provided`
- `independent`
- `production-incident`
- `regression`
- `hard-negative`

---

## 8. Validation Collection

A Collection é **obrigatória** na Fase 1 e será usada na Fase 2.

Deve conter chamadas ao MCP Server/Tool e resultados esperados.

Campos:

- ID;
- endpoint/tool;
- scenario;
- input;
- expected result.

Requisitos:

- executável em teste;
- variáveis documentadas;
- sem credenciais expostas;
- resultado esperado em cada chamada;
- positivos;
- negativos;
- erros relevantes;
- versão;
- owner;
- atualizada.

---

# 9. Fase 2 — Validação Técnica

**Não envolve o agente.**

Objetivo:

> Comprovar que a Tool funciona tecnicamente conforme o contrato.

Seções:

1. Pré-requisitos
2. Contrato técnico
3. Integração MCP
4. Segurança
5. Resiliência e erros
6. Performance e capacidade
7. Observabilidade
8. Evidências
9. Gate
10. Caso de teste
11. Automação futura

### Contrato

Validar:

- required fields;
- tipos;
- restrições;
- invalid values;
- output;
- no-data;
- erros.

### MCP

Validar:

- `tools/list`;
- discovery;
- schema;
- chamada;
- argumentos;
- erros;
- consistência direta vs MCP.

### Segurança

Validar:

- autenticação;
- autorização;
- dados sensíveis;
- secrets;
- permissões;
- OPA.

OPA:

1. avaliar policy;
2. registrar input;
3. registrar decisão;
4. registrar evidência.

### Resiliência

- timeout;
- dependência indisponível;
- resposta inválida;
- retry;
- idempotência;
- erros de auth.

### Performance

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

Usar os SLA/SLO da F1.

### Observabilidade

Trace:

`MCP Client → MCP Server → Tool → Dependency`

### Evidência

Regra:

> Um teste sem evidência verificável não pode ser PASS.

Status:

- PASS
- FAIL
- BLOCKED
- N/A

Gate:

- testes executados;
- critérios atendidos;
- evidências registradas;
- sem falhas críticas.

Saída: **APROVADO PARA FASE 3**

---

# 10. Fase 3 — Validação Funcional

**Não envolve o agente.**

Objetivo:

> **A Tool funciona corretamente do ponto de vista funcional e de negócio?**

Seções:

1. Objetivo
2. Escopo
3. Pré-condições
4. Preparação de cenários
5. Happy path
6. Negativos
7. Fronteiras
8. Hard negatives/fronteiras funcionais
9. Parâmetros
10. Resultado funcional
11. Consistência
12. Dataset
13. Registro
14. Classificação
15. Gate

### Hard negative

Cenário plausível que parece pertencer à Tool, mas pertence a outra Tool ou está fora de escopo.

Na F3 não avaliamos a decisão do agente.

Apenas definimos a fronteira funcional.

### Resultado funcional

Validar:

- conteúdo;
- quantidades;
- filtros;
- ordenação;
- cálculos;
- datas;
- valores;
- relações;
- ausência de dados.

---

# 11. Fase 4 — Avaliação do Uso das Tools pelo Agente

Primeira fase com o agente.

Pergunta:

> **O agente sabe quando e como usar a Tool?**

Validações:

1. Seleção
2. No-Tool
3. Desambiguação
4. Construção de parâmetros
5. Execução
6. Uso do resultado
7. Negativos
8. Fronteiras
9. Hard negatives
10. End-to-End

### Seleção

Validar intenção, Tool correta e paraphrases.

### No-Tool

Garantir que não haja chamadas desnecessárias.

### Desambiguação

Usar Tools concorrentes e fronteiras da F3.

### Parâmetros

Validar required, optional, defaults, tipos, datas, IDs, filtros, quantidades e combinações.

### Execução

Validar Tool, payload, número e ordem das chamadas.

### Resultado

Validar resultados conhecidos, múltiplos, vazios, parciais e opcionais.

Não pode haver dados inventados.

### Hard negatives

Agora avaliamos se o agente escolhe a Tool correta em casos plausíveis de confusão.

### E2E

`Intent → Tool Selection → Parameters → Execution → Result → Final Response`

### Métricas

- Tool Selection Accuracy
- Parameter Accuracy
- No-Tool Accuracy
- Tool Call Accuracy
- Result Usage Accuracy
- End-to-End Accuracy

Segmentar por:

- Happy Path
- Negative
- Boundary
- Hard Negative
- No-Tool
- Ambiguous

Thresholds devem ser definidos antes dos testes.

---

# 12. Fase 5 — Operação, Observabilidade e Monitoramento

Objetivo:

> Transformar as validações em capacidade operacional contínua.

Não é repetição das Fases 2–4.

Seções:

1. Pré-requisitos
2. Logs
3. Métricas
4. Tracing
5. Dashboard
6. Alertas
7. SLO/SLA
8. Runbook operacional
9. Ownership/escalonamento
10. Retenção/acesso
11. Monitoramento do agente
12. Qualidade operacional
13. Teste de incidente

### Logs

Devem permitir reconstruir uma ocorrência sem exposição indevida de dados.

### Métricas

- volume;
- sucesso/erro;
- latência;
- p95/p99;
- disponibilidade;
- timeout;
- retry;
- frequência de seleção;
- falhas após seleção.

### Tracing

`Agente → Tool → API/Dependência → Resposta → Agente`

### Dashboard

Principalmente Datadog.

### Alertas

- erro;
- latência;
- downtime;
- timeout;
- anomalias de volume.

### Runbook operacional

Deve permitir investigação por alguém que não implementou a Tool.

### Incident Test

`Falha → Métrica → Dashboard → Alerta → Owner → Investigação → Escalonamento`

### Gate

Devem existir e estar evidenciados:

- logs;
- métricas;
- tracing;
- dashboard;
- alertas;
- SLO/SLA;
- runbook;
- ownership;
- retenção/acesso;
- monitoramento do agente;
- teste de incidente.

Saída:

**TOOL OPERACIONALIZADA E OBSERVÁVEL**

---

# 13. Fase 6 — Rollout da Tool

Foi adicionada entre F5 e F7.

Objetivo:

> Introduzir a Tool em produção de forma controlada, gradual e reversível.

F5 prepara a capacidade de observação.

F6 usa essa capacidade para decisões:

- GO
- HOLD
- ROLLBACK

## Sessões

### 1. Preparação

Verificar:

- fases anteriores;
- versão;
- produção;
- configuração;
- MCP;
- auth/authz;
- secrets;
- dashboards;
- alertas;
- owners;
- rollback.

### 2. Estratégia

Definir:

- exposição;
- público;
- percentual;
- etapas;
- duração;
- critérios de avanço;
- pausa;
- rollback;
- responsáveis.

Exemplo:

`Certification → Deploy → 0% → Canary → 10% → 25% → 50% → 100%`

### 3. Configuração e Disponibilização

Verificar:

- deploy;
- configuração;
- registro;
- MCP;
- agente;
- permissões;
- secrets;
- feature flags;
- dependências.

### 4. Canary

Monitorar:

- chamadas;
- sucesso;
- erros;
- latência;
- timeout;
- parâmetros;
- disponibilidade;
- agente;
- MCP;
- dependências.

Decisão: GO/HOLD/ROLLBACK.

### 5. Expansão

Monitorar:

- exposição;
- volume;
- erros;
- latência;
- disponibilidade;
- capacidade;
- agente;
- incidentes;
- impacto em outras Tools;
- baseline.

### 6. Comportamento do agente

Verificar:

- frequência de seleção;
- chamadas inadequadas;
- chamadas esperadas ausentes;
- falhas de parâmetros;
- erros;
- uso incorreto de resultados;
- interação com outras Tools;
- chamadas desnecessárias.

### 7. Performance e capacidade

- latência;
- P50;
- P95;
- P99;
- throughput;
- timeouts;
- retries;
- recursos;
- dependências;
- MCP;
- APIs.

### 8. Incidentes

Fluxo:

1. impacto;
2. severidade;
3. relação com rollout;
4. GO/HOLD/ROLLBACK;
5. ação;
6. evidência;
7. comunicação;
8. recuperação.

### 9. Rollback

Verificar:

- disable;
- configuração;
- versão anterior;
- exposição;
- agente;
- dependências;
- comunicação;
- registro.

### 10. Conclusão

Verificar:

- exposição final;
- métricas;
- erros;
- latência;
- disponibilidade;
- agente;
- incidentes;
- capacidade;
- observabilidade;
- rollback;
- evidências;
- aprovação.

### 11. Transição para F7

Registrar:

- documentação;
- versão;
- configuração;
- baseline;
- owners;
- incidentes;
- decisão.

Saída:

**A Tool foi disponibilizada em produção no nível planejado, com rollout concluído e aprovado.**

---

# 14. Fase 7 — Revisão, Revalidação e Ciclo de Vida

Antes era F6. Com a adição do Rollout, tornou-se F7.

Pergunta:

> **A Tool continua válida ao longo do tempo?**

Executada:

- periodicamente;
- após mudanças;
- após incidentes relevantes.

Triggers:

- contrato;
- API;
- schema;
- regras;
- segurança;
- roles;
- secrets;
- dependências;
- MCP;
- agente/modelo;
- performance;
- observabilidade;
- dataset;
- incidentes.

### Verificação de mudanças

Comparar estado atual com última versão validada usando:

- histórico;
- releases;
- docs;
- PRs;
- infraestrutura;
- políticas;
- secrets.

### Impact Analysis

Classificar:

- sem impacto;
- parcial;
- amplo;
- crítico.

Dimensões:

- técnico;
- segurança;
- funcional;
- agente;
- performance;
- observabilidade;
- dados;
- dependências.

### Revalidação

- impacto técnico → F2;
- impacto funcional → F3;
- impacto no agente → F4;
- segurança → revalidar segurança;
- mudança ampla → múltiplas fases.

### Regression

Regressão crítica exige:

- correção;
- rollback;
- bloqueio;
- ou exceção formal.

### Segurança, secrets e permissões

Verificar:

- auth;
- authz;
- roles;
- policies;
- secrets;
- tokens;
- certificados;
- permissões MCP;
- least privilege.

### Secret Breaking

Considerar:

- expiração;
- rotação;
- revogação;
- alteração;
- credencial inválida;
- quebra de acesso.

### Produção

Usar sinais da F5:

- volume;
- sucesso/erro;
- latência;
- p95/p99;
- timeouts;
- retries;
- disponibilidade;
- dependências;
- uso pelo agente;
- distribuição de seleção;
- incidentes.

### Incidentes

Para cada incidente:

- estava coberto pelo dataset?
- causa?
- técnico/funcional/agente?
- novo teste?
- precisa reexecutar alguma fase?

### Dataset

Adicionar:

- novos comportamentos;
- regras;
- fronteiras;
- hard negatives;
- incidentes;
- confusão;
- regressões.

Proveniência:

- `team-provided`
- `independent`
- `production-incident`
- `regression`
- `hard-negative`

### Decisões

- KEEP
- UPDATE
- REVALIDATE
- DEPRECATE
- REPLACE

Fluxo:

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

---

# 15. One-page — Requisitos Atuais

O one-page visual deve apresentar:

**Roadmap de Certificação e Ciclo de Vida de Tools para o Agente**

Subtítulo:

> Da definição à operação contínua, com validação técnica, funcional e do uso pelo agente, observabilidade, rollout e revisão ao longo do tempo.

Cada fase:

- número;
- título;
- objetivo;
- principais atividades;
- **Saída**;
- **Responsáveis desta fase**.

## Importante

A seção **Responsáveis desta fase** deve estar vazia.

Exemplo:

```text
Responsáveis desta fase

[ espaço vazio ]
```

Não colocar símbolos ou texto dentro.

## Rodapé

### Papéis e times

- Owner da Tool
- Agentes Satélite
- SRE/Operações
- Segurança
- Plataforma

### Fluxo geral

`1 → 2 → 3 → 4 → 5 → 6 → 7`

Agrupamento:

- Certificação: F1–F4
- Entrada em produção: F5–F6
- Ciclo de vida: F7

### Decisões no ciclo de vida

- KEEP
- UPDATE
- REVALIDATE
- DEPRECATE
- REPLACE

## Saídas desejadas por fase

**F1:** Pacote completo e pronto para iniciar a validação técnica.

**F2:** Tool tecnicamente aprovada.

**F3:** Contrato funcional da Tool validado, incluindo fronteira funcional.

**F4:** Agente demonstrou capacidade de utilizar a Tool corretamente.

**F5:** Capacidade operacional e observabilidade implementadas.

**F6:** Tool em produção no nível planejado, com rollout concluído e aprovado.

**F7:** Tool mantida, atualizada, revalidada ou descontinuada conforme necessidade.

---

# 16. Backlog / Notas Pessoais — Não misturar automaticamente aos documentos oficiais

1. Revisar documentação MCP existente para identificar campos existentes e lacunas.
2. Abrir ticket formal para controlar SLA do onboarding.
3. Revisar roadmap/processo atual do time antes da formalização.
4. Criar um run recorrente dos tickets de onboarding, possivelmente diário.
5. Garantir dataset com positivos, negativos, hard negatives, no-tool e fronteiras.
6. Adicionar links de dataset, documentação e Datadog na F1.
7. Estudar OPA para políticas de segurança das APIs utilizadas pelo MCP.
8. Estudar criação de Skill em Devin para automação.
9. Tornar Validation Collection obrigatória.
10. Documentar geração do dataset qualitativa e quantitativamente.
11. Incluir Secret Breaking no contexto da role da Tool.

---

# 17. Princípios que o próximo agente deve preservar

1. **Não misturar F2/F3 com F4.** F2 e F3 não usam o agente.
2. **F4 é a primeira fase de avaliação do agente.**
3. **F5 operacionaliza observabilidade; F6 executa rollout.**
4. **F7 é lifecycle/feedback loop, não apenas mais uma rodada de testes.**
5. **Evidência é obrigatória para PASS.**
6. **Dataset do time da Tool é referência, não fonte única da avaliação do agente.**
7. **Hard negatives são essenciais para evitar regressão de Tool selection.**
8. **Thresholds devem existir antes da avaliação.**
9. **Owners reais ainda não estão definidos.**
10. **No one-page, as caixas de “Responsáveis desta fase” devem permanecer vazias.**
11. **A legenda inferior pode mostrar os possíveis papéis, incluindo Plataforma.**
12. **A seção da fase deve se chamar “Saída”, não “Entregas da fase”.**
13. **Agentes Satélite é o nome do time do agente/MCP; não separar esse time em “Plataforma” e “Time do Agente”.**
14. **Plataforma continua como possível papel separado na legenda inferior do one-page.**

---

# 18. Próximos Passos Prováveis

- Revisar novamente as 7 fases.
- Revisar o one-page.
- Confirmar os papéis da legenda.
- Definir owners reais posteriormente.
- Gerar versão final dos PDFs.
- Gerar versão final do one-page.
- Refinar automação do processo.
- Avaliar automação com Devin/Skills.
- Estruturar dataset e pipeline de execução/evidências.
