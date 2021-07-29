---
keywords: extensões de tags, extensão de tag, destinos do launch; extensões de tags da plataforma, extensão de tag da plataforma, destinos do platform launch
title: Extensões de tag no Adobe Experience Platform
description: A Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags do Adobe. A Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 1%

---

# Extensões de tag no Adobe Experience Platform

A Adobe Experience Platform oferece a próxima geração de recursos de gerenciamento de tags do Adobe. A Platform oferece uma forma simples de implantar e gerenciar todas as tags de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado.

Para obter uma introdução às tags, consulte os recursos abaixo:

- [Visão geral das tags](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=pt-BR)
- [Guia de início rápido](../../../tags/quick-start/quick-start.md)

## Como encontrar extensões de tags na interface do Platform {#how-to-find-extensions-in-interface}

Para localizar as extensões na interface da plataforma, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no filtro **[!UICONTROL Tipos]**.

![Filtro de extensões na interface](../../assets/catalog/launch-extensions/filter.png)

## Como funcionam as extensões de tags {#how-extensions-work}

As extensões encaminham os dados brutos do evento para vários tipos de destinos. Pense nas extensões como um tipo de destino **Encaminhamento de eventos** . Esse é um tipo mais simples de integração com plataformas de destino, que só encaminha dados brutos do evento. Exemplos disso são a [Extensão de personalização do Gainsight](../personalization/gainsight.md) ou a [Confirmação de voz da extensão do cliente](../voice/confirmit-digital-feedback.md).

**Perfil/Segmento** Os destinos de exportação no Adobe Experience Platform capturam dados de evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Exemplos disso são o [destino de armazenamento em nuvem do Amazon S3](../cloud-storage/amazon-s3.md) ou o [destino de publicidade do Google Display &amp; Video 360](../advertising/google-dv360.md).

![Extensões de tag em comparação a outros destinos](../../assets/common/launch-and-other-destinations.png)

## Benefícios do uso de extensões de tag {#extensions-benefits}

Os recursos de tags da Platform são gratuitos para os clientes do Experience Cloud. O sistema simplifica a implantação de tags no seu site por meio de extensões fáceis de usar que podem ser instaladas, configuradas, atualizadas e excluídas. As tags deixam um espaço pequeno no seu site e permitem que você mantenha suas páginas carregando rapidamente.

Embora não seja possível ativar segmentos para extensões de tags, é possível configurar regras para encaminhar apenas os dados do evento em determinadas situações. Essa funcionalidade avançada permite encaminhar os dados do evento somente em determinadas situações, em vez de enviar os dados do evento em cada interação. Para obter mais informações, leia sobre as regras na [documentação sobre tags](../../../tags/ui/managing-resources/rules.md).

## Exemplo de casos de uso para extensões {#extensions-use-cases}

As extensões permitem atender a vários casos de uso do cliente. Alguns exemplos de casos de uso para usar extensões são:

- Você pode enviar dados de site ou aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O facebook Pixel indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar seu visitante via Facebook.
- Você pode encaminhar dados de evento de seus sites e aplicativos para o Google Analytics para analisar e tomar decisões com base nesses dados.
- Você pode ativar um aplicativo de caixa de papo no lado do cliente na hora certa com base em como seus usuários estão interagindo com suas páginas, de acordo com as regras configuradas.

## Categorias de extensão {#extension-categories}

As extensões podem se encaixar nas seguintes categorias na Plataforma:

- [Publicidade](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gerenciamento de dados](../data-management/overview.md)
- [Destinos de marketing por email](../email-marketing/overview.md)
- [Personalização](../personalization/overview.md)
- [Pesquisas](../survey/overview.md)
- [Voz do cliente](../voice/overview.md)
