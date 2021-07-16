---
title: Tipos de elementos de dados para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo elemento de dados para uma extensão de tag em uma propriedade da Web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 70%

---

# Tipos de elementos de dados para extensões de borda

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A finalidade de um módulo de biblioteca do tipo elemento de dados é recuperar um pedaço de dados. O método para esta recuperação é personalizável. Tipos de elemento de dados diferentes permitem que os usuários do Adobe Experience Platform recuperem dados do armazenamento local, de um cookie ou de um elemento DOM.

>[!IMPORTANT]
>
>Este documento fornece informações sobre tipos de elementos de dados para extensões da Web. Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [tipos de elementos de dados para extensões de borda](../edge/data-element-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de tags. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Considere uma situação em que você deseja permitir que os usuários recuperem dados de um item de armazenamento local chamado `productName`. Seu módulo pode ser semelhante a:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Se você quiser tornar o nome do item de armazenamento local configurável pelo usuário do Adobe Experience Platform, poderá permitir que o usuário insira um nome e depois salve o nome no objeto `settings`. O objeto pode ser semelhante a:

```js
{
  itemName: "campaignId"
}
```

Para operar no nome do item de armazenamento local definido pelo usuário, seu módulo precisará mudar para:

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Suporte a valores padrão

Esteja ciente de que os usuários têm a opção de configurar um valor padrão para qualquer elemento de dados. Se o módulo da biblioteca de elementos de dados retornar um valor de `undefined` ou `null`, ele será automaticamente substituído pelo valor padrão que o usuário configurou para o elemento de dados.

## Dados do evento contextuais

Se o elemento de dados estiver sendo recuperado como resultado do acionamento de uma regra (por exemplo, elementos de dados são usados nas condições e ações da regra), um segundo argumento será transmitido ao módulo com informações contextuais sobre o evento que acionou a regra. Pode ser benéfico em certos casos e pode ser acessado da seguinte forma:

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

O objeto `event` deve conter as seguintes propriedades:

| Propriedade | Descrição |
| --- | --- |
| `$type` | Uma string que descreve o nome da extensão e o nome do evento, unida usando um ponto. Por exemplo, `youtube.play`. |
| `$rule` | Um objeto que contém informações sobre a regra em execução no momento. O objeto deve conter as seguintes subpropriedades:<ul><li>`id`: a ID da regra em execução no momento.</li><li>`name`: o nome da regra em execução no momento.</li></ul> |

Como alternativa, a extensão que fornece o tipo de evento que acionou a regra pode adicionar outras informações úteis a esse objeto `event`.
