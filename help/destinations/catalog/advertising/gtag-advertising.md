---
keywords: gtag; google gtag; extensão do google; extensão do google gtag; GTAG
title: Extensão de tag do Google
description: A extensão da tag do Google é um destino de publicidade no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---

# Extensão de tag do Google {#gtag-advertising-extension}

>[!IMPORTANT]
>
>A extensão de tag do Google descrita aqui foi substituída pela [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) extensão desenvolvida por [!DNL Acronym]. Você pode encontrar a variável [!DNL Google Global Site Tag (gtag)] no [[!UICONTROL Tags]](../../../tags/home.md) na interface do usuário da coleta de dados ou na interface do usuário do Experience Platform.

## Visão geral {#overview}

Carregar Google `gtag.js` no site para enviar dados de evento para [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Essa extensão adiciona somente o código da tag ao site. Você precisará usar outras extensões do Google para adicionar eventos e ações que usarão gtag.

A tag do Google é uma extensão de publicidade no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão em [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões de tags funcionam no Platform, consulte o [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão de tag do Google](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar tags no Adobe Experience Platform. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso às tags e solicitar que elas concedam a você o **[!UICONTROL manage_properties]** para poder instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão da tag do Google:

No [Interface da plataforma](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se a variável **[!UICONTROL Configurar]** o controle está esmaecido, você está perdendo a variável **[!UICONTROL manage_properties]** permissão. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [Seção da página Propriedades](../../../tags/ui/administration/companies-and-properties.md#properties-page) na documentação das tags.

O fluxo de trabalho o orienta pelas etapas para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e o suporte de instalação, consulte o [Página de tags Google no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Você também pode instalar a extensão diretamente no [Interface do usuário da coleção de dados](https://experience.adobe.com/#/data-collection/). Para obter mais informações, consulte a seção em [adição de uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) na documentação das tags.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode iniciar a configuração das regras.

Você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte o [documentação das tags](../../../tags/ui/managing-resources/rules.md).

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface do usuário da Coleta de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário da plataforma ainda será exibida **[!UICONTROL Instalar]** para a extensão do . Inicie o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o guia no [processo de atualização de extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
