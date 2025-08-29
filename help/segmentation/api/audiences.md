---
title: Endpoint da API de públicos-alvo
description: Use o endpoint de públicos-alvo na API do serviço de segmentação do Adobe Experience Platform para criar, gerenciar e atualizar programaticamente os públicos-alvo da sua organização.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 63fa87ac9777b3ac66d990dd4bfbd202f07b0eba
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 3%

---

# Endpoint de públicos

Um público-alvo é uma coleção de pessoas que compartilham comportamentos e/ou características semelhantes. Essas coleções de pessoas podem ser geradas usando o Adobe Experience Platform ou de fontes externas. Você pode usar o ponto de extremidade `/audiences` na API de segmentação, o que permite recuperar, criar, atualizar e excluir públicos de forma programática.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo da API.

## Recuperar uma lista de públicos {#list}

Você pode recuperar uma lista de todos os públicos-alvo de sua organização fazendo uma solicitação GET para o ponto de extremidade `/audiences`.

**Formato da API**

O ponto de extremidade `/audiences` dá suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara ao listar recursos. Se você fizer uma chamada para esse endpoint sem parâmetros, todos os públicos-alvo disponíveis para sua organização serão recuperados. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

>[!NOTE]
>
>Se você usar este ponto de extremidade sem nenhum parâmetro de consulta, os públicos-alvo inativos **não** serão retornados. No entanto, se você usar este ponto de extremidade em conjunto com o parâmetro de consulta `property=audienceId`, os públicos-alvo inativos **&#x200B;**&#x200B;serão retornados.

Os seguintes parâmetros de consulta podem ser usados ao recuperar uma lista de públicos-alvo:

| Parâmetros de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `start` | Especifica o deslocamento inicial dos públicos-alvo retornados. | `start=5` |
| `limit` | Especifica o número máximo de públicos-alvo retornados por página. | `limit=10` |
| `sort` | Especifica a ordem de classificação dos resultados. Isto foi escrito no formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Um filtro que permite especificar públicos-alvo que **exatamente** correspondam ao valor de um atributo. Isto foi escrito no formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Um filtro que permite especificar públicos-alvo cujos nomes **contenham** o valor fornecido. Esse valor não diferencia maiúsculas de minúsculas. | `name=Sample` |
| `description` | Um filtro que permite especificar públicos cujas descrições **contêm** o valor fornecido. Esse valor não diferencia maiúsculas de minúsculas. | `description=Test Description` |
| `entityType` | Um filtro que permite especificar o tipo de público-alvo que você está procurando. | `entityType=_xdm.context.account` |

**Solicitação**

A solicitação a seguir recupera os dois últimos públicos-alvo criados em sua organização.

+++Uma solicitação de amostra para recuperar uma lista de públicos-alvo.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de públicos-alvo que foram criados em sua organização como JSON.

