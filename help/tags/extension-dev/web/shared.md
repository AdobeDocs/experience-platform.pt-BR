---
title: Módulos compartilhados em extensões da Web
description: Saiba como definir módulos de biblioteca compartilhada para extensões da Web no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 78%

---

# Módulos compartilhados em extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo compartilhado é um mecanismo pelo qual você pode se comunicar com outras extensões. Em implementações do JavaScript, todos os módulos compartilhados são instanciados usando o método [`getSharedModule`](../turbine.md#shared) fornecido pela variável grátis `turbine`.

Ao desenvolver sua própria extensão de tag, você pode definir todos os módulos compartilhados que deseja que ela forneça. Por exemplo, você pode criar um módulo que carregue uma ID de usuário de maneira assíncrona e, em seguida, compartilhe a ID de usuário com qualquer outra extensão por meio de uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise):

```javascript
var userIdPromise = new Promise(/* load user id, then resolve promise */);
module.exports = userIdPromise;
```

No [manifesto da extensão](../manifest.md) é necessário fornecer um nome para esse módulo compartilhado. Se você a nomear como `user-id-promise`, uma extensão diferente poderá acessar esse módulo compartilhado da seguinte maneira:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Os módulos compartilhados podem ser qualquer item que você normalmente poderia exportar de um módulo CommonJS (como funções, objetos, strings, números ou boolianos).
