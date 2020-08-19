---
keywords: launch extensions;launch extension;launch destinations
title: Extensões Experience Platform Launch
seo-title: Extensões Experience Platform Launch
description: O Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. O Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
seo-description: O Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. O Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 21%

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

A Experience Platform Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. O Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. O Launch é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado.

Para obter uma introdução aos recursos do Experience Platform Launch, consulte os recursos abaixo:
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/pt-BR/launch/using/overview.html)
* Experience Platform Launch [rápido de start](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). Start com [Introdução ao Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) e [Publicação da visão geral](https://helpx.adobe.com/br/analytics/how-to/adobe-launch-publishing-process.html)do processo, em seguida, vá para os próximos conceitos.

## Como encontrar as extensões de lançamento na interface CDP em tempo real do Adobe {#how-to-find-extensions-in-interface}

Para localizar as extensões de inicialização na interface CDP em tempo real do Adobe, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no filtro **[!UICONTROL Tipos]** .

![Filtro de extensões na interface](/help/rtcdp/destinations/assets/extensions-filter.png)

## Como funcionam as extensões do Launch {#how-extensions-work}

Inicie extensões para encaminhar dados brutos do evento a vários tipos de destinos. Pense nas extensões como um tipo de destino de Encaminhamento de **Eventos** . Esse é um tipo mais simples de integração com as plataformas de destino, que apenas encaminha dados brutos do evento. Exemplos disso são a extensão [de personalização](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou a [Confirmar voz da extensão](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Cliente.

**Os destinos de exportação** de perfil/segmento no Adobe Real-time Customer Data Platform capturam os dados do evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Exemplos disso são o destino [do armazenamento em nuvem do](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 ou o destino [de publicidade do](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![extensões de Experience Platform Launch em relação a outros destinos](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Benefícios do uso das extensões do Launch {#extensions-benefits}

O Experience Platform Launch é gratuito para clientes Experience Cloud. O Launch simplifica a implantação de tags em seu site por meio de extensões fáceis de usar que podem ser instaladas, configuradas, atualizadas e excluídas. O Launch tem uma pequena área de ocupação em seu site e permite que você mantenha suas páginas carregadas rapidamente.

>[!IMPORTANT]
>
>Embora não seja possível ativar segmentos para Iniciar extensões, é possível configurar regras para encaminhar apenas os dados do evento em determinadas situações. Leia mais abaixo.

Você pode criar *regras* que determinam quando encaminhar dados do evento para extensões. Essa funcionalidade poderosa permite que você encaminhe os dados do evento somente em determinadas situações, em vez de enviar dados do evento em cada interação. Para obter mais informações, leia sobre as regras na documentação [do](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Launch.

## Exemplos de casos de uso para extensões de lançamento {#extensions-use-cases}

As extensões de lançamento permitem atender a vários casos de uso pelo cliente. Alguns exemplos de casos de uso para usar as extensões do Launch são:

* Você pode enviar dados de site ou aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O Pixel do Facebook indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar seu visitante pelo Facebook.
* Você pode encaminhar dados do evento de seus sites e aplicativos para Google Analytics para analisar e tomar decisões com base nesses dados.
* Você pode ativar um aplicativo de chatbox do lado do cliente no momento certo, com base em como seus usuários estão interagindo com suas páginas, de acordo com as regras que você configurou no Launch.


## Categorias de extensão {#extension-categories}

As extensões de inicialização podem ser incluídas nas seguintes categoria em CDP em tempo real do Adobe:

* [Publicidade](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Plataforma gestão de dados](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinos de marketing de email](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalização](/help/rtcdp/destinations/personalization-destinations.md)
* [Pesquisas](/help/rtcdp/destinations/survey-destinations.md)
* [Voz do cliente](/help/rtcdp/destinations/voice-of-customer-destinations.md)
