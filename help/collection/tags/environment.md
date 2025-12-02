---
title: ambiente
description: O ambiente de compilação que a propriedade da tag usa atualmente.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

O objeto `_satellite.environment` declara qual ambiente de compilação a propriedade de marca está usando no momento.

```js
readonly _satellite.environment: Environment
```

## Campos disponíveis

Os seguintes campos estão disponíveis ao chamar este objeto.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Nome | Tipo | Descrição |
|---|---|---|
| **`id`** | `string` | O identificador exclusivo do ambiente. Você pode localizar a ID de ambiente selecionando o ícone **[!UICONTROL Install]** em [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) na interface de marcas. |
| **`stage`** | `development \| staging \| production` | O tipo de ambiente. |
