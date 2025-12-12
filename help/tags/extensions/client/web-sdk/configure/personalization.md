---
title: Definições de configuração do Personalization
description: Defina as configurações de personalização na extensão de tag do Web SDK.
source-git-commit: 9a617b6e97aec22a6726266f2628bd2c2a05da19
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Definições de configuração do Personalization

Esta seção de configuração permite determinar como você deseja ocultar determinadas partes da página enquanto o conteúdo personalizado é carregado. Quando configuradas corretamente, essas configurações garantem que seus visitantes vejam o conteúdo personalizado correto.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Personalization]**.

![Imagem mostrando as configurações de personalização da extensão de marca do Web SDK na interface do usuário de Marcas](../assets/web-sdk-ext-personalization.png)

As opções disponíveis são as seguintes:

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Use esta opção para permitir que o Web SDK leia e grave os cookies herdados `mbox` e `mboxEdgeCluster` usados pelas bibliotecas `at.js` 1.x ou 2.x. Essa configuração ajuda a manter intactos os perfis de visitantes ao mover-se entre páginas usando o Web SDK ou o `at.js` no mesmo site. Se você não tiver o `at.js` implementado em nenhum lugar do seu site, não precisará habilitar essa caixa de seleção. O equivalente a esta caixa de seleção na biblioteca de JavaScript é [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md).

Ao habilitar esta opção, certifique-se de habilitar também o [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) no `targetGlobalSettings()`.

## [!UICONTROL Prehiding style] {#prehiding-style}

O editor de estilo pré-ocultação permite definir regras CSS personalizadas para ocultar seções específicas de uma página. Quando a página é carregada, o Web SDK usa esse estilo para ocultar as seções que precisam ser personalizadas, recupera a personalização e desoculta as seções de página personalizadas. Esse fluxo de trabalho permite que os visitantes vejam o conteúdo personalizado sem ver o processo de recuperação de personalização ser carregado ou cintilar. O equivalente da biblioteca JavaScript a este editor de código é [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md).

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Esta seção não é uma definição de configuração direta, mas um local conveniente em que você pode obter o código de implementação. Implemente esse trecho pré-ocultação na tag `<head>` no site para ocultar o conteúdo desejado enquanto a biblioteca do Web SDK é carregada.

>[!IMPORTANT]
>
>Ao usar o trecho pré-ocultação, o Adobe recomenda usar a mesma regra de CSS entre o trecho pré-ocultação e o estilo pré-ocultação.

## [!UICONTROL Enable personalization storage]

Uma caixa de seleção que permite que o Web SDK armazene eventos de personalização. no armazenamento local do navegador. É importante quando você deseja rastrear quais experiências o visitante viu nos carregamentos de página.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

Um menu suspenso que determina quando o Web SDK coleta automaticamente cliques no conteúdo retornado do Adobe Journey Optimizer.

* **[!UICONTROL Always]**: Coletar todas as interações com apresentações.
* **[!UICONTROL Decorated elements only]**: coletar interações somente em elementos com atributos HTML `data-aep-click-label` ou `data-aep-click-token`.
* **[!UICONTROL Never]**: não coletar interações com apresentações.

A biblioteca de JavaScript equivalente a este menu suspenso é [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Seu valor padrão é [!UICONTROL Always].

## [!UICONTROL Auto click collection for Adobe Target]

Um menu suspenso que determina quando o Web SDK coleta automaticamente cliques no conteúdo retornado do Adobe Target.

* **[!UICONTROL Always]**: Coletar todas as interações com apresentações.
* **[!UICONTROL Decorated elements only]**: coletar interações somente em elementos com atributos HTML `data-aep-click-label` ou `data-aep-click-token`.
* **[!UICONTROL Never]**: não coletar interações com apresentações.

A biblioteca de JavaScript equivalente a este menu suspenso é [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Seu valor padrão é [!UICONTROL Never].
