---
title: Rastreamento de página e link com o Adobe Analytics
seo-title: Rastreamento de links para Adobe Analytics com Adobe Experience Platform Web SDK
description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
seo-description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Envio de dados para a Adobe Analytics

Enquanto no passado havia funções diferentes para distinguir entre uma visualização de página e um link (por exemplo, `s.t(), s.tl()`), no SDK da Web há apenas o `sendEvent` comando. Os dados enviados com um evento determinam se devem ser uma visualização de página ou um link. [Saiba mais sobre links de rastreamento](../track-links.md)

## Envio de uma visualização de página

É possível especificar uma visualização de página definindo a `web.webPageDetails.pageViews.value=1` variável.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Embora o Analytics registre tecnicamente uma visualização de página mesmo se essa variável não estiver definida, é uma prática recomendada definir essa variável sempre que você quiser registrar uma visualização de página para ser explícita nos seus dados e para prova futura da sua implementação.
