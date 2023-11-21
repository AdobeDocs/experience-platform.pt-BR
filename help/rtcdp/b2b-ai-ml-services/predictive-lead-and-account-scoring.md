---
title: Pontuação preditiva de leads e contas no Real-Time CDP B2B
type: Documentation
description: Uma visão geral e mais informações sobre o recurso preditivo de lead e pontuação de conta no Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Pontuação preditiva de leads e contas no Real-Time CDP B2B

Os profissionais de marketing B2B enfrentam vários desafios no topo do funil de marketing. Para serem eficazes, os profissionais de marketing B2B precisam de uma maneira automatizada de qualificar o grande número de pessoas para que possam se concentrar nos alvos de alto valor. A qualificação deve estar alinhada ao resultado final das vendas, não apenas à conversão de marketing.

As contas do são as entidades finais que compram produtos e serviços B2B. A fim de comercializar e vender de forma eficaz, os profissionais de marketing B2B são obrigados a conhecer não só a probabilidade de compra do indivíduo, mas também da conta.

Marketing baseado em conta, em particular, crie estratégias de contas como alvos de marketing. As pontuações de propensão para compra da conta ajudam muito os profissionais de marketing B2B a priorizar entre as contas para maximizar o retorno sobre o investimento.

O serviço de pontuação preditiva de leads e contas lida com os desafios acima, aprendendo e prevendo os eventos de conversão do estágio de oportunidade e agregando atividades de pessoas no nível da conta para produzir as pontuações da conta. As pontuações estão prontamente disponíveis como campos personalizados em perfis de pessoas e perfis de contas e podem ser facilmente incluídas como critérios de segmento para refinar seu público-alvo. Os principais fatores influentes também estão disponíveis no nível agregado e de unidade para ajudar os profissionais de marketing B2B a entender melhor quais elementos determinaram as pontuações.

## Noções básicas sobre lead preditivo e pontuação de conta {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] a fonte de dados é necessária no momento, pois é a única fonte de dados que pode fornecer os eventos de conversão no nível do perfil de pessoa.

A Pontuação preditiva de leads e contas usa um método de aprendizado de máquina baseado em árvore (aumento aleatório de floresta/gradiente) para criar o modelo preditivo de pontuação de leads.

Os administradores têm a capacidade de configurar várias metas de pontuação de perfil, também chamadas de modelos, uma para cada evento de conversão configurado, permitindo que pontuações separadas sejam geradas para cada meta configurada.

A pontuação preditiva de leads e contas é compatível com os seguintes tipos e campos de meta de conversão:

| Tipo de meta | Campos |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Exemplo: `opportunityEvent.dataValueChanges.attributeName` igual a `Stage` e `opportunityEvent.dataValueChanges.newValue` igual a `Contract`</ul> |

O algoritmo considera os seguintes atributos e dados de entrada:

* Perfil de pessoa

| Campo XDM | Obrigatório / Opcional |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obrigatório |
| `workAddress.country` | Opcional |
| `extSourceSystemAudit.createdDate` | Obrigatório |
| `extendedWorkDetails.jobTitle` | Opcional |

>[!NOTE]
> 
>O algoritmo só inspeciona `sourceAccountKey.sourceKey` no grupo de campos Person:personComponents.

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

Vários modelos são compatíveis, com os seguintes limites rígidos definidos:

* Cada sandbox de produção tem direito a cinco modelos.
* Cada sandbox de desenvolvimento tem direito a um modelo.

Os requisitos de qualidade dos dados são os seguintes:

* Idealmente, existem dois anos de dados mais recentes para fins de treinamento.
* O comprimento mínimo de dados necessário é de seis meses, mais a janela de previsão.
* Para cada meta de previsão, são necessários pelo menos 10 eventos de conversão qualificados.

Os trabalhos de pontuação são executados diariamente e os resultados são salvos como atributos de perfil e atributos de conta, que podem ser usados em definições de segmento e personalização. Os insights de análise prontos para uso também estão disponíveis no painel de visão geral da conta.

Consulte a documentação para obter mais informações sobre como [gerenciar lead preditivo e pontuação de conta](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) serviço.

## Exibir resultados preditivos de pontuação de leads e contas {#how-to-view}

Após a execução do trabalho, os resultados são salvos em um novo conjunto de dados do sistema para cada modelo com o nome `LeadsAI.Scores` - ***o nome da pontuação***. Cada grupo de campos de pontuação pode ser localizado em `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Atributo | Descrição |
| --- | --- |
| Pontuação | A probabilidade relativa de um perfil atingir a meta prevista dentro do período definido. Esse valor não deve ser tratado como uma porcentagem de probabilidade, mas sim como a probabilidade de um perfil em comparação com a população geral. Essa pontuação varia de 0 a 100. |
| Percentil | Esse valor fornece informações sobre o desempenho de um perfil em relação a outros perfis com pontuação semelhante. Os percentuais variam de 1 a 100. |
| Tipo de modelo | O tipo de modelo selecionado indica se é uma pontuação de pessoa ou de conta. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Motivos previstos sobre por que um perfil tem probabilidade de conversão. Os fatores são compostos pelos seguintes atributos:<ul><li>Código: o atributo de perfil ou comportamental que influencia positivamente a pontuação prevista de um perfil.</li><li>Valor: o valor do perfil ou atributo comportamental.</li><li>Importância: indica o peso que o perfil ou atributo comportamental tem na pontuação prevista (baixa, média, alta).</li></ul> |

### Exibir pontuações de perfil de cliente

Para exibir as pontuações preditivas de um perfil de pessoa, selecione **[!UICONTROL Perfis]** na seção customer do painel esquerdo e insira o namespace de identidade e o valor de identidade. Depois de concluído, selecione **[!UICONTROL Exibir]**.

Em seguida, selecione o perfil na lista.

![Perfil do cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

A variável **[!UICONTROL Detalhe]** A página agora inclui as pontuações preditivas. Clique no ícone do gráfico ao lado da pontuação preditiva.

![Pontuação preditiva de perfil do cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Uma caixa de diálogo pop-up mostra a pontuação, a distribuição geral da pontuação, os principais fatores influentes para essa pontuação e a definição da meta da pontuação.

![Detalhes da pontuação preditiva do perfil do cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Monitoramento de trabalhos de pontuação preditiva de leads e contas {#monitoring-jobs}

Você pode monitorar métricas básicas e status diário de execução de trabalho por meio do painel. As métricas incluem:

* Total de perfis de pessoa/conta pontuados
* Próximo trabalho de pontuação (data)
* Próximo trabalho de treinamento (data)

Para obter mais informações, consulte a documentação em [monitoramento de trabalhos para lead preditivo e pontuação de conta](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
