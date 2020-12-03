---
keywords: Advertising Cloud;advertising cloud extension; advertising cloud destination
title: Extensão Adobe Advertising Cloud
seo-title: Extensão Adobe Advertising Cloud
description: A extensão Adobe Advertising Cloud é um destino publicitário na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: A extensão Adobe Advertising Cloud é um destino publicitário na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 3%

---


# Extensão Adobe Advertising Cloud {#adobe-advertising-cloud-extension}

## Visão geral {#overview}

Esta é a [!DNL Advertising Cloud] extensão para implementar tags de [!DNL Advertising Cloud] conversão e segmento para o DSP e a Pesquisa (atualmente, o DCO não é compatível).

A Adobe Advertising Cloud é uma extensão de publicidade na Plataforma de dados do cliente em tempo real.

Este destino é uma [!DNL Adobe Experience Platform Launch] extensão. Para obter mais informações sobre como [!DNL Platform Launch] as extensões funcionam no CDP em tempo real, consulte Visão geral [das extensões do](../launch-extensions/overview.md)Experience Platform Launch.

![Extensão Adobe Advertising Cloud](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no catálogo Destinos para todos os clientes que compraram CDP em tempo real.

Para usar essa extensão, você precisa ter acesso a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado. Entre em contato com o administrador da organização para obter acesso [!DNL Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Adobe Advertising Cloud:

Na interface [CDP em tempo](http://platform.adobe.com/)real, vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]** . Consulte [Pré-requisitos](#prerequisites).

Na janela **[!UICONTROL Selecionar propriedade]** de lançamento de plataforma disponível, selecione a [!DNL Platform Launch] propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade em [!DNL Platform Launch]. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da [!DNL Launch] documentação.

O fluxo de trabalho leva você [!DNL Platform Launch] a concluir a instalação.

Você também pode instalar a extensão diretamente na interface [do](https://launch.adobe.com/)Adobe Experience Platform Launch. Consulte [Adicionar uma nova extensão](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) na [!DNL Platform Launch] documentação.


## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode fazer um start ao configurar as regras para ela diretamente no [!DNL Platform Launch].

Em [!DNL Platform Launch], você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a documentação [](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)Regras.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na [!DNL Platform Launch] interface.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário CDP em tempo real ainda exibirá **[!UICONTROL Instalar]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar [!DNL Platform Launch] e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte Atualização [da](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extensão na [!DNL Platform Launch] documentação.
