---
title: Manipulação de respostas de comando
description: Manipule respostas de comandos usando promessas do JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Manipulação de respostas de comando

Alguns comandos do SDK da Web podem retornar um objeto contendo dados potencialmente úteis para sua organização. Você pode escolher o que fazer com esses dados, se desejar. As respostas de comando são valiosas para propostas e destinos, pois exigem dados de Edge Network para funcionar com eficiência.

As respostas de comando usam JavaScript [promessas](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise), atuando como proxy para um valor que não é conhecido quando a promessa é criada. Depois que o valor é conhecido, a promessa é &quot;resolvida&quot; com o valor.

## Manipular respostas de comando usando a extensão de tag do SDK da Web

Crie uma regra que assine o evento **[!UICONTROL Enviar evento concluído]** como parte de uma regra.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Eventos], selecione um evento existente ou crie um evento.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Evento] como **[!UICONTROL Enviar evento concluído]**.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

Você pode então incluir as ações **[!UICONTROL Aplicar propostas]** ou **[!UICONTROL Aplicar resposta]** a esta regra.

1. Ao visualizar a regra criada ou editada acima, selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Aplicar propostas]** ou **[!UICONTROL Aplicar resposta]**, dependendo do comportamento desejado.
1. Defina os campos desejados da ação e clique em **[!UICONTROL Manter alterações]**.

## Manipular respostas de comando usando a biblioteca JavaScript do SDK da Web

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
