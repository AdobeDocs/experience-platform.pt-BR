---
title: Comparação da at.js com o SDK da Web do Experience Platform
description: Saiba como os recursos da at.js se comparam ao SDK da Web do Experience Platform
keywords: target; adobe target; activity.id; experience.id; renderDecisões; decisionScopes; pré-ocultar trecho; vec; Experience Composer baseado em formulário; xdm; públicos-alvo; decisões; escopo; esquema; diagrama do sistema; diagrama
source-git-commit: 6efb40e90cb8c29a0141bb0db6e20cec23f2be9a
workflow-type: tm+mt
source-wordcount: '2277'
ht-degree: 6%

---

# Comparação da biblioteca at.js com o SDK da Web

## Visão geral

Este artigo fornece uma visão geral das diferenças entre os `at.js` e o SDK da Web da Experience Platform.

## Instalação das bibliotecas

### Instalação da at.js

Nós permitimos que nossos clientes baixem a biblioteca diretamente do Adobe Experience Cloud, guia Implementação. A biblioteca at.js é personalizada com as configurações desejadas pelo cliente: clientCode, imsOrgId etc.

### Instalação do SDK da Web

A versão pré-criada está disponível em um CDN. Você pode fazer referência à biblioteca no CDN diretamente na sua página ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e não minificados. A versão não minificada é útil para fins de depuração.

Estrutura do URL: https://cdn1.adoberesources.net/alloy/[VERSÃO]/alloy.min.js OU alloy.js para a versão não minificada.

Por exemplo:

* Minificado: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Não minificado: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)

[Saiba mais](../../fundamentals/installing-the-sdk.md)

## Configuração das bibliotecas

### Configuração da at.js

Ao final de cada arquivo at.js, você encontrará uma seção na qual instanciamos e passamos um objeto de configuração. É personalizável. No download, preenchemos essa seção com as configurações atuais do cliente.

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

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)


### Configuração do SDK da Web

A configuração do SDK é feita com a variável `configure` comando.

>[!IMPORTANT]
>
>`configure` é *always* o primeiro comando chamado.

Exemplo:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Há muitas opções que podem ser definidas durante a configuração. Todas as opções podem ser encontradas abaixo, agrupadas por categoria.

[Saiba mais](../../fundamentals/configuring-the-sdk.md)


## Como solicitar e renderizar automaticamente as ofertas de Carregamento de página do Target

### Uso da at.js

Uso da at.js 2.x, se você ativar a configuração `pageLoadEnabled`, a biblioteca acionará uma chamada para o Target Edge com `execute -> pageLoad`. Se todas as configurações estiverem definidas com os valores padrão, nenhuma codificação personalizada será necessária.Depois que a at.js for adicionada à página e carregada pelo navegador, uma chamada do Target Edge será executada.

### Uso do SDK da Web

Conteúdo criado no Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) pode ser recuperada e renderizada automaticamente pelo SDK.

Para solicitar e renderizar ofertas do Target automaticamente, use a variável `sendEvent` e defina o `renderDecisions` para `true`. Isso força o SDK a renderizar automaticamente qualquer conteúdo personalizado elegível para renderização automática.

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

O SDK da Web do Experience Platform envia automaticamente uma notificação com as ofertas que foram executadas pelo SDK da WEB. Este é um exemplo de como a carga da solicitação de notificação se parece com:

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

Há duas maneiras de disparar uma chamada para o Target Edge que buscará ofertas para carregamento de página.

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

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)

### Uso do SDK da Web

Executar um `sendEvent` comando com escopo especial em `decisionScopes`: `__view__`. Usamos esse escopo como um sinal para buscar todas as atividades de carregamento de página do Target e realizar uma busca prévia em todas as exibições. O SDK da Web também tentará avaliar todas as atividades baseadas na visualização do VEC. No momento, não há suporte para desativar a pré-busca da visualização no SDK da Web.

