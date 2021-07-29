---
keywords: extensão do media analytics, media analytics, extensão de áudio e vídeo
title: Extensão Adobe Media Analytics for Audio and Video
description: A extensão Adobe Medium Analytics for Audio and Video é um destino de análise no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: bf33e3e8-a95b-47e3-a1dc-c8f68f80b080
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 8%

---

# Extensão Adobe Media Analytics for Audio and Video {#adobe-analytics-for-video-extension}

## Visão geral {#overview}

O Adobe Medium Analytics for Audio and Video é um complemento da oferta básica do Analytics que fornece aos clientes avaliações robustas para vídeo, áudio e anúncios.

O Adobe Medium Analytics para áudio e vídeo é uma extensão do Analytics no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão em [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100157.html).

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões de tags funcionam na Platform, consulte a [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão Adobe Media Analytics for Audio and Video](../../assets/catalog/analytics/adobe-video-analytics/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo [!DNL Destinations] para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar tags no Adobe Experience Platform. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso às tags e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Adobe Analytics for Video:

Na [Interface da plataforma](http://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver esmaecido, você não terá a permissão **[!UICONTROL manage_properties]**. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade da tag na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [documentação de tags](../../../tags/ui/administration/companies-and-properties.md).

O fluxo de trabalho direciona você para a interface do usuário da coleta de dados para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão, consulte a [página de extensão Adobe Medium Analytics for Audio and Video](../../../tags/extensions/web/media-analytics/overview.md) na documentação de tags.

Você também pode instalar a extensão diretamente na [Interface do usuário da coleta de dados](https://experience.adobe.com/#/data-collection/). Consulte o guia sobre [adicionar uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obter mais informações.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode iniciar a configuração das regras. Na interface do usuário da Coleta de dados, você pode configurar regras para as extensões instaladas para enviar dados do evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a visão geral em [rules](../../../tags/ui/managing-resources/rules.md) na documentação de tags.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface do usuário da Coleta de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário ainda exibirá **[!UICONTROL Instalar]** para a extensão. Desative o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o guia no [processo de atualização da extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
