---
title: sincronização de perfil em tempo real para mbox3rdPartyId
description: Saiba como usar mbox3rdPartyId com o Adobe Experience Platform Web SDK.
keywords: personalização;destino;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---

# O que é `mbox3rdPartyId`

A mbox3rdPartyId no Adobe Target é a ID de visitante de sua empresa, como a ID de associação do programa de fidelidade da empresa.

Quando um visitante faz logon no site de uma empresa, a empresa normalmente cria uma ID vinculada à conta, ao cartão de fidelidade, ao número de associado ou a outros identificadores aplicáveis do visitante dessa empresa. [Saiba mais](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## Como usar o `mbox3rdPartyId` com o SDK da Web

### Etapa 1: configurar o `Target Third Party ID Namespace`

Configure o `Target Third Party ID Namespace` na sua [Sequência de dados](../../../datastreams/overview.md), usando o Namespace de ID que você deseja usar como uma ID de terceiros para a mbox.
[Saiba mais sobre namespaces de ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR)

![Interface do usuário da plataforma mostrando o campo de namespace da ID de terceiros do Target.](assets/mbox3rdpartyid.png)

### Etapa 2: Enviar o `mbox3rdpartyId` para o Target

Enviar o `mbox3rdpartyId` para o Target no comando `sendEvent`, usando o namespace de ID que você configurou na Etapa 1.
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
