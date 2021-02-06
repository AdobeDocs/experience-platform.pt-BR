---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;tarefas de segmento;trabalho de segmento;API;api;
solution: Experience Platform
title: Ponto Final da API de Serviços de Segmento
topic: developer guide
description: O endpoint de jobs de segmento na API do Adobe Experience Platform Segmentation Service permite que você gerencie programaticamente os jobs de segmento para sua organização.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---


# Ponto de extremidade de trabalhos de segmento

Um trabalho de segmento é um processo assíncrono que cria um novo segmento de audiência. Ela faz referência a uma [definição de segmento](./segment-definitions.md), bem como a qualquer [políticas de mesclagem](../../profile/api/merge-policies.md) controlando como [!DNL Real-time Customer Profile] mescla atributos sobrepostos em seus fragmentos de perfil. Quando uma tarefa de segmento é concluída com êxito, você pode coletar várias informações sobre o segmento, como quaisquer erros que possam ter ocorrido durante o processamento e o tamanho final da sua audiência.

Este guia fornece informações para ajudá-lo a entender melhor os trabalhos de segmento e inclui chamadas de API de amostra para executar ações básicas usando a API.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas à API com êxito, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Recuperar uma lista de trabalhos de segmento {#retrieve-list}

Você pode recuperar uma lista de todos os trabalhos de segmento para a Organização IMS, fazendo uma solicitação de GET para o terminal `/segment/jobs`.

**Formato da API**

O endpoint `/segment/jobs` suporta vários parâmetros de query para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Efetuar uma chamada para este terminal sem parâmetros recuperará todas as tarefas de exportação disponíveis para a sua organização. Vários parâmetros podem ser incluídos, separados por E comercial (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parâmetros do query**

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `start` | Especifica o deslocamento inicial para os trabalhos de segmento retornados. | `start=1` |
| `limit` | Especifica o número de trabalhos de segmento retornados por página. | `limit=20` |
| `status` | Filtros os resultados com base no status. Os valores suportados são NOVO, EM FILA, PROCESSAMENTO, BEM-SUCEDIDO, FALHA, CANCELAMENTO, CANCELADO | `status=NEW` |
| `sort` | Ordena os trabalhos do segmento retornados. Está escrito no formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Os filtros segmentam trabalhos e obtêm correspondências exatas para o filtro fornecido. Ele pode ser escrito em qualquer um dos seguintes formatos: <ul><li>`[jsonObjectPath]==[value]` - filtragem na chave do objeto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtragem dentro do storage</li></ul> | `property=segments~segmentId==workInUS` |

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

>[!NOTE]
>
>A resposta a seguir foi truncada para espaço e mostrará somente o primeiro trabalho retornado.

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
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "existing":10,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento. |
| `status` | O status atual do trabalho de segmento. Os valores potenciais para o status incluem &quot;NOVO&quot;, &quot;PROCESSAMENTO&quot;, &quot;CANCELAMENTO&quot;, &quot;CANCELADO&quot;, &quot;FALHADO&quot; e &quot;SUCEDIDO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento retornadas no trabalho de segmento. |
| `segments.segment.id` | A ID da definição do segmento. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição do segmento, gravada em PQL. |
| `metrics` | Um objeto que contém informações de diagnóstico sobre o trabalho de segmento. |
| `metrics.totalTime` | Um objeto que contém informações sobre o horário em que o trabalho de segmentação começou e terminou, bem como o tempo total gasto. |
| `metrics.profileSegmentationTime` | Um objeto que contém informações sobre o horário em que a avaliação de segmentação começou e terminou, bem como o tempo total gasto. |
| `metrics.segmentProfileCounter` | O número de perfis qualificados por segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | O número de perfis qualificados para cada namespace de identidade com base em cada segmento. |
| `metrics.segmentProfileByStatusCounter` | A contagem de perfis para cada status. Os três status a seguir são suportados: <ul><li>&quot;realizado&quot; - o número de novos perfis que entraram no segmento.</li><li>&quot;existente&quot; - o número de perfis que continuam a existir no segmento.</li><li>&quot;exit&quot; - O número de segmentos de perfil que não existem mais no segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | O número total de perfis mesclados por política de mesclagem. |

## Criar um novo trabalho de segmento {#create}

Você pode criar um novo trabalho de segmento fazendo uma solicitação POST ao terminal `/segment/jobs` e incluindo no corpo a ID da definição de segmento da qual você deseja criar uma nova audiência.

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
]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentId` | A ID da definição de segmento para a qual você deseja criar um trabalho de segmento. Essas definições de segmento podem pertencer a políticas de mesclagem diferentes. Mais informações sobre definições de segmentos podem ser encontradas no [guia do ponto final de definição de segmento](./segment-definitions.md). |

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

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento recém-criado. |
| `status` | O status atual do trabalho de segmento. Como o trabalho de segmento é recém-criado, o status sempre será &quot;NOVO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento para as quais esse trabalho de segmento está sendo executado. |
| `segments.segment.id` | A ID da definição de segmento fornecida. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição do segmento, gravada em PQL. |

## Recuperar um trabalho de segmento específico {#get}

Você pode recuperar informações detalhadas sobre um trabalho de segmento específico, fazendo uma solicitação de GET para o terminal `/segment/jobs` e fornecendo a ID do trabalho de segmento que deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | O valor `id` do trabalho de segmento que você deseja recuperar. |

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

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento. |
| `status` | O status atual do trabalho de segmento. Os valores potenciais para o status incluem &quot;NOVO&quot;, &quot;PROCESSAMENTO&quot;, &quot;CANCELAMENTO&quot;, &quot;CANCELADO&quot;, &quot;FALHADO&quot; e &quot;SUCEDIDO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento retornadas no trabalho de segmento. |
| `segments.segment.id` | A ID da definição do segmento. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição do segmento, gravada em PQL. |
| `metrics` | Um objeto que contém informações de diagnóstico sobre o trabalho de segmento. |

## Recuperar trabalhos de segmento em massa {#bulk-get}

Você pode recuperar informações detalhadas sobre vários trabalhos de segmento, fazendo uma solicitação de POST ao terminal `/segment/jobs/bulk-get` e fornecendo os valores `id` dos trabalhos de segmento no corpo da solicitação.

**Formato da API**

```http
POST /segment/jobs/bulk-get
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 207 com os trabalhos de segmento solicitados.

>[!NOTE]
>
>A resposta a seguir foi truncada para o espaço, mostrando apenas detalhes parciais de cada tarefa de segmento. A resposta completa vai lista os detalhes completos dos trabalhos de segmento solicitados.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
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
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
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
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento. |
| `status` | O status atual do trabalho de segmento. Os valores potenciais para o status incluem &quot;NOVO&quot;, &quot;PROCESSAMENTO&quot;, &quot;CANCELAMENTO&quot;, &quot;CANCELADO&quot;, &quot;FALHADO&quot; e &quot;SUCEDIDO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento retornadas no trabalho de segmento. |
| `segments.segment.id` | A ID da definição do segmento. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição do segmento, gravada em PQL. |

## Cancelar ou excluir um trabalho de segmento específico {#delete}

Você pode excluir um trabalho de segmento específico, fazendo uma solicitação de DELETE ao terminal `/segment/jobs` e fornecendo a ID do trabalho de segmento que deseja excluir no caminho da solicitação.

>[!NOTE]
>
>A resposta da API à solicitação de exclusão é imediata. No entanto, a exclusão real do trabalho de segmento é assíncrona. Em outras palavras, há uma diferença de tempo entre quando a solicitação de exclusão para o trabalho de segmento é feita e quando é aplicada.

**Formato da API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | O valor `id` do trabalho de segmento que você deseja excluir. |

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

Depois de ler este guia, agora você tem um melhor entendimento de como as tarefas de segmento funcionam.