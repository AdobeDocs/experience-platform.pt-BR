---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Lista disponível namespace
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Lista disponível namespace

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

A resposta inclui uma matriz de objetos, com cada objeto representando uma namespace disponível. Namespaces com um valor &quot;personalizado&quot; de &quot;falso&quot; são namespaces padrão, enquanto aquelas com um valor &quot;personalizado&quot; de &quot;verdadeiro&quot; são namespaces que sua organização criou.

>[!NOTE] Essa resposta foi truncada para espaço.

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

Vá para o próximo tutorial para [criar uma namespace personalizada](./create-custom-namespace.md)