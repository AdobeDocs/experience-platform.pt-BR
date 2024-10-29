---
title: Notas de versão da Adobe Experience Platform de outubro de 2024
description: As notas de versão de outubro de 2024 da Adobe Experience Platform.
source-git-commit: a381bdc45ee9c3c7ffb32bb7a7ec43a1233d1556
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 25%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de outubro de 2024**

Atualizações dos recursos e da documentação existentes no Adobe Experience Platform:

- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Serviço de segmentação](#segmentation-service)
- [Sandboxes](#sandboxes)
- [Fontes](#sources)

<!-- ## Dashboards {#dashboards}

Experience Platform provides multiple dashboards through which you can view important insights about your organization's data, as captured during daily snapshots.

**New or updated features**

| Feature | Description |
| --- | --- |
| Data Distiller Templates | Explore multiple templates to gain structured insights into audience data. Use dashboards like **Advanced [!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]**, and **[!UICONTROL Audience Identity Overlaps]** to make data-driven decisions, optimize segmentation, and enhance engagement strategies. See the [Data Distiller Templates guide](../../dashboards/sql-insights-query-pro-mode/templates/overview.md) for more details. |
| Advanced Audience Overlaps | Quickly analyze audience intersections for specific audiences or view all overlaps to uncover valuable insights across your entire audience set. Use these insights to refine segmentation, reduce redundant messaging, and create more targeted campaigns for improved marketing efficiency. See the [Advanced Audience Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) for more details. |
| Audience Comparison enhancements | View a side-by-side comparison of key metrics between different audience groups using the **Audience Comparison** dashboard. With this dashboard you can select specific time frames and KPIs, such as audience size and identity composition, to make more informed decisions about audience segmentation and targeting strategies. Read the [Audience Comparison guide](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) for more information. |
| Audience Trends Visualization | Analyze audience metrics over time with the **[!UICONTROL Audience Trends]** dashboard. Visualize trends for audience size, number of identities, and number of single identity profiles to help you monitor audience evolution, measure growth, and refine your engagement strategies. See the [Audience Trends guide](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) for more details. |
| Identity Overlaps Analysis | Analyze identity overlaps in selected audiences with the **[!UICONTROL Audience Identity Overlaps]** dashboard. View identity trends and breakdowns to understand how different identity types relate within your audience, enhancing identity stitching and improving customer segmentation accuracy. Refer to the [Audience Identity Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) for more details. |

{style="table-layout:auto"}

For more information on dashboards, including how to grant access permissions and create custom widgets, begin by reading the [dashboards overview](../../dashboards/home.md). -->

## Coleção de dados {#collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los para o Edge Network de Experience Platform, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

**Novos recursos**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Tags e extensões | Visualização JSON do Adobe Analytics | Agora você pode usar a extensão de tags da Adobe Analytics para examinar eVars, props e configurações de evento como JSON, que agora pode ser incluído na extensão SDK da Web e exportado para edição. Você também pode carregar ou copiar esses dados e armazená-los em seu dispositivo. Leia a [documentação de extensão do Adobe Analytics](../../tags/extensions/client/analytics/overview.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral da coleção de dados](../../collection/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Recurso | Descrição |
| ----------- | ----------- |
| [Suporte à exportação de matrizes disponível no geral](../../destinations/ui/export-arrays-calculated-fields.md) | Todos os clientes agora podem usar a opção **[!UICONTROL Adicionar campo calculado]** ao ativar públicos-alvo *para destinos baseados em arquivo* para exportar matrizes ou elementos de matrizes inteiras. Observe que ainda é necessário usar a função `array_to_string` para nivelar a matriz em uma cadeia de caracteres no arquivo de destino. <br> ![Adicionar seleção de campo calculado com funções e campos.](../2024/assets/october/array-export.gif "Adicionar campo calculado com uma seleção da função array_to_string e da matriz de organizações."){width="250" align="center" zoomable="yes"} |
| [Aprimoramentos na precisão dos relatórios para destinos de streaming](/help/destinations/ui/export-datasets.md) | A partir de outubro de 2024, o Adobe está lançando uma atualização para aumentar a precisão dos relatórios para destinos de transmissão. Esse aprimoramento garante um melhor alinhamento entre os relatórios da Experience Platform e das plataformas de destino. <br> Antes desta atualização, **[!UICONTROL Falha nas identidades]** incluiu todas as tentativas de ativação. Após essa atualização, somente a última tentativa de ativação será incluída na contagem total. <br> Atualmente, este aprimoramento se aplica ao [destino de Correspondência de Cliente do Google](../../destinations/catalog/advertising/google-customer-match.md), mas será gradualmente implantado em outros destinos de streaming de Experience Platform. Após esse aprimoramento, os usuários do [destino de Correspondência do Cliente do Google](../../destinations/catalog/advertising/google-customer-match.md) poderão observar uma queda esperada em sua contagem de **[!UICONTROL Falha nas identidades]**. |
| Implicações flexíveis da avaliação do público-alvo na [ativação do público-alvo em lote](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Se você executar a [avaliação flexível do público-alvo](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) em públicos que já estão definidos para serem ativados após a avaliação do segmento, os públicos-alvo serão ativados assim que o trabalho de avaliação flexível do público-alvo for concluído, independentemente de quaisquer trabalhos de ativação diários anteriores. <br> Isso pode resultar na exportação de públicos-alvo várias vezes ao dia, com base em suas ações. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de destinos](../../destinations/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| [!BADGE Disponibilidade limitada]{type=Informative} Avaliação flexível de público | A avaliação flexível do público-alvo permite criar rapidamente novos públicos-alvo sob demanda para comunicações sensíveis ao tempo. Mais informações sobre este novo recurso podem ser encontradas na [documentação do Portal de Público](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service], leia a [Visão geral da segmentação](../../segmentation/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Compartilhamento de pacotes de ferramentas de sandbox | Agora você pode usar as ferramentas de sandbox para exportar e importar facilmente configurações de sandbox entre sandboxes em diferentes organizações. Agora há duas categorias de pacotes compartilhados disponíveis:<br><ul><li>**[Pacote privado](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Use o compartilhamento de pacotes privados com organizações que aprovaram a solicitação de compartilhamento da organização de origem.</li><li>**[Pacote público](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** pacotes públicos podem ser compartilhados sem aprovações adicionais e são facilmente importados usando a carga do pacote.</li></ul><br>Para obter mais informações sobre esses recursos, leia o manual sobre [compartilhamento de pacotes entre organizações](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Compartilhamento de pacotes](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) na API de ferramentas de sandbox | Use a API de ferramentas de sandbox para fazer solicitações a dois novos pontos de extremidade, `/handshake` e `/transfer`, para compartilhar entre organizações, buscar e criar solicitações de compartilhamento de pacotes. Uma solicitação adicional foi adicionada ao ponto de extremidade `/packages` para recuperar a carga de um pacote. |

{style="table-layout:auto"}

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes na Experience Platform para assimilar dados de um aplicativo da Adobe ou de uma fonte de dados de terceiros.

**Recurso atualizado**

| Recurso | Descrição |
| --- | --- |
| Suporte para filtrar entidades de atividade padrão em [!DNL Marketo Engage] | Você pode usar a API [!DNL Flow Service] para filtrar entidades de atividade padrão ao assimilar dados da sua origem [!DNL Marketo Engage]. Leia o manual sobre [filtragem [!DNL Marketo] dados de atividade padrão](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).
