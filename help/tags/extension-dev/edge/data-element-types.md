---
title: Tipos de elementos de dados para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo elemento de dados para uma extensão de tag em uma propriedade de borda.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 59%

---

# Tipos de elementos de dados em extensões de borda

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo de biblioteca do tipo elemento de dados recupera dados. O autor do módulo determina como esse pedaço de dados é recuperado. Por exemplo, você pode usar um tipo de elemento de dados para permitir que os usuários do Adobe Experience Platform recuperem dados da camada XDM ou de sua camada de dados personalizada.

>[!IMPORTANT]
>
>Este documento abrange tipos de elementos de dados para extensões de borda. Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [tipos de elementos de dados para extensões da Web](../web/data-element-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de tags. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Caso deseje permitir que os usuários recuperem uma parte dos dados da camada de dados personalizada, o módulo poderá se parecer com este exemplo.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Se você quiser tornar os dados retornados para a camada de dados configuráveis pelo usuário do Adobe Experience Platform, poderá permitir que o usuário insira um nome de chave e, em seguida, salve o nome no objeto `settings`. O objeto pode ser semelhante a.

```js
{
  keyName: "campaignId"
}
```

Para operar no nome do item de armazenamento local definido pelo usuário, seu módulo precisará mudar para:

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Contexto do módulo da biblioteca

Todos os módulos de elementos de dados têm acesso a uma variável `context` que é fornecida quando o módulo é chamado. Você pode saber mais [aqui](./context.md).
