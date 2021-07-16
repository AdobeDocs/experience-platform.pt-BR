---
title: Tipos de condição para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo condição para uma extensão de tag em uma propriedade da Web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 86%

---

# Tipos de condição para extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo de biblioteca de tipo de condição tem uma meta: avaliar se algo é verdadeiro ou falso. O que ele avalia depende de você.

>[!NOTE]
>
>Esse documento abrange tipos de condição para extensões da Web. Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [tipos de condição para extensões de borda](../edge/condition-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões de tags. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Por exemplo, se você deseja avaliar se o usuário está no host `example.com`, seu módulo pode ser semelhante a:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Agora, considere uma situação em que você deseje tornar o nome do host configurável pelo usuário do Adobe Experience Platform Você pode permitir que o usuário insira um nome de host e, depois, salve-o no objeto de configurações. O objeto pode ser semelhante a:

```js
{
  "hostname": "example.com"
}
```

Para operar no nome do host definido pelo usuário, seu módulo precisará ser alterado para:

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Dados do evento contextuais

Um segundo argumento é transmitido ao seu módulo, que contém informações contextuais sobre o evento que acionou a regra. Pode ser benéfico em certos casos e pode ser acessado da seguinte forma:

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
