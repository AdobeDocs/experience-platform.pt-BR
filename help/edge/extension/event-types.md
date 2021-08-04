---
title: Tipos de evento na extensão SDK da Web da Adobe Experience Platform
description: Saiba mais sobre como usar tipos de evento fornecidos pela extensão Adobe Experience Platform Web SDK no Adobe Experience Platform Launch.
solution: Experience Platform
feature: Web SDK
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 1%

---

# Tipos de evento

Esta página descreve os tipos de evento do Adobe Experience Platform fornecidos pela extensão de tag Adobe Experience Platform Web SDK. Eles são usados para [criar regras](https://experienceleague.adobe.com/docs/launch-learn/tutorials/fundamentals/building-rules-in-launch.html) e não devem ser confundidos com o campo [`eventType` no XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=pt-BR).

## [!UICONTROL Enviar evento concluído]

Normalmente, sua propriedade teria uma ou mais regras usando a ação [[!UICONTROL Enviar evento]](action-types.md#send-event) para enviar eventos para a Adobe Experience Platform Edge Network. Cada vez que um evento é enviado para a Edge Network, uma resposta é retornada ao navegador com dados úteis. Sem o tipo de evento [!UICONTROL Send event complete] , você não teria acesso a esses dados retornados.

Para acessar os dados retornados, crie uma regra separada e adicione um evento [!UICONTROL Send event complete] à regra. Essa regra é acionada sempre que uma resposta bem-sucedida é recebida do servidor como resultado de uma ação [!UICONTROL Send event] .

Quando um evento [!UICONTROL Send event complete] aciona uma regra, ele fornece dados retornados do servidor que podem ser úteis para realizar determinadas tarefas. Normalmente, você adicionará uma ação [!UICONTROL Custom code] (da extensão [!UICONTROL Core]) à mesma regra que contém o evento [!UICONTROL Send event complete]. Na ação [!UICONTROL Custom code], seu código personalizado terá acesso a uma variável chamada `event`. Essa variável `event` conterá os dados retornados do servidor.

Sua regra para lidar com dados retornados da Edge Network pode ser semelhante a:

![](./assets/send-event-complete.png)

Abaixo estão alguns exemplos de como executar determinadas tarefas usando a ação [!UICONTROL Custom code] nesta regra.

### Renderizar manualmente o conteúdo personalizado

Na ação Código personalizado , que está na regra para manipular dados de resposta, você pode acessar propostas de personalização que foram retornadas do servidor. Para fazer isso, digite o seguinte código personalizado:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` existir, será uma matriz contendo objetos de apresentação de personalização. As apresentações incluídas na matriz são determinadas, em grande parte, pela forma como o evento foi enviado para o servidor.

Para esse primeiro cenário, suponha que você não tenha marcado a caixa de seleção [!UICONTROL Renderizar decisões] e não tenha fornecido [!UICONTROL escopos de decisão] dentro da ação [!UICONTROL Enviar evento] responsável pelo envio do evento.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

Neste exemplo, a matriz `propositions` contém apenas apresentações relacionadas ao evento que são elegíveis para renderização automática.

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

Ao enviar o evento, a caixa de seleção [!UICONTROL Renderizar decisões] não estava marcada, portanto, o SDK não tentou renderizar automaticamente qualquer conteúdo. No entanto, o SDK ainda recuperou automaticamente o conteúdo elegível para renderização automática e o forneceu para renderizar manualmente se desejar. Observe que cada objeto de proposta tem sua propriedade `renderAttempted` definida como `false`.

Se, em vez disso, você tivesse marcado a caixa de seleção [!UICONTROL Renderizar decisões] ao enviar o evento, o SDK teria tentado renderizar quaisquer propostas qualificadas para renderização automática. Como consequência, cada um dos objetos de proposta teria sua propriedade `renderAttempted` definida como `true`. Nesse caso, não haveria necessidade de renderizar manualmente essas apresentações.

Até agora, você só examinou o conteúdo de personalização qualificado para renderização automática (por exemplo, qualquer conteúdo criado no Adobe Target Visual Experience Composer). Para recuperar qualquer conteúdo de personalização _not_ elegível para renderização automática, solicite o conteúdo fornecendo escopos de decisão usando o campo [!UICONTROL Decidem escopos] na ação [!UICONTROL Enviar evento]. Um escopo é uma string que identifica uma proposta específica que você deseja recuperar do servidor.

A ação [!UICONTROL Send event] seria a seguinte:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

Neste exemplo, se as apresentações forem encontradas no servidor que corresponde ao escopo `salutation` ou `discount`, elas serão retornadas e incluídas na matriz `propositions`. Esteja ciente de que as apresentações qualificadas para renderização automática continuarão a ser incluídas na matriz `propositions`, independentemente de como você configura os campos [!UICONTROL Renderizar decisões] ou [!UICONTROL Escopos de decisão] na ação [!UICONTROL Enviar evento]. A matriz `propositions`, nesse caso, seria semelhante a este exemplo:

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

Nesse ponto, é possível renderizar o conteúdo da proposta da maneira que quiser. Neste exemplo, a proposta que corresponde ao escopo `discount` é uma proposta HTML criada usando o Experience Composer baseado em formulário do Adobe Target. Suponha que você tenha um elemento em sua página com a ID de `daily-special` e deseje renderizar o conteúdo da proposta `discount` no elemento `daily-special`. Faça o seguinte:

1. Extraia apresentações do objeto `event`.
1. Faça o loop por cada proposta, procurando a proposta com um escopo de `discount`.
1. Se você encontrar uma proposta, faça um loop por cada item na proposta, procurando pelo item que é conteúdo HTML. (É melhor verificar do que assumir.)
1. Se você encontrar um item contendo conteúdo HTML, encontre o elemento `daily-special` na página e substitua seu HTML pelo conteúdo personalizado.

Seu código personalizado dentro da ação [!UICONTROL Custom code] pode aparecer da seguinte maneira:

```javascript
var propositions = event.propositions;

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
```

### Acessar tokens de resposta do Adobe Target

O conteúdo de personalização retornado do Adobe Target inclui [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que são detalhes sobre a atividade, oferta, experiência, perfil do usuário, informações geográficas e muito mais. Esses detalhes podem ser compartilhados com ferramentas de terceiros ou usados para depuração. Os tokens de resposta podem ser configurados na interface do usuário do Adobe Target.

Na ação Código personalizado , que está na regra para manipular dados de resposta, você pode acessar propostas de personalização que foram retornadas do servidor. Para fazer isso, digite o seguinte código personalizado:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` existir, será uma matriz contendo objetos de apresentação de personalização. Consulte [Renderizar manualmente o conteúdo personalizado](#manually-render-personalized-content) para obter mais informações sobre o conteúdo de `result.propositions`.

Suponha que você gostaria de coletar todos os nomes de atividades de todas as apresentações que foram renderizadas automaticamente pelo SDK da Web e enviá-las para um único array. Em seguida, você poderia enviar o único array para terceiros. Nesse caso, grave o código personalizado dentro da ação [!UICONTROL Custom code] para:

1. Extraia apresentações do objeto `event`.
1. Faça o loop por cada proposta.
1. Determine se o SDK renderizou a proposta.
1. Em caso positivo, faça um loop por cada item na proposta.
1. Recupere o nome da atividade da propriedade `meta`, que é um objeto contendo tokens de resposta.
1. Encaminhe o nome da atividade para uma matriz.
1. Envie os nomes das atividades para terceiros.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```





