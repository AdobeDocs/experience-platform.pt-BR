---
title: Mapeamento manual de variáveis no Analytics
seo-title: Mapeamento manual de variáveis no Analytics com o SDK da Web
description: Como mapear manualmente variáveis no Analytics usando regras de processamento
seo-description: mapeie manualmente variáveis no Analytics usando regras de processamento com o SDK da Web
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 47%

---


# Mapeamento manual de variáveis no Analytics

O Adobe Experience Platform (AEP) [!DNL Web SDK] pode mapear determinadas variáveis automaticamente, mas as variáveis personalizadas devem ser mapeadas manualmente.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/pt-BR/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html). Em seguida, ele pode ser mapeado para [!DNL Analytics] usar regras [de](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) processamento para preencher [!DNL Analytics] variáveis.

Also, you can use a default set of actions and product lists to send or retrieve data with the AEP [!DNL Web SDK]. Para fazer isso, consulte [Produtos](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/implement/commerce.html).

## Dados de contexto

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. A lista de pares de valores a seguir mostra um exemplo de `context data`:

```javascript
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

Por exemplo, na regra a seguir, o Analytics é definido para preencher **termos de pesquisa interna (eVar2)** com os dados associados a **a.x_atag.search.term (Dados de contexto)**.

![](assets/examplerule.png)


## Esquema do XDM

[!DNL Experience Platform]A utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, torna-se mais fácil manter o significado e, portanto, obter valor dos dados. [!DNL Analytics] os dados de contexto funcionam com a estrutura definida pelo schema.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with the AEP [!DNL Web SDK]. Neste exemplo, o comando `event` corresponde ao [esquema de detalhes de comércio do ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que productListItems `name` e os valores `SKU` sejam rastreados:


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

For more information on tracking events with the AEP [!DNL Web SDK], see [Tracking events](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/fundamentals/tracking-events.html).
