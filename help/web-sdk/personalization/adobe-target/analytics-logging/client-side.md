---
title: Logon do lado do cliente para dados do A4T no SDK da Web da plataforma
description: Saiba como ativar o registro do lado do cliente para o Adobe Analytics for Target (A4T) usando o SDK da Web do Experience Platform.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;registro;sdk da web;experiência;plataforma;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Logon do lado do cliente para dados do A4T no SDK da Web da plataforma

## Visão geral {#overview}

O SDK da Web da Adobe Experience Platform permite coletar dados do [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) no lado do cliente do aplicativo Web.

Registro do lado do cliente significa que os dados relevantes do [!DNL Target] são retornados no lado do cliente, permitindo que você os colete e compartilhe com o Analytics. Essa opção deve ser ativada se você pretende enviar dados manualmente para o Analytics usando a [API de inserção de dados](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Um método para executar isso usando o [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR) está atualmente em desenvolvimento e estará disponível em breve.

Este documento aborda as etapas para configurar o registro A4T do lado do cliente para o SDK da Web e fornece alguns exemplos de implementação para casos de uso comuns.

## Pré-requisitos {#prerequisites}

Este tutorial pressupõe que você esteja familiarizado com os conceitos e processos fundamentais relacionados ao uso do SDK da Web para fins de personalização. Consulte a documentação a seguir se precisar de uma introdução:

* [Configuração do SDK da Web](/help/web-sdk/commands/configure/overview.md)
* [Envio de eventos](/help/web-sdk/commands/sendevent/overview.md)
* [Renderização do conteúdo de personalização](../../rendering-personalization-content.md)

## Configurar o registro do cliente no Analytics {#set-up-client-side-logging}

As subseções a seguir descrevem como habilitar o registro no lado do cliente do Analytics para a implementação do SDK da Web.

### Habilitar o registro do cliente no Analytics {#enable-analytics-client-side-logging}

Para considerar o log de cliente do Analytics habilitado para sua implementação, você deve desabilitar a configuração do Adobe Analytics na sua [sequência de dados](../../../../datastreams/overview.md).

![Configuração de sequência de dados do Analytics desabilitada](../assets/disable-analytics-datastream.png)

### Recuperar dados de [!DNL A4T] do SDK e enviá-los para o Analytics {#a4t-to-analytics}

Para que esse método de relatório funcione corretamente, você deve enviar os dados relacionados a [!DNL A4T] recuperados do comando [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) na ocorrência do Analytics.

Quando o Target Edge calcula uma resposta de apresentações, ele verifica se o registro no lado do cliente do Analytics está ativado (ou seja, se o Analytics está desativado no fluxo de dados). Se o registro no lado do cliente estiver ativado, o sistema adicionará um token do Analytics a cada proposta na resposta.

O fluxo é semelhante a este:

![Fluxo de log do lado do cliente](../assets/analytics-client-side-logging.png)

Este é um exemplo de uma resposta `interact` quando o log no lado do cliente do Analytics está habilitado. Se a proposta for para uma atividade que tenha relatórios do Analytics, ela terá a propriedade `scopeDetails.characteristics.analyticsToken`.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

As apresentações de atividades do Experience Composer baseadas em formulário podem conter itens de métrica de conteúdo e clique na mesma apresentação. Assim, em vez de terem um único token de análise para exibição de conteúdo na propriedade `scopeDetails.characteristics.analyticsToken`, eles podem ter um token de análise de exibição e um token de análise de clique especificados nas propriedades `scopeDetails.characteristics.analyticsDisplayToken` e `scopeDetails.characteristics.analyticsClickToken`, respectivamente.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Todos os valores de `scopeDetails.characteristics.analyticsToken`, bem como `scopeDetails.characteristics.analyticsDisplayToken` (para conteúdo exibido) e `scopeDetails.characteristics.analyticsClickToken` (para métricas de clique) são as cargas do A4T que precisam ser coletadas e incluídas como tag `tnta` na chamada da [API de Inserção de Dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

>[!IMPORTANT]
>
>As propriedades `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` podem conter vários tokens, concatenados como uma única cadeia de caracteres delimitada por vírgulas.
>
>Nos exemplos de implementação fornecidos na próxima seção, vários tokens do Analytics são coletados interativamente. Para concatenar uma matriz de tokens do Analytics, use uma função semelhante a esta:
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Exemplos de implementação {#implementation-examples}

As subseções a seguir demonstram como implementar o registro no lado do cliente do Analytics para casos de uso comuns.

### Atividades do Experience Composer baseadas em formulário {#form-based-composer}

Você pode usar o SDK da Web para controlar a execução de apresentações de [atividades do Adobe Target Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

Quando você solicita apresentações para um escopo de decisão específico, a proposta retornada contém o token apropriado do Analytics. A prática recomendada é encadear o comando `sendEvent` do SDK da Web da Platform e iterar através das propostas retornadas para executá-las enquanto coleta os tokens do Analytics ao mesmo tempo.

Você pode acionar um comando `sendEvent` para um escopo de atividade do Experience Composer baseado em formulário, desta forma:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Aqui, você deve implementar o código para executar as apresentações e construir uma carga que será enviada para o Analytics. Este é um exemplo do que `results.propositions` pode conter:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Para extrair o token do Analytics de uma proposta com itens de conteúdo, é possível implementar uma função semelhante à seguinte:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Uma proposta pode ter diferentes tipos de itens, conforme indicado pela propriedade `schema` do item em questão. Há quatro esquemas de item de proposta compatíveis com as atividades do Experience Composer baseado em formulário:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` e `JSON_SCHEMA` são os esquemas que refletem o tipo da oferta, enquanto `MEASUREMENT_SCHEMA` reflete as métricas que devem ser anexadas a um elemento DOM.

As cargas do Analytics para métricas de cliques devem ser coletadas e enviadas para o Analytics separadamente dos itens de conteúdo, no momento em que o visitante realmente clicar no conteúdo exibido anteriormente.

A seguinte função auxiliar para obter a métrica de cliques A4T payloads será útil neste caso:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Resumo da implementação {#implementation-summary}

Em resumo, as seguintes etapas devem ser executadas ao aplicar atividades do Experience Composer com base em formulário com o SDK da Web da plataforma:

1. Enviar um evento que busque ofertas de atividades do Experience Composer baseadas em formulário;
1. Aplicar as alterações de conteúdo à página;
1. Enviar o evento de notificação `decisioning.propositionDisplay`;
1. Colete os tokens de exibição do Analytics da resposta do SDK e construa uma carga para a ocorrência do Analytics;
1. Enviar a carga para o Analytics usando a [API de inserção de dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Se houver qualquer métrica de clique nas apresentações entregues, os ouvintes de cliques deverão ser configurados de forma que, quando um clique for executado, ele envie o evento de notificação `decisioning.propositionInteract`. O manipulador `onBeforeEventSend` deve ser configurado de modo que, ao interceptar eventos `decisioning.propositionInteract`, as seguintes ações ocorram:
   1. Coletando os tokens de clique do Analytics de `xdm._experience.decisioning.propositions`
   1. Enviando a ocorrência de clique do Analytics com a carga coletada do Analytics por meio da [API de inserção de dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Atividades do Visual Experience Composer {#visual-experience-composer-acitivties}

O SDK da Web permite manipular ofertas criadas com o [Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>As etapas para implementar este caso de uso são muito semelhantes às etapas para [atividades do Experience Composer baseadas em formulário](#form-based-composer). Consulte a seção anterior para obter mais detalhes.

Quando a renderização automática está habilitada, é possível coletar os tokens do Analytics nas apresentações que foram executadas na página. A prática recomendada é encadear o comando `sendEvent` do SDK da Web da Platform e iterar através das propostas retornadas para filtrar aquelas que o SDK da Web tentou renderizar.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Usando `onBeforeEventSend` para manipular métricas de página {#using-onbeforeeventsend}

Usando as atividades do Adobe Target, você pode configurar diferentes métricas na página, anexadas manualmente ao DOM ou anexadas automaticamente ao DOM (atividades criadas no VEC). Ambos os tipos são uma interação atrasada do usuário final na página da Web.

Para levar em conta isso, a prática recomendada é coletar cargas do Analytics usando o gancho do SDK da Web do Adobe Experience Platform `onBeforeEventSend`. O gancho `onBeforeEventSend` deve ser configurado usando o comando `configure` e será refletido em todos os eventos enviados pela sequência de dados.

Este é um exemplo de como `onBeforeEventSent` pode ser configurado para acionar ocorrências do Analytics:

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Próximas etapas {#next-steps}

Este guia abordou o registro no lado do cliente para dados do A4T no SDK da Web. Consulte o manual sobre [registro no lado do servidor](server-side.md) para obter mais informações sobre como lidar com dados do A4T no Edge Network.
