---
title: Rastreamento de links com Adobe Analytics
seo-title: Rastreamento de links para Adobe Analytics com Adobe Experience Platform Web SDK
description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
seo-description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: ab1618a9d8c6cc60407d301dad03983ce432bbbe
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Rastrear links

Os links podem ser definidos manualmente ou acompanhados [automaticamente](#automaticLinkTracking). O rastreamento manual é feito adicionando os detalhes sob a `web.webInteraction` parte do schema. Há três variáveis obrigatórias:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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
  }
});
```

O tipo de link pode ser um dos três valores:

* **`other`:** Um link personalizado
* **`download`:** Um link de download
* **`exit`:** Um link de saída

## Rastreamento automático de links {#automaticLinkTracking}

Por padrão, o SDK da Web captura, [rotula](#labelingLinks)e [registra](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) cliques em tags de link [qualificadas](#qualifyingLinks) . Os cliques são capturados com um ouvinte de evento de [captura](https://www.w3.org/TR/uievents/#capture-phase) que é anexado ao documento.

A desativação do rastreamento automático de links pode ser feita pela [configuração](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) do SDK da Web.

```javascript
clickCollectionEnabled: false
```

### Quais tags se qualificam para o rastreamento de links?{#qualifyingLinks}

O rastreamento automático de link é feito para âncora `A` e `AREA` tags. No entanto, essas tags não são consideradas para rastreamento de link se tiverem um manipulador anexado `onclick` .

### Como os links são rotulados?{#labelingLinks}

Os links são rotulados como um link de download se a tag da âncora incluir um atributo de download ou se o link terminar com uma extensão de arquivo popular. O qualificador do link de download pode ser [configurado](../fundamentals/configuring-the-sdk.md) com uma expressão regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Os links são rotulados como um link de saída se o domínio do público alvo do link for diferente do atual `window.location.hostname`.

Os links que não se qualificam como link de download ou saída são rotulados como &quot;outros&quot;.
