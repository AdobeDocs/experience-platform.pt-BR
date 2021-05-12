---
title: 'Acesso à ECID '
description: Extensão do Adobe Experience Platform Web SDK aproveitando a ECID no Adobe Experience Platform Launch
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---


# Acesso à ECID

O [!DNL Experience Cloud Identity (ECID)] é um identificador persistente para um visitante do site. Em determinadas circunstâncias, você pode preferir acessar a ECID (para enviá-la a um terceiro, por exemplo).

Para acessar a ECID no Adobe Experience Platform Launch, o Adobe recomenda o seguinte:

1. Certifique-se de que a propriedade esteja configurada com a [sequência de componentes da regra](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) ativada.
1. Crie uma nova regra.
1. Adicione um evento [!UICONTROL Library Loaded] à regra.
1. Adicione uma ação [!UICONTROL Custom Condition] à regra com o seguinte código (supondo que o nome que você configurou para a instância do SDK seja `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salve a regra.

Você deve então ser capaz de acessar a ECID nas regras subsequentes usando `%ECID%` ou `_satellite.getVar("ECID")` como você faria com qualquer outro elemento de dados.
