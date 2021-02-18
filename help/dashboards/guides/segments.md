---
keywords: Experience Platform;perfil;segmento;segmentos;segmentação;interface do usuário;UI;personalização;painel de segmento;painel;;;segment;segmentation;user interface;personalization;segment;
title: Painel de segmentos
description: 'A Adobe Experience Platform fornece um painel através do qual você pode visualização informações importantes sobre segmentos criados pela sua organização. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# (Beta) painel de segmentos {#segment-dashboard}

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualização informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmentos na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Adobe Experience Platform Segmentation Service na interface do usuário da plataforma, visite o [guia da interface do usuário do Serviço de segmentação](../../segmentation/ui/overview.md).

## Dados do painel do segmento

O painel do segmento exibe um instantâneo dos dados do atributo (registro) que sua organização tem no repositório de Perfis no Experience Platform. O instantâneo não inclui nenhum dado de evento (série cronológica).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi realizado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmento não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi realizado não serão refletidas no painel até que o próximo instantâneo seja realizado.

## Explorar o painel de segmento

Para navegar até o painel de segmento na interface do usuário da plataforma, selecione **[!UICONTROL Segmentos]** no painel esquerdo, em seguida, selecione a guia **[!UICONTROL Visão geral]** para exibir o painel.

![](../images/segments/dashboard-overview.png)

### Selecionar um segmento

O painel selecionará automaticamente um segmento a ser exibido, mas é possível alterar o segmento exibido usando o menu suspenso. Para escolher um segmento diferente, selecione a lista suspensa ao lado do nome do segmento e selecione o segmento que deseja visualização.

>[!NOTE]
>
>O menu suspenso mostra todos os segmentos criados por sua organização até o momento. Isso pode significar que você precisará rolar para visualização da lista completa dos segmentos disponíveis.

![](../images/segments/change-segment.png)

### Widgets e métricas

O painel de segmentos é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre seu segmento selecionado. A data e a hora &quot;última atualização&quot; no widget mostram quando o último instantâneo dos dados foi realizado.

![](../images/segments/widget-timestamp.png)

## Widgets disponíveis

O Experience Platform fornece vários widgets que você pode usar para visualizar diferentes métricas relacionadas ao seu segmento. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL Tamanho do segmento]](#segment-size)
* [[!UICONTROL Perfis adicionados ao longo do tempo]](#profiles-added-over-time)
* [[!UICONTROL Perfis por namespace]](#profiles-by-namespace)

### [!UICONTROL Tamanho do segmento] {#segment-size}

O widget **[!UICONTROL Tamanho do segmento]** exibe o número total de perfis unidos no segmento selecionado no momento em que o snapshot foi realizado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos dados do Perfil para unir os fragmentos do perfil e formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Perfis adicionados ao longo do tempo] {#profiles-added-over-time}

O widget **[!UICONTROL Perfis adicionados ao longo do tempo]** fornece informações sobre o número total de perfis no segmento como capturados durante o snapshot diário, nos últimos 30 dias. Este widget exibe como o tamanho do segmento pode ter mudado em um período de 30 dias, à medida que novos perfis se qualificam para ou saem do segmento.

Para saber mais sobre a avaliação de segmentos e como os perfis se qualificam e saem dos segmentos, consulte a [documentação do Serviço de Segmentação](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Perfis por namespace] {#profiles-by-namespace}

O widget **[!UICONTROL Perfis por namespace]** exibe o detalhamento das namespaces em todos os perfis unidos no segmento selecionado. O número total de perfis por namespace de identidade ([!UICONTROL namespace de ID] no widget) pode ser maior que o número total de perfis no segmento porque um perfil pode ter várias namespaces associadas a ele. Em outras palavras, a adição dos valores mostrados para cada namespace pode totalizar mais do que o total de perfis no segmento, pois se um cliente interagir com sua marca em mais de um canal, várias namespaces podem estar associadas a esse cliente individual.

Para saber mais sobre namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Próximas etapas

Ao seguir esse documento, você deve ser capaz de localizar o painel de segmento e selecionar um segmento para visualização. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).