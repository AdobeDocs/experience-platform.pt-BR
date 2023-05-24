---
title: Executar comandos do SDK da Web do Adobe Experience Platform
description: Saiba como executar comandos do SDK da Web do Experience Platform
keywords: Executar comandos;commandName;Promises;getLibraryInfo;response objects;consent;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# Executar comandos


Depois que o código base tiver sido implementado na página da Web, você poderá começar a executar comandos com o SDK. Não é necessário aguardar o arquivo externo (`alloy.js`) a ser carregado do servidor antes da execução dos comandos. Se o SDK não tiver terminado de carregar, os comandos serão enfileirados e processados pelo SDK assim que possível.

Os comandos são executados usando a seguinte sintaxe.

```javascript
alloy("commandName", options);
```

A variável `commandName` informa o SDK sobre o que fazer, enquanto `options` são os parâmetros e dados que você deseja passar para um comando. Como as opções disponíveis dependem do comando, consulte a documentação para obter mais detalhes sobre cada comando.

## Uma observação sobre promessas

[Promessas](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) são fundamentais para a forma como o SDK se comunica com o código na sua página da Web. Uma promessa é uma estrutura de programação comum e não é específica desse SDK ou mesmo do JavaScript. Uma promessa atua como um proxy para um valor que não é conhecido quando a promessa é criada. Depois que o valor é conhecido, a promessa é &quot;resolvida&quot; com o valor. As funções de controle podem ser associadas a uma promessa, para que você possa ser notificado quando a promessa for resolvida ou quando ocorrer um erro no processo de resolução da promessa. Para saber mais sobre promessas, leia [este tutorial](https://javascript.info/promise-basics) ou qualquer outro recurso na Web.

## Lidar com sucesso ou falha {#handling-success-or-failure}

Cada vez que um comando é executado, uma promessa é retornada. A promessa representa a conclusão final do comando. No exemplo abaixo, você pode usar `then` e `catch` métodos para determinar quando o comando foi bem-sucedido ou falhou.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Se não for importante para você saber quando o comando será bem-sucedido, remova a variável `then` chame.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Da mesma forma, se não for importante saber quando o comando falhará, você poderá remover a variável `catch` chame.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Objetos de resposta

Todas as promessas retornadas dos comandos são resolvidas com um `result` objeto. O objeto de resultado conterá dados dependendo do comando e do consentimento do usuário. Por exemplo, as informações da biblioteca são passadas como uma propriedade do objeto results no comando a seguir.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Consentimento

Se um usuário não tiver consentido com uma finalidade específica, a promessa ainda será resolvida; no entanto, o objeto de resposta conterá apenas as informações que podem ser fornecidas no contexto do consentimento do usuário.
