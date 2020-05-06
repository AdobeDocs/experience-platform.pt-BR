---
title: Recuperando a Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK para recuperação da Experience Cloud ID
description: Saiba como obter a Adobe Experience Cloud Id.
seo-description: Saiba como obter a Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 13%

---


# (Beta) Recuperando a Experience Cloud ID

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A Adobe Experience Cloud usa uma ID exclusiva para cada consumidor. Se você quiser usar essa ID exclusiva, use o `getIdentity` comando. `getIdentity` retorna o ECID existente para o visitante atual. Para visitantes que ainda não têm um ECID, este comando gera um novo ECID.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da Experience Cloud ID. Ela não é usada em uma implementação padrão.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
