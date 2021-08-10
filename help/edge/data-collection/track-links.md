---
title: Rastrear links usando o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados de link para o Adobe Analytics com o Experience Platform Web SDK
keywords: adobe analytics; analytics; sendEvent; s.t(); s.tl(); webPageDetails; pageViews; webInteraction; interação da web; exibições de página; rastreamento de link; links; rastrear links; clickCollection; coleta de cliques;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: d6460e442a136bf9bd26582f228017a6fb52138c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Rastrear links

Os links podem ser definidos manualmente ou rastreados [automaticamente](#automaticLinkTracking). O rastreamento manual é feito ao adicionar os detalhes na parte `web.webInteraction` do esquema. Há três variáveis obrigatórias:

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
        }
      },
      "name": "My Custom Link", // Name that shows up in the custom links report
      "URL": "https://myurl.com", // The URL of the link
      "type": "other" // values: other, download, exit
    }
  }
});
```

O tipo de link pode ser um dos três valores:

* **`other`:** Um link personalizado
* **`download`:** Um link de download
* **`exit`:** Um link de saída

Esses valores são [mapeados automaticamente](adobe-analytics/automatically-mapped-vars.md) no Adobe Analytics se [configurado](adobe-analytics/analytics-overview.md) para isso.

## Rastreamento automático de links {#automaticLinkTracking}

Por padrão, o SDK da Web captura, rotula e registra cliques em tags de link qualificadas. Os cliques são capturados com um ouvinte de evento de clique [capture](https://www.w3.org/TR/uievents/#capture-phase) anexado ao documento.

O rastreamento automático de link pode ser desativado ao configurar [no SDK da Web.](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)

```javascript
clickCollectionEnabled: false
```

### Quais tags se qualificam para o rastreamento de link?{#qualifyingLinks}

O rastreamento automático de link é feito para as tags de âncora `A` e `AREA`. No entanto, essas tags não são consideradas para o rastreamento de link se tiverem um manipulador `onclick` anexado.

### Como os links são rotulados?{#labelingLinks}

Os links são rotulados como um link de download se a tag da âncora incluir um atributo de download ou se o link terminar com uma extensão de arquivo popular. O qualificador de link de download pode ser [configurado](../fundamentals/configuring-the-sdk.md) com uma expressão regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Os links são rotulados como um link de saída se o domínio de destino do link for diferente do `window.location.hostname` atual.

Os links que não se qualificam como link de download ou de saída são rotulados como &quot;outros&quot;.

### Como os valores de rastreamento de link podem ser filtrados?

Os dados coletados com o rastreamento automático de link podem ser inspecionados e filtrados fornecendo uma função de retorno de chamada [onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

A filtragem de dados de rastreamento de link pode ser útil na preparação de dados para relatórios do Analytics. O rastreamento automático de link captura o nome do link e o URL do link. Nos relatórios do Analytics, o nome do link tem prioridade sobre o URL do link. Se você deseja relatar o URL do link, o nome do link precisa ser removido. O exemplo a seguir mostra uma função `onBeforeEventSend` que remove o nome do link dos links de download:

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

