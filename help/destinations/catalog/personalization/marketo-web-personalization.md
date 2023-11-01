---
keywords: Marketo Web Personalization;marketo personalização da web;extensão Marketo Web Personalization;extensão de personalização da web marketo;marketo;Marketo
title: Extensão do Marketo Web Personalization
description: A extensão Marketo Web Personalization é um destino de personalização no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# Extensão do [!DNL Marketo Web Personalization] {#marketo-web-personalization-extension}

## Visão geral {#overview}

Essa extensão implanta o script para [!DNL Marketo's] Personalização da Web e aplicativos de IA de conteúdo. [!DNL Marketo] A Personalização da Web identifica e personaliza exclusivamente o conteúdo de acordo com as características do visitante da Web, como firmográficos para visitantes anônimos e uma grande variedade de atributos comportamentais na [!DNL Marketo] Plataforma de engajamento para visitantes conhecidos. [!DNL Marketo] A IA de conteúdo contém recursos para recomendações e personalização alimentadas por IA para campanhas da Web e de email que são exclusivas para clientes B2B.

[!DNL Marketo Web Personalization] é uma extensão de personalização no Adobe Experience Platform. Para obter mais informações sobre personalização da Web e IA de conteúdo no Marketo, leia [Visão geral da personalização da Web](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html).

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões funcionam na Platform, consulte a [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão Marketo Web Personalization](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram o Platform.

Para usar essa extensão, você precisa acessar as tags na Adobe Experience Platform. As tags são oferecidas aos clientes do Adobe Experience Cloud como um recurso incluso de valor agregado. Entre em contato com o administrador da organização para obter acesso às tags e solicite que conceda a você a **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar o [!DNL Marketo Web Personalization] extensão:

No [Interface da plataforma](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão no catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se a variável **[!UICONTROL Configurar]** estiver acinzentado, você não tem a **[!UICONTROL manage_properties]** permissão. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [Seção da página Propriedades](../../../tags/ui/administration/companies-and-properties.md#properties-page) de na documentação das tags.

O fluxo de trabalho o orienta pelas etapas necessárias para concluir a instalação.

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
