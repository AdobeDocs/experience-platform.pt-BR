---
keywords: 'Experience Platform;home;popular topics;namespace lista;lista namespace;home;popular topics;; '
solution: Experience Platform
title: Lista de Namespaces de identidade disponíveis
topic: API guide
description: Lista todas as namespaces disponíveis.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---


# Lista de namespaces de identidade disponíveis

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

A resposta inclui uma matriz de objetos, com cada objeto representando uma namespace disponível. Namespaces com um valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL false]&quot; são namespaces padrão, enquanto aquelas com um valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL true]&quot; são namespaces que sua organização criou.

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

Vá para o próximo tutorial para [criar uma namespace personalizada](./create-custom-namespace.md)