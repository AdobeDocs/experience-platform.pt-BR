---
keywords: Experience Platform;página inicial;tópicos populares;api;Controle de acesso baseado em atributo;controle de acesso baseado em atributo
solution: Experience Platform
title: Endpoint da API de Funções
description: O ponto de extremidade /roles na API de controle de acesso baseado em atributos permite gerenciar programaticamente funções no Adobe Experience Platform.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 7%

---

# Endpoint de funções

>[!NOTE]
>
>Se um token de usuário for transmitido, o usuário do token deverá ter uma função de &quot;org admin&quot; para a organização solicitada.

As funções definem o acesso que um(a) admin, especialista ou usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões, e os membros da organização podem ter uma ou mais funções atribuídas, dependendo do escopo do acesso de visualização ou gravação necessário.

O ponto de extremidade `/roles` na API de controle de acesso baseada em atributos permite gerenciar programaticamente funções em sua organização.

## Introdução

O endpoint da API usado neste guia faz parte da API de controle de acesso baseada em atributos. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de funções {#list}

Você pode listar todas as funções existentes pertencentes à sua organização fazendo uma solicitação GET para o ponto de extremidade `/roles`.

**Formato da API**

```http
GET /roles/
```

**Solicitação**

A solicitação a seguir recupera uma lista de funções pertencentes à sua organização.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de funções na organização, incluindo informações sobre o respectivo tipo de função, conjuntos de permissões e atributos de assunto.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde à função. Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes na organização que são provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos do Experience Platform aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à atribuição consultada. |

## Pesquisar uma função {#lookup}

Você pode pesquisar uma função individual fazendo uma solicitação GET que inclua o `roleId` correspondente no caminho da solicitação.

**Formato da API**

```http
GET /roles/{ROLE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera informações de `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes da ID de função consultada, incluindo informações sobre o tipo de função, conjuntos de permissões e atributos de assunto.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde à função. Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes na organização que são provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos do Experience Platform aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à atribuição consultada. |

## Pesquisar assuntos por ID de função

Você também pode recuperar assuntos fazendo uma solicitação GET para o ponto de extremidade `/roles` ao fornecer um {ROLE_ID}.

**Formato da API**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função associada aos assuntos que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera assuntos associados a `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os assuntos associados à ID de função consultada, incluindo a ID de assunto e o tipo de assunto correspondentes.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `roleId` | A ID de função associada ao assunto consultado. |
| `subjectType` | O tipo do assunto consultado. |
| `subjectId` | A ID que corresponde ao assunto consultado. |

## Criar uma função {#create}

Para criar uma nova função, faça uma solicitação POST para o ponto de extremidade `/roles` enquanto fornece valores para o nome, a descrição e o tipo de função da sua função.

**Formato da API**

```http
POST /roles/
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua função. Certifique-se de que o nome da sua função seja descritivo, pois você pode usá-lo para pesquisar informações sobre sua função. |
| `description` | (Opcional) Um valor descritivo que você pode incluir para fornecer mais informações sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |

**Resposta**

Uma resposta bem-sucedida retorna a função recém-criada, com a ID de função correspondente, bem como informações sobre o tipo de função, os conjuntos de permissões e os atributos do assunto.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde à função. Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes na organização que são provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos do Experience Platform aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à atribuição consultada. |

## Atualizar uma função {#patch}

Você pode atualizar as propriedades de uma função fazendo uma solicitação PATCH para o ponto de extremidade `/roles` enquanto fornece a ID de função e os valores correspondentes para as operações que você deseja aplicar.

**Formato da API**

```http
PATCH /roles/{ROLE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função que você deseja atualizar. |

**Solicitação**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| Operações | Descrição |
| --- | --- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar a função. As operações incluem: `add`, `replace` e `remove`. |
| `path` | O caminho do parâmetro a ser atualizado. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a função atualizada, incluindo novos valores para as propriedades que você optou por atualizar.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde à função. Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes na organização que são provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos do Experience Platform aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à atribuição consultada. |

## Atualizar uma função por ID de função {#put}

Você pode atualizar uma função fazendo uma solicitação PUT para o ponto de extremidade `/roles` e especificando a ID da função que corresponde à função que você deseja atualizar.

**Formato da API**

```http
PUT /roles/{ROLE_ID}
```

**Solicitação**

A solicitação a seguir atualiza o nome, a descrição e o tipo de função para a ID de função: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `name` | O nome atualizado de uma função. |
| `description` | A descrição atualizada de uma função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |

**Resposta**

Uma resposta bem-sucedida retorna a função atualizada, incluindo novos valores para o nome, a descrição e o tipo de função.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde à função. Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes na organização que são provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos do Experience Platform aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à atribuição consultada. |

## Atualizar assunto por ID de função

Para atualizar os assuntos associados a uma função, faça uma solicitação PATCH para o ponto de extremidade `/roles` enquanto fornece a ID de função dos assuntos que você deseja atualizar.

**Formato da API**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função associada aos assuntos que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os assuntos associados a `{ROLE_ID}`.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Operações | Descrição |
| --- | --- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar a função. As operações incluem: `add`, `replace` e `remove`. |
| `path` | O caminho do parâmetro a ser atualizado. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna sua função atualizada, incluindo novos valores para os assuntos.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Excluir uma função {#delete}

Para excluir uma função, faça uma solicitação DELETE para o ponto de extremidade `/roles` enquanto especifica a ID da função que você deseja excluir.

**Formato da API**

```http
DELETE /roles/{ROLE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função que você deseja excluir. |

**Solicitação**

A solicitação a seguir exclui a função com a ID de `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a função. Você receberá um status HTTP 404 (Não encontrado) porque a função foi removida da administração.

## Adicionar uma credencial de API {#apicredential}

Para adicionar uma credencial de API, faça uma solicitação PATCH para o ponto de extremidade `/roles` ao fornecer a ID de função dos assuntos.

**Formato da API**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Operações | Descrição |
| --- | --- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar a função. As operações incluem: `add`, `replace` e `remove`. |
| `path` | O caminho do parâmetro a ser adicionado. |
| `value` | O valor com o qual você deseja adicionar o parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.
