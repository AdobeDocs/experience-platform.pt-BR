---
title: Detalhes do modelo de otimização de tempo de envio
description: Saiba mais sobre o modelo de IA usado para Otimização de tempo de envio no Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: d1c7d1038b45bae4c014e3488f55a427c9cb02ed
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Detalhes do modelo de otimização de tempo de envio

## Visão geral do modelo {#model-overview}

* **Nome e versão do modelo**: otimização de tempo de envio
* **Data de lançamento do modelo**: setembro de 2024
* **Finalidade do modelo**: o modelo de Otimização de tempo de envio da Adobe Journey Optimizer escolhe o tempo de envio ideal para mensagens de email e push para maximizar a participação do consumidor, com base no histórico do comportamento de abertura e de clique dos consumidores.
* **Usuários pretendidos**: os principais usuários deste modelo são profissionais de marketing, gerentes de produtos e equipes de engajamento do cliente que utilizam a Adobe Journey Optimizer para impulsionar estratégias de marketing orientadas por dados.
* **Casos de uso**: a Otimização de Tempo de Envio é melhor usada em comunicações de marketing menos urgentes, por exemplo, um anúncio semanal, informações promocionais sobre um novo produto ou informações sobre uma venda de um mês. A Otimização de tempo de envio está disponível apenas para os tipos de ação de Email e Push integrados da Journey Optimizer e não está disponível no momento para mensagens enviadas por meio de ações personalizadas ou para outros tipos de ação.
* **Possível uso incorreto**: a Otimização de Tempo de Envio não deve ser usada para mensagens operacionais urgentes e sensíveis ao tempo, por exemplo, uma confirmação de pedido, uma notificação de redefinição de senha ou uma notificação de alteração da porta de voo.

## Detalhes do modelo {#model-details}

* **Tipo de modelo**: o modelo de Otimização de tempo de envio assimila os dados de comportamento do consumidor da Adobe Journey Optimizer de sua organização e examina eventos de abertura e de clique no nível do usuário para prever quando seus consumidores têm maior probabilidade de se envolver com suas mensagens. O comportamento de abertura e clique no nível do consumidor para cada hora da semana é ponderado e combinado com o comportamento semelhante e geral do consumidor usando um estimador [!DNL Bayesian]. As [!DNL Bayesian] previsões para cada hora da semana são classificadas, resultando em um &quot;mapa de calor&quot; para cada métrica (aberturas de email, cliques de email e aberturas por push), para cada cliente, para prever as horas da semana em que entrar em contato com cada consumidor tem mais e menos probabilidade de resultar no resultado do compromisso desejado.
* **Entrada**: a Otimização de Tempo de Envio utiliza dados de fuso horário do consumidor no campo `timeZone` do grupo de campos [!UICONTROL Detalhes de Preferência], se fornecidos, para determinar o fuso horário de um consumidor. Se o fuso horário de um consumidor não estiver disponível no campo `timeZone`, a Otimização de Tempo de Envio tentará inferir o fuso horário do consumidor, com base na correspondência de fuso horário mais comum com o primeiro endereço postal encontrado armazenado no perfil do consumidor usando o [tipo de dados de endereço postal](../../xdm/data-types/postal-address.md). A Otimização de tempo de envio faz previsões para cada consumidor com base em três tipos de dados comportamentais:
   * O comportamento de abrir e clicar de seus consumidores em geral.
   * O comportamento de abrir e clicar de consumidores semelhantes no mesmo fuso horário.
   * O comportamento de abrir e clicar desse consumidor individual.
* **Saída**: essas previsões são ponderadas e combinadas usando uma abordagem [!DNL Bayesian], resultando em um &quot;mapa de calor&quot; para cada métrica (aberturas de email, cliques de email e aberturas por push), para cada cliente, que indica as horas da semana em que o contato com esse consumidor tem maior e menor probabilidade de resultar no resultado do compromisso desejado (abrir/clicar), conforme ilustrado no exemplo de mapa de calor abaixo:

![O mapa de calor de Otimização de Tempo de Envio.](../images/models/send-time-optimization.png)

* **Exemplo de entrada e saída**: para minimizar o impacto do modelo na riqueza do perfil, as pontuações do modelo são armazenadas e compactadas em três atributos de Perfil armazenados em `_experience.intelligentServices.journeyAI.sendTimeOptimization` e não foram projetadas para serem legíveis por humanos.

## Treinamento de modelo {#model-training}

