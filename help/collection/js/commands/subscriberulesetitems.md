---
title: subscribeRulesetItems
description: Assine cartões de conteúdo para uma superfície específica usando o comando subscribeRulesetItems.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: 3ecfc2258e63a34a739ab8b296437c357d1dd9d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%

---

# `subscribeRulesetItems`

O comando `subscribeRulesetItems` permite assinar apresentações que são o resultado de conjuntos de regras satisfeitos. Você pode fazer isso especificando as superfícies e os esquemas pelos quais filtrar e fornecendo uma função de retorno de chamada.

Os conjuntos de regras são avaliados sempre que um comando [`sendEvent`](sendevent/overview.md) é enviado. A função de retorno de chamada recebe um objeto `result` com uma matriz de propostas dentro dele.

>[!IMPORTANT]
>
>O comando `subscribeRulesetItems` é a única maneira de obter propostas provenientes de conjuntos de regras, já que elas não são retornadas com [`sendEvent`](sendevent/overview.md) resultados. Você deve configurar sua assinatura antes de chamar `sendEvent` para garantir que as apresentações sejam capturadas.


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
| `callback` | Função | Uma função de retorno de chamada que é invocada quando as apresentações são o resultado de conjuntos de regras satisfeitos. A função de retorno de chamada recebe dois parâmetros quando invocada: `result` e `collectEvent`. Consulte [parâmetros de retorno de chamada](#callback-parameters) para obter detalhes. |

>[!TIP]
>
>É possível assinar várias superfícies e esquemas em um único comando transmitindo valores adicionais para as matrizes `surfaces` e `schemas`.

### Parâmetros de retorno de chamada {#callback-parameters}

A função de retorno de chamada recebe os dois parâmetros descritos na tabela abaixo quando chamada.

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| `result` | Objeto | Este objeto contém uma matriz `propositions`.  Essas propostas são o resultado direto de conjuntos de regras satisfeitos. O objeto `result` está estruturado da mesma forma que o [objeto de resultado](command-responses.md) retornado por `sendEvent` usando uma cláusula `then`. |
| `collectEvent` | Função | Uma função de conveniência que você pode usar para enviar eventos do Edge Network para rastrear interações, exibições e outros eventos. |

### Função `collectEvent` {#collectevent-function}

A função `collectEvent` é uma função de conveniência que você pode usar para enviar eventos do Edge Network para rastrear interações, exibições e outros eventos. Aceita os dois parâmetros descritos na tabela abaixo.

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| Tipo de evento | String | Uma string que indica qual tipo de evento de apresentação emitir. Os tipos de evento com suporte são `display`, `interact` ou `dismiss`. |
| `propositions` | Matriz | Uma matriz de propostas correspondentes ao evento. |


A função `collectEvent` pode ser chamada independentemente fora do retorno de chamada. Chamar essa função é útil ao rastrear uma interação ou demissão em um ponto posterior, como em resposta a uma ação do usuário.

```js
collectEvent("interact", propositions);
```

## Assinar cartões de conteúdo usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente às respostas de comando é uma regra que assina o evento [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). O evento permite fornecer os esquemas e superfícies desejados.
