---
title: Renderizar conteúdo personalizado usando o SDK da Web da Adobe Experience Platform
description: Saiba como renderizar conteúdo personalizado com o SDK da Web da Adobe Experience Platform.
keywords: personalização; renderDecisões; sendEvent; decisionScopes; propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 0d8e19d8428191cc0c6c56e629e8c5528a96115c
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---

# Renderizar conteúdo personalizado

O Adobe Experience Platform Web SDK oferece suporte à recuperação de conteúdo personalizado de soluções de personalização Adobe, incluindo [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) e [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=pt-BR).

Além disso, o SDK da Web capacita recursos de personalização da mesma página e da próxima página por meio de destinos de personalização do Adobe Experience Platform, como [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [conexão de personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md). Para saber como configurar o Experience Platform para personalização de mesma página e próxima página, consulte o [guia dedicado](../../destinations/ui/configure-personalization-destinations.md).

Conteúdo criado no Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) pode ser recuperada e renderizada automaticamente pelo SDK. Conteúdo criado no Adobe Target [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ou o Offer Decisioning não pode ser renderizado automaticamente pelo SDK. Em vez disso, você deve solicitar esse conteúdo usando o SDK e, em seguida, renderizar manualmente o conteúdo por conta própria.

## Renderização automática de conteúdo

Ao enviar eventos para o servidor, você pode definir a variável `renderDecisions` para `true`. Isso força o SDK a renderizar automaticamente qualquer conteúdo personalizado elegível para renderização automática.

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

Para acessar qualquer conteúdo de personalização, você pode fornecer uma função de retorno de chamada, que será chamada depois que o SDK receber uma resposta bem-sucedida do servidor. O retorno de chamada é fornecido como `result` objeto , que pode conter uma `propositions` propriedade contendo qualquer conteúdo de personalização retornado. Abaixo está um exemplo de como você fornece uma função de retorno de chamada ao enviar um evento.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Neste exemplo, `result.propositions`, se existir, é uma matriz que contém apresentações de personalização relacionadas ao evento. Por padrão, inclui apenas propostas qualificadas para renderização automática.

O `propositions` matriz pode ser semelhante a este exemplo:

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

No exemplo, a variável `renderDecisions` não foi definida como `true` quando a variável `sendEvent` foi executado, portanto, o SDK não tentou renderizar automaticamente qualquer conteúdo. No entanto, o SDK ainda recuperou automaticamente o conteúdo elegível para renderização automática, e forneceu isso para renderizar manualmente se desejar. Observe que cada objeto de proposta tem seu `renderAttempted` propriedade definida como `false`.

Se, em vez disso, você tivesse definido a variável `renderDecisions` para `true` ao enviar o evento, o SDK tentaria renderizar quaisquer propostas qualificadas para renderização automática (conforme descrito anteriormente). Como consequência, cada um dos objetos de proposta teria seu `renderAttempted` propriedade definida como `true`. Nesse caso, não haveria necessidade de renderizar manualmente essas apresentações.

Até agora, só discutimos o conteúdo de personalização qualificado para renderização automática (ou seja, qualquer conteúdo criado no Adobe Target Visual Experience Composer). Para recuperar qualquer conteúdo de personalização _not_ se qualificável para renderização automática, é necessário solicitar o conteúdo preenchendo a variável `decisionScopes` ao enviar o evento. Um escopo é uma string que identifica uma proposta específica que você deseja recuperar do servidor.

Exemplo:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Neste exemplo, se as apresentações forem encontradas no servidor que corresponde à variável `salutation` ou `discount` são retornadas e incluídas no `result.propositions` matriz. Esteja ciente de que as apresentações qualificadas para renderização automática continuarão a ser incluídas no `propositions` , independentemente de como você configura `renderDecisions` ou `decisionScopes` opções. O `propositions` nesse caso, o array seria semelhante a este exemplo:

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

Nesse ponto, é possível renderizar o conteúdo da proposta da maneira que quiser. Neste exemplo, a proposta que corresponde à variável `discount` O escopo é uma apresentação de HTML criada com o Experience Composer baseado em formulário do Adobe Target. Supondo que você tenha um elemento em sua página com a ID de `daily-special` e deseja renderizar o conteúdo do `discount` proposta na `daily-special` , faça o seguinte:

1. Extrair apresentações do `result` objeto.
1. Faça o loop por cada proposta, procurando pela proposta com um escopo de `discount`.
1. Se você encontrar uma proposta, faça um loop por cada item na proposta, procurando pelo item que é conteúdo de HTML. (É melhor verificar do que assumir.)
1. Se você encontrar um item contendo conteúdo de HTML, encontre a variável `daily-special` na página e substitua seu HTML pelo conteúdo personalizado.
1. Após a renderização do conteúdo, envie um `display` evento.

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
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Se você usar o Adobe Target, os escopos correspondem às mboxes no servidor, exceto que todas são solicitadas de uma vez em vez de individualmente. A mbox global é sempre retornada.

### Gerenciar cintilação

O SDK fornece recursos para [gerenciar cintilação](../personalization/manage-flicker.md) durante o processo de personalização.

## Renderizar apresentações em aplicativos de página única sem incrementar métricas {#applypropositions}

O `applyPropositions` permite renderizar ou executar uma matriz de propostas a partir de [!DNL Target] em aplicativos de página única, sem aumentar o [!DNL Analytics] e [!DNL Target] métricas. Isso aumenta a precisão dos relatórios.

>[!IMPORTANT]
>
>Se as apresentações para a variável `__view__` o escopo foi renderizado no carregamento da página, seus `renderAttempted` sinalizador será definido como `true`. O `applyPropositions` não renderizará novamente o `__view__` propostas de escopo com `renderAttempted: true` sinalizador.

### Caso de uso 1: Renderizar novamente propostas de visualização de aplicativo de página única

O caso de uso descrito na amostra abaixo renderiza novamente as apresentações de visualização do carrinho buscadas e renderizadas anteriormente sem enviar notificações de exibição.

No exemplo abaixo, a variável `sendEvent` é acionado após uma alteração de exibição e salva o objeto resultante em uma constante.

Em seguida, quando a exibição ou um componente é atualizado, a variável `applyPropositions` é chamado, com as apresentações do anterior `sendEvent` , para renderizar novamente as apresentações de exibição.

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
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
    propositions: cartPropositions
});
```

### Caso de uso 2: Renderizar apresentações que não têm um seletor

Esse caso de uso se aplica às ofertas de atividade criadas com o uso da variável [!DNL Target Form-based Experience Composer].

Você deve fornecer o seletor, a ação e o escopo na `applyPropositions` chame.

Suportado `actionTypes` são:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

Se você não fornecer metadados para um escopo de decisão, as apresentações associadas não serão renderizadas.