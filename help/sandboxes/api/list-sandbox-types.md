---
keywords: Experience Platform;home;popular topics;lista sandboxes;home;popular topics; sandboxes
solution: Experience Platform
title: Lista com suporte de tipos de sandbox na API
topic: developer guide
description: Você pode recuperar uma lista de tipos de sandbox suportados para sua organização, fazendo uma solicitação de GET para o endpoint /sandboxTypes.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 2%

---


# Tipos de caixa de proteção suportados pela lista na API

Você pode recuperar uma lista de tipos de sandbox suportados para sua organização, fazendo uma solicitação de GET para o terminal `/sandboxTypes`.

**Formato da API**

```http
GET /sandboxTypes
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de tipos de caixa de proteção compatíveis com sua organização.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
