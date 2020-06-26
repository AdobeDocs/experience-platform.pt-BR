---
title: Renderização de conteúdo personalizado
seo-title: Adobe Experience Platform Web SDK Renderização de conteúdo personalizado
description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform
seo-description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Visão geral das opções de personalização

O Adobe Experience Platform Web SDK oferece suporte à consulta das soluções de personalização na Adobe, incluindo o Adobe Target. Há dois modos para personalização: recuperar conteúdo que pode ser renderizado automaticamente e conteúdo que o desenvolvedor deve renderizar. O SDK também fornece recursos para [gerenciar oscilações](../../edge/solution-specific/target/flicker-management.md).

## Renderização automática de conteúdo

O SDK renderiza automaticamente o conteúdo personalizado quando você envia um evento para o servidor e define `renderDecisions` como uma opção `true` no evento.

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

Você pode solicitar que a lista de decisões seja retornada como uma promessa no `event` comando usando `scopes`. Um escopo é uma string que permite que a solução de personalização saiba qual decisão você deseja.

```javascript
alloy("sendEvent",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
    }
  })
```

Isso retornará uma lista de decisões como um objeto JSON para cada decisão.

```javascript
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
> Se você usar escopos de Público alvo para se tornarem mBoxes no servidor, somente eles serão solicitações ao mesmo tempo, em vez de individualmente. A mbox global é sempre enviada.

### Recuperar conteúdo automático

Se desejar que `result.decisions` as decisões de renderização automática sejam incluídas, é possível definir `renderDecisions` como falso e incluir o escopo especial `__view__`.