Para acessar qualquer conteúdo de personalização, você pode fornecer uma função de retorno de chamada, que será chamada depois que o SDK receber uma resposta bem-sucedida do servidor. O retorno de chamada é fornecido como um objeto de resultado, que pode conter propriedades de propostas contendo qualquer conteúdo de personalização retornado.

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


## Como solicitar mboxes específicas baseadas em formulário do Target


### Uso da at.js

Você pode buscar atividades do Criador baseado em formulário usando o `getOffer` função:

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

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)


### Uso do SDK da Web

Você pode buscar atividades baseadas no Criador baseado em formulário usando o `sendEvent` e transmitindo os nomes da mbox sob a `decisionScopes` opção. O `sendEvent` retornará uma promessa que é resolvida com um objeto contendo as atividades / propostas solicitadas: É assim que a função `propositions` matriz tem a seguinte aparência:

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

Você pode aplicar as atividades do Target usando o `applyOffers` função: `adobe.target.applyOffer(options)`

Exemplo:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=en)

### Uso do SDK da Web

No momento, esse recurso não é compatível com o SDK da Web.

## Como rastrear eventos

### Uso da at.js

Você pode rastrear eventos usando o `trackEvent` ou usando `sendNotifications`.

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

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=en)

### Uso do SDK da Web

Você pode rastrear eventos e ações do usuário chamando a função `sendEvent` , preenchendo o `_experience.decisioning.propositions` Grupo de campos XDM e configuração do `eventType` para um dos dois valores:

* `decisioning.propositionDisplay`: Sinaliza a renderização da atividade do Target.
* `decisioning.propositionInteract`: Sinaliza uma interação do usuário com a atividade, como um clique do mouse.

O `_experience.decisioning.propositions` O grupo de campos XDM é uma matriz de objetos. As propriedades de cada objeto são derivadas da variável `result.propositions` que é retornado no `sendEvent` comando: `{ id, scope, scopeDetails }`

**Exemplo 1 - Rastrear um `decisioning.propositionDisplay` evento após renderizar uma atividade**

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

**Exemplo 2 - Rastrear um `decisioning.propositionInteract` evento depois que ocorre uma métrica de clique**

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

## Como acionar uma alteração de exibição em um aplicativo de página única

### Uso da at.js

Use o `adobe.target.triggerView` . Essa função pode ser chamada sempre que uma nova página é carregada ou quando um componente em uma página é renderizado novamente. adobe.target.triggerView() deve ser implementado para aplicativos de página única (SPA) para usar o Visual Experience Composer (VEC) para criar atividades de teste A/B e direcionamento de experiência (XT). Se adobe.target.triggerView() não estiver implementado no site, o VEC não poderá ser usado para SPA.

**Exemplo**

