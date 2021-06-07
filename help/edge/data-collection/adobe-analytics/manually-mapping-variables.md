---
title: Mapeamento manual de variáveis do Adobe Analytics no SDK da Web da Adobe Experience Platform
description: Saiba como mapear variáveis manualmente no Adobe Analytics usando regras de processamento no SDK da Web do Experience Platform.
seo-description: Mapear variáveis manualmente para o Adobe Analytics usando regras de processamento com o SDK da Web
keywords: adobe analytics, analytics, variáveis, variáveis de mapeamento, variáveis de mapa, contextData, dados de contexto, regras de processamento, regras, xdm, schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: d67c8c0ada6dc4bf07b73547f9e571a8a7386b75
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 16%

---

# Mapeamento manual de variáveis no Adobe Analytics

O Adobe Experience Platform [!DNL Web SDK] pode mapear determinadas variáveis automaticamente, mas as variáveis personalizadas devem ser mapeadas manualmente.

Para dados XDM que não são mapeados automaticamente para [!DNL Analytics], você pode usar [dados de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html) para corresponder ao [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html). Em seguida, ele pode ser mapeado para [!DNL Analytics] usando [regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) para preencher variáveis [!DNL Analytics].

Além disso, é possível usar um conjunto padrão de ações e listas de produtos para enviar ou recuperar dados com o SDK da Web da Adobe Experience Platform. Para fazer isso, consulte [Coletar informações sobre comércio e produto](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Dados de contexto

Para serem usados por [!DNL Analytics], os dados do XDM são nivelados usando a notação de pontos e disponibilizados como `contextData`. A lista de pares de valores a seguir mostra um exemplo de `context data`:

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

Todos os dados coletados pela rede de borda podem ser acessados pelas [regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). Em [!DNL Analytics], você pode usar as regras de processamento para incorporar dados de contexto às variáveis [!DNL Analytics].

Por exemplo, na regra a seguir, o Adobe Analytics é definido para preencher **Termos de pesquisa interna (eVar2)** com os dados associados a **a.x._atag.search.term(Dados de contexto)**.

![](assets/examplerule.png)


## Esquema XDM

O Adobe Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. [!DNL Analytics] os dados de contexto funcionam com a estrutura definida pelo schema .

O exemplo a seguir mostra como o [`event` comando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) pode ser usado com a opção `xdm` para enviar e recuperar dados com o SDK da Web da Adobe Experience Platform. Neste exemplo, o comando `event` corresponde ao [esquema de detalhes de comércio do ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que productListItems `name` e os valores `SKU` sejam rastreados:


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

Para obter mais informações sobre o rastreamento de eventos com Adobe Experience Platform [!DNL Web SDK], consulte [Rastreamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).
