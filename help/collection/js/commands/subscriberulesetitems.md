---
title: subscribeRulesetItems
description: Assine cartões de conteúdo para uma superfície específica usando o comando subscribeRulesetItems.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# `subscribeRulesetItems`

O comando `subscribeRulesetItems` permite assinar apresentações que são o resultado de conjuntos de regras satisfeitos. Você pode fazer isso especificando as superfícies e os esquemas pelos quais filtrar e fornecendo uma função de retorno de chamada.

Sempre que os conjuntos de regras forem avaliados, a função de retorno de chamada receberá um objeto `result` com uma matriz de propostas.

>[!IMPORTANT]
>
>O comando `subscribeRulesetItems` é a única maneira de obter propostas provenientes de conjuntos de regras, já que elas não são retornadas com [`sendEvent`](sendevent/overview.md) resultados.


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

O código acima se inscreve na superfície `web://example.com/#welcome` para cartões de conteúdo e usa o método de conveniência `collectEvent` para emitir eventos `display` para todas as apresentações.

## Opções de comando {#command-options}

Este comando usa um objeto `options` com as seguintes propriedades:

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| `surfaces` | Matriz de string | Uma lista de superfícies. Proposições só serão recebidas pela função de retorno de chamada se corresponderem a uma das superfícies fornecidas aqui. |
| `schemas` | Matriz de string | Uma lista de esquemas. As propostas só serão recebidas pela função de retorno de chamada se corresponderem a um dos esquemas fornecidos aqui. |
| `callback` | Função | Uma função de retorno de chamada que será invocada quando as apresentações forem o resultado de conjuntos de regras satisfeitos. A função de retorno de chamada recebe dois parâmetros quando invocada: `result` e `collectEvent`. Consulte [parâmetros de retorno de chamada](#callback-parameters) para obter detalhes. |

### Parâmetros de retorno de chamada {#callback-parameters}

A função de retorno de chamada recebe os dois parâmetros descritos na tabela abaixo quando chamada.

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| `result` | Objeto | Este objeto contém uma matriz `propositions`.  Essas propostas são o resultado direto de conjuntos de regras satisfeitos. O objeto `result` está estruturado da mesma forma que o [objeto de resultado](command-responses.md) retornado por `sendEvent` usando uma cláusula `then`. |
| `collectEvent` | Função | Uma função de conveniência que você pode usar para enviar eventos do Edge Network para rastrear interações, exibições e outros eventos. |

### Função `collectEvent` {#collectevent-function}

A função `collectEvent` é uma função de conveniência que você pode usar para enviar eventos Edge Network para rastrear interações, exibições e outros eventos. Aceita os dois parâmetros descritos na tabela abaixo.

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| Tipo de evento | String | Uma string que indica qual tipo de evento de apresentação emitir. Os tipos de evento com suporte são `display`, `interact` ou `dismiss`. |
| `propositions` | Matriz | Uma matriz de propostas correspondentes ao evento. |

## Assinar cartões de conteúdo usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente às respostas de comando é uma regra que assina o evento [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). O evento permite fornecer os esquemas e superfícies desejados.
