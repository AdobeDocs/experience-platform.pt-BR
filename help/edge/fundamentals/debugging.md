---
title: Depuração
seo-title: Depuração do Adobe Experience Platform Web SDK
description: Saiba como alternar a depuração do SDK da Web do Experience Platform
seo-description: Saiba como alternar a depuração do SDK da Web do Experience Platform
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Depuração

Quando a depuração está ativada, o SDK gera mensagens para o console do navegador que podem ser úteis na depuração da sua implementação e na compreensão de como o SDK está se comportando. A depuração também resulta em uma validação síncrona do lado do servidor dos dados coletados em relação ao schema que você configurou.

A depuração está desativada por padrão, mas pode ser ativada de três maneiras diferentes:

* `configure` comando
* `setDebug` comando
* parâmetro da string de query

## Alternar a depuração com o comando Configurar

Ao configurar o SDK usando o `configure` comando, ative a depuração definindo a opção `debugEnabled` como `true`.

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

Alterne a depuração com um `debug` comando separado da seguinte maneira:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se você preferir não alterar o código na sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode executar o `debug` comando no console JavaScript do seu navegador a qualquer momento.

## Alternar a depuração com um parâmetro de string de query

Alterne a depuração definindo um parâmetro de string de `alloy_debug` query para `true` ou `false` como segue:

```HTTP
http://example.com/?alloy_debug=true
```

Semelhante ao `debug` comando, se você preferir não alterar o código em sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois é possível definir o parâmetro da string de query ao carregar a página da Web dentro do navegador.

## Prioridade e duração

Quando a depuração é definida pelo parâmetro de string de query ou comando, ela substitui qualquer `debug` opção definida no `debug` `configure` comando. Nesses dois casos, a depuração também permanece ativada durante a sessão. Em outras palavras, se você ativar a depuração usando o comando debug ou o parâmetro da string de query, ela permanecerá ativada até uma das seguintes opções:

* O fim da sessão
* Execute o `debug` comando
* Você define o parâmetro da string de query novamente
