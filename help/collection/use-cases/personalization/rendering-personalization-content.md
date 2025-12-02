---
title: Renderizar conteúdo personalizado usando o Adobe Experience Platform Web SDK
description: Saiba como renderizar conteúdo personalizado com o Adobe Experience Platform Web SDK.
keywords: personalização;renderDecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Renderizar conteúdo personalizado

O Adobe Experience Platform Web SDK oferece suporte à recuperação de conteúdo personalizado de soluções de personalização da Adobe, incluindo o [Adobe Target](https://business.adobe.com/br/products/target/adobe-target.html), o [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=pt-BR) e o [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=pt-BR).

Além disso, o Web SDK habilita recursos de personalização de mesma página e próxima página por meio de destinos de personalização do Adobe Experience Platform, como o [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e a [conexão de personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md). Para saber como configurar o Experience Platform para personalização de mesma página e próxima página, consulte o [guia dedicado](/help/destinations/ui/activate-edge-personalization-destinations.md).

O conteúdo criado no [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR) do Adobe Target e na [Interface do usuário do Web Campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR) do Adobe Journey Optimizer pode ser recuperado e renderizado automaticamente pela SDK. O conteúdo criado no [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=pt-BR) do Adobe Target, no [Canal de experiência baseado em código](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/code-based-experience/get-started-code-based) do Adobe Journey Optimizer ou no Offer Decisioning não pode ser renderizado automaticamente pelo SDK. Em vez disso, você deve solicitar esse conteúdo usando o SDK e, em seguida, renderizar manualmente o conteúdo.

## Renderização automática de conteúdo {#automatic}

Ao enviar eventos para o servidor, você pode definir a opção `renderDecisions` como `true`. Isso força o SDK a renderizar automaticamente qualquer conteúdo personalizado que esteja qualificado para renderização automática.

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

A renderização do conteúdo personalizado é assíncrona, portanto, você não deve fazer suposições sobre quando uma determinada parte do conteúdo terá concluído a renderização.

## Renderização manual do conteúdo {#manual}

Para acessar qualquer conteúdo de personalização, você pode fornecer uma função de retorno de chamada, que será chamada depois que o SDK receber uma resposta bem-sucedida do servidor. Seu retorno de chamada recebe um objeto `result`, que pode conter uma propriedade `propositions` contendo qualquer conteúdo de personalização retornado. Veja abaixo um exemplo de como você forneceria uma função de retorno de chamada ao enviar um evento.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Neste exemplo, `result.propositions`, se existir, é uma matriz contendo propostas de personalização relacionadas ao evento. Por padrão, inclui apenas apresentações qualificadas para renderização automática.

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
    "scopeDetails": {
      ...
    },
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
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

No exemplo, a opção `renderDecisions` não estava definida como `true` quando o comando `sendEvent` foi executado, portanto, o SDK não tentou renderizar conteúdo automaticamente. No entanto, o SDK ainda recuperou automaticamente o conteúdo qualificado para renderização automática e forneceu isso para renderização manual, se você desejar. Observe que cada objeto de proposta tem sua propriedade `renderAttempted` definida como `false`.

Se você tivesse definido a opção `renderDecisions` como `true` ao enviar o evento, o SDK teria tentado renderizar qualquer proposta qualificada para renderização automática (conforme descrito anteriormente). Como consequência, cada objeto de proposta teria sua propriedade `renderAttempted` definida como `true`. Não haveria necessidade de renderizar manualmente essas apresentações nesse caso.

Até agora, discutimos somente o conteúdo de personalização qualificado para renderização automática (ou seja, qualquer conteúdo criado no Visual Experience Composer do Adobe Target ou na interface do usuário de Campanha na Web do Adobe Journey Optimizer). Para recuperar qualquer conteúdo de personalização _não_ qualificado para renderização automática, é necessário solicitar o conteúdo preenchendo a opção `decisionScopes` ao enviar o evento. Um escopo é uma cadeia de caracteres que identifica uma proposta específica que você deseja recuperar do servidor.

Exemplo:

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Neste exemplo, se propostas forem encontradas no servidor que corresponde ao escopo `salutation` ou `discount`, elas serão retornadas e incluídas na matriz `result.propositions`. Esteja ciente de que as propostas qualificadas para renderização automática continuarão a ser incluídas na matriz `propositions`, independentemente de como você configurar as opções `renderDecisions` ou `decisionScopes`. A matriz `propositions`, neste caso, seria semelhante a este exemplo:

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
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
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
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
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
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
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
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

Nesse ponto, é possível renderizar o conteúdo da proposta conforme você julgar necessário. Neste exemplo, a proposta que corresponde ao escopo `discount` é uma proposta de HTML criada usando o Experience Composer baseado em formulário do Adobe Target. Supondo que você tenha um elemento na página com a ID `daily-special` e deseje renderizar o conteúdo da proposta `discount` no elemento `daily-special`, faça o seguinte:

1. Extrair apresentações do objeto `result`.
1. Execute um loop em cada proposta, procurando pela proposta com um escopo de `discount`.
1. Se encontrar uma proposta, percorra cada item na proposta, procurando o item que seja conteúdo do HTML. (É melhor verificar do que supor.)
1. Se você encontrar um item com conteúdo HTML, localize o elemento `daily-special` na página e substitua seu HTML pelo conteúdo personalizado.
1. Depois que o conteúdo for renderizado, envie um evento `display`.

Seu código seria semelhante ao seguinte:

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
    // Rather than assuming there is a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "display" event 
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Se você usar o Adobe Target, os escopos corresponderão às mboxes no servidor, exceto que serão todos solicitados ao mesmo tempo, em vez de individualmente. A mbox global é sempre retornada.

### Gerenciar cintilação

A SDK fornece recursos para [gerenciar a cintilação](../personalization/manage-flicker.md) durante o processo de personalização.

## Renderiza apresentações em aplicativos de página única sem incrementar métricas {#applypropositions}

O comando `applyPropositions` permite renderizar ou executar uma matriz de propostas de [!DNL Target] ou Adobe Journey Optimizer em aplicativos de página única, sem incrementar as métricas [!DNL Analytics] e [!DNL Target]. Isso aumenta a precisão dos relatórios.

>[!IMPORTANT]
>
>Se as propostas para o escopo `__view__` (ou uma superfície da web) foram renderizadas no carregamento da página, o sinalizador `renderAttempted` será definido como `true`. O comando `applyPropositions` não renderizará novamente as propostas de escopo `__view__` (ou superfície da Web) que têm o sinalizador `renderAttempted: true`.

### Caso de uso 1: renderizar novamente as apresentações de exibição do aplicativo de página única

O caso de uso descrito na amostra abaixo renderiza novamente as propostas de visualização do carrinho buscadas e renderizadas anteriormente, sem enviar notificações de exibição.

No exemplo abaixo, o comando `sendEvent` é acionado mediante uma alteração de exibição e salva o objeto resultante em uma constante.

Em seguida, quando a exibição ou um componente é atualizado, o comando `applyPropositions` é chamado, com as propostas do comando `sendEvent` anterior, para renderizar novamente as propostas de exibição.

```js
var cartPropositions = alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "web": {
      "webPageDetails": {
        "viewName": "cart"
      }
    }
  }
}).then(function(result) {
  var propositions = result.propositions;

  // Collect response tokens, etc.
  return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
  "propositions": cartPropositions
});
```

### Caso de uso 2: renderizar apresentações que não têm um seletor

Este caso de uso se aplica a experiências criadas usando o [!DNL Target Form-based Experience Composer] ou o [Canal de experiência baseado em código](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/code-based-experience/get-started-code-based) do Adobe Journey Optimizer.

Você deve fornecer o seletor, a ação e o escopo na chamada `applyPropositions`.

`actionTypes` com suporte são:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
  "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
  // Render propositions on the page by providing additional metadata

  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      "salutation": {
        "selector": "#first-form-based-offer",
        "actionType": "setHtml"
      },
      "discount": {
        "selector": "#second-form-based-offer",
        "actionType": "replaceHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    function sendDisplayEvent(proposition) {
      const {
        id,
        scope,
        scopeDetails = {}
      } = proposition;

      alloy("sendEvent", {
        "xdm": {
          "eventType": "decisioning.propositionDisplay",
          "_experience": {
            "decisioning": {
              "propositions": [{
                "id": id,
                "scope": scope,
                "scopeDetails": scopeDetails
              }],
              "propositionEventType": {
                "display": 1
              }
            }
          }
        }
      });
    }
  });
});
```

Se você não fornecer metadados para um escopo de decisão, as apresentações associadas não serão renderizadas.
