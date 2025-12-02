---
title: getVisitorId
description: Recupere a instância da extensão da tag de serviço da Experience Cloud Visitor ID.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# `getVisitorId()`

O método `_satellite.getVisitorId()` retorna uma instância do [serviço de Adobe Experience Cloud ID](https://experienceleague.adobe.com/pt-br/docs/id-service/using/home) na propriedade de marca, **se** você tiver a extensão do serviço de ID instalada e publicada. Esse método é útil quando você deseja acesso direto à instância da ID de visitante para uso em blocos de código personalizados, configuração avançada de elementos de dados ou solução de problemas de identidade do visitante.

>[!IMPORTANT]
>
>Esse método se aplica somente às propriedades que incluem a extensão independente da tag de serviço da Experience Cloud ID. Isso não se aplica aos recursos do serviço de ID implícito disponíveis na extensão de tag da Web SDK. Consulte o comando [`getIdentity`](/help/collection/js/commands/getidentity.md) se precisar obter uma identidade de visitante usando os recursos do serviço de ID implícita do Web SDK.

Se você chamar este método com a extensão do serviço de ID instalada e publicada, um objeto será retornado semelhante ao objeto obtido após chamar o método [`Visitor.getInstance()`](https://experienceleague.adobe.com/pt-br/docs/id-service/using/id-service-api/methods/getinstance). Se você chamar este método quando a extensão do serviço de ID não estiver instalada ou publicada, o método retornará `null`.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Campos e métodos disponíveis

Consulte os [Métodos](https://experienceleague.adobe.com/pt-br/docs/id-service/using/id-service-api/methods/get-set) do serviço de ID da Experience Cloud na documentação do serviço de ID de visitante da Experience Cloud para ver quais campos e métodos estão disponíveis para você.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
