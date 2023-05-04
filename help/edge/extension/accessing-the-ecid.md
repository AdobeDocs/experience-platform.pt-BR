---
title: Acesso à ECID
description: Saiba como acessar a ID do Experience Cloud por meio de Preparação de dados ou Tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# Acesso à ECID

O [!DNL Experience Cloud Identity (ECID)] é um identificador persistente atribuído a um usuário quando ele visita seu site. Em determinadas circunstâncias, você pode preferir acessar a variável [!DNL ECID] (para enviá-lo a terceiros, por exemplo). Outro caso de uso é definir a variável [!DNL ECID] em um campo XDM personalizado, além de tê-lo no mapa de identidade.

Você pode acessar a ECID por meio de [Preparação de dados para coleta de dados](../datastreams/data-prep.md) (recomendado) ou por meio de tags .

## Acesso à ECID por meio da Preparação de dados (método preferido) {#accessing-ecid-data-prep}

Se você deseja definir a ECID em um campo XDM personalizado, além de tê-la no mapa de identidade, é possível fazer isso definindo a variável `source` para o seguinte caminho:

```js
xdm.identityMap.ECID[0].id
```

Em seguida, defina o destino para um caminho XDM, onde o campo é do tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Tags

Se precisar acessar o [!DNL ECID] no lado do cliente, use a abordagem de tags , conforme descrito abaixo.

1. Certifique-se de que sua propriedade esteja configurada com [sequenciamento de componentes da regra](../../tags/ui/managing-resources/rules.md#sequencing) habilitado.
1. Crie uma nova regra.
1. Adicione um [!UICONTROL Biblioteca carregada] à regra.
1. Adicione um [!UICONTROL Condição personalizada] para a regra com o seguinte código (supondo que o nome que você configurou para a instância do SDK seja `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salve a regra.

Você deve ser capaz de acessar a variável [!DNL ECID] em regras subsequentes que utilizem `%ECID%` ou `_satellite.getVar("ECID")`, como você acessaria qualquer outro elemento de dados.
