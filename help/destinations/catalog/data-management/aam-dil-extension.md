---
keywords: Extensão Audience Manager DIL, gerenciador de público-alvo de destino, extensão dil
title: Extensão Audience Manager DIL
description: A extensão Audience Manager DIL é um destino da Plataforma de gerenciamento de dados (DMP) no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---


# Extensão Audience Manager DIL {#aam-dil-extension}

## Visão geral {#overview}

Esta é a extensão do Adobe Audience Manager Data Integration Library (implementação do lado do cliente). Observação: Essa extensão não deve ser usada para o encaminhamento pelo lado do servidor (SSF) dos dados do Adobe Analytics. Para SSF, use a extensão do Adobe Analytics. Importante: A partir da versão 8.0, o DIL tem uma grande dependência no [!DNL Experience Cloud] Serviço de ID, versão 3.3 ou superior. Implemente o [!DNL Experience Cloud] Serviço de ID e o DIL para obter recursos completos de integração de dados [!DNL Audience Manager].

[!DNL Audience Manager] O DIL é uma extensão da Plataforma de gerenciamento de dados (DMP) no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a [página de extensão do Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) na documentação do Experience Platform Launch.

Este destino é uma extensão [!DNL Experience Platform Launch]. Para obter mais informações sobre como as extensões do Launch funcionam na Platform, consulte a [Visão geral das extensões do Experience Platform Launch](../launch-extensions/overview.md).

![Extensão Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo [!DNL Destinations] para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] O é oferecido aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso a [!DNL Platform Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão do DIL [!DNL Audience Manager]:

Na [Interface da plataforma](http://platform.adobe.com/), vá para **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configure]** no painel direito. Se o controle **[!UICONTROL Configure]** estiver esmaecido, a permissão **[!UICONTROL manage_properties]** não será exibida. Consulte [Pré-requisitos](#prerequisites).

Na janela **[!UICONTROL Select available Launch property]**, selecione a propriedade [!DNL Launch] na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade no Launch. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [Propriedades da página](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) da documentação [!DNL Launch].

O fluxo de trabalho leva você até [!DNL Launch] para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão, consulte a [página de extensão do Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) na documentação [!DNL Experience Launch].

Você também pode instalar a extensão diretamente na [interface do Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Adicionar uma nova extensão](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) na documentação [!DNL Platform Launch].

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode iniciar a configuração das regras diretamente em [!DNL Platform Launch].

Em [!DNL Platform Launch], você pode configurar regras para as extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a [Documentação de regras](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurar, atualizar e excluir a extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na interface [!DNL Platform Launch].

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário da plataforma ainda exibirá **[!UICONTROL Install]** para a extensão. Desative o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para chegar a [!DNL Platform Launch] e configure ou exclua sua extensão.

Para atualizar sua extensão, consulte [Atualização de extensão](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) na documentação [!DNL Platform Launch].



