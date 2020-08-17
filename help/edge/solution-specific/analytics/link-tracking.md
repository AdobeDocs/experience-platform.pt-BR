---
title: Rastreamento de página e link com o Adobe Analytics
seo-title: Rastreamento de links para Adobe Analytics com Adobe Experience Platform Web SDK
description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
seo-description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: b50082405cd0392ff827a83ad82091fbcd370b21
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Envio de dados para a Adobe Analytics

Enquanto no passado havia funções diferentes para diferenciar entre uma visualização de página e um link (por exemplo, `s.t(), s.tl()`), no SDK da Web há apenas o `sendEvent` comando. Os dados enviados com um evento determinam se devem ser uma visualização de página ou um link.

## Envio de uma visualização de página

É possível especificar uma visualização de página definindo a `web.webPageDetails.pageViews.value=1` variável.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Embora o Analytics registre tecnicamente uma visualização de página mesmo se essa variável não estiver definida, é uma prática recomendada definir essa variável sempre que você quiser registrar uma visualização de página para ser explícita nos seus dados e para a sua implementação futura.

## Rastreamento de links

É possível definir links adicionando os detalhes abaixo da parte `web.webInteraction` do schema. Há três variáveis obrigatórias: `web.webInteraction.name`, `web.webInteraction.type` e `web.webInteraction.linkClicks.value`.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

O tipo de link pode ser um dos três valores:

* **`other`:** Um link personalizado
* **`download`:** Um link de download (pode ser rastreado automaticamente pela biblioteca)
* **`exit`:** Um link de saída

### Rastreamento automático de link

O SDK da Web pode rastrear automaticamente todos os cliques em links ativando [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled).

Os links de download são detectados automaticamente com base em tipos de arquivos populares. A lógica de como os downloads são classificados é configurável.
