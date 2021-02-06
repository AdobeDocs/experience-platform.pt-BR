---
keywords: Experience Platform;home;popular tópicos;permissões de controle de acesso;tipos de recurso de controle de acesso;controle de acesso api;topics;permissões de ;tipos de recurso de ; api
solution: Experience Platform
title: Ponto final da API de referência
topic: developer guide
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando o Adobe Admin Console. Você pode lista os nomes de todas as permissões e tipos de recursos fazendo uma solicitação de GET para o endpoint /acl/reference na API do Controle de acesso. Esses nomes podem ser usados em chamadas de API para visualização de políticas eficazes para o usuário atual.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# Ponto de extremidade de referência

Você pode lista os nomes de todas as permissões e tipos de recursos fazendo uma solicitação de GET para o terminal `/acl/reference`. Esses nomes podem ser usados em chamadas de API para [políticas eficazes de visualização](./effective-policies.md) para o usuário atual.

Uma permissão é uma política gerenciada pelo Adobe Admin Console e mapeia para zero ou mais políticas de tipo de recurso. Um tipo de recurso é uma política que permite os recursos de leitura, gravação e/ou exclusão para um tipo específico de recurso [!DNL Platform] (como conjuntos de dados ou schemas).

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

Uma resposta bem-sucedida retorna um objeto `permissions` e um objeto `resource-types`, cada um contendo uma lista completa de nomes para permissões de acesso ou tipos de recursos, respectivamente.

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
