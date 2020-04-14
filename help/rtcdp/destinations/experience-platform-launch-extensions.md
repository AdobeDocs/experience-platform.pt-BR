---
title: Extensões de lançamento da plataforma Experience
seo-title: Extensões de lançamento da plataforma Experience
description: O Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. Ele oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
seo-description: O Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. Ele oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
translation-type: tm+mt
source-git-commit: 98c3356db178507e0a8d94b47030e9490e721e46

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

A Experience Platform Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. Ele oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. O Launch é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído que agrega valor.

Para obter uma introdução aos recursos do Experience Platform Launch, consulte os recursos abaixo:
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/pt-BR/launch/using/overview.html)
* Vídeos [de start](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)rápido do Experience Platform Launch. Start com a [introdução ao Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) e a visão geral [do processo de](https://helpx.adobe.com/br/analytics/how-to/adobe-launch-publishing-process.html)publicação e, em seguida, avance para os próximos conceitos.

## Como localizar as extensões de lançamento na interface CDP em tempo real da Adobe {#how-to-find-extensions-in-interface}

Para localizar as extensões do Launch na interface CDP em tempo real da Adobe, navegue até **[!UICONTROL Destinations > Catalog]** e selecione **[!UICONTROL Extensions]** no **[!UICONTROL Types]** filtro.

![Filtro de extensões na interface](/help/rtcdp/destinations/assets/extensions-filter.png)

## Como funcionam as extensões do Launch {#how-extensions-work}

Inicie extensões para encaminhar dados brutos do evento a vários tipos de destinos. Pense nas extensões como um tipo de destino de Encaminhamento de **Eventos** . Esse é um tipo mais simples de integração com as plataformas de destino, que apenas encaminha dados brutos do evento. Exemplos disso são a extensão [de personalização](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou a [Confirmar voz da extensão](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Cliente.

**Os destinos de exportação** de Perfil/segmento na plataforma de dados do cliente em tempo real da Adobe capturam dados do evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Exemplos disso são o destino [do armazenamento da nuvem](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 ou o destino [de publicidade do](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Extensões do Experience Platform Launch em comparação com outros destinos](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Benefícios do uso das extensões do Launch {#extensions-benefits}

O Experience Platform Launch é gratuito para clientes existentes da Experience Cloud. O Launch simplifica a implantação de tags em seu site por meio de extensões fáceis de usar que podem ser instaladas, configuradas, atualizadas e excluídas. O Launch tem uma pequena área de ocupação em seu site e permite que você mantenha suas páginas carregadas rapidamente.

>[!IMPORTANT]
>
>Embora não seja possível ativar segmentos para Iniciar extensões, é possível configurar regras para encaminhar apenas os dados do evento em determinadas situações. Leia mais abaixo.

Você pode criar *regras* que determinam quando encaminhar dados do evento para extensões. Essa funcionalidade poderosa permite que você encaminhe os dados do evento somente em determinadas situações, em vez de enviar dados do evento em cada interação. Para obter mais informações, leia sobre as regras na documentação [do](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Launch.

## Exemplos de casos de uso para extensões de lançamento {#extensions-use-cases}

As extensões de lançamento permitem atender a vários casos de uso pelo cliente. Alguns exemplos de casos de uso para usar as extensões do Launch são:

* Você pode enviar dados de site ou aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O Pixel do Facebook indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar seu visitante pelo Facebook.
* Você pode encaminhar dados do evento de seus sites e aplicativos para o Google Analytics para analisar e tomar decisões com base nesses dados.
* Você pode ativar um aplicativo de chatbox do lado do cliente no momento certo, com base em como seus usuários estão interagindo com suas páginas, de acordo com as regras que você configurou no Launch.


## categorias de extensão {#extension-categories}

As extensões de inicialização podem ser incluídas nas seguintes categorias no Adobe Real-time CDP:

* [Publicidade](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Plataforma Gestão de dados](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinos de marketing de email](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalização](/help/rtcdp/destinations/personalization-destinations.md)
* [Pesquisas](/help/rtcdp/destinations/survey-destinations.md)
* [Voz do cliente](/help/rtcdp/destinations/voice-of-customer-destinations.md)
