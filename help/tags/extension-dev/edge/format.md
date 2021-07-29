---
title: Módulos de biblioteca em extensões de borda
description: Formatar módulos de biblioteca para extensões de tag em uma propriedade edge .
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 75%

---

# Módulos de biblioteca em extensões de borda

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

>[!IMPORTANT]
>
>Este documento aborda o formato do módulo da biblioteca para extensões de borda. Se você estiver desenvolvendo uma extensão da Web, consulte o guia em [formatar módulos de extensão da Web](../web/format.md).

Um módulo de biblioteca é uma parte do código reutilizável fornecido por uma extensão emitida dentro da biblioteca de tempo de execução de tags no Adobe Experience Platform (a biblioteca que é executada no nó de borda). Por exemplo, um tipo de ação `sendBeacon` terá um módulo de biblioteca que será executado no nó de borda e enviará um beacon.

O módulo da biblioteca está estruturado como um [módulo CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). Em um módulo CommonJS, as seguintes variáveis estão disponíveis para uso:

## [!DNL require]

Uma função `require` está disponível para que você acesse módulos em sua extensão. Qualquer módulo na sua extensão pode ser acessado por um caminho relativo. O caminho relativo deve começar com `./` ou `../`.

Exemplo de uso:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Uma variável livre chamada `module` está disponível e permite exportar a API do módulo.

Exemplo de uso:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Uma variável livre chamada `exports` está disponível e permite exportar a API do módulo.

Exemplo de uso:

```js
exports.sayHello = (…) => { … }
```

É uma alternativa para `module.exports`, mas tem uso mais limitado. Leia [Entender module.exports e exportações em node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) para compreender melhor as diferenças entre `module.exports` e `exports` e as limitações relacionadas ao uso de `exports`. Na dúvida, torne sua vida mais fácil e use `module.exports` em vez de `exports`.

## Assinatura do módulo do lado do servidor

Todos os tipos de módulo (elementos de dados, condições ou ações) fornecidos pela sua extensão serão chamados com os mesmos parâmetros: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
