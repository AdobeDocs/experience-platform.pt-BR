---
title: Módulos compartilhados em extensões da Web
description: Saiba como definir módulos de biblioteca compartilhados para extensões da Web na Adobe Experience Platform.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 81%

---

# Módulos compartilhados em extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um módulo compartilhado é um mecanismo pelo qual você pode se comunicar com outras extensões. Por exemplo, a Extensão A pode carregar dados de forma assíncrona e disponibilizá-los para a Extensão B por meio de uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Em implementações do JavaScript, todos os módulos compartilhados são instanciados usando o método [`getSharedModule`](../turbine.md#shared) fornecido pela variável grátis `turbine`.

Os módulos compartilhados são incluídos nas bibliotecas de tags mesmo quando nunca são chamados de dentro de outras extensões. Para não aumentar desnecessariamente o tamanho da biblioteca, tenha cuidado com o que você expõe como um módulo compartilhado.

Os módulos compartilhados não têm um componente de visualização.

Ao desenvolver sua própria extensão de tag, é possível definir os módulos compartilhados que você deseja que ela forneça. Por exemplo, você pode criar um módulo que carregue uma ID de usuário de maneira assíncrona e, em seguida, compartilhe a ID de usuário com qualquer outra extensão por meio de uma promessa:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

No [manifesto de extensão](../manifest.md), é necessário fornecer um nome para esse módulo compartilhado. Se você a nomear como `user-id-promise`, uma extensão diferente poderá acessar esse módulo compartilhado da seguinte maneira:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Os módulos compartilhados podem ser qualquer item que você normalmente poderia exportar de um módulo CommonJS (como funções, objetos, strings, números ou boolianos).
