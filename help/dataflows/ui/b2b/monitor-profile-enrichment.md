---
description: Use o painel [!UICONTROL Profile Enrichment] para entender se os trabalhos de enriquecimento de perfil foram executados e concluídos com êxito, e para exibir as métricas básicas para medir a eficácia dos enriquecimentos.
solution: Experience Platform
title: Monitorar trabalhos de enriquecimento de perfil
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Monitorar trabalhos de enriquecimento de perfil na interface {#monitor-profile-enrichment}

Use o painel [!UICONTROL Profile Enrichment] para entender se os trabalhos de enriquecimento de perfil foram executados e concluídos com êxito, e para exibir as métricas básicas para medir a eficácia dos enriquecimentos.

Na [Interface do usuário do Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Monitoring]** na navegação à esquerda para acessar o painel [!UICONTROL Monitoring]. No seletor de exibição, selecione **Fluxo B2B** para ver os elementos do painel específicos do [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  O painel [!UICONTROL Monitoring] inclui as métricas básicas da execução bem-sucedida mais recente e o status diário do trabalho até 90 dias retroativos.

## Enriquecimento de perfil de contas relacionadas {#related-accounts}

O painel [!UICONTROL Related accounts] mostra as métricas básicas e o status do trabalho diário específico para o enriquecimento do perfil de [Contas relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Indicação visual de como acessar a tela de monitoramento de trabalhos de enriquecimento de perfil na interface do usuário do Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Os dados no cartão **[!UICONTROL Metrics]** incluem as métricas básicas da execução bem-sucedida mais recente do trabalho Contas Relacionadas.

As seguintes métricas estão disponíveis para trabalhos de enriquecimento de perfil de contas relacionadas:

| Métrica | Descrição |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Indica o total de perfis de conta aos quais sua organização tem acesso. |
| **[!UICONTROL Account groups]** | Indica o número de grupos de contas agrupados pelo trabalho de aprendizado de máquina de contas relacionado. |
| **[!UICONTROL Single-account groups]** | Indica o número de contas que não estão agrupadas com outras contas. |
| **[!UICONTROL Largest group size]** | Indica o tamanho do maior grupo de contas relacionado. O tamanho máximo permitido do grupo é 30. |
| **[!UICONTROL Median group size]** | Indica o tamanho médio dos grupos de contas relacionados na organização. |
| **[!UICONTROL Last successful run]** | Indica a data e a hora da última execução de trabalho de contas relacionadas bem-sucedida. |
| **[!UICONTROL Status]** | Indica o status (bem-sucedido, com falha ou em processamento) do trabalho de contas relacionado. |
| **[!UICONTROL Message]** | Indica uma mensagem de erro ou de aviso para uma execução de tarefa específica. |

## Enriquecimento de perfil de correspondência de contas de cliente potencial {#lead-to-account-matching}

O painel [!UICONTROL Lead to account matching] mostra as métricas básicas e o status diário de execução de trabalho específico para o enriquecimento do perfil [Lead to account matching](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Enriquecimento do perfil de correspondência de contas](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

As seguintes métricas estão disponíveis para trabalhos de enriquecimento do perfil de correspondência de clientes potenciais com contas:

| Métrica | Descrição |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Indica o número total de pessoas associadas a uma conta. |
| **[!UICONTROL Total accounts]** | Indica o número total de contas. |
| **[!UICONTROL Existing persons with accounts]** | Indica o número de pessoas que já estão associadas a uma conta das fontes de dados. |
| **[!UICONTROL Persons matched]** | Indica o número de pessoas que corresponderam a uma conta. |
| **[!UICONTROL Persons unmatched]** | Indica o número de pessoas que não corresponderam a uma conta. |
| **[!UICONTROL Last successful run]** | Indica a data e a hora do último lead bem-sucedido para a execução do trabalho de correspondência de contas. |
| **[!UICONTROL Status]** | Indica o status (bem-sucedido, com falha ou em processamento) do trabalho de correspondência do cliente potencial à conta. |

## Enriquecimento preditivo de perfil de pontuação de leads e contas {#predictive-lead-to-account-scoring}

O painel [!UICONTROL Predictive lead and account scoring] mostra as métricas básicas e o status diário de execução de trabalho específicos para o enriquecimento do perfil de [Pontuação preditiva de leads e contas](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md).

![Enriquecimento preditivo de perfil de pontuação de leads e contas](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

As seguintes métricas estão disponíveis para trabalhos de enriquecimento de perfil de pontuação preditiva de leads e contas:

| Métrica | Descrição |
| --------- | ---------- |
| **[!UICONTROL Job start]** | Indica a data e a hora de início da execução preditiva do trabalho de pontuação de lead e conta. |
| **[!UICONTROL Processing time]** | O tempo total necessário para a conclusão do trabalho. |
| **[!UICONTROL Score name]** | O nome da pontuação do job. |
| **[!UICONTROL Profile type]** | O tipo da pontuação: <ul><li>Pessoa</li><li>Conta</li></ul>. |
| **[!UICONTROL Job type]** | O tipo do trabalho:<ul><li>Pontuação</li><li>Treinamento</li>. |
| **[!UICONTROL Status]** | Indica o status (bem-sucedido, com falha ou em processamento) do lead preditivo e do trabalho de pontuação da conta. |

## Controles de interface do usuário {#ui-controls}

Esta seção descreve várias opções da interface do usuário na interface de monitoramento, que permitem filtrar as métricas exibidas na página.

Use o ícone de seta (![ícone de seta](/help/images/icons/chevron-up.png)) para expandir ou descartar o cartão na parte superior da tela, que mostra informações sobre os trabalhos de enriquecimento de perfil.

![Gravação de tela que mostra o controle da interface do ícone de seta.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Use o botão **[!UICONTROL Metrics and graphs]** para descartar o modo de exibição que mostra as métricas mais recentes.

![Gravação de tela que mostra a alternância de métricas e gráficos.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Use o botão de alternância **[!UICONTROL Show failures only]** para exibir apenas os trabalhos de enriquecimento de perfil com falha.

![Gravação de tela que mostra a opção Mostrar somente falhas.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, agora é possível monitorar e entender com êxito as métricas de trabalhos de enriquecimento de perfil. Consulte os seguintes documentos para obter mais detalhes:

* [Contas relacionadas no Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Guia Contas relacionadas no guia da interface do usuário Perfil de conta](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead para correspondência de contas no Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Pontuação preditiva de leads e contas no Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
