---
title: Rastrear links usando o Adobe Experience Platform Web SDK
description: Saiba como enviar dados de link para a Adobe Analytics com o Experience Platform Web SDK
keywords: adobe analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;page visualização;link tracking;links;track links;click links;clickCollection;click collection;collection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Rastrear links

Os links podem ser definidos manualmente ou rastreados [automaticamente](#automaticLinkTracking). O rastreamento manual é feito adicionando os detalhes na parte `web.webInteraction` do schema. Há três variáveis obrigatórias:

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

## Rastreamento automático de link {#automaticLinkTracking}

Por padrão, o SDK da Web captura, rotula e registra cliques em tags de link qualificadas. Os cliques são capturados com um [capture](https://www.w3.org/TR/uievents/#capture-phase) ouvinte de evento de clique que está anexado ao documento.

O rastreamento automático de links pode ser desativado por [configurar](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) o SDK da Web.

```javascript
clickCollectionEnabled: false
```

### Quais tags se qualificam para rastreamento de link?{#qualifyingLinks}

O rastreamento automático de link é feito para as tags âncora `A` e `AREA`. No entanto, essas tags não são consideradas para rastreamento de link se tiverem um manipulador `onclick` anexado.

### Como os links são rotulados?{#labelingLinks}

Os links são rotulados como um link de download se a tag da âncora incluir um atributo de download ou se o link terminar com uma extensão de arquivo popular. O qualificador do link de download pode ser [configurado](../fundamentals/configuring-the-sdk.md) com uma expressão regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Os links são rotulados como um link de saída se o domínio do público alvo do link for diferente do `window.location.hostname` atual.

Os links que não se qualificam como link de download ou saída são rotulados como &quot;outros&quot;.
