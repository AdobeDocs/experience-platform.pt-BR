---
title: Utilização do Adobe Journey Optimizer com o Experience Platform Web SDK
description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Adobe Journey Optimizer
keywords: ajo;ajo web;adobe jornada otimizer;renderDecisions;superfícies;decisões;propostas;escopo;esquema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Usando [!DNL Adobe Journey Optimizer] com [!DNL Experience Platform Web SDK]

O [!DNL Adobe Experience Platform] [!DNL Web SDK] pode entregar e renderizar experiências personalizadas gerenciadas no [!DNL Adobe Journey Optimizer] para o canal da Web. Você pode usar um editor de WYSIWYG, o [!DNL Adobe Journey Optimizer] [Canal da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR), ou uma interface não visual, o [Canal de Experiência baseado em Código](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/code-based-experience/get-started-code-based) para criar, ativar e entregar suas campanhas do [!DNL Journey Optimizer Web] e experiências de personalização.

>[!IMPORTANT]
>
>Leia a [documentação do Canal da Web do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=pt-BR) para obter informações de introdução à criação e aos relatórios de experiência do [!DNL Journey Optimizer Web].

## Terminologia {#terminology}

**[!UICONTROL Superfície]**: uma superfície da Web é uma página da Web ou um local em uma página identificada por um URI onde o conteúdo de experiência [!DNL Adobe Journey Optimizer] será entregue.

**[!UICONTROL Propositions]**: em [!DNL Adobe Journey Optimizer], as propostas estão correlacionadas à experiência selecionada em um [!DNL Journey Optimizer Campaign].

## Habilitando [!DNL Adobe Journey Optimizer] {#enable-ajo}

Para começar a usar o [!DNL Adobe Journey Optimizer], siga as etapas abaixo.

1. Passe pelos [pré-requisitos](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR#prerequesites) do [!DNL Adobe Journey Optimizer] [Guia de Experiências da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR), especificamente:
   * Configurar [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Habilitar [!DNL Adobe Journey Optimizer] na sua [sequência de dados](../../../datastreams/overview.md).
   * Habilite a opção [!UICONTROL Política de Mesclagem Ativa-na-Edge].

2. Adicione a opção `renderDecisions` aos seus eventos. Defina `renderDecisions` como `true` para renderização automática das propostas de conteúdo do Journey Optimizer entregues nas superfícies da sua página da Web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Como opção, especifique superfícies adicionais em seus eventos. Por padrão, o Web SDK gerará automaticamente a superfície da Web da página da Web atual e a incluirá na solicitação ao Edge Network. Se necessário, superfícies adicionais podem ser incluídas na solicitação especificando-as na opção `personalization.surfaces` do comando `sendEvent` ou na configuração da Extensão Web SDK correspondente **[!UICONTROL Superfícies]** [[!UICONTROL Ação Enviar evento]](../../../tags/extensions/client/web-sdk/action-types.md#send-event).

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extensão-adicionar-superfície](./assets/extension-add-surface.png)

   Superfícies de evento estão incluídas no campo de solicitação `query.personalization.surfaces`:

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. Semelhante a outros recursos de personalização, você pode adicionar um **[trecho pré-ocultação](../manage-flicker.md)** para ocultar apenas determinadas partes da página ao buscar experiências.

## Criação de experiências da Web no Adobe Journey Optimizer {#create-ajo-web-experiences}

Siga as instruções de [criação de campanha da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR#create-web-campaign) do [!DNL Adobe Journey Optimizer] [Guia de Experiências da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR) para criar [!DNL Journey Optimizer Web] campanhas e experiências.

## Renderização de conteúdo personalizado {#rendering-personalized-content}

Consulte a documentação sobre [renderização do conteúdo de personalização](../rendering-personalization-content.md) para obter mais informações.

As propostas Adobe Journey Optimizer para superfícies da web são processadas de maneira semelhante às `__view__` propostas de escopo de decisão. Especificamente, quando a opção `renderDecisions` estiver definida como `true` no comando `sendEvent`, eles serão renderizados automaticamente pelo Web SDK.

Exemplo de proposta de conteúdo do Journey Optimizer:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Depuração {#debugging}

Para depurar implementações de personalização do Adobe Journey Optimizer, use a [Depuração do Web SDK](/help/web-sdk/use-cases/debugging.md). [!DNL Adobe Journey Optimizer] rastreamentos de depuração estão disponíveis ao solucionar problemas usando [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Verifique se há eventos com o prefixo `AJO:`.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
