---
title: Tipos de ação para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo ação para uma extensão de tag em uma propriedade da Web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 65%

---

# Tipos de ação para extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo de biblioteca do tipo ação tem como objetivo executar uma ação predefinida. O que essa ação faz é inteiramente de sua escolha. Deseja enviar um beacon, mostrar uma oferta, agradecer ao usuário por visitar, salvar um cookie ou abrir um bate-papo de suporte?

>[!IMPORTANT]
>
>Esse documento abrange tipos de ação para extensões da Web. Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [tipos de ação para extensões de borda](../edge/action-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de tags. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Por exemplo, para tornar a mensagem configurável pelo usuário do Adobe Experience Platform, é possível permitir que o usuário insira e salve uma mensagem no objeto de configurações. O objeto com esta aparência:

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Para operar na mensagem definida pelo usuário, seu módulo precisará ser alterado para:

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Dados do evento contextuais

Um segundo argumento teria que ser passado para o módulo que contém as informações contextuais sobre o evento que aciona a regra. Pode ser benéfico em certos casos e pode ser acessado da seguinte forma:

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
