---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, painel de perfil, painel
title: Painel Destinos
description: O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os destinos ativos da sua organização.
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (Beta) [!UICONTROL Destinations] painel

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre os destinos ativos de sua organização, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de destinos na interface do usuário e fornece mais informações sobre as métricas exibidas no painel.

Para obter uma visão geral dos destinos, bem como um catálogo de todos os destinos disponíveis no Experience Platform, visite a [visão geral dos destinos](../../destinations/home.md).

## [!UICONTROL Destinations] dados do painel  {#destinations-dashboard-data}

O painel [!UICONTROL Destinations] exibe um instantâneo dos destinos que sua organização habilitou no Perfil de experiência. Os dados no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de destinos não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de destinos

Para navegar até o painel de destinos na interface do usuário da plataforma, selecione **[!UICONTROL Destinations]** no painel à esquerda e selecione a guia **[!UICONTROL Overview]** para exibir o painel.

![](../images/destinations/dashboard-overview.png)

## Widgets disponíveis

O Experience Platform fornece vários widgets que podem ser usados para visualizar métricas diferentes relacionadas aos destinos. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

O widget **[!UICONTROL Most used destinations]** exibe os principais destinos de sua organização por número de segmentos mapeados a partir do último instantâneo. Essa classificação fornece informações sobre quais destinos estão sendo utilizados, além de mostrar potencialmente aqueles que podem ser subutilizados.

Por exemplo, se você configurou um destino ontem, mas não mapeou nenhum segmento para ele, seria possível ver que o destino está subutilizado no momento.

O número de segmentos mapeados mostrados na coluna de contagem de segmentos é preciso a partir do último instantâneo diário. Mapear um novo segmento para o destino não atualizará a contagem até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, conforme vinculado pela guia **[!UICONTROL Browse]**. Você também pode selecionar **[!UICONTROL View All]** para navegar até a guia **[!UICONTROL Browse]** e selecionar o nome de um destino para exibir seus detalhes.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

O widget **[!UICONTROL Recently created destinations]** permite que você veja uma lista dos destinos configurados mais recentemente em sua organização.

A data criada mostrada é precisa do último instantâneo diário. Em outras palavras, se você criar um novo destino, ele não aparecerá na lista até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, conforme vinculado pela guia **[!UICONTROL Browse]**. Você também pode selecionar **[!UICONTROL View All]** para navegar até a guia **[!UICONTROL Browse]** e selecionar o nome de um destino para exibir seus detalhes.

Para saber mais sobre como configurar tipos específicos de destinos, visite a [documentação sobre destinos](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

O widget **[!UICONTROL Recently activated segments]** fornece uma lista dos segmentos mapeados mais recentemente para um destino. Esta lista fornece um instantâneo de quais segmentos e destinos estão sendo usados ativamente no sistema e pode ajudar na solução de problemas de mapeamentos incorretos.

A data atualizada mostrada exibe a última vez que o segmento foi ativado para o destino e é precisa do último instantâneo diário. Em outras palavras, se você ativar um segmento para o destino, a data atualizada não será alterada até que o próximo instantâneo seja tirado.

Selecionar o nome de um segmento na lista mostrada no widget leva você aos detalhes do segmento. Você também pode selecionar **[!UICONTROL View All]** para navegar até a guia de navegação do segmento e, em seguida, selecionar o nome de um segmento para exibir seus detalhes.

Para obter mais informações sobre como trabalhar com segmentos no Experience Platform, comece lendo a [Visão geral do serviço de segmentação](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Próximas etapas

Ao seguir este documento, você agora deve ser capaz de localizar o painel de destinos e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com destinos no Experience Platform, consulte a [documentação de destinos](../../destinations/home.md).
