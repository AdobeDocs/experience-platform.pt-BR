---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Tipos de sandbox suportados pela lista
topic: developer guide
description: Você pode recuperar uma lista de tipos de sandbox suportados para sua organização, fazendo uma solicitação de GET para o endpoint /sandboxTypes.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 2%

---


# Tipos de sandbox suportados pela lista

Você pode recuperar uma lista de tipos de caixa de proteção suportados para sua organização, fazendo uma solicitação de GET para o `/sandboxTypes` ponto de extremidade.

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
