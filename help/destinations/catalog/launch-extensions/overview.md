---
keywords: extensões de tag;extensão de tag;destinos de lançamento; extensões de tag da plataforma;extensão de tag da plataforma;destinos de lançamento da plataforma
title: Extensões de tag no Adobe Experience Platform
description: O Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags da Adobe. O Experience Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 2%

---

# Extensões de tag no Adobe Experience Platform

A Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags da Adobe. O Experience Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. As tags são oferecidas aos clientes do Adobe Experience Cloud como um recurso incluso de valor agregado.

Para obter uma introdução às tags, consulte os recursos abaixo:

- [Visão geral das tags](../../../tags/home.md)
- [Guia de início rápido](../../../tags/quick-start/quick-start.md)

## Como encontrar extensões de tag na interface do Experience Platform {#how-to-find-extensions-in-interface}

Para localizar as extensões na interface do Experience Platform, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no filtro **[!UICONTROL Tipos]**.

![Filtro de extensões na interface](../../assets/catalog/launch-extensions/filter.png)

## Como funcionam as extensões de tag {#how-extensions-work}

Uma [extensão de tag](../../../tags/home.md#extensions) é um pacote de código que aprimora a funcionalidade de um site ou aplicativo móvel. Isso pode incluir o envio de dados brutos do evento para um destino como [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md), mas eles também podem atender a outras funções.

É importante diferenciar entre extensões de encaminhamento de tags e eventos. As extensões exibidas na interface do usuário de destinos do Experience Platform são *extensões de tag*. Consulte a visão geral do encaminhamento de eventos para obter mais informações sobre as [diferenças entre as marcas e o encaminhamento de eventos](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Benefícios do uso de extensões de tag {#extensions-benefits}

Os recursos de tags da Experience Platform são gratuitos para clientes existentes da Experience Cloud. O sistema simplifica a implantação de tags no site por meio de extensões fáceis de usar que você pode instalar, configurar, atualizar e excluir. As tags ocupam pouco espaço no site e permitem que você mantenha suas páginas carregando rapidamente.

Embora não seja possível ativar públicos para extensões de tag, você pode configurar regras para encaminhar apenas dados do evento em determinadas situações. Essa poderosa funcionalidade permite encaminhar os dados do evento somente em determinadas situações, em vez de enviar dados do evento em cada interação. Para obter mais informações, leia sobre as regras na [documentação de tags](../../../tags/ui/managing-resources/rules.md).

## Exemplo de casos de uso para extensões {#extensions-use-cases}

As extensões permitem atender a vários casos de uso do cliente. Alguns exemplos de casos de uso para usar extensões são:

- Você pode enviar dados do site ou do aplicativo nativo para o Facebook por meio da extensão Facebook pixel. O Pixel do Facebook indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar o visitante pelo Facebook.
- Você pode encaminhar dados do evento de seus sites e aplicativos para o Google Analytics para analisar e tomar decisões com base nesses dados.
- Você pode ativar um aplicativo de chatbox no lado do cliente na hora certa com base em como os usuários estão interagindo com as páginas, de acordo com as regras configuradas.

## Categorias de extensão {#extension-categories}

As extensões podem se enquadrar nas seguintes categorias no Experience Platform:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gerenciamento de dados](../data-management/overview.md)
- [Destinos de marketing por email](../email-marketing/overview.md)
- [Personalização](../personalization/overview.md)
- [Pesquisas](../survey/overview.md)
- [Voz do cliente](../voice/overview.md)
