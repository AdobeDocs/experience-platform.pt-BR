---
title: Depuração no Adobe Experience Platform Web SDK
description: Saiba como alternar os recursos de depuração no SDK da Web do Experience Platform.
keywords: depurar o sdk da Web;depurar;configurar;configurar comando;depurar comando;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Depuração

Quando a depuração está ativada, o SDK gera mensagens para o console do navegador que podem ser úteis na depuração da sua implementação e na compreensão de como o SDK está se comportando. A depuração também resulta em uma validação síncrona do lado do servidor dos dados coletados em relação ao schema que você configurou.

A depuração está desativada por padrão, mas pode ser ativada de três maneiras diferentes:

* `configure` comando
* `setDebug` comando
* parâmetro da string de query

## Alternar a depuração com o comando Configurar

Ao configurar o SDK usando o comando `configure`, ative a depuração definindo a opção `debugEnabled` como `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Isso permite a depuração para todos os usuários da página da Web, em vez de somente para seu navegador pessoal.

## Alternar a depuração com o comando Depurar

Alterne a depuração com um comando `debug` separado da seguinte forma:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se você preferir não alterar o código na sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode executar o comando `debug` no console JavaScript do seu navegador a qualquer momento.

## Alternar a depuração com um parâmetro de string de query

Alterne a depuração definindo um parâmetro de sequência de query `alloy_debug` para `true` ou `false` da seguinte forma:

```HTTP
http://example.com/?alloy_debug=true
```

Semelhante ao comando `debug`, se você preferir não alterar o código em sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode definir o parâmetro da string de query ao carregar a página da Web dentro do seu navegador.

## Prioridade e duração

Quando a depuração é definida pelo parâmetro `debug` de comando ou string de query, ela substitui qualquer opção `debug` definida no comando `configure`. Nesses dois casos, a depuração também permanece ativada durante a sessão. Em outras palavras, se você ativar a depuração usando o comando debug ou o parâmetro da string de query, ela permanecerá ativada até uma das seguintes opções:

* O fim da sessão
* Execute o comando `debug`
* Você define o parâmetro da string de query novamente

## Recuperando informações da biblioteca

Geralmente, é útil acessar alguns detalhes por trás da biblioteca que você carregou em seu site. Para fazer isso, execute o comando `getLibraryInfo` da seguinte maneira:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Atualmente, o objeto `libraryInfo` fornecido contém as seguintes propriedades:

* `version` Esta é a versão da biblioteca carregada. Por exemplo, se a versão da biblioteca que está sendo carregada fosse 1.0.0, o valor seria `1.0.0`.
