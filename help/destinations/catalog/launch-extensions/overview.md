---
keywords: extensões de tags, extensão de tag, destinos do launch; extensões de tags da plataforma, extensão de tag da plataforma, destinos do platform launch
title: Extensões de tag no Adobe Experience Platform
description: A Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags do Adobe. A Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Extensões de tag no Adobe Experience Platform

A Adobe Experience Platform fornece a próxima geração de recursos de gerenciamento de tags do Adobe. A Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado.

Para obter uma introdução às tags, consulte os recursos abaixo:

- [Visão geral das tags](../../../tags/home.md)
- [Guia de início rápido](../../../tags/quick-start/quick-start.md)

## Como encontrar extensões de tags na interface do Platform {#how-to-find-extensions-in-interface}

Para encontrar as extensões na interface da plataforma, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no **[!UICONTROL Tipos]** filtro.

![Filtro de extensões na interface](../../assets/catalog/launch-extensions/filter.png)

## Como funcionam as extensões de tags {#how-extensions-work}

A [extensão de tag](../../../tags/home.md#extensions) é um pacote de código que melhora a funcionalidade de um site ou aplicativo móvel. Isso pode incluir o envio de dados brutos do evento para um destino como [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) mas também podem servir outras funções.

É importante diferenciar entre extensões de tag e de encaminhamento de eventos. As extensões exibidas na interface do usuário de destinos da plataforma são *extensões de tag*. Consulte a visão geral do encaminhamento de eventos para obter mais informações sobre o [diferenças entre tags e encaminhamento de eventos](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Benefícios do uso de extensões de tag {#extensions-benefits}

Os recursos de tags da Platform são gratuitos para os clientes do Experience Cloud. O sistema simplifica a implantação de tags no seu site por meio de extensões fáceis de usar que podem ser instaladas, configuradas, atualizadas e excluídas. As tags deixam um espaço pequeno no seu site e permitem que você mantenha suas páginas carregando rapidamente.

Embora não seja possível ativar segmentos para extensões de tags, é possível configurar regras para encaminhar apenas os dados do evento em determinadas situações. Essa funcionalidade avançada permite encaminhar os dados do evento somente em determinadas situações, em vez de enviar os dados do evento em cada interação. Para obter mais informações, leia sobre as regras na [documentação das tags](../../../tags/ui/managing-resources/rules.md).

## Exemplo de casos de uso para extensões {#extensions-use-cases}

As extensões permitem atender a vários casos de uso do cliente. Alguns exemplos de casos de uso para usar extensões são:

- Você pode enviar dados de site ou aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O facebook Pixel indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar seu visitante via Facebook.
- Você pode encaminhar dados de evento de seus sites e aplicativos para o Google Analytics para analisar e tomar decisões com base nesses dados.
- Você pode ativar um aplicativo de caixa de papo no lado do cliente na hora certa com base em como seus usuários estão interagindo com suas páginas, de acordo com as regras configuradas.

## Categorias de extensão {#extension-categories}

As extensões podem se encaixar nas seguintes categorias na Plataforma:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gerenciamento de dados](../data-management/overview.md)
- [Destinos de marketing por email](../email-marketing/overview.md)
- [Personalização](../personalization/overview.md)
- [Pesquisas](../survey/overview.md)
- [Voz do cliente](../voice/overview.md)
