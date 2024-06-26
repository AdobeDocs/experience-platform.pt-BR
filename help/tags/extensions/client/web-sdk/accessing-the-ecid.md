---
title: Acessar a ECID
description: Saiba como acessar a ID de Experience Cloud de Preparo de dados ou Tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# Acessar a ECID

A variável [!DNL Experience Cloud Identity (ECID)] é um identificador persistente atribuído a um usuário quando ele visita seu site. Em determinadas circunstâncias, você pode preferir acessar a variável [!DNL ECID] (para enviá-lo a terceiros, por exemplo). Outro caso de uso é definir o [!DNL ECID] em um campo XDM personalizado, além de tê-lo no mapa de identidade.

Você pode acessar a ECID por meio de [Preparação de dados para coleção de dados](../../../../datastreams/data-prep.md) (recomendado) ou por meio de tags.

## Acessar a ECID por meio do Preparo de dados (método preferencial) {#accessing-ecid-data-prep}

Se você deseja definir a ECID em um campo XDM personalizado, além de tê-la no mapa de identidade, é possível fazer isso definindo o campo `source` ao seguinte caminho:

```js
xdm.identityMap.ECID[0].id
```

Em seguida, defina o destino como um caminho XDM, no qual o campo seja do tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Tags

Se você precisar acessar o [!DNL ECID] no lado do cliente, use a abordagem de tags conforme descrito abaixo.

1. Verifique se a propriedade está configurada com [sequência de componentes da regra](../../../ui/managing-resources/rules.md#sequencing) ativado.
1. Crie uma nova regra. Essa regra deve ser usada exclusivamente para capturar a variável [!DNL ECID] sem quaisquer outras ações importantes.
1. Adicionar um [!UICONTROL Biblioteca carregada] para a regra.
1. Adicionar um [!UICONTROL Custom Code] à regra com o seguinte código (supondo que o nome configurado para a instância do SDK seja `alloy` e ainda não houver um elemento de dados com o mesmo nome):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salve a regra.

Você deverá poder acessar a variável [!DNL ECID] em regras subsequentes usando `%ECID%` ou `_satellite.getVar("ECID")`, como você acessaria qualquer outro elemento de dados.
