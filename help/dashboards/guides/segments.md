---
keywords: Experience Platform, perfil, segmento, segmentos, segmentação, interface do usuário, interface do usuário, personalização, painel de segmentos, painel
title: Painel de segmentos
description: 'O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre segmentos criados por sua organização. '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# (Beta) Painel de segmentos {#segment-dashboard}

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmentos na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Serviço de segmentação da Adobe Experience Platform na interface do usuário da plataforma, visite o [Guia da interface do usuário do Serviço de segmentação](../../segmentation/ui/overview.md).

## Segmentar dados do painel

O painel de segmentos exibe um instantâneo dos dados de atributo (registro) que sua organização tem no armazenamento de Perfil no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmentos não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de segmentos

Para navegar até o painel de segmentos na interface do usuário da plataforma, selecione **[!UICONTROL Segments]** no painel à esquerda e selecione a guia **[!UICONTROL Overview]** para exibir o painel.

![](../images/segments/dashboard-overview.png)

### Selecionar um segmento

O painel selecionará automaticamente um segmento a ser exibido, mas você poderá alterar o segmento exibido usando o menu suspenso. Para escolher um segmento diferente, selecione o menu suspenso ao lado do nome do segmento e selecione o segmento que deseja visualizar.

>[!NOTE]
>
>O menu suspenso mostra todos os segmentos criados por sua organização até agora. Isso pode significar que você precisará rolar a página para visualizar a lista completa de segmentos disponíveis.

![](../images/segments/change-segment.png)

### Widgets e métricas

O painel de segmentos é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre o segmento selecionado. A data e a hora da &quot;última atualização&quot; no widget mostram quando o último instantâneo dos dados foi tirado.

![](../images/segments/widget-timestamp.png)

## Widgets disponíveis

O Experience Platform fornece vários widgets que podem ser usados para visualizar métricas diferentes relacionadas ao seu segmento. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

O widget **[!UICONTROL Segment size]** exibe o número total de perfis mesclados no segmento selecionado no momento em que o instantâneo foi tirado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos seus dados de Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

O widget **[!UICONTROL Profiles added over time]** fornece informações sobre o número total de perfis no segmento conforme capturados durante o instantâneo diário, nos últimos 30 dias. Este widget exibe como o tamanho do segmento pode ter mudado em um período de 30 dias, à medida que novos perfis se qualificam para ou saem do segmento.

Para saber mais sobre a avaliação de segmentos e como os perfis se qualificam e saem dos segmentos, consulte a [documentação do Serviço de segmentação](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

O widget **[!UICONTROL Profiles by namespace]** exibe o detalhamento dos namespaces em todos os perfis mesclados no segmento selecionado. O número total de perfis por namespace de identidade ([!UICONTROL ID namespace] no widget) pode ser maior que o número total de perfis no segmento, pois um perfil pode ter vários namespaces associados a ele. Em outras palavras, adicionar os valores mostrados para cada namespace pode totalizar mais do que o total de perfis no segmento, pois se um cliente interagir com sua marca em mais de um canal, vários namespaces podem ser associados a esse cliente individual.

Para saber mais sobre os namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Próximas etapas

Agora, ao seguir este documento, é possível localizar o painel de segmentos e selecionar um segmento a ser exibido. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).
