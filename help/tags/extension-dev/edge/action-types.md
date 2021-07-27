---
title: Tipos de ação para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo ação para uma extensão de tag em uma propriedade de borda.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 45%

---

# Tipos de ação para extensões de borda

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Em uma regra de tag, uma ação é algo que é executado depois que as condições da regra tenham passado na avaliação. Os tipos de ação são fornecidos por extensões e seus efeitos são totalmente definidos pelo autor da extensão.

Por exemplo, uma extensão pode fornecer um tipo de ação &quot;mostrar o bate-papo de suporte&quot;, que pode exibir uma caixa de diálogo de bate-papo de suporte para ajudar usuários que estejam com dificuldades ao fazer check-out.

Este documento aborda como definir tipos de ação para uma extensão de borda no Adobe Experience Platform.

>[!IMPORTANT]
>
>Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [tipos de ação para extensões da Web](../web/action-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões do Edge. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de ação normalmente consistem no seguinte:

1. Uma exibição mostrada na interface do usuário da Coleta de dados que permite que os usuários modifiquem as configurações da ação.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tags para interpretar as configurações e executar uma ação.

Por exemplo, um módulo para encaminhar alguns dados para um ponto de extremidade de terceiros pode ter esta aparência.

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

Se você quiser tornar o ponto de extremidade configurável pelo usuário e permitir a entrada e a persistência de um ponto de extremidade para o objeto de configurações no módulo, o objeto será semelhante a isso.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Para operar no terminal definido pelo usuário, seu módulo precisaria alterar para o seguinte exemplo.

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
