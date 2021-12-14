---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; exportar trabalhos; api;
solution: Experience Platform
title: Exporte o Ponto de Extremidade da API de Tarefas
topic-legacy: developer guide
description: Os trabalhos de exportação são processos assíncronos usados para manter os membros do segmento do público-alvo em conjuntos de dados. Você pode usar o endpoint /export/jobs na API do Serviço de Segmentação do Adobe Experience Platform, que permite recuperar, criar e cancelar programaticamente trabalhos de exportação.
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 2%

---

# Ponto de extremidade de tarefas de exportação

Os trabalhos de exportação são processos assíncronos usados para manter os membros do segmento do público-alvo em conjuntos de dados. Você pode usar o `/export/jobs` endpoint na API de segmentação do Adobe Experience Platform, que permite recuperar, criar e cancelar programaticamente tarefas de exportação.

>[!NOTE]
>
>Este guia aborda o uso de trabalhos de exportação no [!DNL Segmentation API]. Para obter informações sobre como gerenciar trabalhos de exportação para [!DNL Real-time Customer Profile] , consulte o guia sobre [exportar trabalhos na API de perfil](../../profile/api/export-jobs.md)

## Introdução

Os endpoints usados neste guia fazem parte do [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Recuperar uma lista de trabalhos de exportação {#retrieve-list}

Você pode recuperar uma lista de todos os trabalhos de exportação para sua Organização IMS fazendo uma solicitação de GET para a `/export/jobs` endpoint .

**Formato da API**

O `/export/jobs` O endpoint oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Efetuar uma chamada para esse endpoint sem parâmetros recuperará todos os trabalhos de exportação disponíveis para sua organização. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{LIMIT}` | Especifica o número de trabalhos de exportação retornados. |
| `{OFFSET}` | Especifica o deslocamento das páginas de resultados. |
| `{STATUS}` | Filtra os resultados com base no status . Os valores suportados são &quot;NEW&quot;, &quot;SUCCEEDED&quot; e &quot;FAILED&quot;. |

**Solicitação**

A solicitação a seguir recuperará os dois últimos trabalhos de exportação na organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de tarefas de exportação concluídas com êxito, com base no parâmetro de consulta fornecido no caminho da solicitação.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
        },
        {
            "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
            "errors": [
                {
                    "code": "0090000009",
                    "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
                },
                {
                    "code": "unknown",
                    "msg": "Job aborted.",
                    "callStack": "org.apache.spark.SparkException: Job aborted."
                }
            ],
            "jobType": "BATCH",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized", "existing"]
                    }
                ]
            },
            "id": 722,
            "schema": {
                "name": "_xdm.context.profile"
            },
            "mergePolicy": {
                "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
                "version": 1
            },
            "status": "FAILED",
            "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
            "computeGatewayJobId": {
                "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
            },
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1538573416687,
                    "endTimeInMs": 1538573922551,
                    "totalTimeInMs": 505864
                },
                "profileExportTime": {
                    "startTimeInMs": 1538573872211,
                    "endTimeInMs": 1538573918809,
                    "totalTimeInMs": 46598
                }
            },
            "destination": {
                "datasetId": "5bb4c46757920712f924a3eb",
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `destination` | Informações de destino para os dados exportados:<ul><li>`datasetId`: A ID do conjunto de dados em que os dados foram exportados.</li><li>`segmentPerBatch`: Um valor booleano que mostra se as IDs de segmento foram ou não consolidadas. Um valor &quot;false&quot; significa que todas as IDs de segmento são exportadas para uma única ID de lote. Um valor &quot;true&quot; significa que uma ID de segmento é exportada para uma ID de lote. **Observação:** Definir o valor como true pode afetar o desempenho da exportação de lote.</li></ul> |
| `fields` | Uma lista dos campos exportados, separados por vírgulas. |
| `schema.name` | O nome do schema associado ao conjunto de dados em que os dados devem ser exportados. |
| `filter.segments` | Os segmentos que são exportados. Os seguintes campos estão incluídos:<ul><li>`segmentId`: A ID de segmento para a qual os perfis serão exportados.</li><li>`segmentNs`: Namespace do segmento para um determinado `segmentID`.</li><li>`status`: Uma matriz de strings que fornece um filtro de status para a variável `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: &quot;realizado&quot;, &quot;existente&quot; e &quot;encerrado&quot;. Um valor &quot;realizado&quot; significa que o perfil está inserindo o segmento. Um valor &quot;existente&quot; significa que o perfil continua a estar no segmento. Um valor &quot;existente&quot; significa que o perfil está saindo do segmento.</li></ul> |
| `mergePolicy` | Mesclar informações de política para os dados exportados. |
| `metrics.totalTime` | Um campo que indica o tempo total que o trabalho de exportação levou para ser executado. |
| `metrics.profileExportTime` | Um campo que indica o tempo que os perfis levaram para exportar. |
| `page` | Informações sobre a paginação dos trabalhos de exportação solicitados. |
| `link.next` | Um link para a próxima página de trabalhos de exportação. |

## Criar um novo trabalho de exportação {#create}

Você pode criar um novo trabalho de exportação fazendo uma solicitação de POST para o `/export/jobs` endpoint .

**Formato da API**

```http
POST /export/jobs
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de exportação, configurado pelos parâmetros fornecidos no payload.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `fields` | Uma lista dos campos exportados, separados por vírgulas. Se permanecer em branco, todos os campos serão exportados. |
| `mergePolicy` | Especifica a política de mesclagem para controlar os dados exportados. Inclua esse parâmetro quando houver vários segmentos sendo exportados. Se não for fornecido, a exportação terá a mesma política de mesclagem do segmento em questão. |
| `filter` | Um objeto que especifica os segmentos que serão incluídos no trabalho de exportação por ID, tempo de qualificação ou tempo de assimilação, dependendo das subpropriedades listadas abaixo. Se deixado em branco, todos os dados serão exportados. |
| `filter.segments` | Especifica os segmentos a serem exportados. A omissão desse valor resultará na exportação de todos os dados de todos os perfis. Aceita uma matriz de objetos de segmento, cada um contendo os seguintes campos:<ul><li>`segmentId`: **(Obrigatório se estiver usando `segments`)** ID do segmento para perfis a serem exportados.</li><li>`segmentNs` *(Opcional)* Namespace do segmento para um determinado `segmentID`.</li><li>`status` *(Opcional)* Uma matriz de strings que fornece um filtro de status para a variável `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: `"realized"`, `"existing"`e `"exited"`.  Um valor &quot;realizado&quot; significa que o perfil está inserindo o segmento. Um valor &quot;existente&quot; significa que o perfil continua a estar no segmento. Um valor &quot;existente&quot; significa que o perfil está saindo do segmento.</li></ul> |
| `filter.segmentQualificationTime` | Filtro com base no tempo de qualificação de segmento. A hora de início e/ou de término pode ser fornecida. |
| `filter.segmentQualificationTime.startTime` | Hora de início da qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora de início de uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido em [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. |
| `filter.segmentQualificationTime.endTime` | Tempo final de qualificação de segmento para uma ID de segmento para um status específico. Não fornecido, não haverá filtro no tempo final para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido em [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. |
| `filter.fromIngestTimestamp ` | Limita perfis exportados para incluir apenas aqueles que foram atualizados após esse carimbo de data e hora. O carimbo de data e hora deve ser fornecido em [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. <ul><li>`fromIngestTimestamp` para **perfis**, se previsto: Inclui todos os perfis mesclados em que o carimbo de data e hora atualizado unido é maior que o carimbo de data e hora especificado. Suporta `greater_than` operando.</li><li>`fromIngestTimestamp` para **events**: Todos os eventos assimilados após esse carimbo de data e hora serão exportados correspondendo ao resultado do perfil resultante. Esse não é o momento do evento em si, mas o tempo de assimilação dos eventos.</li> |
| `filter.emptyProfiles` | Um valor booleano que indica se deve ser filtrado para perfis vazios. Os perfis podem conter registros de perfil, registros do ExperienceEvent ou ambos. Perfis sem registros de perfil e somente registros ExperienceEvent são chamados de &quot;emptyProfiles&quot;. Para exportar todos os perfis no armazenamento de perfis, incluindo o &quot;emptyProfiles&quot;, defina o valor de `emptyProfiles` para `true`. If `emptyProfiles` está definida como `false`, somente perfis com registros de perfil na loja são exportados. Por padrão, se `emptyProfiles` não estiver incluído, somente perfis contendo registros de perfil serão exportados. |
| `additionalFields.eventList` | Controla os campos de evento da série de tempo exportados para objetos filhos ou associados fornecendo uma ou mais das seguintes configurações:<ul><li>`fields`: Controle os campos a serem exportados.</li><li>`filter`: Especifica critérios que limitam os resultados incluídos dos objetos associados. Espera um valor mínimo necessário para a exportação, normalmente uma data.</li><li>`filter.fromIngestTimestamp`: Filtra eventos de séries de tempo para aqueles que foram assimilados após o carimbo de data e hora fornecido. Esse não é o momento do evento em si, mas o tempo de assimilação dos eventos.</li><li>`filter.toIngestTimestamp`: Filtra o carimbo de data e hora para aqueles que foram assimilados antes do carimbo de data e hora fornecido. Esse não é o momento do evento em si, mas o tempo de assimilação dos eventos.</li></ul> |
| `destination` | **(Obrigatório)** Informações sobre os dados exportados:<ul><li>`datasetId`: **(Obrigatório)** A ID do conjunto de dados em que os dados devem ser exportados.</li><li>`segmentPerBatch`: *(Opcional)* Um valor booleano que, se não fornecido, padroniza &quot;false&quot;. Um valor &quot;false&quot; exporta todas as IDs de segmento para uma única ID de lote. Um valor &quot;true&quot; exporta uma ID de segmento para uma ID de lote. Observe que definir o valor como &quot;true&quot; pode afetar o desempenho da exportação de lote.</li></ul> |
| `schema.name` | **(Obrigatório)** O nome do schema associado ao conjunto de dados em que os dados devem ser exportados. |
| `evaluationInfo.segmentation` | *(Opcional)* Um valor booleano que, se não for fornecido, assumirá como padrão `false`. Um valor de `true` indica que a segmentação precisa ser feita no trabalho de exportação. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do trabalho de exportação recém-criado.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um valor somente leitura gerado pelo sistema que identifica o trabalho de exportação que acabou de ser criado. |

Como alternativa, se `destination.segmentPerBatch` estava definida como `true`, o `destination` o objeto acima teria um `batches` , conforme mostrado abaixo:

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## Recuperar um trabalho de exportação específico {#get}

Você pode recuperar informações detalhadas sobre um trabalho de exportação específico fazendo uma solicitação do GET para a `/export/jobs` endpoint e fornecer a ID do trabalho de exportação que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` do trabalho de exportação que deseja acessar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o trabalho de exportação especificado.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `destination` | Informações de destino para os dados exportados:<ul><li>`datasetId`: A ID do conjunto de dados em que os dados foram exportados.</li><li>`segmentPerBatch`: Um valor booleano que mostra se as IDs de segmento foram ou não consolidadas. Um valor de `false` significa que todas as IDs de segmento estavam em uma única ID de lote. Um valor de `true` significa que uma ID de segmento é exportada para uma ID de lote.</li></ul> |
| `fields` | Uma lista dos campos exportados, separados por vírgulas. |
| `schema.name` | O nome do schema associado ao conjunto de dados em que os dados devem ser exportados. |
| `filter.segments` | Os segmentos que são exportados. Os seguintes campos estão incluídos:<ul><li>`segmentId`: ID do segmento para perfis a serem exportados.</li><li>`segmentNs`: Namespace do segmento para um determinado `segmentID`.</li><li>`status`: Uma matriz de strings que fornece um filtro de status para a variável `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: &quot;realizado&quot;, &quot;existente&quot; e &quot;encerrado&quot;.  Um valor &quot;realizado&quot; significa que o perfil está inserindo o segmento. Um valor &quot;existente&quot; significa que o perfil continua a estar no segmento. Um valor &quot;existente&quot; significa que o perfil está saindo do segmento.</li></ul> |
| `mergePolicy` | Mesclar informações de política para os dados exportados. |
| `metrics.totalTime` | Um campo que indica o tempo total que o trabalho de exportação levou para ser executado. |
| `metrics.profileExportTime` | Um campo que indica o tempo que os perfis levaram para exportar. |
| `totalExportedProfileCounter` | O número total de perfis exportados em todos os lotes. |

## Cancelar ou excluir um trabalho de exportação específico {#delete}

Você pode solicitar a exclusão do trabalho de exportação especificado, fazendo uma solicitação de DELETE para a `/export/jobs` endpoint e fornecer a ID do trabalho de exportação que você deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` do trabalho de exportação que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 com a seguinte mensagem:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Próximas etapas

Após a leitura deste guia, você tem uma melhor compreensão de como os trabalhos de exportação funcionam.
