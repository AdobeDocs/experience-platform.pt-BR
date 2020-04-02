---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definições de segmento
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guia do desenvolvedor de definições de segmentos

A plataforma Adobe Experience permite criar segmentos que definem um grupo de atributos ou comportamentos específicos a partir de um grupo de perfis.

Este guia do desenvolvedor fornece instruções sobre as seguintes áreas para definições de segmentos:

- [Recuperar uma lista de definições de segmento](#retrieve-a-list-of-segment-definitions)
- [Criar uma nova definição de segmento](#create-a-new-segment-definition)
- [Recuperar uma definição de segmento específica](#retrieve-a-specific-segment-definition)
- [Excluir uma definição de segmento específica](#delete-a-specific-segment-definition)
- [Atualizar uma definição de segmento específica](#update-a-specific-segment-definition)

## Introdução

Os pontos finais da API usados neste guia fazem parte da API de segmentação. Antes de continuar, consulte o guia [do desenvolvedor de](./getting-started.md)Segmentação.

Em particular, a seção [de](./getting-started.md#getting-started) introdução do guia do desenvolvedor de Segmentação inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra no documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da plataforma de experiência.

## Recuperar uma lista de definições de segmento

É possível recuperar uma lista de todas as definições de segmento para a Organização IMS, fazendo uma solicitação GET para o `/segment/definitions` endpoint.

**Formato da API**

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por E comercial (`&`). Os parâmetros disponíveis estão listados abaixo.

**Parâmetros do Query**

A seguir está uma lista de parâmetros de query disponíveis para listar definições de segmentos. Todos esses parâmetros são opcionais. Efetuar uma chamada para este terminal sem parâmetros recuperará todas as definições de segmento disponíveis para a sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `start` | ??? |
| `limit` | Especifica o número de definições de segmento retornadas por página. |
| `page` | Especifica de qual página os resultados das definições de segmento serão start. |
| `sort` | Especificado por qual campo classificar os resultados. |
| `evaluationInfo.continuous.enabled` | Especifica se a definição do segmento está ativada para transmissão. |

**Solicitação**

```shell
cur -X GET https://platform.adobe.io/data/core/ups/segment/definitions?QUERY \
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
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
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
                "value": "{\"nodeType\":\"select\",\"variables\":[{\"nodeType\":\"varDecl\",\"varName\":\"_Checkouts1\",\"from\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"xEvent\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}},\"where\":{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"eventType\",\"object\":{\"nodeType\":\"varRef\",\"varName\":\"_Checkouts1\"}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"commerce.checkouts\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":true}]}}]}"
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
        ... ,
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"and\",\"params\":[{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"points\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"Double\",\"nodeType\":\"literal\",\"value\":2}]},{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"testLoyaltyID\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":false}]}]}"
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
        "totalCount": 4,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 4,
        "limit": 100
    },
    "link": {}
}
```

## Criar uma nova definição de segmento

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
 -d '
 {
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
  "ttlInDays": 60,
  "creationTime": 0,
  "updateTime": 0,
  "updateEpoch": 0
}
 '
```

corpo explicativo

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

explicar o corpo e os cabeçalhos

## Recuperar uma definição de segmento específica

Você pode recuperar informações detalhadas sobre uma definição de segmento específica, fazendo uma solicitação GET ao ponto de extremidade `/segment/definitions` e fornecendo o `id` valor da definição de segmento no caminho da solicitação.

**Formato da API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`: O `id` valor da definição de segmento que você deseja recuperar.

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
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
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

## Excluir uma definição de segmento específica

Você pode solicitar a exclusão de uma definição de segmento especificada, fazendo uma solicitação DELETE para o `/segment/definitions` terminal e fornecendo o `id` valor da definição de segmento no caminho da solicitação.

**Formato da API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}` O `id` valor da definição de segmento que você deseja excluir.

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

É possível atualizar uma definição de segmento especificada, fazendo uma solicitação PATCH para o `/segment/definitions` ponto final e fornecendo o `id` valor da definição de segmento no caminho da solicitação.

**Formato da API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`: O `id` valor da definição de segmento que você deseja atualizar.

**Solicitação**

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
        "value": "workAddress.country = \"US\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}
'
```

corpo explicativo

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-atualizada.

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
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

corpo e cabeçalho explicativos

## Próximas etapas
