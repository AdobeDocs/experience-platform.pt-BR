---
title: Sincronização de perfil em tempo real para mbox3rdPartyId
description: Saiba como usar mbox3rdPartyId com o SDK da Web da Adobe Experience Platform.
keywords: personalização, target, adobe target, renderDecisões, sendEvent, mbox3rdPartyId;
exl-id: null
source-git-commit: b02a7a95be33b28ab79afc7418bb3a644c417fc9
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 9%

---


# O que é o `mbox3rdPartyId`

A mbox3rdPartyId no Adobe Target é a ID de visitante de sua empresa, como a ID de associação do programa de fidelidade da empresa.

Quando um visitante faz logon no site de uma empresa, a empresa normalmente cria uma ID associada à conta, ao cartão de fidelidade, ao número de associação ou a outros identificadores aplicáveis do visitante dessa empresa. [Saiba mais](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## Como utilizar `mbox3rdPartyId` com o SDK da Web

### Etapa 1: Configure o `Target Third Party ID Namespace`

Configure o `Target Third Party ID Namespace` em seu [Datastream](../../fundamentals/datastreams.md), usando o Namespace de ID que você gostaria de usar como uma ID de terceiros da mbox.
[Saiba mais sobre namespaces de ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR)

![](assets/mbox3rdpartyid.png)

### Etapa 2: Envie o `mbox3rdpartyId` para o Target

Envie o `mbox3rdpartyId` para o Target no `sendEvent` usando o namespace da ID que você configurou na Etapa 1.
[Saiba mais sobre como enviar IDs](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


