---
keywords: iniciar extensões;iniciar extensão;iniciar destinos; extensões de inicialização da plataforma;extensão de lançamento da plataforma;destinos de inicialização da plataforma
title: Extensões do Experience Platform Launch
seo-title: Extensões do Experience Platform Launch
description: O Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. O Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
seo-description: O Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. O Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 19%

---


# Extensões do Adobe Experience Platform Launch {#overview.md}

A Adobe Experience Platform Launch é a próxima geração de recursos de gerenciamento de tags da Adobe. O Platform Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. O Launch de plataforma é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado.

Para obter uma introdução aos recursos do Experience Platform Launch, consulte os recursos abaixo:
- Adobe Experience Platform Launch [documentação](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html)
- Vídeos de start rápido do Adobe Experience Platform Launch [](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Start com [Introdução ao Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) e [Visão geral do processo de publicação](https://helpx.adobe.com/br/analytics/how-to/adobe-launch-publishing-process.html), em seguida, vá para os próximos conceitos.

## Como localizar as extensões do Launch de plataforma na interface da plataforma {#how-to-find-extensions-in-interface}

Para localizar as extensões de lançamento de plataforma na interface da plataforma, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no filtro **[!UICONTROL Tipos]**.

![Filtro de extensões na interface](../../assets/catalog/launch-extensions/filter.png)

## Como funcionam as extensões de lançamento de plataforma {#how-extensions-work}

As extensões de lançamento de plataforma encaminham os dados brutos do evento para vários tipos de destinos. Pense nas extensões como um tipo de destino **Encaminhamento de Eventos**. Esse é um tipo mais simples de integração com as plataformas de destino, que apenas encaminha dados brutos do evento. Exemplos disso são a [extensão de personalização Gainsight](../personalization/gainsight.md) ou a [Confirmação de voz da extensão do cliente](../voice/confirmit-digital-feedback.md).

**Perfil/Segmento** Os destinos de exportação no Adobe Experience Platform capturam os dados do evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Exemplos disso são o [destino do armazenamento de nuvem do Amazon S3](../cloud-storage/amazon-s3.md) ou o [destino de publicidade do Google Display &amp; Video 360](../advertising/google-dv360.md).

![extensões de Experience Platform Launch em relação a outros destinos](../../assets/common/launch-and-other-destinations.png)

## Benefícios do uso das extensões de lançamento de plataforma {#extensions-benefits}

A Adobe Experience Platform Launch é grátis para os clientes atuais do Experience Cloud. O Platform Launch simplifica a implantação de tags em seu site por meio de extensões fáceis de usar que podem ser instaladas, configuradas, atualizadas e excluídas. O Platform Launch tem uma pequena área de ocupação em seu site e permite que você mantenha suas páginas carregadas rapidamente.

>[!IMPORTANT]
>
>Embora não seja possível ativar segmentos para extensões do Platform Launch, é possível configurar regras para encaminhar apenas dados do evento em determinadas situações. Leia mais abaixo.

Você pode criar *regras* que determinam quando encaminhar dados do evento para extensões. Essa funcionalidade poderosa permite que você encaminhe os dados do evento somente em determinadas situações, em vez de enviar dados do evento em cada interação. Para obter mais informações, leia sobre as regras na [documentação da Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Exemplos de casos de uso para extensões do Platform Launch {#extensions-use-cases}

As extensões de lançamento de plataforma permitem atender a vários casos de uso pelo cliente. Alguns exemplos de casos de uso para usar extensões do Platform Launch são:

- Você pode enviar dados de site ou aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O Pixel do Facebook indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar seu visitante pelo Facebook.
- Você pode encaminhar dados do evento de seus sites e aplicativos para Google Analytics para analisar e tomar decisões com base nesses dados.
- Você pode ativar um aplicativo de chatbox do lado do cliente no momento certo, com base em como seus usuários estão interagindo com suas páginas, de acordo com as regras que você configurou no Platform Launch.

## Categorias de extensão {#extension-categories}

As extensões de lançamento de plataforma podem ser incluídas nas seguintes categorias na Plataforma:

- [Publicidade](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma gestão de dados](../data-management/overview.md)
- [Destinos de marketing de email](../email-marketing/overview.md)
- [Personalização](../personalization/overview.md)
- [Pesquisas](../survey/overview.md)
- [Voz do cliente](../voice/overview.md)
