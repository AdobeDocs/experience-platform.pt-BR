---
title: Envio de dados para a Adobe Analytics usando o SDK da Web
description: Saiba como enviar dados para a Adobe Analytics com o SDK da Web da Adobe Experience Platform.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Enviar dados para a Adobe Analytics usando o SDK da Web

O SDK da Web do Experience Platform pode enviar dados para o Adobe Analytics por meio do Edge Network de Experience Platform. O Adobe fornece várias opções para enviar dados para o Adobe Analytics usando o SDK da Web:

* Adicione o [**[!UICONTROL grupo de campos do Adobe Analytics ExperienceEvent]**](../../xdm/field-groups/event/analytics-full-extension.md) ao esquema e use o [`XDM` objeto](../commands/sendevent/xdm.md).
* Use o objeto [`data` &#x200B;](../commands/sendevent/data.md) para enviar dados para a Adobe Analytics sem um esquema XDM.
* Use [variáveis de dados de contexto](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/page-vars/contextdata) e [regras de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) geradas automaticamente.

## Usar o objeto `XDM` {#use-xdm-object}

Se quiser usar um esquema predefinido específico do Adobe Analytics, você pode adicionar o [grupo de campos do esquema do Adobe Analytics ExperienceEvent](../../xdm/field-groups/event/analytics-full-extension.md) ao seu esquema. Depois de adicionado, é possível preencher esse esquema usando o objeto `xdm` no SDK da Web para enviar dados a um conjunto de relatórios. Quando os dados chegam ao Edge Network, eles traduzem o objeto XDM em um formato que o Adobe Analytics entende.

Há duas maneiras de enviar dados para a Adobe Analytics por meio do SDK da Web:

* [Enviar dados para a Adobe Analytics usando a extensão de tag do SDK da Web](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Enviar dados para a Adobe Analytics usando a biblioteca JavaScript do SDK da Web](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Consulte [Mapeamento da variável de objeto XDM para o Adobe Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/aep-edge/xdm-var-mapping) no guia de implementação do Adobe Analytics para obter uma referência completa dos campos XDM e como eles são mapeados para variáveis do Analytics.

## Usar o objeto `data` {#use-data-object}

Como alternativa ao uso do objeto XDM, você pode usar o objeto de dados. O objeto de dados é direcionado para implementações que atualmente usam o AppMeasurement, tornando a atualização para o SDK da Web muito mais fácil.

Dependendo de você estar usando o AppMeasurement ou a extensão de tag do Analytics, consulte os guias a seguir para obter detalhes sobre como migrar para o SDK da Web:

* [Migrar da extensão de marca do Adobe Analytics para a extensão de marca do SDK da Web](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migrar do AppMeasurement para o SDK da Web](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Consulte a documentação sobre [mapeamento de variáveis de objetos de dados para o Adobe Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/aep-edge/data-var-mapping) no guia de implementação do Adobe Analytics para obter uma referência completa dos campos de objetos de dados e como eles são mapeados para variáveis do Analytics.

## Usar variáveis de dados de contexto {#use-context-data-variables}

Todas as variáveis que não são mapeadas automaticamente estão disponíveis como [variáveis de dados de contexto](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/page-vars/contextdata). Em seguida, você pode usar [regras de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) para mapear variáveis de dados de contexto para variáveis do Analytics. Por exemplo, se você tivesse um esquema XDM personalizado com aparência semelhante ao seguinte:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

Em seguida, esses campos seriam as chaves de dados de contexto disponíveis na interface Regras de processamento:

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## Perguntas frequentes

+++Como faço para diferenciar chamadas de exibição de página de chamadas de rastreamento de link no SDK da Web?

O AppMeasurement no Adobe Analytics usa chamadas de método separadas para exibições de página ([`t()` método](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/functions/t-method)) e chamadas de rastreamento de link ([`tl()` método](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/functions/tl-method)). O SDK da Web fornece apenas o comando [`sendEvent`](../commands/sendevent/overview.md) para enviar exibições de página e rastreamento de link. Os dados incluídos em um evento determinam se é uma [exibição de página](https://experienceleague.adobe.com/pt-br/docs/analytics/components/metrics/page-views) ou um [evento de página](https://experienceleague.adobe.com/pt-br/docs/analytics/components/metrics/page-events) no Adobe Analytics.

Por padrão, todos os eventos são considerados exibições de página no Adobe Analytics. Se você quiser definir um evento do SDK da Web para uma chamada de rastreamento de link do Adobe Analytics, defina os seguintes campos:

* **objeto XDM**: `xdm.web.webInteraction.name`, `web.webInteraction.type` e `web.webInteraction.URL`
* **Objeto de dados**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType` e `data.__adobe.analytics.linkURL`
* **Dados de contexto**: sem suporte

Consulte o [`tl()` método](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/functions/tl-method) no guia de implementação do Adobe Analytics para obter mais informações.

Se você habilitar [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) no comando `configure`, esses campos serão preenchidos para você.

+++

+++Como um fluxo de dados diferencia dados de outros serviços com dados destinados ao Adobe Analytics?

Todos os eventos enviados para um fluxo de dados são passados para todos os serviços configurados. Por exemplo, se você fizer chamadas separadas para personalização e Analytics, ambos os eventos serão enviados para o Analytics e Target. Esses eventos são registrados nos relatórios do Analytics e podem afetar métricas como taxa de rejeição.

Se você usar o SDK da Web, essas chamadas normalmente são combinadas no comando [`sendEvent`](../commands/sendevent/overview.md).

+++
