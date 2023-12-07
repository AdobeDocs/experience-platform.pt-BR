---
title: Depuração no Adobe Experience Platform Web SDK
description: Saiba como alternar os recursos de depuração no SDK da Web do Experience Platform.
keywords: depurando sdk da web;depurando;configurar;configurar comando;depurar comando;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Depuração

Quando a depuração está ativada, o SDK envia mensagens para o console do navegador que podem ser úteis na depuração da implementação e no entendimento de como o SDK está se comportando.

A depuração está desativada por padrão, mas pode ser ativada de quatro maneiras diferentes:

* `configure` comando
* `setDebug` comando
* parâmetro da sequência de consulta
* Alternando em Ativar depuração no Adobe Experience Platform Debugger. O Adobe Experience Platform é uma ferramenta poderosa que examina as páginas da Web e ajuda a depurar problemas de implementação com os produtos Experience Cloud. o Adobe Experience Platform Debugger está disponível como um [Cromo](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) extensão. A depuração pode ser ativada na guia de configuração da seção AEP Web SDK.

![Imagem da interface do usuário do Experience Platform Debugger mostrando a tela de configuração.](../assets/enable-debugging.png)

## Alternar a depuração com o comando Configurar

Ao configurar o SDK usando a variável `configure` , ative a depuração definindo o parâmetro `debugEnabled` opção para `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Isso permite a depuração para todos os usuários da página da Web, em vez de somente para o seu navegador pessoal.

## Alternar a depuração com o comando Depurar

Alternar a depuração com uma `debug` comando da seguinte maneira:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se preferir não alterar o código na página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do site, isso é particularmente útil, pois é possível executar o `debug` no console JavaScript do navegador a qualquer momento.

## Alternar a depuração com um parâmetro da string de consulta

Alternar a depuração definindo um `alloy_debug` parâmetro da sequência de consulta para `true` ou `false` do seguinte modo:

```HTTP
http://example.com/?alloy_debug=true
```

Semelhante ao `debug` , se preferir não alterar o código na sua página Web ou não quiser que as mensagens de registro sejam produzidas para todos os utilizadores do seu Web site, isto é particularmente útil porque pode definir o parâmetro da sequência de consulta quando carregar a página Web no seu browser.

## Prioridade e duração

Quando a depuração é definida por meio da variável `debug` ou parâmetro de string de consulta, ele substitui qualquer `debug` opção definida na variável `configure` comando. Nesses dois casos, a depuração também permanece ativada durante a sessão. Em outras palavras, se você habilitar a depuração usando o comando debug ou o parâmetro da string de consulta, ele permanecerá habilitado até que uma das seguintes opções:

* O fim da sua sessão
* Você executa o `debug` comando
* Você define o parâmetro da sequência de consulta novamente

## Recuperando informações da biblioteca

Geralmente, é útil acessar alguns dos detalhes por trás da biblioteca que você carregou em seu site. Para fazer isso, execute o `getLibraryInfo` comando da seguinte maneira:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Atualmente, as `libraryInfo` contém as seguintes propriedades:

* `version`: esta é a versão da biblioteca carregada. Por exemplo, se a versão da biblioteca que está sendo carregada fosse 1.0.0, o valor seria `1.0.0`. Quando a biblioteca é executada dentro da extensão de tag (chamada de &quot;AEP Web SDK&quot;), a versão é a versão da biblioteca e a versão da extensão de tag é unida com um sinal &quot;+&quot;. Por exemplo, se a versão da biblioteca fosse 1.0.0 e a versão da extensão de tag fosse 1.2.0, o valor seria `1.0.0+1.2.0`.
* `commands`: esses são todos os comandos disponíveis compatíveis com a biblioteca carregada.
* `configs`: essas são todas as configurações atuais na biblioteca carregada.
