---
title: Uso do Adobe Journey Optimizer com o SDK da Web da plataforma
description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform usando o Adobe Journey Optimizer
keywords: ajo; ajo web; adobe jornada otimizer; renderDecisões; superfícies; decisões; propostas; escopo; esquema
exl-id: e608952c-9598-11ed-b382-d72064651cac
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Usando [!DNL Adobe Journey Optimizer] com o [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] O pode entregar e renderizar experiências personalizadas gerenciadas no [!DNL Adobe Journey Optimizer] para o canal da Web. Você pode usar um editor WYSIWYG, [!DNL Adobe Journey Optimizer] [Interface do usuário do Campaign da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), para criar, ativar e entregar seu [!DNL Journey Optimizer Web] campanhas e experiências de personalização.

>[!IMPORTANT]
>
>Leia o [Documentação do Canal da Web do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) para obter informações sobre a introdução ao [!DNL Journey Optimizer Web] criação e relatórios de experiência.

## Terminologia {#terminology}

**[!UICONTROL Superfície]**: Uma superfície da Web é uma propriedade da Web identificada por um URL em que a variável [!DNL Adobe Journey Optimizer] o conteúdo da experiência será entregue.

**[!UICONTROL Propostas]**: Em [!DNL Adobe Journey Optimizer], as apresentações estão correlacionadas à experiência selecionada de uma [!DNL Journey Optimizer Campaign].

## Habilitar [!DNL Adobe Journey Optimizer] {#enable-ajo}

Para começar a usar [!DNL Adobe Journey Optimizer]siga as etapas abaixo.

1. Percorra o [pré-requisitos](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) do [!DNL Adobe Journey Optimizer] [Guia de experiências na Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), especificamente:
   * Configurar [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Habilitar [!DNL Adobe Journey Optimizer] em seu [datastream](../../datastreams/overview.md).
   * Ative o [!UICONTROL Política de Mesclagem Ativa On-Edge] opção.

2. Adicione o `renderDecisions` aos seus eventos. Definir `renderDecisions` para `true` para renderização automática das propostas de conteúdo do Journey Optimizer entregues nas superfícies da página da Web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Como opção, especifique superfícies adicionais em seus eventos. Por padrão, o SDK da Web gerará automaticamente a superfície da Web da página da Web atual e a incluirá na solicitação para a Edge Network. Se necessário, superfícies adicionais podem ser incluídas na solicitação especificando-as na variável `personalization.surfaces` da `sendEvent` ou no comando correspondente **[!UICONTROL Superfícies]** [[!UICONTROL Enviar evento] ação](../../extension/action-types.md#send-event) configuração da extensão do SDK da Web.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extensão-adicionar-superfície](./assets/extension-add-surface.png)

   As superfícies do evento são incluídas no `query.personalization.surfaces` campo de solicitação:

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

4. Semelhante a outros recursos de personalização, é possível adicionar um **[pré-ocultar trecho](../manage-flicker.md)** para ocultar apenas determinadas partes da página ao buscar experiências.

## Criar experiências da Web do Adobe Journey Optimizer {#create-ajo-web-experiences}

Siga as [criação de campanha da web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) instruções da [!DNL Adobe Journey Optimizer] [Guia de experiências na Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) para criar [!DNL Journey Optimizer Web] campanhas e experiências.

## Renderização de conteúdo personalizado {#rendering-personalized-content}

Consulte a documentação em [renderização do conteúdo de personalização](../rendering-personalization-content.md) para obter mais informações.

As propostas do Adobe Journey Optimizer para superfícies da Web são processadas de maneira semelhante ao `__view__` propostas de escopo de decisão. Especificamente, quando `renderDecisions` está definida como `true` no `sendEvent` serão renderizadas automaticamente pelo SDK da Web.

Exemplo de apresentação de conteúdo do Journey Optimizer:

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

Para depurar implementações de personalização do Adobe Journey Optimizer, use [[!DNL Web SDK] depuração](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] os rastreamentos de depuração estão disponíveis ao solucionar problemas usando [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Verifique se há eventos com a variável `AJO:` prefixo.

![Assurance-ajo-trace](./assets/assurance-ajo-trace.png)

