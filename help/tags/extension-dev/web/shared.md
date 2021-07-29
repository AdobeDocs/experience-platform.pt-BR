---
title: Módulos compartilhados em extensões da Web
description: Saiba como definir módulos de biblioteca compartilhada para extensões da Web no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 65%

---

# Módulos compartilhados em extensões da Web

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo compartilhado é um mecanismo pelo qual você pode se comunicar com outras extensões. Por exemplo, a Extensão A pode carregar dados de forma assíncrona e disponibilizá-los para a Extensão B por meio de uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Em implementações do JavaScript, todos os módulos compartilhados são instanciados usando o método [`getSharedModule`](../turbine.md#shared) fornecido pela variável grátis `turbine`.

Os módulos compartilhados são incluídos nas bibliotecas de tags mesmo quando nunca são chamados de dentro de outras extensões. Para não aumentar desnecessariamente o tamanho da biblioteca, tenha cuidado com o que você expõe como um módulo compartilhado.

Os módulos compartilhados não têm um componente de visualização.

Ao desenvolver sua própria extensão de tag, você pode definir todos os módulos compartilhados que deseja que ela forneça. Por exemplo, você pode criar um módulo que carregue uma ID de usuário de maneira assíncrona e, em seguida, compartilhe a ID de usuário com qualquer outra extensão por meio de uma promessa:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

No manifesto [da extensão](../manifest.md), é necessário fornecer um nome para este módulo compartilhado. Se você a nomear como `user-id-promise`, uma extensão diferente poderá acessar esse módulo compartilhado da seguinte maneira:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Os módulos compartilhados podem ser qualquer item que você normalmente poderia exportar de um módulo CommonJS (como funções, objetos, strings, números ou boolianos).
