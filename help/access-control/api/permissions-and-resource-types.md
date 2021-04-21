---
keywords: Experience Platform, home, tópicos populares, permissões de controle de acesso, tipos de recursos de controle de acesso, api de controle de acesso
solution: Experience Platform
title: Endpoint da API de referência
topic-legacy: developer guide
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando a Adobe Admin Console. Você pode listar os nomes de todas as permissões e tipos de recursos fazendo uma solicitação do GET para o endpoint /acl/reference na API de Controle de Acesso. Esses nomes podem ser usados em chamadas de API para exibir políticas eficazes para o usuário atual.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# Ponto de extremidade de referência

Você pode listar os nomes de todas as permissões e tipos de recursos fazendo uma solicitação de GET para o endpoint `/acl/reference`. Esses nomes podem ser usados em chamadas de API para [visualizar políticas efetivas](./effective-policies.md) para o usuário atual.

Uma permissão é uma política gerenciada por meio da Adobe Admin Console e mapeia para zero ou mais políticas do tipo recurso. Um tipo de recurso é uma política que permite recursos de leitura, gravação e/ou exclusão para um tipo específico de recurso [!DNL Platform] (como conjuntos de dados ou esquemas).

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