```javascript
adobe.target.triggerView("homeView")
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=en)


### Uso do SDK da Web

Para acionar ou sinalizar uma alteração de exibição de aplicativo de página única, defina a variável `web.webPageDetails.viewName` propriedade sob o `xdm` da `sendEvent` comando. O SDK da Web verificará o cache de exibição, se houver ofertas para o `viewName` especificado em `sendEvent` ele os executará e enviará um evento de notificação de exibição.

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

## Como aproveitar os tokens de resposta

O conteúdo de personalização retornado do Adobe Target inclui [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que são detalhes sobre a atividade, oferta, experiência, perfil do usuário, informações geográficas e muito mais. Esses detalhes podem ser compartilhados com ferramentas de terceiros ou usados para depuração. Os tokens de resposta podem ser configurados na interface do usuário do Adobe Target.

### Uso da at.js

Use eventos personalizados da at.js para ouvir a resposta do Target e ler os tokens de resposta.

**Exemplo**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)


### Uso do SDK da Web

>[!IMPORTANT]
>
>Certifique-se de que você esteja usando o SDK da Web da plataforma versão 2.6.0 ou posterior.

Os tokens de resposta são retornados como parte do `propositions` expostos no resultado da `sendEvent` comando. Cada proposta contém uma matriz de `items`e cada item terá uma `meta` objeto preenchido com tokens de resposta se estiverem ativados na interface do usuário do administrador do Target. [Saiba mais](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)

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

Usando a at.js, você pode gerenciar a cintilação definindo `bodyHidingEnabled: true` para que a at.js seja a que cuidaria de pré-ocultar os contêineres personalizados antes de buscar e aplicar as alterações do DOM.
As seções de página que contêm conteúdo personalizado podem ser pré-ocultadas ao substituir a at.js `bodyHiddenStyle`.
Por padrão `bodyHiddenStyle` oculta todo o HTML `body`.
Ambas as configurações podem ser substituídas usando `window.targetGlobalSettings`. `window.targetGlobalSettings` deve ser colocada antes de carregar a at.js.

### Uso do SDK da Web

Usando o SDK da Web, o cliente pode configurar seu estilo de pré-ocultação no comando configure, como no exemplo abaixo:

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Ao carregar a SDK da Web assíncrona, recomendamos que o seguinte snippet seja inserido na página antes da injeção do SDK da Web:

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

Há dois tipos de registro do A4T que são compatíveis com o uso da at.js:

* Registro no lado do cliente do Analytics
* Registro no lado do servidor do Analytics

#### Registro no lado do cliente do Analytics

**Exemplo 1: Uso da configuração global do Target**

O registro no lado do cliente do Analytics pode ser ativado ao configurar `analyticsLogging: client_side` nas configurações da at.js ou substituindo o `window.targetglobalSettings` objeto.
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

Exemplo 2: Configurando em cada `getOffers` função:

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

Esta é a aparência da carga da resposta:

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

A carga do Analytics (`tnta` (token) deve ser incluído na ocorrência do Analytics usando [API de inserção de dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Registro no lado do servidor do Analytics

O registro no lado do servidor do Analytics pode ser ativado ao configurar `analyticsLogging: server_side` nas configurações da at.js ou substituindo o `window.targetglobalSettings` objeto.
Em seguida, os dados fluem da seguinte maneira:

![](assets/a4t-server-side-atjs.png)

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=en)

### Uso do SDK da Web

O SDK da Web também suporta:

* Registro do lado do cliente do Analytics
* Registro no lado do servidor do Analytics

#### Registro no lado do cliente do Analytics

O registro no lado do cliente do Analytics é ativado quando o Adobe Analytics é desativado para essa configuração do DataStream.

![](assets/analytics-disabled-datastream-config.png)

O cliente tem acesso ao token do Analytics (`tnta`) que precisa ser compartilhado com o Analytics usando [API de inserção de dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
em encadeando o `sendEvent` e percorra a matriz de propostas resultante.

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

Este é um diagrama para mostrar como os dados fluem quando o lado do cliente do Analytics está ativado:

![](assets/analytics-client-side-logging.png)

#### Registro no lado do servidor do Analytics

O registro no lado do servidor do Analytics é ativado quando o Analytics é ativado para essa configuração do DataStream.

![](assets/analytics-enabled-datastream-config.png)

Quando o Registro de análises do lado do servidor é ativado, a carga A4T que precisa ser compartilhada com o Analytics para que os relatórios do Analytics mostrem impressões e conversões corretas é compartilhada no nível da borda da experiência, para que o cliente não precise fazer nenhum processamento adicional.

Veja como os dados fluem para nossos sistemas quando o Registro de análises do lado do servidor está ativado:

![](assets/analytics-server-side-logging.png)

## Como definir as configurações globais do Target

### Uso da at.js

Você pode substituir as configurações na biblioteca at.js usando `window.targetGlobalSettings`, em vez de definir as configurações na interface do usuário do Target Standard/Premium ou usar APIs REST.

A substituição deve ser definida antes que at.js seja carregada ou em Administration > Implementation > Edit at.js Settings > Code Settings > Library Header.

Exemplo:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)

### Uso do SDK da Web

Esse recurso não é compatível com o SDK da Web.

## Como atualizar atributos de perfil do Target

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

### Uso do SDK da Web

Para atualizar um perfil do Target, use o `sendEvent` e defina o `data.__adobe.target` , como prefixar os nomes das chaves usando `profile`.

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

## Como usar o Target Recommendations

### Uso da at.js

**Exemplo 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.productName": "T-shirt",
     "entity.productId": "1234"
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
            "entity.productName": "T-shirt",
            "entity.productId": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=en)


### Uso do SDK da Web

Para enviar dados do Recommendation, use o `sendEvent` e defina o `data.__adobe.target` , como prefixar os nomes das chaves usando `entity`.

**Exemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.productName": "T-shirt",
        "entity.productId": "1234"
      }
    }
  }
});
```

