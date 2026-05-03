---
title: Definições de configuração do Brand Concierge
description: Configure a persistência de sessão e os tempos limite de transmissão para o bate-papo do Brand Concierge.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 16%

---

# Definições de configuração do Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>O Brand Concierge para o Web SDK está atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Configurações ao usar o Brand Concierge na propriedade."

A seção **[!UICONTROL Brand Concierge]** permite controlar como as sessões de chat do Brand Concierge se comportam na extensão de tag da Web SDK.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Brand Concierge]**.

As seguintes opções estão disponíveis:

## [!UICONTROL Sticky conversation session]

Uma caixa de seleção que mantém sessões do Brand Concierge em carregamentos de página usando um cookie de sessão. Essa opção está desabilitada por padrão. Consulte [`conversation`](/help/collection/js/commands/configure/conversation.md) na documentação da biblioteca do JavaScript para obter orientação sobre como configurar esse valor.

## [!UICONTROL Stream timeout (seconds)]

O tempo máximo, em segundos, para aguardar partes do fluxo de conversa antes de acionar um erro de tempo limite. O valor padrão é `10` segundos.

## [!UICONTROL Collect sources]

Uma caixa de seleção que coleta origens se um usuário navegou para a página de um link em uma conversa do Brand Concierge. Desmarcado por padrão. Se habilitada, a biblioteca verifica o parâmetro de cadeia de caracteres de consulta `adobe_brand_concierge_source` e preenche seu valor em `xdm.channel.referringSource`.
