---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Trabalhos de segmento
topic: developer guide
translation-type: tm+mt
source-git-commit: db4cdbfb7719d94919c896162ca7875fdf7d2502

---


# Guia do desenvolvedor de trabalhos de segmento

Um trabalho de segmento é um processo assíncrono que cria um novo segmento de audiência. Ele faz referência a uma definição de segmento, bem como a quaisquer políticas de mesclagem que controlam como o Perfil de cliente em tempo real mescla atributos sobrepostos em seus fragmentos de perfil. Quando uma tarefa de segmento é concluída com êxito, você pode coletar várias informações sobre o segmento, como quaisquer erros que possam ter ocorrido durante o processamento e o tamanho final da sua audiência.

Este guia fornece informações para ajudá-lo a entender melhor os trabalhos de segmento e inclui chamadas de API de amostra para executar ações básicas usando a API.

## Introdução

Os pontos finais da API usados neste guia fazem parte da API de segmentação. Antes de continuar, consulte o guia [do desenvolvedor de](./getting-started.md)Segmentação.

Em particular, a seção [de](./getting-started.md#getting-started) introdução do guia do desenvolvedor de Segmentação inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra no documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da plataforma de experiência.

## Recuperar uma lista de trabalhos de segmento

Você pode recuperar uma lista de todos os trabalhos de segmento para a Organização IMS, fazendo uma solicitação GET para o `/segment/jobs` endpoint.

**Formato da API**

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por E comercial (`&`). Os parâmetros disponíveis estão listados abaixo.

**Parâmetros do Query**

A seguir está uma lista de parâmetros de query disponíveis para listar trabalhos de segmento. Todos esses parâmetros são opcionais. Efetuar uma chamada para este terminal sem parâmetros recuperará todos os trabalhos de segmento disponíveis para a sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `start` | Especifica o deslocamento inicial para os trabalhos de segmento retornados. |
| `limit` | Especifica o número de trabalhos de segmento retornados por página. |
| `status` | Filtros os resultados com base no status. Os valores suportados são NOVO, EM FILA, PROCESSAMENTO, BEM-SUCEDIDO, FALHA, CANCELAMENTO, CANCELADO |
| `sort` | Ordena os trabalhos do segmento retornados. É escrito no formato `[attributeName]:[desc|asc]`. |
| `property` | Os Filtros segmentam trabalhos e obtêm correspondências exatas para o filtro fornecido. Ele pode ser escrito em qualquer um dos seguintes formatos: <ul><li>`[jsonObjectPath]==[value]` - filtragem na chave do objeto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtragem dentro do storage</li></ul> |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de trabalhos de segmento para a organização IMS especificada como JSON. A resposta a seguir retorna uma lista de todos os trabalhos de segmento bem-sucedidos para a organização IMS.

>[!NOTE] A resposta a seguir foi truncada para espaço e mostrará somente o primeiro trabalho retornado.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Criar um novo trabalho de segmento

Você pode criar um novo trabalho de segmento fazendo uma solicitação POST para o `/segment/jobs` terminal.

**Formato da API**

```http
POST /segment/jobs
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]
 '
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do seu trabalho de segmento recém-criado.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

## Recuperar um trabalho de segmento específico

Você pode recuperar informações detalhadas sobre um trabalho de segmento específico, realizando uma solicitação GET para o `/segment/jobs` terminal e fornecendo o `id` valor do trabalho de segmento no caminho da solicitação.

**Formato da API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | O `id` valor do trabalho de segmento que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o trabalho de segmento especificado.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

## Cancelar ou excluir um trabalho de segmento específico

Você pode solicitar a exclusão de um trabalho de segmento especificado, fazendo uma solicitação DELETE para o `/segment/jobs` terminal e fornecendo o `id` valor do trabalho de segmento no caminho da solicitação.

**Formato da API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | O `id` valor do trabalho de segmento que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 com as seguintes informações.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Próximas etapas

Depois de ler este guia, agora você tem um melhor entendimento de como as tarefas de segmento funcionam. Para obter mais informações sobre Segmentação, leia a visão geral [da](../home.md)Segmentação.