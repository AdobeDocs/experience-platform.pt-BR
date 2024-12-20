---
title: Tipos de condição para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo condição para uma extensão de tag em uma propriedade da Web.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 69%

---

# Tipos de condição para extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

No contexto de uma regra, uma condição é avaliada após a ocorrência de um evento. Todas as condições devem retornar verdadeiro para que a regra continue a ser processada. A exceção é quando os usuários colocam as condições explicitamente em um bucket de &quot;exceção&quot;, nesse caso, todas as condições no bucket devem retornar falso para que a regra continue o processamento.

Como exemplo, uma extensão pode fornecer um tipo de condição &quot;visor contém&quot;, na qual o usuário do poderia especificar um seletor de CSS. Quando a condição é avaliada no site do cliente, a extensão pode encontrar elementos que correspondam ao seletor de CSS e retornar se algum deles está contido no visor do usuário.

Este documento aborda como definir tipos de condição para uma extensão da Web no Adobe Experience Platform.

>[!NOTE]
>
>Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [tipos de condição para extensões de borda](../edge/condition-types.md).
>
>Este documento supõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões da Web. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de condição geralmente consistem no seguinte:

1. Uma [visualização](./views.md) mostrada na interface do usuário do Experience Platform e na interface da Coleção de dados que permite aos usuários modificar as configurações para a condição.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tag para interpretar as configurações e avaliar uma condição.

Um módulo de biblioteca do tipo condição tem uma meta: avaliar se algo é verdadeiro ou falso. O que ele avalia depende de você.

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
