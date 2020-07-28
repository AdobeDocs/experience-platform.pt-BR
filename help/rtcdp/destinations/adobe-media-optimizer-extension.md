---
title: Extensão do Adobe Analytics
seo-title: Extensão do Adobe Analytics
description: A extensão Adobe Analytics é um destino analítico no Adobe Real-time Customer Data Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: A extensão Adobe Analytics é um destino analítico no Adobe Real-time Customer Data Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 11%

---


# Adobe Analytics Extension {#adobe-analytics-extension}

## Visão geral {#overview}

O Adobe Analytics é uma solução líder do setor que torna você capaz de entender seus clientes como pessoas e orientar seus negócios com informações de inteligência de clientes.

A Adobe Analytics é uma extensão de análise no Adobe Real-time Customer Data Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100156.html).

Este destino é uma [!DNL Experience Platform Launch] extensão. Para obter mais informações sobre como [!DNL Launch] as extensões funcionam no CDP em tempo real do Adobe, consulte Visão geral [das extensões do](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Extensão do Adobe Analytics](/help/rtcdp/destinations/assets/adobe-analytics-extension.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no catálogo de Destinos para todos os clientes que compraram o Adobe Real-time CDP.

Para usar essa extensão, você precisa ter acesso a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado. Entre em contato com o administrador da organização para obter acesso [!DNL Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Adobe Analytics:

1. Na interface [CDP em tempo real do](http://platform.adobe.com/)Adobe, vá para **[!UICONTROL Destinos > Catálogo]**.
2. Selecione a extensão do catálogo ou use a barra de pesquisa.
3. Clique no destino para realçá-lo e selecione **[!UICONTROL Instalar extensão]** no painel direito. Se o controle **[!UICONTROL Instalar extensão]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]** . Consulte [Pré-requisitos](#prerequisites).
4. Na janela **[!UICONTROL Selecionar propriedade]** de inicialização disponível, selecione a [!DNL Launch] propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade em [!DNL Launch]. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da [!DNL Launch] documentação.
5. O fluxo de trabalho leva você [!DNL Launch] a concluir a instalação.

Para obter informações sobre as opções de configuração de extensão, consulte a página [de extensão do](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) Adobe Analytics na [!DNL Experience Launch] documentação.

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



