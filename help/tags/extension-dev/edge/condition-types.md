---
title: Tipos de condição para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo condição para uma extensão de borda no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 63%

---

# Tipos de condição para extensões de borda

>[!NOTE]
>
> O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo de biblioteca do tipo condição avalia se algo é verdadeiro ou falso e retorna um valor booleano.

>[!IMPORTANT]
>
>Este documento abrange tipos de condição para extensões de borda. Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [tipos de condição para extensões da Web](../web/condition-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de tags. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Por exemplo, se você quiser avaliar se o usuário está no host `example.com`, seu módulo pode ter esta aparência.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Se você quiser que o nome de host seja configurável pelo usuário para permitir a entrada de um nome de host e salvá-lo no objeto de configurações, o objeto pode ser semelhante a este exemplo.

```js
{
  "hostname": "example.com"
}
```

Para operar no nome do host definido pelo usuário, seu módulo precisará ser alterado para:

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Resultado da condição

O resultado retornado por um módulo de condição pode ser um dos seguintes:

1. Um valor booliano (`true` ou `false`).
1. Uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) que retorna um valor booliano depois de resolvida.

## Contexto do módulo da biblioteca

Todos os módulos de condição têm acesso a uma variável `context` que é fornecida quando o módulo é chamado. Você pode saber mais [aqui](./context.md).
