---
title: Tipos de elementos de dados para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo elemento de dados para uma extensão de tag em uma propriedade da Web.
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 67%

---

# Tipos de elementos de dados para extensões da Web

Nas tags de coleção de dados, os elementos de dados são essencialmente aliases de dados em uma página. Esses dados podem ser encontrados em parâmetros de cadeia de caracteres de consulta, cookies, elementos DOM ou outros locais. Um elemento de dados pode ser referenciado por regras e atua como uma abstração para acessar esses dados.

Os tipos de elementos de dados são fornecidos por extensões e permitem que os usuários configurem elementos de dados para acessar dados de uma maneira específica. Por exemplo, uma extensão pode fornecer um tipo de elemento de dados &quot;item de armazenamento local&quot; no qual o usuário do pode especificar um nome de item de armazenamento local. Quando o elemento de dados é referenciado por uma regra, a extensão pode procurar o valor do item do armazenamento local usando o nome do item do armazenamento local fornecido pelo usuário ao configurar o elemento de dados.

Este documento aborda como definir tipos de elementos de dados para uma extensão da Web no Adobe Experience Platform.

>[!IMPORTANT]
>
>Se você estiver desenvolvendo uma extensão de borda, consulte o manual em [tipos de elementos de dados para extensões de borda](../edge/data-element-types.md).
>
>Este documento pressupõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões da Web. Se você precisar de uma introdução, consulte a visão geral sobre [formatação do módulo de biblioteca](./format.md) antes de retornar a este guia.

Os tipos de elementos de dados normalmente consistem no seguinte:

1. Uma [visualização](./views.md) mostrada na interface do usuário do Experience Platform e na interface da Coleção de dados que permite aos usuários modificar as configurações do elemento de dados.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tag para interpretar as configurações e recuperar dados.

Considere uma situação em que você deseja permitir que os usuários recuperem dados de um item de armazenamento local chamado `productName`. Seu módulo pode ser semelhante a:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Se você quiser que o nome do item de armazenamento local seja configurável pelo usuário do Adobe Experience Platform, poderá permitir que o usuário insira um nome e depois o salve no objeto `settings`. O objeto pode ser semelhante a:

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
