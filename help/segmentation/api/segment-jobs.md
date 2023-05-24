---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;trabalhos de segmento;trabalho de segmento;API;api;
solution: Experience Platform
title: Ponto de extremidade da API de trabalhos de segmento
description: O endpoint de trabalhos de segmento na API do Serviço de segmentação do Adobe Experience Platform permite gerenciar de forma programática os trabalhos de segmento da sua organização.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 3%

---

# Ponto de extremidade de trabalhos de segmento

Um trabalho de segmento é um processo assíncrono que cria um segmento de público-alvo sob demanda. Faz referência a uma [definição de segmento](./segment-definitions.md), bem como qualquer [políticas de mesclagem](../../profile/api/merge-policies.md) controlando como [!DNL Real-Time Customer Profile] O mescla atributos sobrepostos nos fragmentos de perfil. Quando um trabalho de segmento é concluído com sucesso, você pode coletar várias informações sobre o segmento, como erros que possam ter ocorrido durante o processamento e o tamanho máximo do seu público-alvo.

Este guia fornece informações para ajudar você a entender melhor os trabalhos de segmento e inclui chamadas de API de exemplo para executar ações básicas usando a API.

## Introdução

Os endpoints usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Recuperar uma lista de trabalhos do segmento {#retrieve-list}

Você pode recuperar uma lista de todos os cargos do segmento para sua organização fazendo uma solicitação GET para a `/segment/jobs` terminal.

**Formato da API**

A variável `/segment/jobs` O endpoint oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Fazer uma chamada para esse ponto de extremidade sem parâmetros recuperará todos os trabalhos de exportação disponíveis para sua organização. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parâmetros de consulta**

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `start` | Especifica o deslocamento inicial dos trabalhos de segmento retornados. | `start=1` |
| `limit` | Especifica o número de trabalhos de segmento retornados por página. | `limit=20` |
| `status` | Filtra os resultados com base no status. Os valores compatíveis são NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELING, CANCELED | `status=NEW` |
| `sort` | Ordena os trabalhos do segmento retornados. É gravado no formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtra trabalhos de segmento e obtém correspondências exatas para o filtro fornecido. Ele pode ser escrito em um dos seguintes formatos: <ul><li>`[jsonObjectPath]==[value]` - filtrando na chave do objeto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtragem dentro da matriz</li></ul> | `property=segments~segmentId==workInUS` |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de trabalhos de segmento para a organização especificada como JSON. No entanto, a resposta será diferente, dependendo do número de segmentos no trabalho de segmento.

**Menor que ou igual a 1500 segmentos no trabalho do segmento**

Se você tiver menos de 1500 segmentos em execução no seu trabalho de segmento, uma lista completa de todos os segmentos será exibida na `children.segments` atributo.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço e mostrará apenas a primeira tarefa retornada.

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

**Mais de 1500 segmentos**

Se você tiver mais de 1500 segmentos em execução no seu trabalho de segmento, a variável `children.segments` atributo será exibido `*`, indicando que todos os segmentos estão sendo avaliados.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço e mostrará apenas a primeira tarefa retornada.

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
                    "segmentId": "*",
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
                "totalProfiles": 13146432,
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
| `status` | O status atual do trabalho do segmento. Os valores potenciais para o status incluem &quot;NOVO&quot;, &quot;PROCESSANDO&quot;, &quot;CANCELANDO&quot;, &quot;CANCELADO&quot;, &quot;FALHA&quot; e &quot;BEM-SUCEDIDO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento retornadas no trabalho de segmento. |
| `segments.segment.id` | A ID da definição do segmento. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição de segmento, escrita em PQL. |
| `metrics` | Um objeto que contém informações de diagnóstico sobre o trabalho do segmento. |
| `metrics.totalTime` | Um objeto que contém informações sobre os horários em que o trabalho de segmentação começou e terminou, bem como o tempo total gasto. |
| `metrics.profileSegmentationTime` | Um objeto que contém informações sobre os horários em que a avaliação da segmentação começou e terminou, bem como o tempo total gasto. |
| `metrics.segmentProfileCounter` | O número de perfis qualificados por segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | O número de perfis qualificados para cada namespace de identidade com base no segmento. |
| `metrics.segmentProfileByStatusCounter` | A contagem de perfis para cada status. Os três status a seguir são compatíveis: <ul><li>&quot;realizado&quot; - O número de perfis qualificados para o segmento.</li><li>&quot;encerrado&quot; - o número de segmentos de perfil que não existem mais no segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | O número total de perfis mesclados por política de mesclagem. |

## Criar um novo trabalho de segmento {#create}

Você pode criar um novo trabalho de segmento fazendo uma solicitação POST para o `/segment/jobs` e incluir no corpo a ID da definição de segmento a partir da qual você deseja criar um novo público-alvo.

**Formato da API**

```http
POST /segment/jobs
```

Ao criar um novo trabalho de segmento, a solicitação e a resposta serão diferentes dependendo do número de segmentos no trabalho de segmento.

**Menor que ou igual a 1500 segmentos no trabalho do segmento**

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    }
 ]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentId` | A ID da definição de segmento para a qual você deseja criar um trabalho de segmento. Essas definições de segmento podem pertencer a diferentes políticas de mesclagem. Mais informações sobre definições de segmento podem ser encontradas no [guia de endpoint de definição de segmento](./segment-definitions.md). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o trabalho de segmento recém-criado.

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
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
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento recém-criado. |
| `status` | O status atual do trabalho do segmento. Como o trabalho do segmento é recém-criado, o status sempre será &quot;NOVO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento para as quais esse trabalho de segmento está sendo executado. |
| `segments.segment.id` | A ID da definição de segmento fornecida. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição de segmento, escrita em PQL. |

**Mais de 1500 segmentos**

**Solicitação**

>[!NOTE]
>
>Embora você possa criar um trabalho de segmento com mais de 1500 segmentos, isso é **altamente não recomendado**.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schema.name` | O nome do esquema dos segmentos. |
| `segments.segmentId` | Ao executar um trabalho de segmento com mais de 1500 segmentos, você precisará passar `*` como a ID do segmento para indicar que você deseja executar um trabalho de segmentação com todos os segmentos. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do trabalho de segmento recém-criado.

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
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
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento recém-criado. |
| `status` | O status atual do trabalho do segmento. Como o trabalho do segmento é recém-criado, o status sempre será `NEW`. |
| `segments` | Um objeto que contém informações sobre as definições de segmento para as quais esse trabalho de segmento está sendo executado. |
| `segments.segment.id` | A variável `*` significa que esse trabalho de segmento está sendo executado para todos os segmentos na organização. |

