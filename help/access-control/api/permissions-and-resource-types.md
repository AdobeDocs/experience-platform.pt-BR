---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso permissões;controle de acesso tipos de recurso;api de controle de acesso
solution: Experience Platform
title: Endpoint de API de referência
description: O endpoint de referência na API de Controle de acesso permite exibir os nomes das permissões e dos tipos de recursos disponíveis, que podem ser usados para exibir políticas de controle de acesso eficazes para o usuário atual.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# Endpoint de referência

>[!NOTE]
>
>Se um token de usuário for transmitido, o usuário do token deverá ter uma função de &quot;org admin&quot; para a organização solicitada.

Você pode listar os nomes de todas as permissões e tipos de recursos fazendo uma solicitação GET para o ponto de extremidade `/acl/reference`. Esses nomes podem ser usados em chamadas de API para [exibir as políticas de controle de acesso efetivo](./effective-policies.md) para o usuário atual.

Uma permissão é uma política gerenciada por meio da Adobe Admin Console e mapeada para zero ou mais políticas do tipo recurso. Um tipo de recurso é uma política que habilita recursos de leitura, gravação e/ou exclusão para um tipo específico de recurso [!DNL Platform] (como conjuntos de dados ou esquemas).

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
