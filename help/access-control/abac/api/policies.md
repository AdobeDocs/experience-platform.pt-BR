---
keywords: Experience Platform, home, tópicos populares, api, Controle de acesso com base em atributos, controle de acesso com base em atributos
solution: Experience Platform
title: Endpoint da API de políticas
description: O endpoint /Policies na API de Controle de acesso com base em atributo permite gerenciar programaticamente as políticas no Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 3%

---

# Ponto de extremidade de políticas

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível em uma versão limitada para clientes de assistência médica com base nos EUA. Esse recurso estará disponível para todos os clientes da Real-time Customer Data Platform assim que for totalmente lançado.

Políticas são declarações que reúnem atributos para estabelecer ações admissíveis e não permissíveis. As políticas podem ser locais ou globais e podem substituir outras políticas. O `/policies` O endpoint na API de controle de acesso baseada em atributos permite gerenciar políticas de forma programática, incluindo informações sobre as regras que as regem, bem como suas respectivas condições de assunto.

## Introdução

O endpoint da API usado neste guia faz parte da API de controle de acesso baseada em atributos. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de políticas {#list}

Faça uma solicitação do GET para `/policies` endpoint para listar todas as políticas existentes na organização.

**Formato da API**

```http
GET /policies
```

**Solicitação**

A solicitação a seguir recupera uma lista de políticas existentes.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de políticas existentes.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde a uma política. Esse identificador é gerado automaticamente e pode ser usado para pesquisar, atualizar e excluir uma política. |
| `imsOrgId` | A organização na qual a política consultada está acessível. |
| `createdBy` | A ID do usuário que criou a política. |
| `createdAt` | A hora em que a política foi criada. O `createdAt` é exibida no carimbo de data e hora da época unix. |
| `modifiedBy` | A ID do usuário que atualizou a política pela última vez. |
| `modifiedAt` | A hora em que a política foi atualizada pela última vez. O `modifiedAt` é exibida no carimbo de data e hora da época unix. |
| `name` | O nome da política. |
| `description` | (Opcional) Uma propriedade que pode ser adicionada para fornecer mais informações sobre uma política específica. |
| `status` | O status atual de uma política. Esta propriedade define se uma política está atualmente `active` ou `inactive`. |
| `subjectCondition` | As condições aplicadas a um assunto. Um assunto é um usuário com determinados atributos que solicita acesso a um recurso para executar uma ação. Nesse caso, `subjectCondition` são condições semelhantes a query aplicadas aos atributos de assunto. |
| `rules` | O conjunto de regras que define uma política. As regras definem quais combinações de atributos são autorizadas para que o assunto execute com êxito uma ação no recurso. |
| `rules.effect` | O efeito que resulta após considerar os valores para `action`, `condition` e `resource`. Os valores possíveis incluem: `permit`, `deny`ou `indeterminate`. |
| `rules.resource` | O ativo ou objeto que um assunto pode ou não acessar.  Os recursos podem ser arquivos, aplicativos, servidores ou até mesmo APIs. |
| `rules.condition` | As condições aplicadas a um recurso. Por exemplo, se um recurso for um schema, um schema pode ter determinados rótulos aplicados a ele que contribuem para que uma ação contra esse schema seja permissível ou não. |
| `rules.action` | A ação que um assunto tem permissão para fazer contra um recurso consultado. Os valores possíveis incluem: `read`, `create`, `edit`e `delete`. |

## Pesquisar detalhes da política por ID {#lookup}

Faça uma solicitação do GET para `/policies` endpoint ao fornecer uma ID de política no caminho da solicitação para recuperar informações sobre essa política individual.

**Formato da API**

```http
GET /policies/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {POLICY_ID} | A ID da política que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera informações sobre uma política individual.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma solicitação bem-sucedida retorna informações sobre a ID de política consultada.

```json
{
    "id": "13138ef6-c007-495d-837f-0a248867e219",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652859368555,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652890780206,
    "name": "Documentation-Copy",
    "description": "xyz",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        },
        {
            "effect": "Deny",
            "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde a uma política. Esse identificador é gerado automaticamente e pode ser usado para pesquisar, atualizar e excluir uma política. |
| `imsOrgId` | A organização na qual a política consultada está acessível. |
| `createdBy` | A ID do usuário que criou a política. |
| `createdAt` | A hora em que a política foi criada. O `createdAt` é exibida no carimbo de data e hora da época unix. |
| `modifiedBy` | A ID do usuário que atualizou a política pela última vez. |
| `modifiedAt` | A hora em que a política foi atualizada pela última vez. O `modifiedAt` é exibida no carimbo de data e hora da época unix. |
| `name` | O nome da política. |
| `description` | (Opcional) Uma propriedade que pode ser adicionada para fornecer mais informações sobre uma política específica. |
| `status` | O status atual de uma política. Esta propriedade define se uma política está atualmente `active` ou `inactive`. |
| `subjectCondition` | As condições aplicadas a um assunto. Um assunto é um usuário com determinados atributos que solicita acesso a um recurso para executar uma ação. Nesse caso, `subjectCondition` são condições semelhantes a query aplicadas aos atributos de assunto. |
| `rules` | O conjunto de regras que define uma política. As regras definem quais combinações de atributos são autorizadas para que o assunto execute com êxito uma ação no recurso. |
| `rules.effect` | O efeito que resulta após considerar os valores para `action`, `condition` e `resource`. Os valores possíveis incluem: `permit`, `deny`ou `indeterminate`. |
| `rules.resource` | O ativo ou objeto que um assunto pode ou não acessar.  Os recursos podem ser arquivos, aplicativos, servidores ou até mesmo APIs. |
| `rules.condition` | As condições aplicadas a um recurso. Por exemplo, se um recurso for um schema, um schema pode ter determinados rótulos aplicados a ele que contribuem para que uma ação contra esse schema seja permissível ou não. |
| `rules.action` | A ação que um assunto tem permissão para fazer contra um recurso consultado. Os valores possíveis incluem: `read`, `create`, `edit`e `delete`. |


## Criar uma política {#create}

Para criar uma nova política, faça uma solicitação de POST para a `/policies` endpoint .

**Formato da API**

```http
POST /policies
```

**Solicitação**

A solicitação a seguir cria uma nova política chamada: `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "read"
          ]
        }
      ]
    }'
```

| Parâmetro | Descrição |
| --- | --- |
| `name` | O nome da política. |
| `description` | (Opcional) Uma propriedade que pode ser adicionada para fornecer mais informações sobre uma política específica. |
| `imsOrgId` | A organização que contém a política. |
| `rules` | O conjunto de regras que define uma política. As regras definem quais combinações de atributos são autorizadas para que o assunto execute com êxito uma ação no recurso. |
| `rules.effect` | O efeito que resulta após considerar os valores para `action`, `condition` e `resource`. Os valores possíveis incluem: `permit`, `deny`ou `indeterminate`. |
| `rules.resource` | O ativo ou objeto que um assunto pode ou não acessar.  Os recursos podem ser arquivos, aplicativos, servidores ou até mesmo APIs. |
| `rules.condition` | As condições aplicadas a um recurso. Por exemplo, se um recurso for um schema, um schema pode ter determinados rótulos aplicados a ele que contribuem para que uma ação contra esse schema seja permissível ou não. |
| `rules.action` | A ação que um assunto tem permissão para fazer contra um recurso consultado. Os valores possíveis incluem: `read`, `create`, `edit`e `delete`. |

**Resposta**

Uma solicitação bem-sucedida retorna a política recém-criada, incluindo sua ID de política exclusiva e regras associadas.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID que corresponde a uma política. Esse identificador é gerado automaticamente e pode ser usado para pesquisar, atualizar e excluir uma política. |
| `name` | O nome de uma política. |
| `rules` | O conjunto de regras que define uma política. As regras definem quais combinações de atributos são autorizadas para que o assunto execute com êxito uma ação no recurso. |
| `rules.effect` | O efeito que resulta após considerar os valores para `action`, `condition` e `resource`. Os valores possíveis incluem: `permit`, `deny`ou `indeterminate`. |
| `rules.resource` | O ativo ou objeto que um assunto pode ou não acessar.  Os recursos podem ser arquivos, aplicativos, servidores ou até mesmo APIs. |
| `rules.condition` | As condições aplicadas a um recurso. Por exemplo, se um recurso for um schema, um schema pode ter determinados rótulos aplicados a ele que contribuem para que uma ação contra esse schema seja permissível ou não. |
| `rules.action` | A ação que um assunto tem permissão para fazer contra um recurso consultado. Os valores possíveis incluem: `read`, `create`, `edit`e `delete`. |


## Atualizar uma política por ID de política {#put}

Para atualizar as regras de uma política individual, faça uma solicitação de PUT para a `/policies` endpoint ao fornecer a ID da política que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PUT /policies/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {POLICY_ID} | A ID da política que você deseja atualizar. |

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "read"
        ]
      }
    ]
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna a política atualizada.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Atualizar propriedades da política {#patch}

Para atualizar as propriedades de uma política individual, faça uma solicitação de PATCH para a variável `/policies` endpoint ao fornecer a ID da política que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /policies/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {POLICY_ID} | A ID da política que você deseja atualizar. |

**Solicitação**

A solicitação a seguir substitui o valor de `/description` na ID da política `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
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

Uma resposta bem-sucedida retorna a ID da política consultada com uma descrição atualizada.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Excluir uma política {#delete}

Para excluir uma política, faça uma solicitação de DELETE para a `/policies` endpoint ao fornecer a ID da política que deseja excluir.

**Formato da API**

```http
DELETE /policies/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {POLICY_ID} | A ID da política que deseja excluir. |

**Solicitação**

A solicitação a seguir exclui a política com a ID de `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a política. Você receberá um status HTTP 404 (Not Found) porque a política foi removida da administração.
