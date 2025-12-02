---
title: empresa
description: Obtenha informações sobre a organização IMS proprietária da propriedade de tag implementada.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

O objeto `_satellite.company` exibe informações sobre a organização IMS proprietária da propriedade de marca.

```ts
readonly _satellite.company: Company
```

## Campos disponíveis

Os seguintes campos estão disponíveis ao chamar este objeto:

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Nome | Tipo | Descrição |
| --- | --- | --- |
| **`orgId`** | `string` | A ID da organização IMS da propriedade de tag. |
| **`dynamicCdnEnabled`** | `boolean` | Determina se a propriedade da tag usa o recurso de switching dinâmica de CDN da Adobe. Se definido como `true`, ele alterna automaticamente a CDN da qual um visitante solicita sua tag com base em sua localização. |
| **`cdnAllowList`** | `string[]` | As CDNs permitidas para carregar a propriedade de tag do. |

Informações semelhantes também estão contidas em `_satellite._container.company`. Consulte [`_container`](container.md) para obter mais informações.