+++Um exemplo de resposta que contém os dois últimos públicos-alvo criados que pertencem à sua organização

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "totalPages": 21,
      "sortField": "name",
      "sort": "asc", 
      "pageSize": 5,
      "limit": 5,
      "start": "0",
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Propriedade | Tipo de público-alvo | Descrição |
| -------- | ------------- | ----------- | 
| `id` | Ambos | Um identificador somente leitura gerado pelo sistema para o público-alvo. |
| `audienceId` | Ambos | Se o público for gerado pela Platform, o valor será igual ao `id`. Se o público-alvo for gerado externamente, esse valor será fornecido pelo cliente. |
| `schema` | Ambos | O esquema do Experience Data Model (XDM) do público-alvo. |
| `imsOrgId` | Ambos | A ID da organização à qual o público pertence. |
| `sandbox` | Ambos | Informações sobre a sandbox à qual o público-alvo pertence. Mais informações sobre sandboxes podem ser encontradas na [visão geral das sandboxes](../../sandboxes/home.md). |
| `name` | Ambos | O nome do público. |
| `description` | Ambos | Uma descrição do público. |
| `expression` | Gerado pela plataforma | A expressão Profile Query Language (PQL) do público-alvo. Mais informações sobre expressões PQL podem ser encontradas no [guia de expressões PQL](../pql/overview.md). |
| `mergePolicyId` | Gerado pela plataforma | A ID da política de mesclagem à qual o público-alvo está associado. Mais informações sobre políticas de mesclagem podem ser encontradas no [guia de políticas de mesclagem](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Gerado pela plataforma | Mostra como o público-alvo será avaliado. Os possíveis métodos de avaliação incluem batch, síncrono (streaming) ou contínuo (borda). Mais informações sobre os métodos de avaliação podem ser encontradas na [visão geral da segmentação](../home.md) |
| `dependents` | Ambos | Uma matriz de IDs de público-alvo que dependem do público-alvo atual. Isso seria usado se você estivesse criando um público-alvo que é um segmento de um segmento. |
| `dependencies` | Ambos | Uma matriz de IDs de público-alvo das quais o público-alvo depende. Isso seria usado se você estivesse criando um público-alvo que é um segmento de um segmento. |
| `type` | Ambos | Um campo gerado pelo sistema que mostra se o público-alvo é gerado pela Platform ou um público-alvo gerado externamente. Os valores possíveis incluem `SegmentDefinition` e `ExternalSegment`. Um `SegmentDefinition` refere-se a um público-alvo gerado na Platform, enquanto um `ExternalSegment` refere-se a um público-alvo que não foi gerado na Platform. |
| `originName` | Ambos | Um campo que se refere ao nome da origem do público-alvo. Para públicos gerados pela Platform, esse valor será `REAL_TIME_CUSTOMER_PROFILE`. Para públicos gerados no Audience Orchestration, esse valor será `AUDIENCE_ORCHESTRATION`. Para públicos gerados no Adobe Audience Manager, esse valor será `AUDIENCE_MANAGER`. Para outros públicos gerados externamente, esse valor será `CUSTOM_UPLOAD`. |
| `createdBy` | Ambos | A ID do usuário que criou o público-alvo. |
| `labels` | Ambos | Uso de dados no nível do objeto e rótulos de controle de acesso baseados em atributos que são relevantes para o público-alvo. |
| `namespace` | Ambos | O namespace ao qual o público-alvo pertence. Os valores possíveis incluem `AAM`, `AAMSegments`, `AAMTraits` e `AEPSegments`. |
| `linkedAudienceRef` | Ambos | Um objeto que contém identificadores para outros sistemas relacionados ao público-alvo. |

+++

## Criar um novo público {#create}

Você pode criar um novo público fazendo uma solicitação POST para o ponto de extremidade `/audiences`.

**Formato da API**

```http
POST /audiences
```

**Solicitação**

+++ Um exemplo de solicitação para criar um público-alvo gerado pela Platform

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "AEPSegments",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `name` | O nome do público. |
| `description` | Uma descrição do público. |
| `type` | Um campo que mostra se o público-alvo é gerado pela Platform ou um público-alvo gerado externamente. Os valores possíveis incluem `SegmentDefinition` e `ExternalSegment`. Um `SegmentDefinition` refere-se a um público-alvo gerado na Platform, enquanto um `ExternalSegment` refere-se a um público-alvo que não foi gerado na Platform. |
| `expression` | A expressão Profile Query Language (PQL) do público-alvo. Mais informações sobre expressões PQL podem ser encontradas no [guia de expressões PQL](../pql/overview.md). |
| `schema` | O esquema do Experience Data Model (XDM) do público-alvo. |
| `labels` | Uso de dados no nível do objeto e rótulos de controle de acesso baseados em atributos que são relevantes para o público-alvo. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o público recém-criado.

+++Um exemplo de resposta ao criar um público-alvo gerado pela Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Pesquisar um público-alvo especificado {#get}

Você pode pesquisar informações detalhadas sobre um público-alvo específico fazendo uma solicitação GET para o ponto de extremidade `/audiences` e fornecendo a ID do público-alvo que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | A ID do público-alvo que você está tentando recuperar. Observe que este é o campo `id`, e é **não** o campo `audienceId`. |

**Solicitação**

+++Um exemplo de solicitação para recuperar um público-alvo

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o público-alvo especificado.

+++Um exemplo de resposta ao recuperar um público-alvo gerado pela Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Substituir um público-alvo {#put}

Você pode atualizar (substituir) um público-alvo específico fazendo uma solicitação PUT para o ponto de extremidade `/audiences` e fornecendo a ID do público-alvo que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{AUDIENCE_ID}` | A ID do público que você deseja atualizar. Observe que este é o campo `id`, e é **não** o campo `audienceId`. |

**Solicitação**

+++Um exemplo de solicitação para atualizar um público-alvo inteiro.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country=\"US\""
    }
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `audienceId` | A ID da audiência. Para públicos gerados externamente, esse valor pode ser fornecido pelo usuário. |
| `name` | O nome do público. |
| `namespace` | O namespace do público. |
| `description` | Uma descrição do público. |
| `type` | Um campo gerado pelo sistema que mostra se o público-alvo é gerado pela Platform ou um público-alvo gerado externamente. Os valores possíveis incluem `SegmentDefinition` e `ExternalSegment`. `SegmentDefinition` refere-se a um público-alvo gerado no Experience Platform, enquanto `ExternalSegment` refere-se a um público-alvo que não foi gerado no Experience Platform. |
| `expression` | Um objeto que contém a expressão PQL do público-alvo. |
| `lifecycleState` | O status do público. Os valores possíveis incluem `draft`, `published` e `inactive`. `draft` representa quando o público-alvo é criado, `published` quando o público-alvo é publicado e `inactive` quando o público-alvo não está mais ativo. |
| `datasetId` | A ID do conjunto de dados em que os dados de público-alvo podem ser encontrados. |
| `labels` | Uso de dados no nível do objeto e rótulos de controle de acesso baseados em atributos que são relevantes para o público-alvo. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do público recém-atualizado. Observe que os detalhes do seu público-alvo serão diferentes dependendo se for um público-alvo gerado pela Experience Platform ou um público gerado externamente.

+++Um exemplo de resposta ao atualizar um público-alvo inteiro.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Atualizar um público {#patch}

Você pode atualizar um público-alvo específico fazendo uma solicitação PATCH para o ponto de extremidade `/audiences` e fornecendo a ID do público-alvo que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{AUDIENCE_ID}` | A ID do público que você deseja atualizar. Observe que este é o campo `id`, e é **não** o campo `audienceId`. |

**Solicitação**

+++ Um exemplo de solicitação para atualizar um público-alvo.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "op": "add",
        "path": "/lifecycleState",
        "value": "inactive"
    }
 ]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `op` | O tipo de operação PATCH executada. Para este ponto de extremidade, este valor é **sempre** `/add`. |
| `path` | O caminho do campo a ser atualizado. Campos gerados pelo sistema, como `id`, `audienceId` e `namespace` **não podem** ser editados. |
| `value` | O novo valor atribuído à propriedade especificada em `path`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com o público-alvo atualizado.

+++Um exemplo de resposta ao corrigir um campo em um público-alvo.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab5",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "inactive",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Excluir um público {#delete}

Você pode excluir um público-alvo específico fazendo uma solicitação DELETE para o ponto de extremidade `/audiences` e fornecendo a ID do público-alvo que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{AUDIENCE_ID}` | A ID do público-alvo que você deseja excluir. Observe que este é o campo `id`, e é **não** o campo `audienceId`. |

**Solicitação**

+++ Um exemplo de solicitação para excluir um público-alvo.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 sem mensagem.

## Recuperar vários públicos-alvo {#bulk-get}

Você pode recuperar vários públicos fazendo uma solicitação POST para o ponto de extremidade `/audiences/bulk-get` e fornecendo as IDs dos públicos que deseja recuperar.

**Formato da API**

```http
POST /audiences/bulk-get
```

**Solicitação**

+++ Uma solicitação de amostra para recuperar vários públicos-alvo.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 207 com informações com os públicos-alvo solicitados.

+++ Um exemplo de resposta ao recuperar vários públicos-alvo.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## Próximas etapas

Depois de ler este guia, você compreenderá melhor como criar, gerenciar e excluir públicos-alvo usando a API do Adobe Experience Platform. Para obter mais informações sobre o gerenciamento de público usando a interface do usuário, leia o [guia da interface de segmentação](../ui/overview.md).
