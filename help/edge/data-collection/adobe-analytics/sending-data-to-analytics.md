---
title: Envio de dados para o Adobe Analytics usando o Adobe Experience Platform Web SDK
description: Saiba como enviar dados para a Adobe Analytics usando o Adobe Experience Platform Web SDK.
keywords: adobe analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;page visualização;link tracking;links;track links;click links;clickCollection;click collection;collection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Envio de dados para a Adobe Analytics

Enquanto no passado havia funções diferentes para distinguir entre uma visualização de página e um link (por exemplo, `s.t(), s.tl()`), no SDK da Web há apenas o comando `sendEvent`. Os dados enviados com um evento determinam se devem ser uma visualização de página ou um link. [Saiba mais sobre links](../track-links.md) de rastreamento.

## Envio de uma visualização de página

Você pode especificar uma visualização de página definindo a variável `web.webPageDetails.pageViews.value=1`.

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
