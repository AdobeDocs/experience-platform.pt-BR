---
title: xdm
description: O objeto alinhado ao esquema enviado para o Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# `xdm`

A variável `xdm` objeto contém a carga de dados enviada para o Adobe. Os campos definidos nesse objeto são mapeados diretamente para elementos definidos no esquema do conjunto de dados.

A Adobe Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Este campo tem um limite máximo de 32 KB.

## Configurar o objeto XDM usando a extensão SDK da Web

Defina o **[!UICONTROL XDM]** nas ações de uma regra de tag. A variável [Objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) O fornece uma interface intuitiva para mapear outros elementos de dados para seus respectivos campos XDM.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Forneça o elemento de dados que contém o objeto desejado na variável **[!UICONTROL XDM]** campo.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Configurar o objeto XDM usando a biblioteca JavaScript do SDK da Web

Defina o `xdm` ao executar o `sendEvent` comando. Verifique se a hierarquia nesse objeto corresponde ao esquema do conjunto de dados configurado. É possível incluir os `xdm` e o [`data`](data.md) objeto no mesmo `sendEvent` comando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

O exemplo a seguir usa o [Grupo de campos de esquema de Detalhes do comércio](/help/xdm/field-groups/event/commerce-details.md):

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
