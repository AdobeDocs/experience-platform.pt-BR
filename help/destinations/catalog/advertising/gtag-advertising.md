---
keywords: gtag;extensão google;extensão google;extensão google gtag;gtag;gtag;gtag;google extension;google gtag extension;GTAG
title: extensão gtag do Google
description: A extensão gtag do Google é um destino de publicidade na Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---

# extensão gtag do Google {#gtag-advertising-extension}

>[!IMPORTANT]
>
>A extensão gtag do Google descrita aqui foi substituída pelo [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) extensão desenvolvida por [!DNL Acronym]. Você pode encontrar o [!DNL Google Global Site Tag (gtag)] extensão na [[!UICONTROL Tags]](../../../tags/home.md) na interface da Coleção de dados ou na interface do Experience Platform.

## Visão geral {#overview}

Carregar o Google `gtag.js` no site para enviar dados do evento para o [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Essa extensão só adiciona o código gtag ao site. Será necessário usar outras extensões do Google para adicionar eventos e ações que usarão gtag.

O Google gtag é uma extensão de publicidade da Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão em [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões funcionam na Platform, consulte a [visão geral das extensões de tag](../launch-extensions/overview.md).

![extensão gtag do Google](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram o Platform.

Para usar essa extensão, você precisa acessar as tags na Adobe Experience Platform. As tags são oferecidas aos clientes do Adobe Experience Cloud como um recurso incluso de valor agregado. Entre em contato com o administrador da organização para obter acesso às tags e solicite que conceda a você a **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão gtag do Google:

No [Interface da plataforma](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão no catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se a variável **[!UICONTROL Configurar]** estiver acinzentado, você não tem a **[!UICONTROL manage_properties]** permissão. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [Seção da página Propriedades](../../../tags/ui/administration/companies-and-properties.md#properties-page) de na documentação das tags.

O fluxo de trabalho o orienta pelas etapas necessárias para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e suporte de instalação, consulte [Página do Google Gtag no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Também é possível instalar a extensão diretamente no [Interface da coleção de dados](https://experience.adobe.com/#/data-collection/). Para obter mais informações, consulte a seção sobre [adicionar uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) na documentação das tags.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode começar a configurar regras.

Você pode configurar regras para as extensões instaladas para enviar dados do evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a [documentação das tags](../../../tags/ui/managing-resources/rules.md).

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface da coleção de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário da Platform ainda será exibida **[!UICONTROL Instalar]** para a extensão. Inicie o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o guia no [processo de atualização de extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
