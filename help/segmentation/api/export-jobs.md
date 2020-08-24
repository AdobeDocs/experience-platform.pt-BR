---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportar ponto de extremidade de trabalhos
topic: developer guide
translation-type: tm+mt
source-git-commit: 6ddb420ad3c4df3096dac456c58afc7a4916ce51
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 2%

---


# Exportar ponto de extremidade de trabalhos

Os trabalhos de exportação são processos assíncronos usados para persistir membros de segmentos de audiência em conjuntos de dados. Você pode usar o `/export/jobs` endpoint na API de segmentação do Adobe Experience Platform, que permite recuperar, criar e cancelar programaticamente trabalhos de exportação.

>[!NOTE]
>
>Este guia cobre o uso de trabalhos de exportação no [!DNL Segmentation API]. Para obter informações sobre como gerenciar trabalhos de exportação para [!DNL Real-time Customer Profile] dados, consulte o guia sobre trabalhos de [exportação na API do Perfil](../../profile/api/export-jobs.md)

## Introdução

Os pontos de extremidade usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter informações importantes que você precisa saber para fazer chamadas à API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Recuperar uma lista de trabalhos de exportação {#retrieve-list}

É possível recuperar uma lista de todos os trabalhos de exportação para a Organização IMS, fazendo uma solicitação de GET para o `/export/jobs` endpoint.

**Formato da API**

O `/export/jobs` terminal suporta vários parâmetros de query para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Efetuar uma chamada para este terminal sem parâmetros recuperará todas as tarefas de exportação disponíveis para a sua organização. Vários parâmetros podem ser incluídos, separados por E comercial (`&`).

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
| `{STATUS}` | Filtros os resultados com base no status. Os valores suportados são &quot;NOVO&quot;, &quot;BEM-SUCEDIDO&quot; e &quot;FALHADO&quot;. |

**Solicitação**

A solicitação a seguir recuperará os dois últimos trabalhos de exportação dentro da Organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de trabalhos de exportação concluídos com êxito, com base no parâmetro de query fornecido no caminho da solicitação.

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
| `destination` | Informações de destino para os dados exportados:<ul><li>`datasetId`: A ID do conjunto de dados no qual os dados foram exportados.</li><li>`segmentPerBatch`: Um valor booliano que mostra se as IDs de segmento estão ou não consolidadas. Um valor de &quot;false&quot; significa que todas as IDs de segmento são exportadas para uma única ID de lote. Um valor &quot;true&quot; significa que uma ID de segmento é exportada para uma ID de lote. **Observação:** Definir o valor como true pode afetar o desempenho da exportação em lote.</li></ul> |
| `fields` | Uma lista dos campos exportados, separada por vírgulas. |
| `schema.name` | O nome do schema associado ao conjunto de dados no qual os dados devem ser exportados. |
| `filter.segments` | Os segmentos que são exportados. Os seguintes campos estão incluídos:<ul><li>`segmentId`: A ID de segmento para a qual os perfis serão exportados.</li><li>`segmentNs`: Namespace do segmento para o determinado `segmentID`.</li><li>`status`: Uma matriz de strings que fornece um filtro de status para o `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: &quot;realizado&quot;, &quot;existente&quot; e &quot;encerrado&quot;.</li></ul> |
| `mergePolicy` | Mesclar informações de política para os dados exportados. |
| `metrics.totalTime` | Um campo que indica o tempo total que o trabalho de exportação levou para ser executado. |
| `metrics.profileExportTime` | Um campo que indica o tempo que os perfis levaram para exportar. |
| `page` | Informações sobre a paginação dos trabalhos de exportação solicitados. |
| `link.next` | Um link para a próxima página de trabalhos de exportação. |

## Criar um novo trabalho de exportação {#create}

Você pode criar um novo trabalho de exportação, fazendo uma solicitação POST para o `/export/jobs` endpoint.

**Formato da API**

```http
POST /export/jobs
```

**Solicitação**

A solicitação a seguir cria uma nova tarefa de exportação, configurada pelos parâmetros fornecidos na carga.

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
| `fields` | Uma lista dos campos exportados, separada por vírgulas. Se deixado em branco, todos os campos serão exportados. |
| `mergePolicy` | Especifica a política de mesclagem para reger os dados exportados. Inclua esse parâmetro quando houver vários segmentos sendo exportados. Se não fornecido, a exportação adotará a mesma política de mesclagem que o segmento especificado. |
| `filter` | Um objeto que especifica os segmentos que serão incluídos na tarefa de exportação por ID, tempo de qualificação ou tempo de assimilação, dependendo das subpropriedades listadas abaixo. Se deixados em branco, todos os dados serão exportados. |
| `filter.segments` | Especifica os segmentos a serem exportados. A omissão desse valor resultará na exportação de todos os dados de todos os perfis. Aceita uma matriz de objetos de segmento, cada um contendo os seguintes campos:<ul><li>`segmentId`: **(Obrigatório se estiver usando`segments`)** a ID do segmento para perfis a serem exportados.</li><li>`segmentNs` *(Opcional)* namespace de segmento para o determinado `segmentID`.</li><li>`status` *(Opcional)* Uma matriz de strings que fornece um filtro de status para o `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Possible values include: `"realized"`, `"existing"`, and `"exited"`.</li></ul> |
| `filter.segmentQualificationTime` | Filtrar com base no tempo de qualificação do segmento. A hora e/ou a hora de término do start podem ser fornecidas. |
| `filter.segmentQualificationTime.startTime` | Hora do start de qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora do start para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | Hora de término da qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora de término para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | Limita os perfis exportados a incluírem apenas os que foram atualizados após esse carimbo de data e hora. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` para **perfis**, se fornecidos: Inclui todos os perfis unidos nos quais o carimbo de data e hora atualizado unido é maior que o carimbo de data e hora fornecido. Suporta `greater_than` operando.</li><li>`fromIngestTimestamp` para **eventos**: Todos os eventos ingeridos após esse carimbo de data e hora serão exportados, correspondendo ao resultado do perfil resultante. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos.</li> |
| `filter.emptyProfiles` | Um valor booliano que indica se deve ser filtrado para perfis vazios. Perfis podem conter registros de perfis, registros ExperienceEvent ou ambos. Perfis sem registros de perfis e somente registros ExperienceEvent são chamados de &quot;emptyProfiles&quot;. Para exportar todos os perfis no repositório de perfis, incluindo &quot;emptyProfiles&quot;, defina o valor de `emptyProfiles` como `true`. Se `emptyProfiles` estiver definido como `false`, somente perfis com registros de perfis na loja serão exportados. Por padrão, se `emptyProfiles` o atributo não estiver incluído, somente os perfis que contêm registros de perfis serão exportados. |
| `additionalFields.eventList` | Controla os campos de evento da série de tempo exportados para objetos filhos ou associados, fornecendo uma ou mais das seguintes configurações:<ul><li>`fields`: Controle os campos a serem exportados.</li><li>`filter`: Especifica critérios que limitam os resultados incluídos dos objetos associados. Espera um valor mínimo necessário para exportação, geralmente uma data.</li><li>`filter.fromIngestTimestamp`: Filtros eventos de séries de tempo para os que foram ingeridos após o carimbo de data e hora fornecido. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos.</li><li>`filter.toIngestTimestamp`: Filtros o carimbo de data e hora para aqueles que foram ingeridos antes do carimbo de data e hora fornecido. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos.</li></ul> |
| `destination` | **(Obrigatório)** Informações sobre os dados exportados:<ul><li>`datasetId`: **(Obrigatório)** A ID do conjunto de dados no qual os dados devem ser exportados.</li><li>`segmentPerBatch`: *(Opcional)* Um valor booliano que, se não fornecido, assume como padrão &quot;false&quot;. Um valor de &quot;false&quot; exporta todas as IDs de segmento para uma única ID de lote. Um valor &quot;true&quot; exporta uma ID de segmento para uma ID de lote. Observe que definir o valor como &quot;true&quot; pode afetar o desempenho de exportação em lote.</li></ul> |
| `schema.name` | **(Obrigatório)** O nome do schema associado ao conjunto de dados no qual os dados devem ser exportados. |
| `evaluationInfo.segmentation` | *(Opcional)* Um valor booliano que, se não fornecido, assumirá o padrão `false`. Um valor de `true` indica que a segmentação precisa ser feita no trabalho de exportação. |

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

Como alternativa, se `destination.segmentPerBatch` tivesse sido definido como `true`, o `destination` objeto acima teria uma `batches` matriz, como mostrado abaixo:

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
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

Você pode recuperar informações detalhadas sobre um trabalho de exportação específico, fazendo uma solicitação de GET para o ponto final e fornecendo a ID do trabalho de exportação que deseja recuperar no caminho da solicitação. `/export/jobs`

**Formato da API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` da tarefa de exportação que você deseja acessar. |

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
| `destination` | Informações de destino para os dados exportados:<ul><li>`datasetId`: A ID do conjunto de dados no qual os dados foram exportados.</li><li>`segmentPerBatch`: Um valor booliano que mostra se as IDs de segmento estão ou não consolidadas. Um valor de `false` significa que todas as IDs de segmento estavam em uma única ID de lote. Um valor de `true` significa que uma ID de segmento é exportada para uma ID de lote.</li></ul> |
| `fields` | Uma lista dos campos exportados, separada por vírgulas. |
| `schema.name` | O nome do schema associado ao conjunto de dados no qual os dados devem ser exportados. |
| `filter.segments` | Os segmentos que são exportados. Os seguintes campos estão incluídos:<ul><li>`segmentId`: ID do segmento para perfis a serem exportados.</li><li>`segmentNs`: Namespace do segmento para o determinado `segmentID`.</li><li>`status`: Uma matriz de strings que fornece um filtro de status para o `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: &quot;realizado&quot;, &quot;existente&quot; e &quot;encerrado&quot;.</li></ul> |
| `mergePolicy` | Mesclar informações de política para os dados exportados. |
| `metrics.totalTime` | Um campo que indica o tempo total que o trabalho de exportação levou para ser executado. |
| `metrics.profileExportTime` | Um campo que indica o tempo que os perfis levaram para exportar. |
| `totalExportedProfileCounter` | O número total de perfis exportados em todos os lotes. |

## Cancelar ou excluir um trabalho de exportação específico {#delete}

Você pode solicitar a exclusão do trabalho de exportação especificado, fazendo uma solicitação de DELETE para o `/export/jobs` ponto final e fornecendo a ID do trabalho de exportação que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` da tarefa de exportação que você deseja excluir. |

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

Depois de ler este guia, agora você tem um melhor entendimento de como as tarefas de exportação funcionam.