---
keywords: Experience Platform, home, tópicos populares, permissões de controle de acesso, tipos de recursos de controle de acesso, api de controle de acesso
solution: Experience Platform
title: Endpoint da API de referência
description: O endpoint de referência na API de Controle de Acesso permite exibir os nomes das permissões e dos tipos de recursos disponíveis, que podem ser usados para exibir políticas eficazes de controle de acesso para o usuário atual.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# Ponto de extremidade de referência

>[!NOTE]
>
>Se um token de usuário estiver sendo transmitido, o usuário do token deverá ter uma função &quot;org admin&quot; para a organização solicitada.

Você pode listar os nomes de todas as permissões e tipos de recursos, fazendo uma solicitação de GET para o `/acl/reference` endpoint . Esses nomes podem ser usados em chamadas de API para [exibir políticas eficazes de controle de acesso](./effective-policies.md) para o usuário atual.

Uma permissão é uma política gerenciada por meio da Adobe Admin Console e mapeia para zero ou mais políticas do tipo recurso. Um tipo de recurso é uma política que permite recursos de leitura, gravação e/ou exclusão para um tipo específico de [!DNL Platform] (como conjuntos de dados ou esquemas).

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna um `permissions` e um `resource-types` , cada um contendo uma lista completa de nomes para permissões de acesso ou tipos de recursos, respectivamente.

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
