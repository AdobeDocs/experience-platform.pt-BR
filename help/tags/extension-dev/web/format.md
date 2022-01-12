---
title: Módulos de biblioteca em extensões da Web
description: Saiba como formatar módulos de biblioteca para extensões da Web no Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 93%

---

# Módulos de biblioteca em extensões da Web

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

>[!IMPORTANT]
>
>Este documento aborda o formato do módulo de biblioteca para extensões da Web. Se você estiver desenvolvendo uma extensão de borda, consulte o manual sobre [formatação de módulos de extensão de borda](../edge/format.md).

Um módulo de biblioteca consiste em código reutilizável fornecido por uma extensão emitida na biblioteca de tempo de execução de tag na Adobe Experience Platform. Essa biblioteca é executada no site do cliente. Por exemplo, um tipo de evento `gesture` terá um módulo de biblioteca que será executado no site do cliente e detectará os gestos do usuário.

O módulo da biblioteca está estruturado como um [módulo CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules). Em um módulo CommonJS, as seguintes variáveis estão disponíveis para uso:

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

Quando a biblioteca de tempo de execução de tag for executada, os módulos serão &quot;instalados&quot; imediatamente e suas exportações serão armazenadas em cache. Presumindo o seguinte módulo:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` serão registrados imediatamente, enquanto `runs when necessary` serão registrados somente depois que a função exportada for chamada pelo mecanismo de tag. Embora possa ser desnecessário para a finalidade de seu módulo específico, você pode aproveitar isso executando qualquer configuração necessária antes de exportar a função.
