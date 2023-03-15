---
title: Tipos de evento na extensão SDK da Web do Adobe Experience Platform
description: Saiba mais sobre como usar os tipos de evento fornecidos pela extensão Adobe Experience Platform Web SDK no Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Tipos de evento

Esta página descreve os tipos de evento do Adobe Experience Platform fornecidos pela extensão de tag do SDK da Web da Adobe Experience Platform. Eles são usados para [regras de build](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) e não devem ser confundidas com o [`eventType` campo no XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=pt-BR).

## [!UICONTROL Enviar evento concluído]

Normalmente, sua propriedade teria uma ou mais regras usando o [[!UICONTROL Enviar evento] ação](action-types.md#send-event) para enviar eventos ao Adobe Experience Platform Edge Network. Cada vez que um evento é enviado ao Edge Network, uma resposta é retornada ao navegador com dados úteis. Sem o [!UICONTROL Enviar evento concluído] tipo de evento, você não teria acesso a esses dados retornados.

Para acessar os dados retornados, crie uma regra separada e adicione um [!UICONTROL Enviar evento concluído] para a regra. Essa regra é acionada sempre que uma resposta bem-sucedida é recebida do servidor como resultado de um [!UICONTROL Enviar evento] ação.

Quando um [!UICONTROL Enviar evento concluído] evento aciona uma regra, ele fornece dados retornados do servidor que podem ser úteis para realizar determinadas tarefas. Normalmente, você adicionará um [!UICONTROL Código personalizado] ação (a partir do [!UICONTROL Núcleo] extensão) para a mesma regra que contém a variável [!UICONTROL Enviar evento concluído] evento. No [!UICONTROL Código personalizado] ação, seu código personalizado terá acesso a uma variável chamada `event`. Este `event` conterá os dados retornados do servidor.

Sua regra para tratar dados retornados da Rede de borda pode ser semelhante a:

![](./assets/send-event-complete.png)

Abaixo estão alguns exemplos de como executar determinadas tarefas usando o [!UICONTROL Código personalizado] ação nesta regra.

### Renderizar manualmente o conteúdo personalizado

Na ação Código personalizado, que está na regra para manipular dados de resposta, você pode acessar propostas de personalização que foram retornadas do servidor. Para fazer isso, você digitaria o seguinte código personalizado:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` existe, é uma matriz que contém objetos de apresentação de personalização. As propostas incluídas no array são determinadas, em grande parte, pela forma como o evento foi enviado ao servidor.

Para este primeiro cenário, suponha que você não tenha verificado a [!UICONTROL Renderizar decisões] e não forneceram nenhuma [!UICONTROL escopos de decisão] dentro do [!UICONTROL Enviar evento] ação responsável por enviar o evento.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

Neste exemplo, a variável `propositions` matriz contém apenas apresentações relacionadas ao evento que são elegíveis para renderização automática.

A variável `propositions` A matriz pode ser semelhante a este exemplo:

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

Ao enviar o evento, a variável [!UICONTROL Renderizar decisões] A caixa de seleção não estava marcada, portanto, o SDK não tentou renderizar automaticamente qualquer conteúdo. No entanto, o SDK ainda recuperou automaticamente o conteúdo qualificado para renderização automática e o forneceu para renderização manual, se você desejar. Observe que cada objeto de proposta tem seu `renderAttempted` propriedade definida como `false`.

Se, em vez disso, você tivesse [!UICONTROL Renderizar decisões] ao enviar o evento, o SDK tentaria renderizar qualquer proposta qualificada para renderização automática. Como consequência, cada um dos objetos de proposta teria seu `renderAttempted` propriedade definida como `true`. Não haveria necessidade de renderizar manualmente essas apresentações nesse caso.

Até agora, você só acessou um conteúdo de personalização qualificado para renderização automática (por exemplo, qualquer conteúdo criado no Visual Experience Composer do Adobe Target). Para recuperar qualquer conteúdo de personalização _não_ qualificados para renderização automática, solicite o conteúdo fornecendo escopos de decisão usando o [!UICONTROL Escopos de decisão] no campo [!UICONTROL Enviar evento] ação. Um escopo é uma cadeia de caracteres que identifica uma proposta específica que você deseja recuperar do servidor.

A variável [!UICONTROL Enviar evento] ação seria semelhante a:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

Neste exemplo, se as apresentações forem encontradas no servidor que corresponde à variável `salutation` ou `discount` escopo, elas são retornadas e incluídas no `propositions` matriz. Esteja ciente de que as apresentações qualificadas para renderização automática continuarão a ser incluídas no `propositions` independentemente de como você configura o [!UICONTROL Renderizar decisões] ou [!UICONTROL Escopos de decisão] campos no [!UICONTROL Enviar evento] ação. A variável `propositions` nesse caso, a matriz seria semelhante a este exemplo:

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

Nesse ponto, é possível renderizar o conteúdo da proposta conforme você julgar necessário. Neste exemplo, a proposta que corresponde ao parâmetro `discount` o escopo é uma apresentação de HTML criada usando o Experience Composer baseado em formulário do Adobe Target. Suponha que você tenha um elemento na página com a ID de `daily-special` e desejarem renderizar o conteúdo do `discount` apresentação na `daily-special` elemento. Faça o seguinte:

1. Extrair apresentações do `event` objeto.
1. Execute um loop em cada proposta, procurando pela proposta com um escopo de `discount`.
1. Se encontrar uma proposta, percorra cada item na proposta, procurando o item que seja conteúdo de HTML. (É melhor verificar do que supor.)
1. Se encontrar um item com conteúdo HTML, localize o `daily-special` elemento na página e substitua seu HTML pelo conteúdo personalizado.

Seu código personalizado no [!UICONTROL Código personalizado] A ação do pode parecer como a seguir:

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

### Acesso aos tokens de resposta do Adobe Target

O conteúdo de personalização retornado do Adobe Target inclui [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que são detalhes sobre a atividade, oferta, experiência, perfil do usuário, informações geográficas e muito mais. Esses detalhes podem ser compartilhados com ferramentas de terceiros ou usados para depuração. Os tokens de resposta podem ser configurados na interface do usuário do Adobe Target.

Na ação Código personalizado, que está na regra para manipular dados de resposta, você pode acessar propostas de personalização que foram retornadas do servidor. Para fazer isso, digite o seguinte código personalizado:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` existe, é uma matriz que contém objetos de apresentação de personalização. Consulte [Renderizar manualmente o conteúdo personalizado](#manually-render-personalized-content) para obter mais informações sobre o conteúdo de `result.propositions`.

Suponha que você deseje coletar todos os nomes de atividades de todas as propostas que foram renderizadas automaticamente pelo SDK da Web e enviá-las para um único array. Em seguida, você pode enviar o array único para terceiros. Nesse caso, escreva um código personalizado dentro do [!UICONTROL Código personalizado] ação para:

1. Extrair apresentações do `event` objeto.
1. Execute um loop em cada proposta.
1. Determine se o SDK renderizou a proposta.
1. Nesse caso, percorra cada item na proposta.
1. Recupere o nome da atividade da `meta` que é um objeto que contém tokens de resposta.
1. Transfira o nome da atividade para um storage.
1. Envie os nomes da atividade para terceiros.

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
