---
title: Renderizar conteúdo personalizado usando o SDK da Web da Adobe Experience Platform
description: Saiba como renderizar conteúdo personalizado com o SDK da Web da Adobe Experience Platform.
keywords: personalização; renderDecisões; sendEvent; decisionScopes; propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Renderizar conteúdo personalizado

O Adobe Experience Platform Web SDK oferece suporte à recuperação de conteúdo personalizado de soluções de personalização no Adobe, incluindo [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) e [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=pt-BR). O conteúdo criado no Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) pode ser recuperado e renderizado automaticamente pelo SDK. O conteúdo criado no Adobe Target [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ou Offer Decisioning não pode ser renderizado automaticamente pelo SDK. Em vez disso, você deve solicitar esse conteúdo usando o SDK e, em seguida, renderizar manualmente o conteúdo por conta própria.

## Renderização automática de conteúdo

Ao enviar eventos para o servidor, você pode definir a opção `renderDecisions` como `true`. Isso força o SDK a renderizar automaticamente qualquer conteúdo personalizado elegível para renderização automática.

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

A renderização do conteúdo personalizado é assíncrona, portanto, não é necessário fazer suposições sobre quando um determinado conteúdo terá concluído a renderização.

## Renderização manual do conteúdo

Para acessar qualquer conteúdo de personalização, você pode fornecer uma função de retorno de chamada, que será chamada depois que o SDK receber uma resposta bem-sucedida do servidor. A chamada de retorno é fornecida com um objeto `result`, que pode conter uma propriedade `propositions` contendo qualquer conteúdo de personalização retornado. Abaixo está um exemplo de como você fornece uma função de retorno de chamada ao enviar um evento.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Neste exemplo, `result.propositions`, se existir, é uma matriz contendo apresentações de personalização relacionadas ao evento. Por padrão, inclui apenas propostas qualificadas para renderização automática.

A matriz `propositions` pode ser semelhante a este exemplo:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

No exemplo, a opção `renderDecisions` não estava definida como `true` quando o comando `sendEvent` era executado, portanto, o SDK não tentava renderizar automaticamente nenhum conteúdo. No entanto, o SDK ainda recuperou automaticamente o conteúdo elegível para renderização automática, e forneceu isso para renderizar manualmente se desejar. Observe que cada objeto de proposta tem sua propriedade `renderAttempted` definida como `false`.

Se, em vez disso, você tivesse definido a opção `renderDecisions` como `true` ao enviar o evento, o SDK teria tentado renderizar quaisquer propostas qualificadas para renderização automática (conforme descrito anteriormente). Como consequência, cada um dos objetos de proposta teria sua propriedade `renderAttempted` definida como `true`. Nesse caso, não haveria necessidade de renderizar manualmente essas apresentações.

Até agora, só discutimos o conteúdo de personalização qualificado para renderização automática (ou seja, qualquer conteúdo criado no Adobe Target Visual Experience Composer). Para recuperar qualquer conteúdo de personalização _not_ elegível para renderização automática, é necessário solicitar o conteúdo preenchendo a opção `decisionScopes` ao enviar o evento. Um escopo é uma string que identifica uma proposta específica que você deseja recuperar do servidor.

Exemplo:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Neste exemplo, se as apresentações forem encontradas no servidor que corresponde ao escopo `salutation` ou `discount`, elas serão retornadas e incluídas na matriz `result.propositions`. Esteja ciente de que as apresentações qualificadas para renderização automática continuarão a ser incluídas na matriz `propositions`, independentemente de como você configura as opções `renderDecisions` ou `decisionScopes`. A matriz `propositions`, nesse caso, seria semelhante a este exemplo:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

Nesse ponto, é possível renderizar o conteúdo da proposta da maneira que quiser. Neste exemplo, a proposta que corresponde ao escopo `discount` é uma proposta HTML criada usando o Experience Composer baseado em formulário do Adobe Target. Supondo que você tenha um elemento em sua página com a ID de `daily-special` e deseje renderizar o conteúdo da apresentação `discount` no elemento `daily-special`, faça o seguinte:

1. Extraia apresentações do objeto `result`.
1. Faça o loop por cada proposta, procurando a proposta com um escopo de `discount`.
1. Se você encontrar uma proposta, faça um loop por cada item na proposta, procurando pelo item que é conteúdo HTML. (É melhor verificar do que assumir.)
1. Se você encontrar um item contendo conteúdo HTML, encontre o elemento `daily-special` na página e substitua seu HTML pelo conteúdo personalizado.

Seu código seria o seguinte:

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        break;
      }
    }
  }

  if (discountHtml) {
    // Discount HTML exists. Time to render it.
    var dailySpecialElement = document.getElementById("daily-special");
    dailySpecialElement.innerHTML = discountHtml;
  }
});
```


>[!TIP]
>
>Se você usar o Adobe Target, os escopos correspondem às mboxes no servidor, exceto que todas são solicitadas de uma vez em vez de individualmente. A mbox global é sempre retornada.

### Gerenciar cintilação

O SDK fornece recursos para [gerenciar a cintilação](../personalization/manage-flicker.md) durante o processo de personalização.
