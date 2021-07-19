---
keywords: Extensão do Analytics, extensão do analytics, análise de destino
title: Extensão do Adobe Analytics
description: A extensão Adobe Analytics é um destino de análise no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 95b6e079-09a6-4262-bd01-11f155286aa9
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 11%

---

# Extensão do Adobe Analytics

## Visão geral {#overview}

O Adobe Analytics é uma solução líder do setor que torna você capaz de entender seus clientes como pessoas e orientar seus negócios com informações de inteligência de clientes.

O Adobe Analytics é uma extensão do Analytics no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão em [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100156.html).

Este destino é uma extensão [!DNL Adobe Experience Platform Launch]. Para obter mais informações sobre como as extensões [!DNL Platform Launch] funcionam na plataforma, consulte [Visão geral das extensões do Experience Platform Launch](../launch-extensions/overview.md).

![Extensão do Adobe Analytics](../../assets/catalog/analytics/adobe-analytics/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo de Destinos para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] O é oferecido aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso a [!DNL Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Adobe Analytics:

Na [Interface da plataforma](http://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver esmaecido, você não terá a permissão **[!UICONTROL manage_properties]**. Consulte [Pré-requisitos](#prerequisites).

Na janela **[!UICONTROL Select available Platform launch property]**, selecione a propriedade [!DNL Platform Launch] na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade em [!DNL Platform Launch]. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [Propriedades da página](../../../tags/ui/administration/companies-and-properties.md#properties-page) da documentação [!DNL Launch].

O fluxo de trabalho leva você até [!DNL Platform Launch] para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão, consulte a [página de extensão do Adobe Analytics](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) na documentação Experiência [!DNL Launch].

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
