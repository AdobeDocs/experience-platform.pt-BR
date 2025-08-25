---
solution: Experience Platform
title: Endpoint da API de definições de segmento
description: O endpoint de definições de segmento na API do Serviço de segmentação do Adobe Experience Platform permite gerenciar de forma programática as definições de segmento da sua organização.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 5f19bd0601770115cae859fd6dc85bd9c9f6e92c
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 3%

---

# Endpoint de definições de segmento

>[!WARNING]
>
>A criação de públicos-alvo usando entidades B2B usando a API do serviço de segmentação está obsoleta. Não é mais possível criar públicos-alvo usando as seguintes entidades B2B: Conta, Relação conta-pessoa, Campanha, Membro da campanha, Lista de marketing, Membro da lista de marketing, Oportunidade e Relação oportunidade-pessoa. Para obter mais informações, leia o guia em [Atualizações da arquitetura do Real-Time CDP B2B edition](../../rtcdp/b2b-architecture-upgrade.md).

O Adobe Experience Platform permite criar definições de segmento que definem um grupo de atributos ou comportamentos específicos a partir de um grupo de perfis. Uma definição de segmento é um objeto que encapsula uma consulta gravada em [!DNL Profile Query Language] (PQL). As definições de segmento são aplicadas aos perfis para criar públicos. Esse objeto (definição de segmento) também é chamado de predicado PQL. Os predicados da PQL definem as regras para a definição de segmento com base nas condições relacionadas a qualquer registro ou dados de série temporal fornecidos a [!DNL Real-Time Customer Profile]. Consulte o [guia do PQL](../pql/overview.md) para obter mais informações sobre como gravar consultas do PQL.

Este guia fornece informações para ajudá-lo a entender melhor as definições de segmento e inclui chamadas de API de exemplo para executar ações básicas usando a API.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo da API.

## Recuperar uma lista de definições de segmento {#list}

Você pode recuperar uma lista de todas as definições de segmento para sua organização fazendo uma solicitação GET para o ponto de extremidade `/segment/definitions`.

**Formato da API**

O ponto de extremidade `/segment/definitions` dá suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Fazer uma chamada para esse endpoint sem parâmetros recuperará todas as definições de segmento disponíveis para sua organização. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parâmetros de consulta**

+++ Uma lista de parâmetros de consulta disponíveis.

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `start` | Especifica o deslocamento inicial para as definições de segmento retornadas. | `start=4` |
| `limit` | Especifica o número de definições de segmento retornadas por página. | `limit=20` |
| `page` | Especifica a página a partir da qual os resultados das definições de segmento começarão. | `page=5` |
| `sort` | Especifica por qual campo classificar os resultados. É gravado no seguinte formato: `[attributeName]:[desc/asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Especifica se a definição do segmento é habilitada para streaming. | `evaluationInfo.continuous.enabled=true` |

+++

**Solicitação**

A solicitação a seguir recuperará as duas últimas definições de segmento publicadas em sua organização.

+++ Uma solicitação de amostra para recuperar uma lista de definições de segmento.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de definições de segmento para a organização especificada como JSON.

+++ Uma resposta de amostra ao recuperar uma lista de definições de segmento.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

+++

## Criar uma nova definição de segmento {#create}

Você pode criar uma nova definição de segmento fazendo uma solicitação POST para o ponto de extremidade `/segment/definitions`.

>[!IMPORTANT]
>
>As definições de segmento criadas por meio da API **não podem** ser editadas usando o Construtor de segmentos.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

Ao criar uma nova definição de segmento, você pode criá-la no formato `pql/text` ou `pql/json`.

>[!BEGINTABS]

>[!TAB Usando pql/text]

+++ Uma solicitação de amostra para criar uma definição de segmento.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome exclusivo pelo qual se referir à definição do segmento. |
| `description` | (Opcional) Uma descrição da definição de segmento que você está criando. |
| `expression` | Uma entidade que contém campos e informações sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, somente o &quot;PQL&quot; é compatível. |
| `expression.format` | Indica a estrutura da expressão no valor. Os valores suportados incluem `pql/text` e `pql/json`. |
| `expression.value` | Uma expressão que está em conformidade com o tipo indicado em `expression.format`. |
| `evaluationInfo` | (Opcional) O tipo de definição de segmento que você está criando. Se você quiser criar um segmento em lote, defina `evaluationInfo.batch.enabled` como verdadeiro. Se você deseja criar um segmento de transmissão, defina `evaluationInfo.continuous.enabled` como verdadeiro. Se você quiser criar um segmento de borda, defina `evaluationInfo.synchronous.enabled` como verdadeiro. Se deixado em branco, a definição do segmento será criada como um segmento **batch**. |
| `schema` | O schema associado às entidades no segmento. Consiste de um campo `id` ou `name`. |

+++

>[!TAB Usando pql/json]

+++ Uma solicitação de amostra para criar uma definição de segmento.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome exclusivo pelo qual se referir à definição do segmento. |
| `description` | (Opcional) Uma descrição da definição de segmento que você está criando. |
| `evaluationInfo` | (Opcional) O tipo de definição de segmento que você está criando. Se você quiser criar um segmento em lote, defina `evaluationInfo.batch.enabled` como verdadeiro. Se você deseja criar um segmento de transmissão, defina `evaluationInfo.continuous.enabled` como verdadeiro. Se você quiser criar um segmento de borda, defina `evaluationInfo.synchronous.enabled` como verdadeiro. Se deixado em branco, a definição do segmento será criada como um segmento **batch**. |
| `schema` | O schema associado às entidades no segmento. Consiste de um campo `id` ou `name`. |
| `expression` | Uma entidade que contém campos e informações sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, somente o &quot;PQL&quot; é compatível. |
| `expression.format` | Indica a estrutura da expressão no valor. |
| `expression.value` | Uma expressão que está em conformidade com o tipo indicado em `expression.format`. |

+++

>[!ENDTABS]

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-criada.

+++ Um exemplo de resposta ao criar uma definição de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `evaluationInfo` | Um objeto que indica o tipo de avaliação pelo qual a definição do segmento será submetida. Pode ser segmentação em lote, de fluxo (também conhecida como contínua) ou de borda (também conhecida como síncrona). |

+++

## Recuperar uma definição de segmento específica {#get}

Você pode recuperar informações detalhadas sobre uma definição de segmento específica fazendo uma solicitação GET para o ponto de extremidade `/segment/definitions` e fornecendo a ID da definição de segmento que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_ID}` | O valor `id` da definição de segmento que você deseja recuperar. |

