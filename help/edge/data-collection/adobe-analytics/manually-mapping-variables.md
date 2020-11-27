---
title: Mapeamento manual de variáveis no Adobe Analytics
seo-title: Mapeamento manual de variáveis no Adobe Analytics com o SDK da Web
description: Como mapear variáveis manualmente no Adobe Analytics usando regras de processamento
seo-description: Mapeie manualmente variáveis no Adobe Analytics usando regras de processamento com o SDK da Web
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 206b5addd6baf5a120b469b21313ee86ac1fe53b
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 35%

---


# Mapeamento manual de variáveis no Adobe Analytics

O Adobe Experience Platform [!DNL Web SDK] pode mapear determinadas variáveis automaticamente, mas as variáveis personalizadas devem ser mapeadas manualmente.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/pt-BR/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html). Em seguida, ele pode ser mapeado para [!DNL Analytics] usar regras [de](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) processamento para preencher [!DNL Analytics] variáveis.

Além disso, você pode usar um conjunto padrão de ações e listas de produtos para enviar ou recuperar dados com o Adobe Experience Platform Web SDK. Para fazer isso, consulte [Produtos](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/implement/commerce.html).

## Dados de contexto

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. A lista de pares de valores a seguir mostra um exemplo de `context data`:

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## Regras de processamento

Todos os dados coletados pela rede de borda podem ser acessados pelas [regras de processamento](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

For example, in the following rule, Adobe Analytics is set to populate **Internal Search terms (eVar2)** with the data associated with **a.x._atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Schema XDM

A Adobe Experience Platform usa schemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, torna-se mais fácil manter o significado e, portanto, obter valor dos dados. [!DNL Analytics] os dados de contexto funcionam com a estrutura definida pelo schema.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with Adobe Experience Platform Web SDK. Neste exemplo, o comando `event` corresponde ao [esquema de detalhes de comércio do ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que productListItems `name` e os valores `SKU` sejam rastreados:


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Para obter mais informações sobre como rastrear eventos com o Adobe Experience Platform [!DNL Web SDK], consulte [Rastreamento de eventos](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/fundamentals/tracking-events.html).
