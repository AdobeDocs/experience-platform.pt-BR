---
title: Mapeamento manual de variáveis no Analytics
seo-title: Mapeamento manual de variáveis no Analytics com o SDK da Web
description: Como mapear manualmente variáveis no Analytics usando regras de processamento
seo-description: mapeie manualmente variáveis para o Analytics usando regras de processamento com o SDK da Web
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 11%

---


# Mapeamento manual de variáveis no Analytics

O Adobe Experience Platform (AEP) [!DNL Web SDK] pode mapear determinadas variáveis automaticamente, mas as variáveis personalizadas devem ser mapeadas manualmente.

Para dados XDM que não são mapeados automaticamente para [!DNL Analytics], você pode usar dados [de](https://docs.adobe.com/content/help/pt-BR/analytics/implementation/vars/page-vars/contextdata.html) contexto para corresponder ao seu [schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html). Em seguida, ele pode ser mapeado para [!DNL Analytics] usar regras [de](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) processamento para preencher [!DNL Analytics] variáveis.

Além disso, você pode usar um conjunto padrão de ações e listas de produtos para enviar ou recuperar dados com o AEP [!DNL Web SDK]. Para fazer isso, consulte [Produtos](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Dados de contexto

Para serem usados por [!DNL Analytics], os dados XDM são nivelados usando a notação de pontos e disponibilizados como `contextData`. A lista de pares de valores a seguir mostra um exemplo de `context data`:

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

Todos os dados coletados pela rede de borda podem ser acessados pelas regras [de](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)processamento. Em [!DNL Analytics], é possível usar regras de processamento para incorporar dados de contexto em [!DNL Analytics] variáveis.

Por exemplo, na regra a seguir, o Analytics é definido para preencher termos de Pesquisa **interna (eVar2)** com os dados associados a **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Schema XDM

[!DNL Experience Platform] usa schemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, torna-se mais fácil manter o significado e, portanto, obter valor dos dados. [!DNL Analytics] os dados de contexto funcionam com a estrutura definida pelo schema.

O exemplo a seguir mostra como o [`event` comando](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) pode ser usado com a `xdm` opção para enviar e recuperar dados com o AEP [!DNL Web SDK]. Neste exemplo, o `event` comando corresponde ao Schema [Detalhes de Comércio de](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent para que productListItems `name` e `SKU` valores sejam rastreados:


```
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

Para obter mais informações sobre o rastreamento de eventos com o AEP [!DNL Web SDK], consulte [Rastreamento de eventos](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
