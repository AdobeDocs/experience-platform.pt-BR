---
title: Acesso à ECID
description: Saiba como acessar a Experience Cloud ID (ECID) nas tags do Adobe Experience Platform
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 5%

---


# Acesso à ECID

O [!DNL Experience Cloud ID (ECID)] é um identificador de Experience Cloud persistente que pode ajudar você a identificar visitantes do site. Em determinadas circunstâncias, como enviar o identificador para uma plataforma de terceiros, talvez seja necessário acessar o [!DNL ECID].

Para acessar o [!DNL ECID] nas tags , siga as etapas abaixo:

1. Certifique-se de que sua propriedade esteja configurada com [sequenciamento de componentes da regra](../../tags/ui/managing-resources/rules.md#sequencing) habilitado.
2. Crie uma nova regra.
3. Adicione um [!UICONTROL Biblioteca carregada] à regra.
4. Adicione um [!UICONTROL Condição personalizada] à regra, com o seguinte código (supondo que o nome que você configurou para a instância do SDK seja `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Salve a regra.

Agora você deve conseguir acessar a variável [!DNL ECID] nas regras subsequentes, usando `%ECID%` ou `_satellite.getVar("ECID")`, semelhante à forma como você acessa qualquer outro elemento de dados.