* **Dados de treinamento e pré-processamento**: o conjunto de dados de treinamento para cada organização é originado apenas de seus próprios dados na Adobe Experience Platform.
   * Quando o recurso de Otimização de tempo de envio está habilitado para sua organização, o modelo é treinado em eventos de email e push, envio, abertura e cliques em todas as jornadas e ações da organização nas últimas 16 semanas, independentemente de essas ações usarem a Otimização de tempo de envio. Isso permite que a Otimização de tempo de envio se beneficie de todos os dados gerados pelos seus consumidores.
   * Os modelos são inicialmente treinados e pontuados semanalmente. Após 16 semanas, os modelos são retreinados e remarcados mensalmente. A pontuação do modelo inclui todos os perfis de clientes, existentes e novos, desde a última execução de pontuação.
   * As mensagens enviadas pela Otimização de tempo de envio recebem uma das seguintes opções:
      * Um tempo de envio de mensagem de &quot;exploração&quot;, selecionado para testar tempos de envio diferentes e observar como os consumidores respondem.
      * Uma hora de envio de mensagem &quot;otimizada&quot;, selecionada para maximizar as taxas de clique/abertura. 5% dos eventos de envio recebem um tempo de envio de &quot;exploração&quot; e 95% dos eventos de envio são &quot;otimizados&quot;.
   * Os tempos de envio de exploração são selecionados aleatoriamente a partir dos tempos de envio disponibilizados pelo tempo máximo de espera configurado. Por exemplo, caso uma mensagem seja selecionada às 9h de quarta-feira com a Otimização de tempo de envio ativada e um tempo de espera máximo de 3 horas, os tempos de envio de exploração para a mensagem serão divididos uniformemente entre 9h, 10h, 11h e 12h.

## Avaliação do modelo {#model-evaluation}

* **Avaliação do modelo**: a Otimização de Tempo de Envio pode aumentar a taxa de cliques em emails e a taxa de abertura de push no intervalo de aproximadamente 2% a 10% em todas as mensagens otimizadas por uma organização.
   * Por exemplo, se uma organização que envia emails sem otimização de tempo de envio tiver uma taxa de cliques de 5,0% em média, o mesmo conjunto de emails com otimização de tempo de envio pode resultar em uma taxa de cliques de até 5,5% em média (5,0% * (1+10%) = 5,5%).
   * Devido à variabilidade em tamanhos pequenos de amostra, um benefício da Otimização de tempo de envio pode não ser observável em envios de mensagem única.
   * É mais provável que as organizações aproveitem melhor a Otimização de tempo de envio quando:
      * As jornadas existentes usam tempos de envio fixos e não bem otimizados;
      * A variabilidade no comportamento do consumidor (cliques e aberturas) corresponde à localização e às preferências do consumidor;
      * As organizações usam a Otimização de hora de envio em uma fração maior de mensagens de email e push;
      * As organizações escolhem tempos máximos de espera dentro do intervalo recomendado de 6 a 12 horas.

## Implantação do modelo {#model-deployment}

* **Atualização de modelo**: inicialmente, os modelos são treinados e pontuados semanalmente. Após 16 semanas, os modelos são retreinados e remarcados mensalmente. A pontuação do modelo inclui todos os perfis do consumidor, existentes e novos, desde a última execução de pontuação.

## Equidade e viés {#fairness-and-bias}

* **Integridade do modelo**: a inferência incorreta do fuso horário de um consumidor pode resultar no envio de uma mensagem antes do ideal para um determinado consumidor ou depois do ideal para um determinado consumidor. No entanto, todos os consumidores em uma comunicação que utiliza a Otimização de tempo de envio receberão uma mensagem e terão a oportunidade de interagir com ela. Além disso, esse modelo não utiliza dados demográficos do consumidor ou proxies para dados demográficos, apenas dados comportamentais do consumidor e de fuso horário do consumidor são utilizados. Por conseguinte, as preocupações em matéria de equidade são limitadas e atenuadas.
* **Polarização de dados**: a inferência incorreta do fuso horário de um consumidor pode resultar no envio de uma mensagem antes do ideal para um determinado consumidor ou depois do ideal para um determinado consumidor. No entanto, todos os consumidores em uma comunicação que utiliza a Otimização de tempo de envio receberão uma mensagem e terão a oportunidade de interagir com ela. Além disso, esse modelo não utiliza dados demográficos do consumidor ou proxies para dados demográficos, apenas dados comportamentais do consumidor e de fuso horário do consumidor são utilizados. Portanto, as preocupações com viés são limitadas e atenuadas.

## Robustez {#robustness}

* **Robustez do modelo**: perfis sem dados de evento de interação suficientes (geralmente o caso de novos perfis) receberão um horário de envio imediato, um horário de envio de exploração na janela selecionada ou um horário de envio com base no horário de envio de maior desempenho entre todos os clientes.

## Considerações éticas {#ethical-considerations}

* **Considerações éticas associadas ao modelo**: a inferência incorreta do fuso horário de um consumidor pode resultar no envio de uma mensagem antes do ideal para um determinado consumidor ou depois do ideal para um determinado consumidor. No entanto, todos os consumidores em uma comunicação que utiliza a Otimização de tempo de envio receberão uma mensagem e terão a oportunidade de interagir com ela. Além disso, esse modelo não utiliza dados demográficos do consumidor ou proxies para dados demográficos, apenas dados comportamentais do consumidor e de fuso horário do consumidor são utilizados. Portanto, as preocupações éticas são limitadas e atenuadas.