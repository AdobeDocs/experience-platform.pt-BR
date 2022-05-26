---
keywords: Experience Platform, home, tópicos populares, api, Controle de acesso com base em atributos, controle de acesso com base em atributos
solution: Experience Platform
title: Ponto de Extremidade da API de Funções
description: O endpoint /funções na API de Controle de Acesso Baseado em Atributo permite gerenciar programaticamente funções no Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 4%

---

# Ponto de extremidade de funções

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível em uma versão limitada para clientes de assistência médica com base nos EUA. Esse recurso estará disponível para todos os clientes da Real-time Customer Data Platform assim que for totalmente lançado.

As funções definem o acesso que um administrador, especialista ou usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões e os membros da organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de acesso de exibição ou gravação necessário.

O `/roles` O endpoint na API de controle de acesso baseada em atributos permite gerenciar programaticamente as funções em sua organização.

## Introdução

O endpoint da API usado neste guia faz parte da API de controle de acesso baseada em atributos. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de funções {#list}

Você pode listar todas as funções existentes que pertencem à sua organização, fazendo uma solicitação do GET para a `/roles` endpoint .

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

Uma resposta bem-sucedida retorna uma lista de funções em sua organização, incluindo informações sobre os respectivos tipos de função, conjuntos de permissões e atributos de assunto.

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
| `id` | A ID que corresponde à função . Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas a partir de uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes dentro da organização que foram provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos da Plataforma aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à função consultada. |

## Procurar uma função {#lookup}

Você pode pesquisar uma função individual fazendo uma solicitação do GET que inclui o `roleId` no caminho da solicitação.

**Formato da API**

```http
GET /roles/{ROLE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera informações para `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes para a ID de função consultada, incluindo informações sobre o tipo de função, conjuntos de permissões e atributos de assunto.

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
| `id` | A ID que corresponde à função . Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas a partir de uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes dentro da organização que foram provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos da Plataforma aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à função consultada. |

## Pesquisar assuntos por ID de função

Também é possível recuperar assuntos fazendo uma solicitação do GET para o `/roles` endpoint ao fornecer um {ROLE_ID}.

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

Uma resposta bem-sucedida retorna os assuntos associados à ID de função consultada, incluindo a ID de assunto correspondente e o tipo de assunto.

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

Para criar uma nova função, faça uma solicitação de POST para a função `/roles` endpoint enquanto fornece valores para o nome, a descrição e o tipo da função da sua função.

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
| `description` | (Opcional) Um valor descritivo que pode ser incluído para fornecer mais informações sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |

**Resposta**

Uma resposta bem-sucedida retorna sua função recém-criada, com sua ID de função correspondente, bem como informações sobre seu tipo de função, conjuntos de permissões e atributos de assunto.

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
| `id` | A ID que corresponde à função . Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas a partir de uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes dentro da organização que foram provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos da Plataforma aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à função consultada. |

## Atualizar uma função {#patch}

Você pode atualizar as propriedades de uma função fazendo uma solicitação de PATCH para a função `/roles` endpoint ao fornecer a ID da função correspondente e os valores para as operações que deseja aplicar.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar a função. As operações incluem: `add`, `replace`e `remove`. |
| `path` | O caminho do parâmetro a ser atualizado. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a função atualizada, incluindo novos valores para as propriedades que você escolheu atualizar.

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
| `id` | A ID que corresponde à função . Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas a partir de uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes dentro da organização que foram provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos da Plataforma aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à função consultada. |

## Atualizar uma função por ID de função {#put}

Você pode atualizar uma função fazendo uma solicitação de PUT para o `/roles` endpoint e especificando a ID da função que corresponde à função que deseja atualizar.

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

Um bem-sucedido retorna sua função atualizada, incluindo novos valores para seu nome, descrição e tipo de função.

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
| `id` | A ID que corresponde à função . Essa ID é gerada automaticamente. |
| `name` | O nome da sua função. |
| `description` | A propriedade description fornece informações adicionais sobre sua função. |
| `roleType` | O tipo designado da função. Os valores possíveis para o tipo de função são: `user-defined` e `system-defined`. |
| `permissionSets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas a partir de uma função predefinida que contém um grupo de permissões. |
| `sandboxes` | Essa propriedade exibe as sandboxes dentro da organização que foram provisionadas para uma função específica. |
| `subjectAttributes` | Os atributos que indicam a correlação entre um assunto e os recursos da Plataforma aos quais eles têm acesso. |
| `subjectAttributes.labels` | Exibe os rótulos de uso de dados aplicados à função consultada. |

## Atualizar assunto por ID de função

Para atualizar os assuntos associados a uma função, faça uma solicitação de PATCH para a função `/roles` endpoint ao fornecer a ID da função dos assuntos que deseja atualizar.

**Formato da API**

```http
PATCH /roles/{ROLE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {ROLE_ID} | A ID da função associada aos assuntos que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os assuntos associados ao `{ROLE_ID}`.

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
        "path": "/subjects",
        "value": "New subjects"
      }
    ]
  }'
```

| Operações | Descrição |
| --- | --- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar a função. As operações incluem: `add`, `replace`e `remove`. |
| `path` | O caminho do parâmetro a ser atualizado. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna os assuntos atualizados associados à ID de função consultada.

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `subjectId` | A ID de um assunto. |
| `subjectType` | O tipo de assunto. |

## Excluir uma função {#delete}

Para excluir uma função, faça uma solicitação de DELETE para a função `/roles` endpoint ao especificar a ID da função que deseja excluir.

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

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a função. Você receberá um status HTTP 404 (Not Found) porque a função foi removida da administração.
