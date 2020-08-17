---
title: Renderização de conteúdo personalizado
seo-title: Adobe Experience Platform Web SDK Renderização de conteúdo personalizado
description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform
seo-description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform
translation-type: tm+mt
source-git-commit: c342e8d7698c1d213658f3f1dae751edbde04b83
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Visão geral das opções de personalização

A Adobe Experience Platform [!DNL Web SDK] oferece suporte para consultar as soluções de personalização no Adobe, incluindo a Adobe Target. Há dois modos para personalização: recuperar conteúdo que pode ser renderizado automaticamente e conteúdo que o desenvolvedor deve renderizar. O SDK também fornece recursos para [gerenciar oscilações](../../edge/solution-specific/target/flicker-management.md).

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

Você pode solicitar que a lista de decisões seja retornada como uma promessa no `sendEvent` comando, especificando a `decisionScopes` opção. Um escopo é uma string que permite que a solução de personalização saiba qual decisão você deseja.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
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
> Se você usar [!DNL Target], os escopos se tornarão mBoxes no servidor, somente eles serão solicitados de uma vez em vez de individualmente. A mbox global é sempre enviada.

### Recuperar conteúdo automático

Se você quiser que `result.decisions` as decisões de renderização automática sejam incluídas e NÃO tiver a opção Permitir a renderização automática, você poderá definir `renderDecisions` como `false`e incluir o escopo especial `__view__`.
