---
title: Rastrear links usando o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados de links para o Adobe Analytics com o SDK da Web do Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;rastreamento de links;links;rastrear links;clickCollection;coleção de cliques;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: dac14cd358922b577c71f8d9b7f7c9b7e1b4f87d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Rastrear links

Os links podem ser definidos manualmente ou rastreados [automaticamente](#automaticLinkTracking). O rastreamento manual é feito adicionando os detalhes em `web.webInteraction` parte do esquema. Há três variáveis necessárias:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

O tipo de link pode ser um destes três valores:

* **`other`:** Um link personalizado
* **`download`:** Um link de download
* **`exit`:** Um link de saída

Esses valores são [mapeado automaticamente](adobe-analytics/automatically-mapped-vars.md) no Adobe Analytics se [configurado](adobe-analytics/analytics-overview.md) para fazer isso.

## Rastreamento automático de links {#automaticLinkTracking}

Por padrão, o SDK da Web captura, rótulos e registros de cliques em tags de link qualificadas. Os cliques são capturados com um [capturar](https://www.w3.org/TR/uievents/#capture-phase) clique em ouvinte de eventos anexado ao documento.

O rastreamento automático de links pode ser desativado por [configurando](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) o SDK da Web.

```javascript
clickCollectionEnabled: false
```

### Quais tags se qualificam para rastreamento de links?{#qualifyingLinks}

O rastreamento automático de links é feito para âncora `A` e `AREA` específicos. No entanto, essas tags não serão consideradas para o rastreamento de links se tiverem uma anexada `onclick` manipulador.

### Como os links são rotulados?{#labelingLinks}

Os links são rotulados como um link de download se a tag âncora incluir um atributo de download ou se o link terminar com uma extensão de arquivo popular. O qualificador de link de download pode ser [configurado](../fundamentals/configuring-the-sdk.md) com uma expressão regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Os links são rotulados como um link de saída se o domínio de destino do link for diferente do atual `window.location.hostname`.

Os links que não se qualificam como link de download ou de saída são rotulados como &quot;outros&quot;.

### Como os valores de rastreamento de link podem ser filtrados?

Os dados coletados com o rastreamento automático de links podem ser inspecionados e filtrados fornecendo uma [função de retorno de chamada onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

A filtragem dos dados de rastreamento de link pode ser útil na preparação de dados para os relatórios do Analytics. O rastreamento automático de links captura o nome do link e o URL do link. Nos relatórios do Analytics, o nome do link tem prioridade sobre o URL do link. Se desejar relatar o URL do link, o nome do link precisa ser removido. O exemplo a seguir mostra uma `onBeforeEventSend` função que remove o nome do link para links de download:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

