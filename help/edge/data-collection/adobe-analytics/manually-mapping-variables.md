---
title: Mapeamento manual de variáveis do Adobe Analytics no Adobe Experience Platform Web SDK
description: Saiba como mapear variáveis manualmente no Adobe Analytics usando regras de processamento no SDK da Experience Platform Web.
seo-description: Mapeie manualmente variáveis no Adobe Analytics usando regras de processamento com o SDK da Web
keywords: adobe analytics;analytics;variáveis;mapear variáveis;mapear variáveis;contextData;context Data;Regras de processamento;regras;xdm;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 33%

---


# Mapeamento manual de variáveis no Adobe Analytics

O Adobe Experience Platform [!DNL Web SDK] pode mapear determinadas variáveis automaticamente, mas as variáveis personalizadas devem ser mapeadas manualmente.

Para dados XDM que não são mapeados automaticamente para [!DNL Analytics], você pode usar [dados de contexto](https://docs.adobe.com/content/help/pt-BR/analytics/implementation/vars/page-vars/contextdata.html) para corresponder ao seu [schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html). Em seguida, ele pode ser mapeado para [!DNL Analytics] usando [regras de processamento](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) para preencher as variáveis [!DNL Analytics].

Além disso, você pode usar um conjunto padrão de ações e listas de produtos para enviar ou recuperar dados com o Adobe Experience Platform Web SDK. Para fazer isso, consulte [Produtos](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/implement/commerce.html).

## Dados de contexto

Para serem usados por [!DNL Analytics], os dados XDM são nivelados usando a notação de pontos e disponibilizados como `contextData`. A lista de pares de valores a seguir mostra um exemplo de `context data`:

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

Todos os dados coletados pela rede de borda podem ser acessados pelas [regras de processamento](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). Em [!DNL Analytics], você pode usar as regras de processamento para incorporar dados de contexto às variáveis [!DNL Analytics].

Por exemplo, na regra a seguir, o Adobe Analytics está definido para preencher **termos de Pesquisa interna (eVar2)** com os dados associados a **a.x._atag.search.term(Dados de contexto)**.

![](assets/examplerule.png)


## Schema XDM

A Adobe Experience Platform usa schemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, torna-se mais fácil manter o significado e, portanto, obter valor dos dados. [!DNL Analytics] os dados de contexto funcionam com a estrutura definida pelo schema.

O exemplo a seguir mostra como o [`event` comando](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/fundamentals/tracking-events.html) pode ser usado com a opção `xdm` para enviar e recuperar dados com o Adobe Experience Platform Web SDK. Neste exemplo, o comando `event` corresponde ao [esquema de detalhes de comércio do ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que productListItems `name` e os valores `SKU` sejam rastreados:


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

Para obter mais informações sobre o rastreamento de eventos com o Adobe Experience Platform [!DNL Web SDK], consulte [Rastreamento de eventos](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
