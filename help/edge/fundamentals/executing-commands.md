---
title: Execução de comandos
seo-title: Execução de comandos do SDK da Web do Adobe Experience Platform
description: Saiba como executar comandos do SDK da Web da Experience Platform
seo-description: Saiba como executar comandos do SDK da Web da Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Executando comandos

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Depois que o código base for implementado em sua página da Web, você poderá começar a executar comandos com o SDK. Não é necessário aguardar o carregamento do arquivo externo \(`alloy.js`\) do servidor antes de executar comandos. Se o SDK não tiver concluído o carregamento, os comandos serão enfileirados e processados pelo SDK assim que possível.

Os comandos são executados usando a seguinte sintaxe.

```javascript
alloy("commandName", options);
```

O `commandName` informa ao SDK o que fazer, embora `options` sejam os parâmetros e dados que você gostaria de passar para um comando. Como as opções disponíveis dependem do comando, consulte a documentação para obter mais detalhes sobre cada comando.

## Uma nota sobre promessas

[As promessas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) são fundamentais para como o SDK se comunica com o código na sua página da Web. Uma promessa é uma estrutura de programação comum e não é específica para esse SDK ou mesmo para JavaScript. Uma promessa atua como um proxy para um valor que não é conhecido quando a promessa é criada. Quando o valor é conhecido, a promessa é &quot;resolvida&quot; com o valor. As funções de manipulador podem ser associadas a uma promessa, para que você possa ser notificado quando a promessa tiver sido resolvida ou quando um erro tiver ocorrido no processo de resolução da promessa. Para saber mais sobre as promessas, leia [este tutorial](https://javascript.info/promise-basics) ou qualquer outro recurso na web.

## Lidar com sucesso ou falha

Cada vez que um comando é executado, uma promessa é retornada. A promessa representa a conclusão final do comando. No exemplo abaixo, você pode usar `then` e `catch` métodos para determinar quando o comando foi bem-sucedido ou falhou.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Se não for importante saber quando o comando é bem-sucedido, você poderá remover a `then` chamada.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Da mesma forma, se você não souber quando o comando falhar, poderá remover a `catch` chamada.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## Supressão de erros

Se a promessa for rejeitada e você não tiver adicionado uma `catch` chamada, o erro &quot;borbulha para cima&quot; e é registrado no console do desenvolvedor do seu navegador, independentemente de o registro estar ativado no SDK da Web da Adobe Experience Platform. Se isso for uma preocupação para você, é possível definir a opção de `suppressErrors` configuração como `true` descrito em [Configuração do SDK](configuring-the-sdk.md).
