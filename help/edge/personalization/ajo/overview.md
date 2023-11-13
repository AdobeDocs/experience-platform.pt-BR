---
title: Utilização do Adobe Journey Optimizer com o SDK da Web da plataforma
description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Adobe Journey Optimizer
keywords: ajo;ajo web;adobe jornada otimizer;renderDecisions;superfícies;decisões;propostas;escopo;esquema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# Usar [!DNL Adobe Journey Optimizer] com o [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] podem fornecer e renderizar experiências personalizadas gerenciadas no [!DNL Adobe Journey Optimizer] ao canal da web. Você pode usar um editor WYSIWYG, [!DNL Adobe Journey Optimizer] [Interface do Campaign da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), para criar, ativar e entregar seus [!DNL Journey Optimizer Web] campanhas e experiências de personalização.

>[!IMPORTANT]
>
>Leia o [Documentação do canal da Web do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=pt-BR) para obter informações sobre a introdução ao [!DNL Journey Optimizer Web] criação e relatórios de experiência.

## Terminologia {#terminology}

**[!UICONTROL Superficial]**: uma superfície da web é uma propriedade da web identificada por um URL em que o [!DNL Adobe Journey Optimizer] o conteúdo da experiência será entregue.

**[!UICONTROL Apresentações]**: Em [!DNL Adobe Journey Optimizer], as apresentações estão correlacionadas à experiência selecionada em uma [!DNL Journey Optimizer Campaign].

## Ativando [!DNL Adobe Journey Optimizer] {#enable-ajo}

Para começar a usar o [!DNL Adobe Journey Optimizer], siga as etapas abaixo.

1. Passe pelo [pré-requisitos](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) do [!DNL Adobe Journey Optimizer] [Guia de experiências na Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), especificamente:
   * Configurar [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Ativar [!DNL Adobe Journey Optimizer] no seu [sequência de dados](../../../datastreams/overview.md).
   * Ativar o [!UICONTROL Política de mesclagem ativa na borda] opção.

2. Adicione o `renderDecisions` aos seus eventos. Definir `renderDecisions` para `true` para renderização automática de apresentações de conteúdo do Journey Optimizer entregues nas superfícies da página da Web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Como opção, especifique superfícies adicionais em seus eventos. Por padrão, o SDK da Web gerará automaticamente a superfície da Web para a página da Web atual e a incluirá na solicitação para a Rede de borda. Se necessário, superfícies adicionais podem ser incluídas na solicitação especificando-as no `personalization.surfaces` opção do `sendEvent` ou no comando correspondente **[!UICONTROL Superfícies]** [[!UICONTROL Enviar evento] ação](../../../tags/extensions/client/web-sdk/action-types.md#send-event) configuração da extensão SDK da Web.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extensão-adicionar-superfície](./assets/extension-add-surface.png)

   Superfícies de evento são incluídas no `query.personalization.surfaces` campo de solicitação:

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

4. Semelhante a outros recursos de personalização, você pode adicionar um **[pré-ocultação de trecho](../manage-flicker.md)** para ocultar apenas determinadas partes da página ao buscar experiências.

## Criação de experiências da Web no Adobe Journey Optimizer {#create-ajo-web-experiences}

Siga as [criação de campanha na web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) instruções do [!DNL Adobe Journey Optimizer] [Guia de experiências na Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) para criar [!DNL Journey Optimizer Web] campanhas e experiências.

## Renderização de conteúdo personalizado {#rendering-personalized-content}

Consulte a documentação em [renderização do conteúdo de personalização](../rendering-personalization-content.md) para obter mais informações.

As propostas do Adobe Journey Optimizer para superfícies da Web são processadas de maneira semelhante à `__view__` propostas de escopo de decisão. Especificamente, quando `renderDecisions` está definida como `true` no `sendEvent` Esses comandos serão renderizados automaticamente pelo SDK da Web.

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

Para depurar implementações de personalização do Adobe Journey Optimizer, use [[!DNL Web SDK] depuração](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] os rastreamentos de depuração estão disponíveis ao solucionar problemas usando [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Verifique se há eventos com o `AJO:` prefixo.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
