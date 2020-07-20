---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definições de segmento
topic: developer guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 4%

---


# Ponto de extremidade de definições de segmentos

O Adobe Experience Platform permite criar segmentos que definem um grupo de atributos ou comportamentos específicos a partir de um grupo de perfis. Uma definição de segmento é um objeto que encapsula um query gravado em [!DNL Profile Query Language] (PQL). Esse objeto também é chamado de predicado PQL. Os predicados de PQL definem as regras para o segmento com base nas condições relacionadas a qualquer registro ou dados de série de tempo que você fornecer [!DNL Real-time Customer Profile]. Consulte o guia [](../pql/overview.md) PQL para obter mais informações sobre como escrever query PQL.

Este guia fornece informações para ajudá-lo a entender melhor as definições de segmentos e inclui exemplos de chamadas de API para executar ações básicas usando a API.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter informações importantes que você precisa saber para fazer chamadas à API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Recuperar uma lista de definições de segmento {#list}

É possível recuperar uma lista de todas as definições de segmento para a Organização IMS, fazendo uma solicitação GET para o `/segment/definitions` endpoint.

**Formato da API**

O `/segment/definitions` terminal suporta vários parâmetros de query para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Efetuar uma chamada para este terminal sem parâmetros recuperará todas as definições de segmento disponíveis para a sua organização. Vários parâmetros podem ser incluídos, separados por E comercial (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parâmetros do Query**

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `start` | Especifica o deslocamento inicial para as definições de segmento retornadas. | `start=4` |
| `limit` | Especifica o número de definições de segmento retornadas por página. | `limit=20` |
| `page` | Especifica de qual página os resultados das definições de segmento serão start. | `page=5` |
| `sort` | Especifica por qual campo classificar os resultados. Está escrito no seguinte formato: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Especifica se a definição do segmento está ativada para transmissão. | `evaluationInfo.continuous.enabled=true` |

**Solicitação**

A solicitação a seguir recuperará as duas últimas definições de segmento publicadas na sua Organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de definições de segmento para a organização IMS especificada como JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Criar uma nova definição de segmento {#create}

Você pode criar uma nova definição de segmento, fazendo uma solicitação POST para o `/segment/definitions` ponto de extremidade.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | **Obrigatório.** Um nome exclusivo pelo qual fazer referência ao segmento. |
| `schema` | **Obrigatório.** O schema associado às entidades no segmento. Consiste em um campo `id` ou `name` . |
| `expression` | **Obrigatório.** Uma entidade que contém informações de campos sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, apenas &quot;PQL&quot; é suportado. |
| `expression.format` | Indica a estrutura da expressão no valor. Atualmente, o formato a seguir é compatível: <ul><li>`pql/text`: Uma representação textual de uma definição de segmento, de acordo com a gramática PQL publicada.  Por exemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Uma expressão que esteja em conformidade com o tipo indicado em `expression.format`. |
| `description` | Uma descrição legível da definição. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição do segmento recém-criado.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Uma ID gerada pelo sistema da definição de segmento recém-criada. |
| `evaluationInfo` | Um objeto gerado pelo sistema que informa a que tipo de avaliação a definição do segmento será submetida. Pode ser em lote, contínuo (também conhecido como streaming) ou segmentação síncrona. |

## Recuperar uma definição de segmento específica {#get}

Você pode recuperar informações detalhadas sobre uma definição de segmento específica, fazendo uma solicitação GET para o `/segment/definitions` endpoint e fornecendo a ID da definição de segmento que deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_ID}` | O `id` valor da definição de segmento que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a definição de segmento especificada.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Uma ID somente leitura gerada pelo sistema da definição do segmento. |
| `name` | Um nome exclusivo pelo qual fazer referência ao segmento. |
| `schema` | O schema associado às entidades no segmento. Consiste em um campo `id` ou `name` . |
| `expression` | Uma entidade que contém informações de campos sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, apenas &quot;PQL&quot; é suportado. |
| `expression.format` | Indica a estrutura da expressão no valor. Atualmente, o formato a seguir é compatível: <ul><li>`pql/text`: Uma representação textual de uma definição de segmento, de acordo com a gramática PQL publicada.  Por exemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Uma expressão que esteja em conformidade com o tipo indicado em `expression.format`. |
| `description` | Uma descrição legível da definição. |
| `evaluationInfo` | Um objeto gerado pelo sistema que informa a que tipo de avaliação, lote, contínuo (também conhecido como streaming) ou síncrono a definição do segmento será submetida. |

## Definições de segmento de recuperação em massa {#bulk-get}

Você pode recuperar informações detalhadas sobre várias definições de segmento especificadas, fazendo uma solicitação POST ao `/segment/definitions/bulk-get` ponto final e fornecendo os `id` valores das definições de segmento no corpo da solicitação.

**Formato da API**

```http
POST /segment/definitions/bulk-get
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 207 com as definições de segmento solicitadas.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Uma ID somente leitura gerada pelo sistema da definição do segmento. |
| `name` | Um nome exclusivo pelo qual fazer referência ao segmento. |
| `schema` | O schema associado às entidades no segmento. Consiste em um campo `id` ou `name` . |
| `expression` | Uma entidade que contém informações de campos sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, apenas &quot;PQL&quot; é suportado. |
| `expression.format` | Indica a estrutura da expressão no valor. Atualmente, o formato a seguir é compatível: <ul><li>`pql/text`: Uma representação textual de uma definição de segmento, de acordo com a gramática PQL publicada.  Por exemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Uma expressão que esteja em conformidade com o tipo indicado em `expression.format`. |
| `description` | Uma descrição legível da definição. |
| `evaluationInfo` | Um objeto gerado pelo sistema que informa a que tipo de avaliação, lote, contínuo (também conhecido como streaming) ou síncrono a definição do segmento será submetida. |

## Excluir uma definição de segmento específica {#delete}

Você pode solicitar a exclusão de uma definição de segmento específica, fazendo uma solicitação DELETE ao `/segment/definitions` ponto final e fornecendo a ID da definição de segmento que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_ID}` | O `id` valor da definição de segmento que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 sem nenhuma mensagem.

## Atualizar uma definição de segmento específica

Você pode atualizar uma definição de segmento específica, fazendo uma solicitação PATCH para o `/segment/definitions` ponto final e fornecendo a ID da definição de segmento que deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_ID}` | O `id` valor da definição de segmento que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualizará o país do endereço de trabalho dos EUA para o Canadá.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-atualizada. Observe como o país do endereço de trabalho foi atualizado dos EUA (EUA) para o Canadá (CA).

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## Próximas etapas

Depois de ler este guia, agora você tem um melhor entendimento de como as definições de segmentos funcionam. Para obter mais informações sobre como criar um segmento, leia o tutorial sobre a [criação de um segmento](../tutorials/create-a-segment.md) .