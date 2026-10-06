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

