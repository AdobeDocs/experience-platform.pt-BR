---
title: Comparação da at.js com o Experience Platform Web SDK
description: Saiba como os recursos da at.js se comparam ao Experience Platform Web SDK
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;ocultando previamente o trecho;vec;Criador de experiências baseado em formulário;xdm;públicos-alvo;decisões;escopo;esquema;diagrama do sistema;diagrama
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 3%

---

# Comparação da biblioteca at.js com a Web SDK

## Visão geral

Este artigo fornece uma visão geral das diferenças entre a biblioteca `at.js` e o Experience Platform Web SDK.

## Instalação de bibliotecas

### Instalação da at.js

Permitimos que nossos clientes baixem a biblioteca diretamente da Adobe Experience Cloud, guia Implementação. A biblioteca at.js é personalizada com configurações que o cliente tem como: clientCode, imsOrgId etc.

### Instalação do Web SDK

A versão pré-criada está disponível em um CDN. Você pode fazer referência à biblioteca na CDN diretamente na sua página ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e não minificados. A versão não reduzida é útil para fins de depuração.

Consulte [Instalar o Web SDK usando a biblioteca JavaScript](/help/web-sdk/install/library.md) para obter mais informações.

## Configuração das bibliotecas

### Configuração da at.js

No final de cada arquivo da at.js, você encontrará uma seção na qual instanciamos e passamos um objeto de configuração. É personalizável. No download, preenchemos essa seção com as configurações atuais do cliente.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=pt-BR)


### Configuração do Web SDK

A configuração da SDK é feita com o comando [`configure`](/help/web-sdk/commands/configure/overview.md). O comando `configure` é *sempre* chamado primeiro.

## Como solicitar e renderizar automaticamente ofertas do Target de carregamento de página

### Uso da at.js

Usando a at.js 2.x, se você habilitar a configuração `pageLoadEnabled`, a biblioteca disparará uma chamada para o Target Edge com `execute -> pageLoad`. Se todas as configurações forem definidas com os valores padrão, nenhuma codificação personalizada será necessária. Depois que a at.js for adicionada à página e carregada pelo navegador, uma chamada de Edge do Target será executada.

### Utilização do Web SDK

O conteúdo criado no [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR) do Adobe Target pode ser recuperado e renderizado automaticamente pela SDK.

Para solicitar e renderizar automaticamente ofertas do Target, use o comando `sendEvent` e defina a opção `renderDecisions` como `true`. Isso força o SDK a renderizar automaticamente qualquer conteúdo personalizado que esteja qualificado para renderização automática.

Exemplo:

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

O Experience Platform Web SDK envia automaticamente uma notificação com as ofertas que foram executadas pelo WEB SDK. Este é um exemplo de como uma carga de solicitação de notificação se parece com:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Saiba mais](../rendering-personalization-content.md)

## Como solicitar e NÃO renderizar automaticamente as ofertas do Target de carregamento de página

### Uso da at.js

Há duas maneiras de acionar uma chamada para o Target Edge que buscará ofertas para o carregamento de página.

Exemplo 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Exemplo 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=pt-BR)

### Utilização do Web SDK

Execute um comando `sendEvent` com um escopo especial em `decisionScopes`: `__view__`. Usamos esse escopo como um sinal para buscar todas as atividades de carregamento de página do Target e realizar uma busca prévia por todas as exibições. O Web SDK também tentará avaliar todas as atividades baseadas em visualização do VEC. No momento, a desabilitação da busca prévia de visualização não é suportada no Web SDK.

Para acessar qualquer conteúdo de personalização, você pode fornecer uma função de retorno de chamada, que será chamada depois que o SDK receber uma resposta bem-sucedida do servidor. Sua chamada de retorno recebe um objeto de resultado, que pode conter propriedades de apresentações contendo qualquer conteúdo de personalização retornado.

Exemplo:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Saiba mais](../rendering-personalization-content.md#manually-rendering-content)


## Como solicitar mboxes específicas do Target com base em formulário


### Uso da at.js

Você pode buscar atividades do Form Based Composer usando a função `getOffer`:

Exemplo 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Exemplo 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=pt-BR)


### Utilização do Web SDK

