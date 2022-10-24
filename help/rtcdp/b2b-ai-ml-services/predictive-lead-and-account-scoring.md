---
title: Lead preditivo e pontuação de conta no Real-Time CDP B2B
type: Documentation
description: Uma visão geral e mais informações sobre o lead preditivo e o recurso de pontuação de conta na Experience Platform CDP B2B.
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Lead preditivo e pontuação de conta no Real-Time CDP B2B

Os profissionais de marketing B2B enfrentam vários desafios no topo do funil de marketing. Para serem eficazes, os profissionais de marketing B2B precisam de uma maneira automatizada de qualificar o grande número de pessoas para que possam se concentrar nos alvos de alto valor. A qualificação deve ser alinhada ao resultado final das vendas, não apenas à conversão de marketing.

Contas são as entidades que compram produtos e serviços B2B. Para comercializar e vender eficazmente, os profissionais de marketing B2B têm de saber não só a probabilidade de compra da pessoa, mas também a probabilidade de compra da conta.

Marketing baseado em conta, em particular, estrategize contas como alvos de marketing. As pontuações de propensão de conta para comprar ajudam muito os profissionais de marketing B2B a priorizar as contas para maximizar o retorno sobre o investimento.

O serviço preditivo de lead e pontuação de contas trata dos desafios acima, aprendendo e prevendo os eventos de conversão do estágio de oportunidade, e agregando atividades pessoais no nível da conta para produzir as pontuações da conta. As pontuações estão prontamente disponíveis como campos personalizados em perfis de pessoa e perfis de conta, e podem ser facilmente incluídas como critérios de segmento para refinar seu público-alvo. Os principais fatores influentes também estão disponíveis no nível agregado e unitário para ajudar os profissionais de marketing B2B a entender melhor quais elementos levaram as pontuações.

## Noções básicas sobre lead preditivo e pontuação de conta {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] atualmente, a fonte de dados é necessária, pois é a única fonte de dados que pode fornecer os eventos de conversão no nível do perfil da pessoa.

A Pontuação preditiva de lead e conta usa um método de aprendizado de máquina baseado em árvore (aumento aleatório de floresta/gradiente) para criar o modelo preditivo de pontuação de lead.

Os administradores têm a capacidade de configurar várias metas de pontuação de perfil, também conhecidas como modelos, uma para cada evento de conversão configurado, permitindo que pontuações separadas sejam geradas para cada meta configurada.

A pontuação preditiva de lead e conta suporta os seguintes tipos e campos de meta de conversão:

| Tipo de meta | Campos |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Exemplo: `opportunityEvent.dataValueChanges.attributeName` igual `Stage` e `opportunityEvent.dataValueChanges.newValue` igual `Contract`</ul> |

O algoritmo considera os seguintes atributos e dados de entrada:

* Perfil da pessoa

| Campo XDM | Obrigatório / Opcional |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obrigatório |
| `workAddress.country` | Opcional |
| `extSourceSystemAudit.createdDate` | Obrigatório |
| `extendedWorkDetails.jobTitle` | Opcional |

>[!NOTE]
> 
>O algoritmo só inspeciona `sourceAccountKey.sourceKey` no grupo de campos Person:personComponents .

* Perfil da conta

| Campo XDM | Obrigatório / Opcional |
| --- | --- |
| `accountKey.sourceKey` | Obrigatório |
| `extSourceSystemAudit.createdDate` | Obrigatório |
| `accountOrganization.industry` | Opcional |
| `accountOrganization.numberOfEmployees` | Opcional |
| `accountOrganization.annualRevenue.amount` | Opcional |

* Evento de experiência

| Campo XDM | Obrigatório / Opcional |
| --- | --- |
| `_id` | Obrigatório |
| `personKey.sourceKey` | Obrigatório |
| `timestamp` | Obrigatório |
| `eventType` | Obrigatório |

Há suporte para vários modelos, com os seguintes limites rígidos definidos:

* Cada sandbox de produção tem direito a cinco modelos.
* Cada sandbox de desenvolvimento tem direito a um modelo.

Os requisitos de qualidade dos dados são os seguintes:

* Idealmente, há dois anos dos dados mais recentes para fins de formação.
* O comprimento mínimo de dados necessário é de seis meses mais a janela de previsão.
* Para cada meta de previsão, são necessários pelo menos 10 eventos de conversão qualificados.

As tarefas de pontuação são executadas diariamente e os resultados são salvos como atributos de perfil e atributos de conta, que podem ser usados em definições e personalização de segmento. Os insights de análise prontos também estão disponíveis no painel de visão geral da conta.

Consulte a documentação para obter mais informações sobre como [gerenciar lead preditivo e pontuação de conta](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) serviço.

## Exibir resultados previsíveis de lead e pontuação de contas {#how-to-view}

Após a execução do trabalho, os resultados são salvos em um novo conjunto de dados do sistema para cada modelo sob o nome `LeadsAI.Scores` - ***o nome da pontuação***. Cada grupo de campo de pontuação pode estar localizado em `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Atributo | Descrição |
| --- | --- |
| Pontuação | A probabilidade relativa de um perfil atingir a meta prevista dentro do período definido. Este valor não deve ser tratado como uma porcentagem de probabilidade, mas sim a probabilidade de um perfil em comparação com a população geral. Essa pontuação varia de 0 a 100. |
| Percentil | Esse valor fornece informações sobre o desempenho de um perfil em relação a outros perfis com pontuação semelhante. Os percentis variam de 1 a 100. |
| Tipo de modelo | O tipo de modelo selecionado indica se é uma pontuação de pessoa ou conta. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Motivos previstos para a conversão provável de um perfil. Os fatores são compostos pelos seguintes atributos:<ul><li>Código: O perfil ou atributo comportamental que influencia positivamente a pontuação prevista de um perfil.</li><li>Valor: O valor do perfil ou do atributo comportamental.</li><li>Importância: Indica o peso que o perfil ou atributo comportamental tem na pontuação prevista (baixo, médio, alto).</li></ul> |

### Exibir pontuações do perfil do cliente

Para exibir as pontuações preditivas de um perfil de pessoa, selecione **[!UICONTROL Perfis]** na seção customer do painel esquerdo e, em seguida, insira o namespace de identidade e o valor de identidade. Depois de concluído, selecione **[!UICONTROL Exibir]**.

Em seguida, selecione o perfil na lista.

![Perfil do cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

O **[!UICONTROL Detalhe]** agora inclui as pontuações preditivas. Clique no ícone do gráfico ao lado da pontuação preditiva.

![Pontuação preditiva do perfil do cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Uma caixa de diálogo pop-up mostra a pontuação, a distribuição geral da pontuação, os principais fatores influentes para essa pontuação e a definição da meta da pontuação.

![Detalhes da pontuação preditiva do perfil do cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Monitorar trabalhos preditivos de lead e pontuação de contas {#monitoring-jobs}

Você pode monitorar métricas básicas e o status diário de execução de tarefas por meio do painel. As métricas incluem:

* Total de perfis de pessoa/conta pontuados
* Próximo trabalho de pontuação (data)
* Próximo emprego de formação (data)

Para obter mais informações, consulte a documentação em [monitorar tarefas para lead preditivo e pontuação de contas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
