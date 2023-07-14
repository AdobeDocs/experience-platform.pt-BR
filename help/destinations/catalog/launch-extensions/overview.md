---
keywords: extensões de tag;extensão de tag;destinos de lançamento; extensões de tag da plataforma;extensão de tag da plataforma;destinos de platforms launch
title: Extensões de tag no Adobe Experience Platform
description: A Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags do Adobe. O Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Extensões de tag no Adobe Experience Platform

A Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags do Adobe. O Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. As tags são oferecidas aos clientes do Adobe Experience Cloud como um recurso incluso de valor agregado.

Para obter uma introdução às tags, consulte os recursos abaixo:

- [Visão geral das tags](../../../tags/home.md)
- [Guia de início rápido](../../../tags/quick-start/quick-start.md)

## Como encontrar extensões de tag na interface da Platform {#how-to-find-extensions-in-interface}

Para encontrar as extensões na interface da Platform, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no **[!UICONTROL Tipos]** filtro.

![Filtro de extensões na interface](../../assets/catalog/launch-extensions/filter.png)

## Como funcionam as extensões de tag {#how-extensions-work}

A [extensão de tag](../../../tags/home.md#extensions) O é um pacote de códigos que melhora a funcionalidade de um site ou aplicativo móvel. Isso pode incluir o envio de dados brutos do evento para um destino como [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) mas elas também podem desempenhar outras funções.

É importante diferenciar entre extensões de encaminhamento de tags e eventos. As extensões exibidas na interface do usuário de destinos da Platform são *extensões de tag*. Consulte a visão geral do encaminhamento de eventos para obter mais informações sobre o [diferenças entre tags e encaminhamento de eventos](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Benefícios do uso de extensões de tag {#extensions-benefits}

Os recursos de tag da Platform são gratuitos para clientes do Experience Cloud existentes. O sistema simplifica a implantação de tags no site por meio de extensões fáceis de usar que você pode instalar, configurar, atualizar e excluir. As tags ocupam pouco espaço no site e permitem que você mantenha suas páginas carregando rapidamente.

Embora não seja possível ativar públicos para extensões de tag, você pode configurar regras para encaminhar apenas dados do evento em determinadas situações. Essa poderosa funcionalidade permite encaminhar os dados do evento somente em determinadas situações, em vez de enviar dados do evento em cada interação. Para obter mais informações, leia sobre as regras na seção [documentação das tags](../../../tags/ui/managing-resources/rules.md).

## Exemplo de casos de uso para extensões {#extensions-use-cases}

As extensões permitem atender a vários casos de uso do cliente. Alguns exemplos de casos de uso para usar extensões são:

- Você pode enviar dados do site ou do aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O Pixel do facebook indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar o visitante por meio do Facebook.
- Você pode encaminhar dados do evento de seus sites e aplicativos para o Google Analytics para analisar e tomar decisões com base nesses dados.
- Você pode ativar um aplicativo de chatbox no lado do cliente na hora certa com base em como os usuários estão interagindo com as páginas, de acordo com as regras configuradas.

## Categorias de extensão {#extension-categories}

As extensões podem se enquadrar nas seguintes categorias na Platform:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gerenciamento de dados](../data-management/overview.md)
- [Destinos de marketing por email](../email-marketing/overview.md)
- [Personalização](../personalization/overview.md)
- [Pesquisas](../survey/overview.md)
- [Voz do cliente](../voice/overview.md)
