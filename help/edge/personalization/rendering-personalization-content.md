---
title: Renderizar conteúdo personalizado usando o Adobe Experience Platform Web SDK
description: Saiba como renderizar conteúdo personalizado com o Adobe Experience Platform Web SDK.
keywords: personalização;renderDecisions;sendEvent;DecisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Renderizar conteúdo personalizado

A Adobe Experience Platform [!DNL Web SDK] oferece suporte à consulta das soluções de personalização no Adobe, incluindo a Adobe Target. Há dois modos para personalização: recuperar conteúdo que pode ser renderizado automaticamente e conteúdo que o desenvolvedor deve renderizar. O SDK também fornece recursos para [gerenciar o flicker](../personalization/manage-flicker.md).

## Renderização automática de conteúdo

O SDK renderiza automaticamente o conteúdo personalizado quando você envia um evento para o servidor e define `renderDecisions` como `true` como uma opção no evento.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

A renderização de conteúdo personalizado é assíncrona, portanto, não deve haver nenhuma suposição sobre quando um determinado conteúdo faz parte da página.

## Renderização manual do conteúdo

Você pode solicitar que a lista de decisões seja retornada como uma promessa no comando `sendEvent` especificando a opção `decisionScopes`. Um escopo é uma string que permite que a solução de personalização saiba qual decisão você deseja.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

Isso retornará uma lista de decisões como um objeto JSON para cada decisão.

```json
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> Se você usar [!DNL Target], os escopos se tornarão mBoxes no servidor, somente eles serão solicitados de uma vez em vez de individualmente. A mbox global é sempre enviada.

### Recuperar conteúdo automático

Se você deseja que `result.decisions` inclua as decisões que podem ser renderizadas automaticamente e NÃO tenha a Ativação para renderizá-las automaticamente, você pode definir `renderDecisions` como `false` e incluir o escopo especial `__view__`.
