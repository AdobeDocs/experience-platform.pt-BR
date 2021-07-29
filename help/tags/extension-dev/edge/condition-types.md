---
title: Tipos de condição para extensões de borda
description: Saiba como definir um módulo de biblioteca do tipo condição para uma extensão de borda no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 53%

---

# Tipos de condição para extensões de borda

>[!NOTE]
>
> A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Em uma regra de tag, uma condição é avaliada após a ocorrência de um evento. Todas as condições devem retornar verdadeiro para que a regra continue a ser processada. Os tipos de condição são fornecidos por extensões e avaliam se algo é verdadeiro ou falso, retornando um valor booleano.

Como exemplo, uma extensão pode fornecer um tipo de condição &quot;visor contém&quot;, na qual o usuário do poderia especificar um seletor de CSS. Quando a condição é avaliada no site do cliente, a extensão pode encontrar elementos que correspondam ao seletor de CSS e retornar se algum deles está contido no visor do usuário.

Este documento aborda como definir tipos de condição para uma extensão de borda no Adobe Experience Platform.

>[!IMPORTANT]
>
>Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [tipos de condição para extensões da Web](../web/condition-types.md).
>
>Este documento também pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões do Edge. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de condição normalmente consistem no seguinte:

1. Uma exibição mostrada na interface do usuário da Coleta de dados que permite que os usuários modifiquem as configurações da condição.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tags para interpretar as configurações e avaliar uma condição.

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
