---
title: Definições de configuração do Brand Concierge
description: Configure a persistência de sessão e os tempos limite de transmissão para o bate-papo do Brand Concierge.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# Definições de configuração do Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>O Brand Concierge para o Web SDK está atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Configurações ao usar o Brand Concierge na sua propriedade."

A seção **[!UICONTROL Brand Concierge]** permite controlar como as sessões de chat do Brand Concierge se comportam na extensão de tag da Web SDK.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Brand Concierge]**.

As opções disponíveis são as seguintes:

## [!UICONTROL Sticky conversation session]

Uma caixa de seleção que mantém sessões do Brand Concierge em carregamentos de página usando um cookie de sessão. Essa opção está desativada por padrão. Consulte [`conversation`](/help/collection/js/commands/configure/conversation.md) na documentação da biblioteca do JavaScript para obter orientação sobre como configurar esse valor.

## [!UICONTROL Stream timeout (seconds)]

O tempo máximo, em segundos, para aguardar partes do fluxo de conversa antes de acionar um erro de tempo limite. O valor padrão é `10` segundos.