Você pode buscar atividades baseadas no Form Based Composer usando o comando `sendEvent` e passando os nomes da mbox sob a opção `decisionScopes`. O comando `sendEvent` retornará uma promessa que é resolvida com um objeto contendo as atividades/propostas solicitadas:
Esta é a aparência da matriz `propositions`:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Exemplo:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Saiba mais](../rendering-personalization-content.md#manually-rendering-content)

## Como aplicar as atividades do Target

### Uso da at.js

Você pode aplicar as atividades do Target usando a função `applyOffers`: `adobe.target.applyOffer(options)`

Exemplo:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Saiba mais sobre o comando `applyOffers` na [documentação dedicada](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=pt-BR).


### Utilização do Web SDK

Você pode aplicar as atividades do Target usando o comando `applyPropositions`.

Exemplo:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Saiba mais sobre o comando `applyPropositions` na [documentação dedicada](../../personalization/rendering-personalization-content.md#applypropositions).

## Como rastrear eventos

### Uso da at.js

Você pode rastrear eventos usando a função `trackEvent` ou `sendNotifications`.

Essa função envia uma solicitação para relatar ações do usuário, como cliques e conversões. Ele não fornece atividades na resposta.


**Exemplo 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Exemplo 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=pt-BR)

### Utilização do Web SDK

Você pode rastrear eventos e ações do usuário chamando o comando `sendEvent`, preenchendo o grupo de campos XDM `_experience.decisioning.propositions` e definindo o `eventType` como um dos dois valores:

* `decisioning.propositionDisplay`: Sinaliza a renderização da atividade do Target.
* `decisioning.propositionInteract`: Sinaliza uma interação do usuário com a atividade, como um clique do mouse.

O grupo de campos XDM `_experience.decisioning.propositions` é uma matriz de objetos. As propriedades de cada objeto são derivadas do `result.propositions` que é retornado no comando `sendEvent`: `{ id, scope, scopeDetails }`

**Exemplo 1 - Rastrear um evento `decisioning.propositionDisplay` após renderizar uma atividade**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
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

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
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
```

**Exemplo 2 - Rastrear um evento `decisioning.propositionInteract` após a ocorrência de uma métrica de cliques**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Saiba mais](../rendering-personalization-content.md#manually-rendering-content)

**Exemplo 3 - Rastrear um evento disparado após executar uma ação**

Este exemplo rastreia um evento que foi acionado após a execução de uma ação específica, como clicar em um botão.
Você pode adicionar outros parâmetros personalizados por meio do objeto de dados `__adobe.target`.

Você também pode adicionar o objeto XDM `commerce`.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## Como acionar uma alteração de exibição em um Aplicativo de página única

### Uso da at.js

Use a função `adobe.target.triggerView`. Essa função pode ser chamada sempre que uma nova página é carregada ou quando um componente em uma página é renderizado novamente. adobe.target.triggerView() deve ser implementado para aplicativos de página única (SPAs) para usar o Visual Experience Composer (VEC) para criar atividades de teste A/B e direcionamento de experiência (XT). Se adobe.target.triggerView() não estiver implementado no site, o VEC não poderá ser usado para SPA.

**Exemplo**

```javascript
adobe.target.triggerView("homeView")
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=pt-BR)


### Utilização do Web SDK

Para acionar ou sinalizar uma Alteração de Exibição de aplicativo de página única, defina a propriedade `web.webPageDetails.viewName` na opção `xdm` do comando `sendEvent`. O Web SDK verificará o cache de exibição. Se houver ofertas para o `viewName` especificado em `sendEvent`, ele as executará e enviará um evento de notificação de exibição.

**Exemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Saiba mais](./spa-implementation.md#implementing-xdm-views)

## Como utilizar tokens de resposta

O conteúdo do Personalization retornado do Adobe Target inclui [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=pt-BR), que são detalhes sobre a atividade, a oferta, a experiência, o perfil do usuário, as informações geográficas e muito mais. Esses detalhes podem ser compartilhados com ferramentas de terceiros ou usados para depuração. Os tokens de resposta podem ser configurados na interface do usuário do Adobe Target.

### Uso da at.js

Use eventos personalizados da at.js para ouvir a resposta do Target e ler os tokens de resposta.

**Exemplo**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=pt-BR)


### Utilização do Web SDK

>[!IMPORTANT]
>
>Verifique se você está usando o Experience Platform Web SDK versão 2.6.0 ou posterior.

Os Tokens de Resposta são retornados como parte de `propositions`, que são expostos no resultado do comando `sendEvent`. Cada proposta contém uma matriz de `items` e cada item terá um objeto `meta` preenchido com Tokens de resposta se eles estiverem habilitados na interface do administrador do Target. [Saiba mais](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=pt-BR)

**Exemplo**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Saiba mais](./accessing-response-tokens.md)

## Como gerenciar a cintilação

### Uso da at.js

