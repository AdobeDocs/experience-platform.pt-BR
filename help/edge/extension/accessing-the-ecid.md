---
title: Acessar a ECID
description: Extensão do SDK da Web da Adobe Experience Platform utilizando ECID em tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---

# Acessar a ECID

A variável [!DNL Experience Cloud Identity (ECID)] é um identificador persistente para um visitante do site. Em determinadas circunstâncias, você pode preferir acessar a ECID (para enviá-la a terceiros, por exemplo).

Para acessar a ECID nas tags, o Adobe recomenda o seguinte:

1. Verifique se a propriedade está configurada com [sequência de componentes da regra](../../tags/ui/managing-resources/rules.md#sequencing) ativado.
1. Crie uma nova regra.
1. Adicionar um [!UICONTROL Biblioteca carregada] para a regra.
1. Adicionar um [!UICONTROL Condição personalizada] à regra com o seguinte código (supondo que o nome configurado para a instância do SDK seja `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salve a regra.

Você deve poder acessar a ECID em regras subsequentes usando `%ECID%` ou `_satellite.getVar("ECID")` como você faria com qualquer outro elemento de dados.
