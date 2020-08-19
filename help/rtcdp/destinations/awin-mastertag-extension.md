---
keywords: Awin Advertiser mastertag extension;mastertag tag;Awin;awin;AWIN
title: Awin Advertiser Mastertag extension
seo-title: Awin Advertiser Mastertag extension
description: A extensão Awin Advertiser Mastertag é um destino publicitário na Plataforma de dados do cliente em tempo real do Adobe. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: null
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 5%

---


# [!DNL Awin Advertiser Mastertag] extensão {#awin-mastertag-extension}

## Visão geral {#overview}

A [!DNL MasterTag] é uma biblioteca JavaScript que contém todas as funções necessárias para a solução de rastreamento Awin e deve ser anexada incondicionalmente a cada página do site, incluindo a página de confirmação, mas excluindo qualquer página que exibe ou processa informações de pagamento.

[!DNL Awin Advertiser Mastertag] é uma extensão de anúncio na Plataforma de dados do cliente em tempo real do Adobe. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Este destino é uma [!DNL Experience Platform Launch] extensão. Para obter mais informações sobre como as extensões do Launch funcionam no Adobe Real-time CDP, consulte Visão geral [das extensões do](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Extensão Awin Advertiser Mastertag na interface do usuário](/help/rtcdp/destinations/assets/awin-mastertag-extension.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram o Adobe Real-time CDP.

Para usar essa extensão, você precisa ter acesso a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado. Entre em contato com o administrador da organização para obter acesso [!DNL Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a [!DNL Awin Advertiser Mastertag] extensão:

1. Na interface [CDP em tempo real do](http://platform.adobe.com/)Adobe, vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
2. Selecione a extensão do catálogo ou use a barra de pesquisa.
3. Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]** . Consulte [Pré-requisitos](#prerequisites).
4. Na janela **[!UICONTROL Selecionar propriedade]** de inicialização disponível, selecione a [!DNL Launch] propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade em [!DNL Launch]. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da [!DNL Launch] documentação.
5. O fluxo de trabalho leva você [!DNL Launch] a concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e suporte de instalação, consulte a página [Awin Advertiser Mastertag no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Você também pode instalar a extensão diretamente na interface [do](https://launch.adobe.com/)Experience Platform Launch. Consulte [Adicionar uma nova extensão](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) na [!DNL Launch] documentação.


## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode fazer um start ao configurar as regras para ela diretamente no [!DNL Launch].

Em [!DNL Launch], você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a documentação [](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Regras.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na [!DNL Launch] interface.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário CDP em tempo real do Adobe ainda exibirá **[!UICONTROL Instalar]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar [!DNL Launch] e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte Atualização [da](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extensão na [!DNL Launch] documentação.
