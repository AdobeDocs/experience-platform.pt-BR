---
title: Envio de dados para a Adobe Analytics usando o SDK da Web
description: Saiba como enviar dados para a Adobe Analytics com o SDK da Web da Adobe Experience Platform.
keywords: adobe analytics;analytics;dados mapeados;vars mapeadas;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# Enviar dados para a Adobe Analytics usando o SDK da Web

O Adobe Experience Platform Web SDK pode enviar dados para a Adobe Analytics por meio da Adobe Experience Platform Edge Network. Quando os dados chegam à rede de borda, eles traduzem o objeto XDM em um formato que a Adobe Analytics entende.

## Grupo de campos XDM

Para facilitar a captura das métricas mais comuns do Adobe Analytics, o Adobe fornece um grupo de campos direcionado para o Adobe Analytics que você pode usar. Para obter mais detalhes sobre esse esquema, consulte [Grupo de campos de esquema de Extensão completa do Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md).

## Mapeamento de variável

A Rede de borda mapeia automaticamente muitas variáveis XDM. Consulte [Mapeamento de variáveis do Analytics na rede de borda](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=pt-BR) no guia de implementação do Adobe Analytics para obter uma lista abrangente de variáveis mapeadas automaticamente.

Todas as variáveis que não são mapeadas automaticamente estão disponíveis como [Variáveis de dados de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=pt-BR). Você pode então usar [Regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) para mapear variáveis de dados de contexto para variáveis do Analytics. Por exemplo, se você tivesse um esquema XDM personalizado com aparência semelhante ao seguinte:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Em seguida, essas seriam as chaves de dados de contexto disponíveis na interface Regras de processamento:

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Com a coleção Rede de borda, todos os eventos são enviados para o Analytics e quaisquer outros serviços que você configurou para o fluxo de dados. Por exemplo, se você tiver o Analytics e o Target configurados como serviços e fizer chamadas separadas para personalização e para o Analytics, ambos os eventos serão enviados para o Analytics e o Target. Esses eventos são registrados nos relatórios do Analytics e podem afetar métricas como taxa de rejeição.

## Exibições de página e chamadas de rastreamento de link

O AppMeasurement no Adobe Analytics usa chamadas de método separadas para exibições de página ([`t()` método](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) e chamadas de rastreamento de link ([`tl()` método](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). O SDK da Web fornece apenas o [`sendEvent`](../commands/sendevent/overview.md) comando para enviar exibições de página e rastreamento de link. Os dados incluídos em um evento determinam se ele é um [exibição de página](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html?lang=pt-BR) ou um [evento de página](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) no Adobe Analytics.

Por padrão, todos os eventos são considerados exibições de página no Adobe Analytics. Se você quiser definir um evento do SDK da Web para uma chamada de rastreamento de link do Adobe Analytics, defina os seguintes campos XDM:

* **`web.webInteraction.URL`**: O URL do link.
* **`web.webInteraction.name`**: O nome da dimensão Link personalizado, Link de download ou Link de saída, dependendo do valor em `web.webInteraction.type`
* **`web.webInteraction.type`**: determina o tipo de link clicado. Os valores válidos incluem `other` (Links personalizados), `download` (Links de download) e `exit` (Links de saída).

Se você habilitar [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) no `configure` esses campos XDM serão preenchidos para você.
