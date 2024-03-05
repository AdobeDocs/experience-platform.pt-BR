---
title: Manipulação de respostas de comando
description: Manipule respostas de comandos usando promessas JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Manipulação de respostas de comando

Alguns comandos do SDK da Web podem retornar um objeto contendo dados potencialmente úteis para sua organização. Você pode escolher o que fazer com esses dados, se desejar. As respostas de comando são valiosas para propostas e destinos, pois exigem dados da Rede de borda para funcionar com eficiência.

As respostas de comando usam JavaScript [promessas](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise), atuando como um proxy para um valor que não é conhecido quando a promessa é criada. Depois que o valor é conhecido, a promessa é &quot;resolvida&quot; com o valor.

## Manipular respostas de comando usando a extensão de tag do SDK da Web

Crie uma regra que assine a **[!UICONTROL Enviar evento concluído]** evento como parte de uma regra.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Eventos], selecione um evento existente ou crie um evento.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de evento] para **[!UICONTROL Enviar evento concluído]**.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

É possível incluir as ações **[!UICONTROL Aplicar apresentações]** ou **[!UICONTROL Aplicar resposta]** a esta regra.

1. Ao visualizar a regra criada ou editada acima, selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Aplicar apresentações]** ou **[!UICONTROL Aplicar resposta]**, dependendo do comportamento desejado.
1. Defina os campos desejados da ação e clique em **[!UICONTROL Manter alterações]**.

## Manipular respostas de comando usando a biblioteca JavaScript do SDK da Web

Use o `then` e `catch` métodos para determinar quando um comando é bem-sucedido ou falha. Você pode omitir `then` ou `catch` se os objetivos não forem importantes para a implementação.

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

Todas as promessas retornadas dos comandos usam um `result` objeto. Por exemplo, você pode obter informações da biblioteca do `result` objeto usando o [`getLibraryInfo`](getlibraryinfo.md) comando:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

O conteúdo deste `result` depende de uma combinação de qual comando você usa e do consentimento do usuário. Se um usuário não tiver consentido com uma finalidade específica, o objeto de resposta conterá apenas informações que podem ser fornecidas no contexto do consentimento do usuário.