## Como usar IDs de terceiros

### Uso da at.js

Usando a at.js, há várias maneiras de enviar `mbox3rdPartyId`, usando `getOffer` ou `getOffers`:

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

Ou há uma maneira de configurar o `mbox3rdPartyId` ou em `targetPageParams` ou `targetPageParamsAll`.
Ao configurá-lo em `targetPageParams`, ele será enviado nos pedidos de `target-global-mbox` também conhecido como `pag-lLoad`.
A recomendação deve ser definida usando `targetPageParamsAll` como será enviado em cada solicitação do target.
A vantagem de usar `targetPageParamsAll` é que você pode definir a variável `mbox3rdPartyId` na página uma vez, e isso garantirá que todas as solicitações do target tenham o direito de `mbox3rdPartyId`.

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

[Saiba mais](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=en)

### Uso do SDK da Web

O SDK da Web é compatível com a ID de terceiros do Target. No entanto, requer mais algumas etapas. Antes de mergulhar na solução, deveríamos falar um pouco sobre `identityMap`.
O Mapa de identidade permite que os clientes enviem várias identidades. Todas as identidades são namespacadas. Cada namespace pode ter uma ou mais identidades. Uma identidade específica pode ser marcada como primária.
Com esse conhecimento em mente, podemos ver quais são as etapas necessárias para configurar o sdk da Web para usar a ID de terceiros do Target.

1. Configure o namespace que conterá a ID de terceiros do Target na exibição Configuração do fluxo de dados:

![](assets/mbox-3-party-id-setup.png)

1. Envie esse namespace de identidade em cada comando sendEvent como este:

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

Ao usar a at.js, há duas maneiras de configurar os tokens de propriedade, usando `targetPageParams` ou `targetPageParamsAll`. Usando `targetPageParams` adiciona o token de propriedade ao `target-global-mbox` , mas usando `targetPageParamsAll` adiciona o token a todas as chamadas do target:

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

### Uso do SDK da Web

Usando o SDK da Web, os clientes podem configurar a propriedade em um nível superior, ao configurar a configuração do Fluxo de dados, no namespace Adobe Target:
![](assets/at-property-setup.png)
Isso significa que cada chamada do Target para essa configuração específica do Fluxo de dados conterá esse token de propriedade.

## Como fazer a busca prévia de mboxes

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

OBSERVAÇÃO: É altamente recomendável garantir que cada `mbox` no `mboxes` matriz tem seu próprio índice. Geralmente, a primeira mbox tem `index=0`, o próximo `index=1`, etc.

### Uso do SDK da Web

No momento, essa funcionalidade não é compatível com o SDK da Web.

## Como depurar minha implementação do Target

### Uso da at.js

A at.js expõe esses recursos de depuração:

* Mbox Disable - Desative o Target para buscar e renderizar a página e verificar se está quebrada sem interações do Target
* Mbox Debug - at.js registra cada ação
* Target Trace - com um token de rastreamento de mbox gerado na Bullseye, um objeto de rastreamento com detalhes que participaram do processo de decisão está disponível em `window.___target_trace` objeto

Observação: Todos esses recursos de depuração estão disponíveis com recursos aprimorados no [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Uso do SDK da Web

Você tem vários recursos de depuração ao usar o SDK da Web:

* Usando [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
* [Depuração de SDK da Web ativada](../../../edge/fundamentals/debugging.md)
* Use [Ganchos de monitoramento do SDK da Web](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Use [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html?lang=en)
* Target Trace
