---
keywords: Extensão de mastertag do Awin Advertiser; mastertag; Awin; awin; AWIN
title: Extensão Awin Advertiser Mastertag
description: A extensão Awin Advertiser Mastertag é um destino de publicidade no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 99a9ea40-b89f-4503-91a7-60cc8e1cd6d3
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 3%

---

# [!DNL Awin Advertiser Mastertag] extensão {#awin-mastertag-extension}

## Visão geral {#overview}

O [!DNL MasterTag] é uma biblioteca JavaScript que contém todas as funções necessárias para a solução de rastreamento do Awin e deve ser anexada incondicionalmente a todas as páginas do site, incluindo a página de confirmação, mas excluindo qualquer página que exibe ou processe informações de pagamento.

[!DNL Awin Advertiser Mastertag] O é uma extensão de publicidade no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão em [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Este destino é uma extensão [!DNL Experience Platform Launch]. Para obter mais informações sobre como as extensões do Launch funcionam na Platform, consulte a [Visão geral das extensões do Experience Platform Launch](../launch-extensions/overview.md).

![Extensão Awin Advertiser Mastertag na interface do usuário](../../assets/catalog/advertising/awin-mastertag/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo [!DNL Destinations] para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] O é oferecido aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso a [!DNL Platform Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão [!DNL Awin Advertiser Mastertag]:

Na [Interface da plataforma](http://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver esmaecido, você não terá a permissão **[!UICONTROL manage_properties]**. Consulte [Pré-requisitos](#prerequisites).

Na janela **[!UICONTROL Select available Platform launch property]**, selecione a propriedade [!DNL Platform Launch] na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade em [!DNL Platform Launch]. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [Propriedades da página](../../../tags/ui/administration/companies-and-properties.md#properties-page) da documentação [!DNL Launch].

O fluxo de trabalho leva você até [!DNL Platform Launch] para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e o suporte de instalação, consulte a página [Awin Advertiser Mastertag no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Você também pode instalar a extensão diretamente na [interface do Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Adicionar uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) na documentação [!DNL Platform Launch].


## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode iniciar a configuração das regras diretamente em [!DNL Platform Launch].

Em [!DNL Platform Launch], você pode configurar regras para as extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a [Documentação de regras](../../../tags/ui/managing-resources/rules.md).

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na interface [!DNL Platform Launch].

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário da plataforma ainda exibirá **[!UICONTROL Instalar]** para a extensão. Desative o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para chegar a [!DNL Platform Launch] e configure ou exclua sua extensão.

Para atualizar sua extensão, consulte [Atualização de extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação [!DNL Platform Launch].
