---
keywords: Experience Platform;home;popular topics;access control permissions;access control resource types;access control api
solution: Experience Platform
title: Nomes de listas de permissões e tipos de recursos
topic: developer guide
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando o Adobe Admin Console. Você pode lista os nomes de todas as permissões e tipos de recursos fazendo uma solicitação de GET para o endpoint /acl/reference. Esses nomes podem ser usados em chamadas de API para visualização de políticas eficazes para o usuário atual.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# Nomes de listas de permissões e tipos de recursos

Você pode lista os nomes de todas as permissões e tipos de recursos, fazendo uma solicitação de GET para o `/acl/reference` endpoint. Esses nomes podem ser usados em chamadas de API para [visualização de políticas](./effective-policies.md) eficazes para o usuário atual.

Uma **permissão** é uma política gerenciada pelo Adobe Admin Console e mapeia para zero ou mais políticas de tipo de recurso. Um tipo **de** recurso é uma política que permite os recursos de leitura, gravação e/ou exclusão para um tipo específico de [!DNL Platform] recurso (como conjuntos de dados ou schemas).

**Formato da API**

```http
GET /acl/reference
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna um `permissions` objeto e um `resource-types` objeto, cada um contendo uma lista completa de nomes para permissões de acesso ou tipos de recursos, respectivamente.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
