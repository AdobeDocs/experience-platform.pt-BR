---
title: Acessar a ECID
description: Saiba como acessar a Experience Cloud ID por meio do Preparo de dados ou de Tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: 19e85ef4dbaeb90712ad9cd6ad4cb9a1a6b0c6a5
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# Acessar a ECID

O [!DNL Experience Cloud Identity (ECID)] é um identificador persistente atribuído a um usuário quando ele visita seu site. Em determinadas circunstâncias, você pode preferir acessar o [!DNL ECID] (para enviá-lo a terceiros, por exemplo). Outro caso de uso é configurar o [!DNL ECID] em um campo XDM personalizado, além de tê-lo no mapa de identidade.

Você pode acessar a ECID por meio do [Preparo de dados para a coleção de dados](/help/datastreams/data-prep.md) (recomendado) ou por meio de tags.

## Acessar a ECID por meio do Preparo de dados (método preferencial) {#accessing-ecid-data-prep}

Este método usa o [Preparo de Dados para a Coleção de Dados](/help/datastreams/data-prep.md) para configurar um mapeamento personalizado para o `ECID`.

Consulte a documentação do [Preparo de Dados para a Coleção de Dados](/help/datastreams/data-prep.md) para saber como usar este recurso.

Se você deseja definir a ECID em um campo XDM personalizado, além de tê-la no mapa de identidade, faça isso definindo o `source` para o seguinte caminho:

```js
xdm.identityMap.ECID[0].id
```

Em seguida, defina o destino como um caminho XDM, onde o campo é do tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Tags

Se você precisar acessar o [!DNL ECID] no lado do cliente, use a abordagem de tags conforme descrito abaixo.

1. Verifique se a propriedade está configurada com a habilitação da [sequência de componentes da regra](/help/tags/ui/managing-resources/rules.md#sequencing).
1. Crie uma nova regra. Esta regra deve ser usada exclusivamente para capturar o [!DNL ECID] sem nenhuma outra ação importante.
1. Adicionar um evento [!UICONTROL Library Loaded] à regra.
1. Adicione uma ação [!UICONTROL Custom Code] à regra com o seguinte código (supondo que o nome configurado para a instância do SDK seja `alloy` e já não exista um elemento de dados com o mesmo nome):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salve a regra.

Você poderá acessar [!DNL ECID] nas regras subsequentes usando `%ECID%` ou `_satellite.getVar("ECID")`, como acessaria qualquer outro elemento de dados.