**Solicitação**

+++ Uma solicitação de amostra para recuperar uma definição de segmento.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a definição de segmento especificada.

+++ Uma resposta de amostra ao recuperar uma definição de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Uma ID somente leitura gerada pelo sistema da definição de segmento. |
| `name` | Um nome exclusivo pelo qual se referir à definição do segmento. |
| `schema` | O schema associado às entidades no segmento. Consiste de um campo `id` ou `name`. |
| `expression` | Uma entidade que contém campos e informações sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, somente o &quot;PQL&quot; é compatível. |
| `expression.format` | Indica a estrutura da expressão no valor. No momento, o seguinte formato é compatível: <ul><li>`pql/text`: uma representação textual de uma definição de segmento, de acordo com a gramática do PQL publicada.  Por exemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Uma expressão que está em conformidade com o tipo indicado em `expression.format`. |
| `description` | Uma descrição legível da definição. |
| `evaluationInfo` | Um objeto que indica que tipo de avaliação, lote, streaming (também conhecido como contínuo) ou borda (também conhecido como síncrono), a definição do segmento será submetida. |

+++

## Definições de segmento de recuperação em massa {#bulk-get}

Você pode recuperar informações detalhadas sobre várias definições de segmento especificadas fazendo uma solicitação POST para o ponto de extremidade `/segment/definitions/bulk-get` e fornecendo os valores `id` das definições de segmento no corpo da solicitação.

**Formato da API**

```http
POST /segment/definitions/bulk-get
```

**Solicitação**

+++ Uma solicitação de exemplo ao usar o ponto de extremidade get em massa.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Propriedade | Descrição |
| -------- | ----------- |
| `ids` | Uma matriz que contém objetos que indicam as IDs das definições de segmento que você deseja recuperar. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 207 com as definições de segmento solicitadas.

+++ Uma resposta de exemplo ao usar o ponto de extremidade get em massa.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
| `id` | Uma ID somente leitura gerada pelo sistema da definição de segmento. |
| `name` | Um nome exclusivo pelo qual se referir à definição do segmento. |
| `schema` | O schema associado às entidades no segmento. Consiste de um campo `id` ou `name`. |
| `expression` | Uma entidade que contém campos e informações sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, somente o &quot;PQL&quot; é compatível. |
| `expression.format` | Indica a estrutura da expressão no valor. No momento, o seguinte formato é compatível: <ul><li>`pql/text`: uma representação textual de uma definição de segmento, de acordo com a gramática do PQL publicada.  Por exemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Uma expressão que está em conformidade com o tipo indicado em `expression.format`. |
| `description` | Uma descrição legível da definição. |
| `evaluationInfo` | Um objeto que indica que tipo de avaliação, lote, streaming (também conhecido como contínuo) ou borda (também conhecido como síncrono), a definição do segmento será submetida. |

+++

## Excluir uma definição de segmento específica {#delete}

Você pode solicitar a exclusão de uma definição de segmento específica fazendo uma solicitação DELETE para o ponto de extremidade `/segment/definitions` e fornecendo a ID da definição de segmento que deseja excluir no caminho da solicitação.

>[!NOTE]
>
> Uma definição de segmento usada em uma ativação de destino **não pode** ser excluída.

**Formato da API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_ID}` | O valor `id` da definição de segmento que você deseja excluir. |

**Solicitação**

+++ Um exemplo de solicitação para excluir uma definição de segmento.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 sem mensagem.

## Atualizar uma definição de segmento específica

Você pode atualizar uma definição de segmento específica fazendo uma solicitação PATCH para o ponto de extremidade `/segment/definitions` e fornecendo a ID da definição de segmento que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_ID}` | O valor `id` da definição de segmento que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualizará o país do endereço comercial dos EUA para o Canadá.

>[!NOTE]
>
>Como essa chamada de API **substitui** o conteúdo da definição de segmento, certifique-se de **todos** que os campos que você deseja manter estão incluídos como parte do corpo da solicitação.

+++ Uma solicitação de amostra para atualizar uma definição de segmento.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-atualizada.

+++ Um exemplo de resposta ao atualizar uma definição de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

+++

## Converter definição de segmento

Você pode converter uma definição de segmento entre `pql/text` e `pql/json` ou `pql/json` para `pql/text` fazendo uma solicitação POST para o ponto de extremidade `/segment/conversion`.

**Formato da API**

```http
POST /segment/conversion
```

**Solicitação**

A solicitação a seguir alterará o formato da definição de segmento de `pql/text` para `pql/json`.

+++ Uma solicitação de amostra para converter a definição do segmento.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "payloadSchema": "string"
    }'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-convertida.

+++ Um exemplo de resposta ao converter a definição do segmento.

```json
{
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

+++

## Próximas etapas

Depois de ler este guia, você compreenderá melhor como as definições de segmento funcionam. Para obter mais informações sobre como criar um segmento, leia o tutorial [criando um segmento](../tutorials/create-a-segment.md).
