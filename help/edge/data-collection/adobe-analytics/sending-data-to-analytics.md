---
title: Envio de dados para a Adobe Analytics usando o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados para a Adobe Analytics usando o SDK da Web da Adobe Experience Platform.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;rastreamento de links;links;rastrear links;clickCollection;coleção de cliques;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Envio de dados para o Adobe Analytics

Enquanto no passado havia diferentes funções para distinguir entre uma exibição de página e um link (por exemplo, `s.t(), s.tl()`), no SDK da Web, há apenas a variável `sendEvent` comando. Os dados enviados com um evento determinam se ele deve ser uma exibição de página ou um link. [Saiba mais sobre links de rastreamento](../track-links.md).

## Envio de uma exibição de página

É possível especificar uma visualização de página definindo a variável `web.webPageDetails.pageViews.value=1` variável.

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

Embora o Analytics registre tecnicamente uma exibição de página, mesmo que essa variável não esteja definida, é uma prática recomendada defini-la sempre que você quiser registrar uma exibição de página para ser explícita em seus dados e para comprovar futuramente sua implementação.
