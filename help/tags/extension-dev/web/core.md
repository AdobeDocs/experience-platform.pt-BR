---
title: Módulos principais da biblioteca para extensões da Web
description: Saiba mais sobre os módulos de biblioteca principais que você pode usar nas extensões da Web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 92%

---

# Módulos principais da biblioteca para extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Esse documento fornece uma lista dos módulos principais da biblioteca que você pode usar em suas extensões da Web. Você pode acessar esses módulos usando `require('@adobe/{MODULE}')`, em que `{MODULE}` é o nome do módulo principal que deseja usar.

## [!DNL reactor-object-assign]

`reactor-object-assign` imita o método nativo [`Object.assign`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) copiando propriedades de objetos de origem para um objeto de destino.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

O objeto `reactor-cookie` é um utilitário para ler e gravar cookies. Consulte o [pacote npm js-cookie](https://www.npmjs.com/package/js-cookie) para obter mais informações.

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` representa o objeto [`Document`](https://developer.mozilla.org/pt-BR/docs/Web/API/Document). Isso pode ser benéfico ao testar o módulo, permitindo que os testes injetem um objeto fictício `document` usando utilitários como [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` é um utilitário para analisar e serializar [sequências de consulta](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

O utilitário tem os seguintes métodos:

* `queryString.parse({STRING})`: analisa uma sequência de consulta em um objeto. Caracteres `?`, `#` e `&` à esquerda na sequência de consulta são ignorados.
* `queryString.stringify({OBJECT})`: transforma um objeto em uma sequência de consulta.

### [!DNL reactor-load-script]

`reactor-load-script` é uma função que carrega um script quando recebe um URL. Uma tag de script será criada e colocada no nó `head` do documento. Uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) será retornada, podendo ser usada para determinar quando o carregamento do script for bem-sucedido ou falhar.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` é um construtor que imita a [API Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) nativa no ECMAScript 6. Se a API Promise nativa estiver disponível, ela será retornada.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` representa o objeto [`Window`](https://developer.mozilla.org/pt-BR/docs/Web/API/Window). Isso pode ser benéfico ao testar o módulo, permitindo que os testes injetem um objeto fictício `Window` usando utilitários como [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
