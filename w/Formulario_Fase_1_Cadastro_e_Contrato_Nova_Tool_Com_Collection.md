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

