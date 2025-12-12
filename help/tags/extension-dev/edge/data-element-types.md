---
title: Tipos de elementos de dados para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo elemento de dados para uma extensão de tag em uma propriedade de ponta.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 50%

---

# Tipos de elementos de dados em extensões de borda

Nas tags, os elementos de dados são aliases de dados em uma página da Web ou móvel, independentemente de onde esses dados se encontrem no evento recebido pelo servidor. Um elemento de dados pode ser referenciado por regras e atua como uma abstração para acessar esses dados. Quando a localização dos dados for alterada no futuro (como a alteração da chave de evento que contém o valor), um único elemento de dados poderá ser reconfigurado, enquanto todas as regras que referenciam esse elemento de dados poderão permanecer inalteradas.

Os tipos de elementos de dados são fornecidos por extensões e o autor da extensão determina como esses dados são recuperados. Por exemplo, você pode usar um tipo de elemento de dados para permitir que os usuários do Adobe Experience Platform recuperem dados da camada XDM ou de sua camada de dados personalizada.

Este documento aborda como definir tipos de elementos de dados para uma extensão de borda no Adobe Experience Platform.

>[!IMPORTANT]
>
>Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [tipos de elementos de dados para extensões da Web](../web/data-element-types.md).
>
>Este documento pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de borda. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de elementos de dados normalmente consistem no seguinte:

1. Uma visualização mostrada na interface do usuário do Experience Platform e na interface da Coleção de dados que permite aos usuários modificar as configurações do elemento de dados.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tag para interpretar as configurações e recuperar dados.

Caso deseje permitir que os usuários recuperem dados da camada de dados personalizada, o módulo poderá ter a aparência deste exemplo.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Se quiser fazer com que os dados retornados da camada de dados se tornem configuráveis para o usuário da Adobe Experience Platform, você poderá permitir que o usuário insira um nome-chave e depois salve-o no objeto `settings`. O objeto pode ser semelhante a.

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
