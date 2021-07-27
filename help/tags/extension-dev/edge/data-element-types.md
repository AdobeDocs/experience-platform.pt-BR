---
title: Tipos de elementos de dados para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo elemento de dados para uma extensão de tag em uma propriedade de borda.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 35%

---

# Tipos de elemento de dados em extensões de borda

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Em tags, os elementos de dados são aliases de dados em uma página da Web ou móvel, independentemente de onde esses dados sejam encontrados no evento recebido pelo servidor. Um elemento de dados pode ser referenciado por regras e atua como uma abstração para acessar esses dados. Quando a localização dos dados for alterada no futuro (como alterar a chave de evento que contém o valor), um único elemento de dados poderá ser reconfigurado, enquanto todas as regras que fazem referência a esse elemento de dados poderão permanecer inalteradas.

Os tipos de elementos de dados são fornecidos por extensões, e o autor da extensão determina como esses dados são recuperados. Por exemplo, você pode usar um tipo de elemento de dados para permitir que os usuários do Adobe Experience Platform recuperem dados da camada XDM ou de sua camada de dados personalizada.

Este documento aborda como definir tipos de elementos de dados para uma extensão de borda no Adobe Experience Platform.

>[!IMPORTANT]
>
>Se estiver desenvolvendo uma extensão da Web, consulte o guia sobre [tipos de elementos de dados para extensões da Web](../web/data-element-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões do Edge. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de elementos de dados normalmente consistem no seguinte:

1. Uma exibição mostrada na interface do usuário da Coleta de dados que permite que os usuários modifiquem as configurações do elemento de dados.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tags para interpretar as configurações e recuperar partes de dados.

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
