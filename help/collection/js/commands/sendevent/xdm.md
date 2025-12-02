---
title: xdm
description: Saiba como enviar dados para o Adobe por meio do objeto alinhado ao esquema XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

O objeto `xdm` contém a carga de dados enviada para o Adobe. Os campos definidos nesse objeto são mapeados diretamente para elementos definidos no esquema do conjunto de dados.

A Adobe Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Defina o objeto `xdm` ao executar o comando `sendEvent`. Verifique se a hierarquia nesse objeto corresponde ao esquema do conjunto de dados configurado. Você pode incluir os objetos `xdm` e [`data`](data.md) no mesmo comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

O exemplo a seguir usa o [grupo de campos de esquema de Detalhes do Commerce](/help/xdm/field-groups/event/commerce-details.md):

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```

## Usar o objeto `xdm` usando a extensão de tag do Web SDK

O objeto `xdm` está disponível como um [elemento de dados de variável](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) ou [elemento de dados de objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) ao usar a extensão de marca Web SDK. A Adobe recomenda usar um elemento de dados variável na maioria dos casos.
