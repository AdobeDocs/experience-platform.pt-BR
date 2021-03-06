---
title: 'Acesso à ECID '
description: Extensão do SDK da Web da Adobe Experience Platform aproveitando a ECID nas tags
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---


# Acesso à ECID

O [!DNL Experience Cloud Identity (ECID)] é um identificador persistente para um visitante do site. Em determinadas circunstâncias, você pode preferir acessar a ECID (para enviá-la a um terceiro, por exemplo).

Para acessar a ECID nas tags, o Adobe recomenda o seguinte:

1. Certifique-se de que a propriedade esteja configurada com a [sequência de componentes da regra](../../tags/ui/managing-resources/rules.md#sequencing) ativada.
1. Crie uma nova regra.
1. Adicione um evento [!UICONTROL Biblioteca carregada] à regra.
1. Adicione uma ação [!UICONTROL Condição personalizada] à regra com o seguinte código (supondo que o nome que você configurou para a instância do SDK seja `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salve a regra.

Você deve então ser capaz de acessar a ECID nas regras subsequentes usando `%ECID%` ou `_satellite.getVar("ECID")` como você faria com qualquer outro elemento de dados.
