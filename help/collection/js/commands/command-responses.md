---
title: Manipulação de respostas de comando
description: Manipule respostas de comandos usando promessas do JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Manipulação de respostas de comando

Alguns comandos do Web SDK podem retornar um objeto que contém dados potencialmente úteis para sua organização. Você pode escolher o que fazer com esses dados, se desejar. As respostas de comando são valiosas para propostas e destinos, pois exigem dados do Edge Network para funcionar com eficiência.

As respostas de comando usam JavaScript [promessas](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise), atuando como proxy para um valor que não é conhecido quando a promessa é criada. Depois que o valor é conhecido, a promessa é &quot;resolvida&quot; com o valor.

Use os métodos `then` e `catch` para determinar quando um comando é bem-sucedido ou falha. Você pode omitir `then` ou `catch` se as finalidades não forem importantes para a implementação.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Todas as promessas retornadas dos comandos usam um objeto `result`. Por exemplo, você pode obter informações da biblioteca do objeto `result` usando o comando [`getLibraryInfo`](getlibraryinfo.md):

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

O conteúdo deste objeto `result` depende de uma combinação de qual comando você usa e do consentimento do usuário. Se um usuário não tiver consentido com uma finalidade específica, o objeto de resposta conterá apenas informações que podem ser fornecidas no contexto do consentimento do usuário.

## Respostas de comando usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente às respostas de comando é uma regra que assina o evento [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete). Você pode então incluir ações como [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) ou [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) nessa regra.
