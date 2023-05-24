---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;públicos-alvo;público-alvo;API;api;
title: Endpoint da API de públicos-alvo
description: O ponto de extremidade de públicos-alvo na API do serviço de segmentação do Adobe Experience Platform permite gerenciar programaticamente os públicos-alvo da sua organização.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 5%

---

# Endpoint de públicos

>[!IMPORTANT]
>
>O endpoint do público-alvo está atualmente na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Um público-alvo é uma coleção de pessoas que compartilham comportamentos e/ou características semelhantes. Essas coleções de pessoas podem ser geradas usando o Adobe Experience Platform ou de fontes externas. Você pode usar o `/audiences` endpoint na API de segmentação, que permite recuperar, criar, atualizar e excluir públicos de forma programática.

## Introdução

Os endpoints usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Recuperar uma lista de públicos {#list}

Você pode recuperar uma lista de todos os públicos-alvo de sua organização fazendo uma solicitação GET para a `/audiences` terminal.

**Formato da API**

A variável `/audiences` O endpoint oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara ao listar recursos. Se você fizer uma chamada para esse endpoint sem parâmetros, todos os públicos-alvo disponíveis para sua organização serão recuperados. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Os seguintes parâmetros de consulta podem ser usados ao recuperar uma lista de públicos-alvo:

| Parâmetro de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `start` | Especifica o deslocamento inicial dos públicos-alvo retornados. | `start=5` |
| `limit` | Especifica o número máximo de públicos-alvo retornados por página. | `limit=10` |
| `sort` | Especifica a ordem de classificação dos resultados. Isso é gravado no formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Um filtro que permite especificar públicos que **exatamente** corresponder a um valor de atributo. Isso é gravado no formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Um filtro que permite especificar públicos cujos nomes **contain** o valor fornecido. Esse valor não diferencia maiúsculas de minúsculas. | `name=Sample` |
| `description` | Um filtro que permite especificar públicos cujas descrições **contain** o valor fornecido. Esse valor não diferencia maiúsculas de minúsculas. | `description=Test Description` |
| `withMetrics` | Um filtro que retorna as métricas, além dos públicos-alvo. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Para públicos-alvo, as métricas são retornadas em `metrics` e contém informações sobre contagens de perfis, criação e carimbos de data e hora de atualização.

**Nenhuma métrica**

O seguinte par de solicitação/resposta é usado quando o `withMetrics` parâmetro de consulta ausente.

**Solicitação**

A solicitação a seguir recupera os últimos cinco públicos-alvo criados em sua organização.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Resposta** {#no-metrics}

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de públicos-alvo que foram criados em sua organização como JSON.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço e mostra apenas o primeiro público-alvo retornado.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Propriedade | Tipo de público | Descrição |
| -------- | ------------- | ----------- | 
| `id` | Ambos | Um identificador somente leitura gerado pelo sistema para o público-alvo. |
| `audienceId` | Ambos | Se o público-alvo for gerado pela Platform, ele terá o mesmo valor que o `id`. Se o público-alvo for gerado externamente, esse valor será fornecido pelo cliente. |
| `schema` | Ambos | O esquema do Experience Data Model (XDM) do público-alvo. |
| `imsOrgId` | Ambos | A ID da organização à qual o público pertence. |
| `sandbox` | Ambos | Informações sobre a sandbox à qual o público-alvo pertence. Mais informações sobre sandboxes podem ser encontradas no [visão geral das sandboxes](../../sandboxes/home.md). |
| `name` | Ambos | O nome do público-alvo. |
| `description` | Ambos | Uma descrição do público. |
| `expression` | Gerado pela plataforma | A expressão Profile Query Language (PQL) do público-alvo. Mais informações sobre expressões PQL podem ser encontradas no [Guia de expressões PQL](../pql/overview.md). |
| `mergePolicyId` | Gerado pela plataforma | A ID da política de mesclagem à qual o público-alvo está associado. Mais informações sobre políticas de mesclagem podem ser encontradas no [guia de políticas de mesclagem](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Gerado pela plataforma | Mostra como o público-alvo será avaliado. Os possíveis métodos de avaliação incluem batch, streaming ou edge. Mais informações sobre os métodos de avaliação podem ser encontradas no [visão geral da segmentação](../home.md) |
| `dependents` | Ambos | Uma matriz de IDs de público-alvo que dependem do público-alvo atual. Isso seria usado se você estivesse criando um público-alvo que é um segmento de um segmento. |
| `dependencies` | Ambos | Uma matriz de IDs de público-alvo das quais o público-alvo depende. Isso seria usado se você estivesse criando um público-alvo que é um segmento de um segmento. |
| `type` | Ambos | Um campo gerado pelo sistema que mostra se o público-alvo é gerado pela Platform ou um público-alvo gerado externamente. Os valores possíveis incluem `SegmentDefinition` e `ExternalAudience`. A `SegmentDefinition` refere-se a um público-alvo gerado na Platform, enquanto um `ExternalAudience` refere-se a um público-alvo que não foi gerado na Platform. |
| `createdBy` | Ambos | A ID do usuário que criou o público-alvo. |
| `labels` | Ambos | Uso de dados no nível do objeto e rótulos de controle de acesso baseados em atributos que são relevantes para o público-alvo. |
| `namespace` | Ambos | O namespace ao qual o público-alvo pertence. Os valores possíveis incluem `AAM`, `AAMSegments`, `AAMTraits`, e `AEPSegments`. |
| `audienceMeta` | Externo | Metadados criados externamente do público criado externamente. |

**Com métricas**

O seguinte par de solicitação/resposta é usado quando o `withMetrics` parâmetro de consulta está presente.

**Solicitação**

A solicitação a seguir recupera os últimos cinco públicos-alvo, com métricas, criados em sua organização.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de públicos-alvo, com métricas, para a organização especificada como JSON.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço e mostra apenas o primeiro público-alvo retornado.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "realized": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

As propriedades da lista a seguir **exclusivo** para o `withMetrics` resposta. Se quiser saber as propriedades padrão do público-alvo, leia a [seção anterior](#no-metrics).

| Propriedade | Descrição |
| -------- | ----------- |
| `metrics.imsOrgId` | A ID da organização do público-alvo. |
| `metrics.sandbox` | As informações de sandbox relacionadas ao público-alvo. |
| `metrics.jobId` | A ID do trabalho de segmento que está processando o público. |
| `metrics.type` | O tipo de trabalho do segmento. Isso pode ser `export` ou `batch_segmentation`. |
| `metrics.id` | A ID do público. |
| `metrics.data` | Métricas relacionadas ao público-alvo. Isso inclui informações como o número total de perfis incluídos no público-alvo, o número total de perfis por namespace e o número total de perfis por status. |
| `metrics.createEpoch` | Uma marca de data e hora que mostra quando o público-alvo foi criado. |
| `metrics.updateEpoch` | Um carimbo de data e hora que mostra quando o público foi atualizado pela última vez. |

## Crie um novo público-alvo {#create}

Você pode criar um novo público-alvo fazendo uma solicitação POST para a `/audiences` terminal.

**Formato da API**

```http
POST /audiences
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
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
| `name` | O nome do público-alvo. |
| `description` | Uma descrição do público. |
| `type` | Um campo que mostra se o público-alvo é gerado pela Platform ou um público-alvo gerado externamente. Os valores possíveis incluem `SegmentDefinition` e `ExternalAudience`. A `SegmentDefinition` refere-se a um público-alvo gerado na Platform, enquanto um `ExternalAudience` refere-se a um público-alvo que não foi gerado na Platform. |
| `expression` | A expressão Profile Query Language (PQL) do público-alvo. Mais informações sobre expressões PQL podem ser encontradas no [Guia de expressões PQL](../pql/overview.md). |
| `schema` | O esquema do Experience Data Model (XDM) do público-alvo. |
| `labels` | Uso de dados no nível do objeto e rótulos de controle de acesso baseados em atributos que são relevantes para o público-alvo. |

**Resposta**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Pesquisar um público-alvo especificado {#get}

Você pode pesquisar informações detalhadas sobre um público-alvo específico fazendo uma solicitação GET ao `/audiences` e fornecendo a ID do público-alvo que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parâmetro | Descrição |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | A ID do público-alvo que você está tentando recuperar. |
| `property=withmetrics==true` | Um parâmetro de consulta opcional que você pode usar se quiser recuperar um público especificado com as métricas de público. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o público-alvo especificado. A resposta será diferente dependendo se o público-alvo for gerado com o Adobe Experience Platform ou fontes externas.

**Gerado pela plataforma**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Gerado externamente**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Atualizar um campo em um público {#update-field}

Você pode atualizar os campos de público-alvo específico fazendo uma solicitação PATCH para o `/audiences` e fornecendo a ID do público-alvo que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{AUDIENCE_ID}` | A ID do público que você deseja atualizar. |

**Solicitação**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `op` | Para atualizar públicos-alvo, esse valor sempre é `add`. |
| `path` | O caminho do campo que você deseja atualizar. |
| `value` | O valor para o qual você deseja atualizar o campo. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o público recém-atualizado.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
        "value": "workAddress.country = \"CA\""
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
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Atualizar um público {#put}

Você pode atualizar (substituir) um público-alvo específico fazendo uma solicitação PUT para o `/audiences` e fornecendo a ID do público-alvo que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Solicitação**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `audienceId` | A ID da audiência. Isso é usado por públicos externos |
| `name` | O nome do público-alvo. |
| `namespace` |  |
| `description` | Uma descrição do público. |
| `type` | Um campo gerado pelo sistema que mostra se o público-alvo é gerado pela Platform ou um público-alvo gerado externamente. Os valores possíveis incluem `SegmentDefinition` e `ExternalAudience`. A `SegmentDefinition` refere-se a um público-alvo gerado na Platform, enquanto um `ExternalAudience` refere-se a um público-alvo que não foi gerado na Platform. |
| `lifecycle` | O status do público. Os valores possíveis incluem `draft`, `published`, `inactive`, e `archived`. `draft` representa quando o público é criado, `published` quando o público é publicado, `inactive` quando o público-alvo não estiver mais ativo e `archived` se o público for excluído. |
| `datasetId` | A ID do conjunto de dados em que os dados de público-alvo podem ser encontrados. |
| `labels` | Uso de dados no nível do objeto e rótulos de controle de acesso baseados em atributos que são relevantes para o público-alvo. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do público recém-atualizado. Observe que os detalhes do seu público-alvo serão diferentes dependendo se for um público-alvo gerado pela Platform ou um público gerado externamente.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Excluir um público {#delete}

Você pode excluir um público-alvo específico fazendo uma solicitação DELETE para a `/audiences` e fornecendo a ID do público-alvo que você deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{AUDIENCE_ID}` | A ID do público-alvo que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 sem mensagem.
