---
keywords: extensão do media analytics;media analytics;extensão de áudio e vídeo
title: Extensão Adobe Media Analytics for Audio and Video
description: A extensão do Adobe Media Analytics para áudio e vídeo é um destino de análise no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: bf33e3e8-a95b-47e3-a1dc-c8f68f80b080
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# Extensão Adobe Media Analytics for Audio and Video {#adobe-analytics-for-video-extension}

## Visão geral {#overview}

O Adobe Media Analytics para áudio e vídeo é um complemento da oferta básica do Analytics que fornece aos clientes uma avaliação robusta de vídeo, áudio e anúncios.

O Adobe Media Analytics para áudio e vídeo é uma extensão de análise no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100157.html).

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões funcionam na Experience Platform, consulte a [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão Adobe Media Analytics for Audio and Video](../../assets/catalog/analytics/adobe-video-analytics/catalog.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no catálogo [!DNL Destinations] para todos os clientes que compraram o Experience Platform.

Para usar essa extensão, você precisa acessar as tags na Adobe Experience Platform. As tags são oferecidas aos clientes do Adobe Experience Cloud como um recurso incluso de valor agregado. Entre em contato com o administrador da organização para obter acesso às tags e solicite a concessão da permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Adobe Analytics for Video:

Na [interface do Experience Platform](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão no catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver esmaecido, você não terá a permissão **[!UICONTROL manage_properties]**. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade da tag na qual você deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [documentação de tags](../../../tags/ui/administration/companies-and-properties.md).

O fluxo de trabalho direciona você à interface da Coleção de dados para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão, consulte a [página de extensão do Adobe Media Analytics para áudio e vídeo](../../../tags/extensions/client/media-analytics/overview.md) na documentação das tags.

Você também pode instalar a extensão diretamente na [Interface da Coleção de Dados](https://experience.adobe.com/#/data-collection/). Consulte o guia em [adicionando uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obter mais informações.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode começar a configurar regras. Na interface da Coleção de dados, é possível configurar regras para as extensões instaladas para enviar dados do evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a visão geral sobre [regras](../../../tags/ui/managing-resources/rules.md) na documentação de tags.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface da coleção de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface ainda exibirá **[!UICONTROL Instalar]** para a extensão. Inicie o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o manual no [processo de atualização da extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
