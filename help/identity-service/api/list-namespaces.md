---
keywords: Experience Platform, home, tópicos populares, lista de namespace, namespace de lista
solution: Experience Platform
title: Listar namespaces de identidade disponíveis
topic-legacy: API guide
description: Liste todos os namespaces disponíveis.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 5%

---

# Listar namespaces de identidade disponíveis

**Formato da API**

```http
GET /idnamespace/identities
```

**Solicitação**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui uma matriz de objetos, com cada objeto representando um namespace disponível. Os namespaces com um valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL false]&quot; são namespaces padrão, enquanto aqueles com um valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL true]&quot; são namespaces criados por sua organização.

>[!NOTE]
>
>Essa resposta foi truncada para espaço.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Próximas etapas

Prossiga para o próximo tutorial para [criar um namespace personalizado](./create-custom-namespace.md)
