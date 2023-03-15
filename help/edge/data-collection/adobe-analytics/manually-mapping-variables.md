---
title: Mapeamento manual de variáveis do Adobe Analytics no SDK da Web da Adobe Experience Platform
description: Saiba como mapear variáveis manualmente no Adobe Analytics usando regras de processamento no SDK da Web do Experience Platform.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;análise;variáveis;mapeamento variáveis;mapear variáveis;contextData;contexto Dados;Regras de processamento;regras;xdm;esquema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 9392a90b70699b79949095e178ea77dd34d313a3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 25%

---

# Mapeamento manual de variáveis no Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] O pode mapear determinadas variáveis automaticamente, mas as variáveis personalizadas devem ser mapeadas manualmente.

Para dados XDM não mapeados automaticamente para [!DNL Analytics], você pode usar [dados de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=pt-BR) para corresponder ao seu [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR). Então, ele pode ser mapeado em [!DNL Analytics] usar [regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=pt-BR) para preencher [!DNL Analytics] variáveis.

Além disso, é possível usar um conjunto padrão de ações e listas de produtos para enviar ou recuperar dados com o Adobe Experience Platform Web SDK. Para fazer isso, consulte [Coletar informações de comércio e produto](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Dados de contexto

A ser usado por [!DNL Analytics], os dados do XDM são nivelados por meio de uma notação de pontos e disponibilizados como `contextData`. A lista de pares de valores a seguir mostra um exemplo do que é `context data` parece que quando está nivelado:

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

Todos os dados coletados pela rede de borda podem ser acessados pelas [regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=pt-BR). Entrada [!DNL Analytics], você pode usar as regras de processamento para incorporar dados de contexto no [!DNL Analytics] variáveis.

Por exemplo, na regra a seguir, o Adobe Analytics é definido para preencher **Condições de pesquisa interna (eVar 2)** com os dados associados a **a.x._atag.search.term(Dados de contexto)**.

![](assets/examplerule.png)


## Esquema XDM

A Adobe Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. [!DNL Analytics] os dados de contexto funcionam com a estrutura definida pelo esquema.

O exemplo a seguir mostra como a variável [`event` comando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=pt-BR) pode ser usado com o `xdm` opção para enviar e recuperar dados com o Adobe Experience Platform Web SDK. Neste exemplo, o comando `event` corresponde ao [esquema de detalhes de comércio do ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que productListItems `name` e os valores `SKU` sejam rastreados:


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

Para obter mais informações sobre o rastreamento de eventos com o Adobe Experience Platform [!DNL Web SDK], consulte [Rastreamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=pt-BR).
