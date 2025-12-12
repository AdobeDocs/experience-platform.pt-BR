---
title: Tipos de ação para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo ação para uma extensão de tag em uma propriedade de borda.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 65%

---

# Tipos de ação para extensões de borda

Em uma regra de tag, uma ação é algo que é executado depois que as condições da regra passam na avaliação. Os tipos de ação são fornecidos por extensões e seus efeitos são totalmente definidos pelo autor da extensão.

Por exemplo, uma extensão pode fornecer um tipo de ação &quot;mostrar o bate-papo de suporte&quot;, que pode exibir uma caixa de diálogo de bate-papo de suporte para ajudar usuários que estejam com dificuldades ao fazer check-out.

Este documento aborda como definir tipos de ação para uma extensão de borda no Adobe Experience Platform.

>[!IMPORTANT]
>
>Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [tipos de ação para extensões da Web](../web/action-types.md).
>
>Este documento pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de borda. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de ação geralmente consistem no seguinte:

1. Uma visualização mostrada na interface do usuário do Experience Platform e na interface da Coleção de dados que permite que os usuários modifiquem as configurações da ação.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tag para interpretar as configurações e executar uma ação.

Por exemplo, um módulo para encaminhar alguns dados a um endpoint de terceiros pode ter esta aparência.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Se você quiser tornar o endpoint configurável pelo usuário e permitir a entrada e a persistência de um endpoint para o objeto de configurações no módulo, o objeto terá aparência semelhante a esta.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Para operar no endpoint definido pelo usuário, o módulo precisará ser alterado para o exemplo a seguir.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Resultado da ação

O resultado retornado por um módulo de ação pode ser qualquer item. Se a ação precisar executar uma tarefa assíncrona, você poderá retornar uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) que retornará o resultado desejado após sua resolução.

O resultado da ação é armazenado em uma chave `ruleStash` que é disponibilizada para todos os módulos por meio do parâmetro `context` (`context.arc.ruleStash`). Você pode saber mais sobre `ruleStash` [aqui](./context.md#rulestash).