Usando a at.js, você pode gerenciar a cintilação definindo `bodyHidingEnabled: true` para que a at.js seja a pessoa que cuidará disso
pré-ocultar os contêineres personalizados antes de buscar e aplicar as alterações do DOM.
As seções de página que contêm conteúdo personalizado podem ser pré-ocultas substituindo a at.js `bodyHiddenStyle`.
Por padrão, `bodyHiddenStyle` oculta todo o HTML `body`.
Ambas as configurações podem ser substituídas usando `window.targetGlobalSettings`. `window.targetGlobalSettings` deve ser colocado antes de carregar at.js.

### Utilização do Web SDK

Usando o Web SDK, o cliente pode definir seu estilo de pré-ocultação no comando de configuração, como no exemplo abaixo:

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Ao carregar o Web SDK async, recomendamos que o seguinte trecho seja inserido na página antes que o Web SDK seja inserido:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Como o A4T está sendo tratado

### Uso da at.js

Há dois tipos de registro A4T compatíveis com o uso da at.js:

* Registro do Analytics no lado do cliente
* Registro do lado do servidor do Analytics

#### Registro do Analytics no lado do cliente

**Exemplo 1: Usando Configuração Global de Destino**

O registro de log do cliente do Analytics pode ser habilitado definindo-se `analyticsLogging: client_side` nas configurações da at.js ou substituindo-se o objeto `window.targetglobalSettings`.
Quando essa opção é configurada, o formato da carga retornada é semelhante ao seguinte:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

A carga pode ser encaminhada para o Analytics por meio da API de inserção de dados.

Exemplo 2: configurando-o em cada função `getOffers`:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Esta é a aparência da carga de resposta:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

A carga do Analytics (`tnta` token) deve ser incluída na ocorrência do Analytics usando a [API de Inserção de Dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Registro do lado do servidor do Analytics

O log do Analytics Server Side pode ser habilitado ao configurar o `analyticsLogging: server_side` nas configurações da at.js ou ao substituir o objeto `window.targetglobalSettings`.
Em seguida, os dados fluem da seguinte maneira:

![Diagrama mostrando o fluxo de trabalho do log do Analytics Server Side](assets/a4t-server-side-atjs.png)

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=pt-BR)

### Utilização do Web SDK

O Web SDK também é compatível com:

* Registro do Analytics no lado do cliente
* Registro do Analytics Server Side

#### Registro do Analytics no lado do cliente

O Log do cliente do Analytics é ativado quando o Adobe Analytics é desativado para essa configuração de DataStream.

![Diagrama mostrando o fluxo de trabalho de log do Analytics Client Side](assets/analytics-disabled-datastream-config.png)

O cliente tem acesso ao token do Analytics (`tnta`) que precisa ser compartilhado com o Analytics usando a [API de Inserção de Dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
para entrar, encadeie o comando `sendEvent` e repita por meio da matriz de propostas resultante.

**Exemplo**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Este é um diagrama para mostrar como os dados fluem quando o Analytics Client Side está ativado:

![Diagrama de fluxo de dados no log do Analytics Client Side](assets/analytics-client-side-logging.png)

#### Registro do lado do servidor do Analytics

O registro no lado do servidor do Analytics é ativado quando o Analytics é ativado para essa configuração de DataStream.

![Interface do usuário de sequências de dados mostrando as configurações do Analytics.](assets/analytics-enabled-datastream-config.png)

Quando o Registro de análise do lado do servidor estiver ativado, a carga do A4T que precisa ser compartilhada com o Analytics para que os relatórios do Analytics sejam exibidos
as impressões e conversões corretas são compartilhadas no nível do Edge Network, para que o cliente não precise fazer nenhum processamento adicional.

Veja como os dados fluem para nossos sistemas quando o registro do Server Side Analytics está ativado:

![Diagrama mostrando o fluxo de dados no log do Server Side Analytics](assets/analytics-server-side-logging.png)

## Como definir as configurações globais do Target

### Uso da at.js

Você pode substituir as configurações na biblioteca at.js usando `window.targetGlobalSettings`, em vez de definir as configurações na interface do usuário do Target Standard/Premium ou usar APIs REST.

A substituição deve ser definida antes que a at.js seja carregada ou em Administração > Implementação > Editar configurações da at.js > Configurações de código > Cabeçalho da biblioteca.

Exemplo:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=pt-BR)

### Utilização do Web SDK

Este recurso não tem suporte no Web SDK.

## Como atualizar atributos do perfil do Target

### Uso da at.js

**Exemplo 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Exemplo 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Utilização do Web SDK

