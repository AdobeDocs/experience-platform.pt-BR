---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tipos de sandbox suportados pela Lista
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 4%

---


# Tipos de sandbox suportados pela Lista

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
