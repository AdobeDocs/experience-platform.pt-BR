---
keywords: Experience Platform, home, tópicos populares, sandboxes de lista
solution: Experience Platform
title: Listar tipos de sandbox compatíveis na API
topic: guia do desenvolvedor
description: Você pode recuperar uma lista dos tipos de sandbox suportados para sua organização fazendo uma solicitação do GET para o endpoint /sandboxTypes .
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 2%

---


# Listar tipos de sandbox compatíveis na API

Você pode recuperar uma lista dos tipos de sandbox suportados para sua organização fazendo uma solicitação de GET para o endpoint `/sandboxTypes`.

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
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de tipos de sandbox compatíveis com sua organização.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