Para atualizar um perfil de Destino, use o comando `sendEvent` e defina a propriedade `data.__adobe.target`, prefixando os nomes de chave com `profile`.

**Exemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Como usar as Recomendações do Target

### Uso da at.js

**Exemplo 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Exemplo 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=pt-BR)


### Utilização do Web SDK

Para enviar dados de Recomendação, use o comando `sendEvent` e defina a propriedade `data.__adobe.target`, prefixando os nomes de chave usando `entity`.

**Exemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## Como usar IDs de terceiros

### Uso da at.js

Ao usar a at.js, há várias maneiras de enviar `mbox3rdPartyId`, usando `getOffer` ou `getOffers`:

**Exemplo 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Exemplo 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

Ou há uma maneira de configurar o `mbox3rdPartyId` em `targetPageParams` ou `targetPageParamsAll`.
Ao ser configurado em `targetPageParams`, ele será enviado nas solicitações para `target-global-mbox` também conhecidas como `pag-lLoad`.
A recomendação deve ser definida usando `targetPageParamsAll`, pois será enviada em cada solicitação de público-alvo.
A vantagem de usar o `targetPageParamsAll` é que você pode definir o `mbox3rdPartyId` na página uma vez e isso garantirá que todas as solicitações do target tenham o `mbox3rdPartyId` correto.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=pt-BR)

### Utilização do Web SDK

O Web SDK oferece suporte à ID de terceiros do Target. No entanto, requer mais algumas etapas. Antes de mergulhar na solução, devemos falar um pouco sobre `identityMap`.
O Mapa de identidade permite que os clientes enviem várias identidades. Todas as identidades têm namespace. Cada namespace pode ter uma ou mais identidades. Uma identidade específica pode ser marcada como primária.
Com esse conhecimento em mente, podemos ver quais são as etapas necessárias para configurar o sdk da Web para usar a ID de terceiros do Target.

1. Configure o namespace que conterá a ID de terceiros do Target na página de configuração do fluxo de dados:

![Interface do usuário de sequências de dados mostrando o campo de namespace de ID de terceiros do Target](assets/mbox-3-party-id-setup.png)

1. Envie esse namespace de identidade em cada comando sendEvent, desta forma:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Como definir tokens de propriedade

### Uso da at.js

Ao usar a at.js, há duas maneiras de configurar os tokens de propriedade, usando `targetPageParams` ou `targetPageParamsAll`. Usar `targetPageParams` adiciona o token de propriedade à chamada `target-global-mbox`, mas usar `targetPageParamsAll` adiciona o token a todas as chamadas de destino:

**Exemplo 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Exemplo 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Utilização do Web SDK

Usando o Web SDK, os clientes podem definir a propriedade em um nível superior, ao definir a configuração do fluxo de dados, no namespace do Adobe Target:
![Interface do usuário de fluxos de dados mostrando as configurações do Adobe Target.](assets/at-property-setup.png)
Isso significa que cada chamada do Target para essa configuração específica do Fluxo de dados conterá o token de propriedade.

## Como realizar uma busca prévia de mboxes

### Uso da at.js

Essa funcionalidade está disponível somente na at.js 2.x. A at.js 2.x tem uma nova função chamada `getOffers`. `getOffers` permite que os clientes busquem previamente conteúdo para uma ou mais mboxes. Exemplo:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

OBSERVAÇÃO: é altamente recomendável garantir que cada `mbox` na matriz `mboxes` tenha seu próprio índice. Normalmente, a primeira mbox tem `index=0`, a próxima `index=1`, etc.

### Utilização do Web SDK

No momento, não há suporte para essa funcionalidade no Web SDK.

## Como depurar minha implementação do Target

### Uso da at.js

A at.js expõe estes recursos de depuração:

* Desativação da mbox - desative o Target na busca e renderização para verificar se a página foi quebrada sem as interações do Target
* Depuração da mbox - a at.js registra cada ação
* Rastreamento de Destino - com um token de rastreamento de mbox gerado no Marcador, um objeto de rastreamento com detalhes que participaram do processo de decisão está disponível no objeto `window.___target_trace`

Observação: todos esses recursos de depuração estão disponíveis com recursos aprimorados no [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Utilização do Web SDK

Você tem vários recursos de depuração ao usar o Web SDK:

* Usando o [Assurance](/help/assurance/home.md)
* [Depuração do Web SDK ativada](/help/web-sdk/use-cases/debugging.md)
* Usar [ganchos de monitoramento do Web SDK](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Usar [Adobe Experience Platform Debugger](/help/debugger/home.md)
* Rastreamento de destino