## Recuperar um trabalho de segmento específico {#get}

Você pode recuperar informações detalhadas sobre um trabalho de segmento específico fazendo uma solicitação GET à `/segment/jobs` e forneça a ID do trabalho de segmento que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | A variável `id` valor do trabalho de segmento que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o trabalho de segmento especificado.  No entanto, a resposta será diferente dependendo do número de segmentos no trabalho de segmento.

**Menor que ou igual a 1500 segmentos no trabalho do segmento**

Se você tiver menos de 1500 segmentos em execução no seu trabalho de segmento, uma lista completa de todos os segmentos será exibida na `children.segments` atributo.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
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

**Mais de 1500 segmentos**

Se você tiver mais de 1500 segmentos em execução no seu trabalho de segmento, a variável `children.segments` atributo será exibido `*`, indicando que todos os segmentos estão sendo avaliados.

```json
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
            "segmentId": "*"
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
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
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador somente leitura gerado pelo sistema para o trabalho de segmento. |
| `status` | O status atual do trabalho do segmento. Os valores potenciais para o status incluem &quot;NOVO&quot;, &quot;PROCESSANDO&quot;, &quot;CANCELANDO&quot;, &quot;CANCELADO&quot;, &quot;FALHA&quot; e &quot;BEM-SUCEDIDO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento retornadas no trabalho de segmento. |
| `segments.segment.id` | A ID da definição do segmento. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição de segmento, escrita em PQL. |
| `metrics` | Um objeto que contém informações de diagnóstico sobre o trabalho do segmento. |

## Trabalhos de recuperação de segmentos em massa {#bulk-get}

Você pode recuperar informações detalhadas sobre vários trabalhos de segmento fazendo uma solicitação POST para o `/segment/jobs/bulk-get` terminal e fornecendo a  `id` valores dos trabalhos de segmento no corpo da solicitação.

**Formato da API**

```http
POST /segment/jobs/bulk-get
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Uma resposta bem-sucedida retorna o status HTTP 207 com os trabalhos de segmento solicitados. No entanto, o valor da `children.segments` o atributo difere dependendo se o trabalho de segmento está em execução para mais de 1500 segmentos.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço, mostrando apenas detalhes parciais de cada trabalho de segmento. A resposta completa listará os detalhes completos para os trabalhos do segmento solicitados.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "*"
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
| `status` | O status atual do trabalho do segmento. Os valores potenciais para o status incluem &quot;NOVO&quot;, &quot;PROCESSANDO&quot;, &quot;CANCELANDO&quot;, &quot;CANCELADO&quot;, &quot;FALHA&quot; e &quot;BEM-SUCEDIDO&quot;. |
| `segments` | Um objeto que contém informações sobre as definições de segmento retornadas no trabalho de segmento. |
| `segments.segment.id` | A ID da definição do segmento. |
| `segments.segment.expression` | Um objeto que contém informações sobre a expressão da definição de segmento, escrita em PQL. |

## Cancelar ou excluir um trabalho de segmento específico {#delete}

Você pode excluir um trabalho de segmento específico fazendo uma solicitação DELETE para o `/segment/jobs` e forneça a ID do trabalho de segmento que você deseja excluir no caminho da solicitação.

>[!NOTE]
>
>A resposta da API à solicitação de exclusão é imediata. No entanto, a exclusão real do trabalho de segmento é assíncrona. Em outras palavras, há uma diferença de tempo entre quando a solicitação de exclusão para o trabalho do segmento é feita e quando é aplicada.

**Formato da API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | A variável `id` valor do trabalho de segmento que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Após ler este guia, agora você tem uma melhor compreensão de como os trabalhos de segmento funcionam.
