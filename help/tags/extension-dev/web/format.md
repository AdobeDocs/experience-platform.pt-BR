---
title: Módulos de biblioteca em extensões da Web
description: Saiba como formatar módulos de biblioteca para extensões da Web no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 77%

---

# Módulos de biblioteca em extensões da Web

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

>[!IMPORTANT]
>
>Este documento aborda o formato do módulo de biblioteca para extensões da Web. Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [formatação de módulos de extensão de borda](../edge/format.md).

Um módulo de biblioteca é um pedaço de código reutilizável fornecido por uma extensão emitida dentro da biblioteca de tempo de execução de tag no Adobe Experience Platform. Essa biblioteca é executada no site do cliente. Por exemplo, um tipo de evento `gesture` terá um módulo de biblioteca que será executado no site do cliente e detectará os gestos do usuário.

O módulo da biblioteca está estruturado como um [módulo CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). Em um módulo CommonJS, as seguintes variáveis estão disponíveis para uso:

## [!DNL require]

Uma função `require` está disponível para você acessar:

1. Módulos principais fornecidos por tags. Esses módulos podem ser acessados usando `require('@adobe/reactor-name-of-module')`. Consulte o documento nos [módulos principais](./core.md) disponíveis para obter mais informações.
1. Outros módulos na sua extensão. Qualquer módulo na sua extensão pode ser acessado por um caminho relativo. O caminho relativo deve começar com `./` ou `../`.

Exemplo de uso:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

Uma variável livre chamada `module` está disponível e permite exportar a API do módulo.

Exemplo de uso:

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

Uma variável livre chamada `exports` está disponível e permite exportar a API do módulo.

Exemplo de uso:

```javascript
exports.sayHello = function(…) { … }
```

É uma alternativa para `module.exports`, mas tem uso mais limitado. Leia [Entender module.exports e exportações em node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) para compreender melhor as diferenças entre `module.exports` e `exports` e as limitações relacionadas ao uso de `exports`. Na dúvida, torne sua vida mais fácil e use `module.exports` em vez de `exports`.

## Execução e armazenamento em cache

Quando a biblioteca de tempo de execução da tag for executada, os módulos serão &quot;instalados&quot; imediatamente e suas exportações serão armazenadas em cache. Presumindo o seguinte módulo:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` será registrado imediatamente, enquanto  `runs when necessary` será registrado somente quando a função exportada for chamada pelo mecanismo de tag. Embora possa ser desnecessário para a finalidade de seu módulo específico, você pode aproveitar isso executando qualquer configuração necessária antes de exportar a função.
