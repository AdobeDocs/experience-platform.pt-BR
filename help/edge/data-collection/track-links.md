---
title: Rastrear links usando o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados de link para o Adobe Analytics com o Experience Platform Web SDK
keywords: adobe analytics; analytics; sendEvent; s.t(); s.tl(); webPageDetails; pageViews; webInteraction; interação da web; exibições de página; rastreamento de link; links; rastrear links; clickCollection; coleta de cliques;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Rastrear links

Os links podem ser definidos manualmente ou rastreados [automaticamente](#automaticLinkTracking). O rastreamento manual é feito ao adicionar os detalhes na guia `web.webInteraction` parte do schema. Há três variáveis obrigatórias:

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

A partir da versão 2.15.0, o SDK da Web captura o `region` do elemento HTML clicado. Isso habilita o [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=pt-BR) recursos de relatórios no Adobe Analytics.

O tipo de link pode ser um dos três valores:

* **`other`:** Um link personalizado
* **`download`:** Um link de download
* **`exit`:** Um link de saída

Esses valores são [mapeado automaticamente](adobe-analytics/automatically-mapped-vars.md) no Adobe Analytics se [configurado](adobe-analytics/analytics-overview.md) para fazer isso.

## Rastreamento automático de links {#automaticLinkTracking}

Por padrão, o SDK da Web captura, rotula e registra cliques em tags de link qualificadas. Os cliques são capturados com um [captura](https://www.w3.org/TR/uievents/#capture-phase) clique em ouvinte de evento anexado ao documento.

O rastreamento automático de link pode ser desativado por [configuração](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) o SDK da Web.

```javascript
clickCollectionEnabled: false
```

### Quais tags se qualificam para o rastreamento de link?{#qualifyingLinks}

O rastreamento automático de link é feito para âncora `A` e `AREA` tags. No entanto, essas tags não são consideradas para o rastreamento de link se tiverem um `onclick` manipulador.

### Como os links são rotulados?{#labelingLinks}

Os links são rotulados como um link de download se a tag da âncora incluir um atributo de download ou se o link terminar com uma extensão de arquivo popular. O qualificador de link de download pode ser [configurado](../fundamentals/configuring-the-sdk.md) com uma expressão regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Os links são rotulados como um link de saída se o domínio de destino do link for diferente do atual `window.location.hostname`.

Os links que não se qualificam como link de download ou de saída são rotulados como &quot;outros&quot;.

### Como os valores de rastreamento de link podem ser filtrados?

Os dados coletados com o rastreamento automático de link podem ser inspecionados e filtrados fornecendo um [Função de retorno de chamada onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

A filtragem de dados de rastreamento de link pode ser útil na preparação de dados para relatórios do Analytics. O rastreamento automático de link captura o nome do link e o URL do link. Nos relatórios do Analytics, o nome do link tem prioridade sobre o URL do link. Se você deseja relatar o URL do link, o nome do link precisa ser removido. O exemplo a seguir mostra um `onBeforeEventSend` que remove o nome do link dos links de download:

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

A partir do SDK da Web versão 2.15.0, os dados coletados com o rastreamento automático de link podem ser inspecionados, aumentados ou filtrados fornecendo um [Função de retorno de chamada onBeforeLinkClickSend](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Essa função de retorno de chamada é executada somente quando um evento de clique em link automático ocorre.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

Ao filtrar os eventos de rastreamento de link, use o `onBeforeLinkClickSend` comando, o Adobe recomenda retornar `false` para os cliques em links que não devem ser rastreados. Qualquer outra resposta fará com que o SDK da Web envie os dados para a Edge Network.


>[!NOTE]
>
>** Quando as duas variáveis `onBeforeEventSend` e `onBeforeLinkClickSend` as funções de retorno de chamada são definidas, o SDK da Web executa a variável `onBeforeLinkClickSend` função de retorno de chamada para filtrar e aumentar o evento de interação de clique em link, seguido pela variável `onBeforeEventSend` função de retorno de chamada.