---
title: Tipos de ação para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo ação para uma extensão de tag em uma propriedade da Web.
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 70%

---

# Tipos de ação para extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

No contexto de tags de coleção de dados, uma ação é algo que é executado depois que um evento de regra ocorre e todas as condições são aprovadas na avaliação.

Por exemplo, uma extensão pode fornecer um tipo de ação &quot;mostrar o bate-papo de suporte&quot;, que pode exibir uma caixa de diálogo de bate-papo de suporte para ajudar usuários que estejam com dificuldades ao fazer check-out.

Este documento aborda como definir tipos de ação para uma extensão da Web no Adobe Experience Platform.

>[!IMPORTANT]
>
>Esse documento abrange tipos de ação para extensões da Web. Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [tipos de ação para extensões de borda](../edge/action-types.md).
>
>Este documento pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões da Web. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de ação geralmente consistem no seguinte:

1. Uma [visualização](./views.md) mostrada na interface do usuário do Experience Platform e na interface da Coleção de dados que permite aos usuários modificar as configurações da ação.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tag para interpretar as configurações e executar uma ação.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Por exemplo, para tornar a mensagem configurável pelo usuário da Adobe Experience Platform, é possível permitir que o usuário insira e salve uma mensagem no objeto de configurações. O objeto tem esta aparência:

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
