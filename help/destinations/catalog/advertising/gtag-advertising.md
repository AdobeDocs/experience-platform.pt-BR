---
keywords: gtag;google gtag;google extension;google gtag extension;gtag extension;GTAG
title: Destino da extensão do Google gtag
description: A extensão da gtag do Google é um destino publicitário no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 3%

---


# Extensão do Google gtag {#gtag-advertising-extension}

Carregue o `gtag.js` do Google em seu site para enviar dados de evento para [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Essa extensão só adiciona o código da tag ao seu site. Você precisará usar outras extensões do Google para adicionar eventos e ações que usarão gtag.

O Google gtag é uma extensão de publicidade no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão em [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Este destino é uma extensão Adobe Experience Platform Launch. Para obter mais informações sobre como as extensões de lançamento de plataforma funcionam na Plataforma, consulte [Visão geral das extensões do Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Extensão do Google gtag](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no catálogo [!DNL Destinations] para todos os clientes que compraram a Plataforma.

Para usar essa extensão, você precisa acessar o Adobe Experience Platform Launch. O Launch de plataforma é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado. Entre em contato com o administrador da organização para obter acesso ao Platform Launch e peça que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão do Google gtag:

Na [Interface da plataforma](http://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configure]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]**. Consulte [Pré-requisitos](#prerequisites).

Na janela **[!UICONTROL Selecione a propriedade Platform Launch disponível]**, selecione a propriedade Platform Launch na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade no Launch da plataforma. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [Propriedades da página](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) da documentação do Launch de plataforma.

O fluxo de trabalho leva você ao Platform Launch para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e o suporte de instalação, consulte a [página de tags do Google no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Você também pode instalar a extensão diretamente na [interface do Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Adicionar uma nova extensão](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) na documentação do Launch da plataforma.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, é possível configurar o start das regras para ela diretamente no Platform Launch.

No Platform Launch, você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte [Documentação das regras](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na interface do Platform Launch.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário da plataforma ainda exibirá **[!UICONTROL Install]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar o Launch da plataforma e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte [Atualização da extensão](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) na documentação do Launch da plataforma.
