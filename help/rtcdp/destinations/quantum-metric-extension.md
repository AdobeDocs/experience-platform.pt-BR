---
title: Extensão da métrica quântica
seo-title: Extensão da métrica quântica
description: A extensão de métrica quântica é um destino analítico na Platform de dados do cliente em tempo real da Adobe. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: A extensão de métrica quântica é um destino analítico no Platform de dados do cliente em tempo real da Adobe. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 4%

---


# [!DNL Quantum Metric] Extensão {#quantum-metric-extension}

## Visão geral {#overview}

[!DNL Quantum Metric's] a integração com o Adobe Launch facilita a implantação sem código da tag de coleta de [!DNL Quantum Metric's] dados. Além disso, essa extensão oferta a capacidade de capturar Elementos de dados de inicialização que contêm informações úteis da [!DNL Quantum Metric] API.

[!DNL Quantum Metric] é uma extensão de análise na Adobe Real-time Customer Data Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101535.quantum-metric-extension-for-adobe-launch.html).

Este destino é uma extensão de Experience Platform Launch. Para obter mais informações sobre como as extensões do Launch funcionam no Adobe Real-time CDP, consulte Visão geral [das extensões do](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Extensão de métrica quântica](assets/quantum-metric-extension.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram a Adobe Real-time CDP.

Para usar essa extensão, você precisa acessar o Experience Platform Launch. O Experience Platform Launch é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído que agrega valor. Entre em contato com o administrador da organização para obter acesso ao Launch e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a [!DNL Quantum Metric] extensão:

1. Na interface [CDP em tempo real da](http://platform.adobe.com/)Adobe, vá para **[!UICONTROL Destinos > Catálogo]**.
2. Selecione a extensão do catálogo ou use a barra de pesquisa.
3. Clique no destino para realçá-lo e selecione **[!UICONTROL Instalar extensão]** no painel direito. Se o controle **[!UICONTROL Instalar extensão]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]** . Consulte [Pré-requisitos](#prerequisites).
4. Na janela **[!UICONTROL Selecionar propriedade]** de inicialização disponível, selecione a propriedade Iniciar na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade no Launch. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da documentação do Launch.
5. O fluxo de trabalho leva você ao Launch para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e suporte de instalação, consulte a página Métrica [quântica no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101535.quantum-metric-extension-for-adobe-launch.html).

Você também pode instalar a extensão diretamente na interface [do](https://launch.adobe.com/)Experience Platform Launch. Consulte [Adicionar uma nova extensão](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) na documentação do Launch.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode start configurando regras para ela diretamente no Launch.

Em Iniciar, você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a documentação [](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Regras.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na interface do Launch.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário do Adobe Real-time CDP ainda exibirá **[!UICONTROL Instalar]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar Iniciar e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte Atualização [da](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extensão na documentação do Launch.