---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportar dados usando APIs
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 1%

---


# Exportar dados do Perfil usando APIs

O Perfil do cliente em tempo real permite que você crie uma única visualização de clientes individuais, reunindo dados de várias fontes, incluindo dados de atributos e dados comportamentais. Os dados disponíveis no Perfil podem ser exportados para um conjunto de dados para processamento adicional. Este tutorial fornece instruções passo a passo para criar e gerenciar trabalhos de exportação usando a API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentação.

Além de criar um trabalho de exportação, você também pode acessar os dados do Perfil usando a API de acesso ao Perfil e as projeções. Consulte o tutorial [da API de acesso ao](../../profile/api/entities.md) Perfil ou o tutorial sobre como [configurar destinos de borda e projeções](../../profile/api/edge-projections.md) para obter mais informações sobre esses outros padrões de acesso.

## Introdução

Este tutorial requer um entendimento prático dos vários serviços de Adobe Experience Platform envolvidos no trabalho com dados de Perfis. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [Serviço](../home.md)de segmentação de Adobe Experience Platform: Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
- [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

### Cabeçalhos obrigatórios

Este tutorial também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito às APIs da Platform. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. As solicitações às APIs da Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar um trabalho de exportação

Exportar dados de Perfil requer primeiro criar um conjunto de dados no qual os dados serão exportados e, em seguida, iniciar um novo trabalho de exportação. Ambas as etapas podem ser realizadas usando APIs de Experience Platform, com a primeira usando a API de serviço de catálogo e a última usando a API de Perfil do cliente em tempo real. As instruções detalhadas para completar cada etapa são descritas nas seções a seguir.

- [Criar um conjunto de dados](#create-a-target-dataset) de público alvo - Crie um conjunto de dados para manter os dados exportados.
- [Iniciar uma nova tarefa](#initiate-export-job) de exportação - Preencha o conjunto de dados com dados de Perfil individual do XDM.

### Criar um conjunto de dados de público alvo

Ao exportar dados do Perfil, um conjunto de dados do público alvo deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o schema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar um segmento, o conjunto de dados deve ser baseado no Schema de União de Perfil individual (`https://ns.adobe.com/xdm/context/profile__union`) do XDM. Um schema união é um schema gerado pelo sistema e somente leitura que agregação os campos de schemas que compartilham a mesma classe, neste caso, que é a classe de Perfil Individual XDM. Para obter mais informações sobre schemas de visualização de união, consulte a seção Perfil do cliente em tempo [real do guia](../../xdm/schema/composition.md#union)do desenvolvedor do Registro de Schemas.

As etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faz referência ao Schema de União de Perfil individual XDM usando a API de catálogo. Você também pode usar a interface do usuário do Adobe Experience Platform para criar um conjunto de dados que faça referência ao schema da união. As etapas para usar a interface do usuário são descritas [neste tutorial da interface do usuário para exportar segmentos](./create-dataset-export-segment.md) , mas também são aplicáveis aqui. Depois de concluído, você pode retornar a este tutorial para prosseguir com as etapas para [iniciar um novo trabalho](#initiate-export-job)de exportação.

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa para [iniciar um novo trabalho](#initiate-export-job)de exportação.

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome descritivo para o conjunto de dados. |
| `schemaRef.id` | A ID da visualização de união (schema) à qual o conjunto de dados será associado. |
| `fileDescription.persisted` | Um valor booliano que, quando definido como `true`, permite que o conjunto de dados persista na visualização da união. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID exclusiva, gerada pelo sistema, do conjunto de dados recém-criado. Uma ID de conjunto de dados configurada corretamente é necessária para exportar com êxito os dados do Perfil.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Iniciar trabalho de exportação

Depois que você tiver um conjunto de dados que persiste na união, poderá criar um trabalho de exportação para persistir os dados do Perfil no conjunto de dados, fazendo uma solicitação POST ao `/export/jobs` ponto final na API do Perfil do cliente em tempo real e fornecendo os detalhes dos dados que deseja exportar no corpo da solicitação.

**Formato da API**

```http
POST /export/jobs
```

**Solicitação**

A solicitação a seguir cria uma nova tarefa de exportação, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita os campos de dados a serem incluídos na exportação somente àqueles fornecidos neste parâmetro. O mesmo parâmetro também está disponível ao criar um segmento, portanto os campos no segmento podem já ter sido filtrados. A omissão desse valor resultará na inclusão de todos os campos nos dados exportados. |
| `mergePolicy` | *(Opcional)* Especifica a política de mesclagem para reger os dados exportados. Inclua esse parâmetro quando houver vários segmentos sendo exportados. Se esse valor for omitido, o Serviço de exportação usará a política de mesclagem fornecida pelo segmento. |
| `mergePolicy.id` | A ID da política de mesclagem. |
| `mergePolicy.version` | A versão específica da política de mesclagem a ser usada. A omissão desse valor assumirá como padrão a versão mais recente. |
| `filter` | *(Opcional)* Especifica um ou mais dos seguintes filtros a serem aplicados ao segmento antes da exportação. |
| `filter.segments` | *(Opcional)* Especifica os segmentos a serem exportados. A omissão desse valor resultará na exportação de todos os dados de todos os perfis. Aceita uma matriz de objetos de segmento, cada um contendo os seguintes campos:<ul><li>`segmentId`: **(Obrigatório se estiver usando`segments`)** a ID do segmento para perfis a serem exportados.</li><li>`segmentNs` *(Opcional)* namespace de segmento para o determinado `segmentID`.</li><li>`status` *(Opcional)* Uma matriz de strings que fornece um filtro de status para o `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: `"realized"`, `"existing"`e `"exited"`.</br></br>Para obter mais informações, consulte o tutorial [de](./create-a-segment.md)criação de segmentos.</li></ul> |
| `filter.segmentQualificationTime` | *(Opcional)* Filtrar com base no tempo de qualificação do segmento. A hora e/ou a hora de término do start podem ser fornecidas. |
| `filter.segmentQualificationTime.startTime` | *(Opcional)* Hora do start de qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora do start para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Opcional)* Hora de término da qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora de término para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | *(Opcional)* Limita os perfis exportados a incluírem apenas os que foram atualizados após esse carimbo de data e hora. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` para **perfis**, se fornecidos: Inclui todos os perfis unidos nos quais o carimbo de data e hora atualizado unido é maior que o carimbo de data e hora fornecido. Suporta `greater_than` operando.</li><li>`fromTimestamp` para **eventos**: Todos os eventos ingeridos após esse carimbo de data e hora serão exportados, correspondendo ao resultado do perfil resultante. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos.</li> |
| `filter.emptyProfiles` | *(Opcional)* Booliano. Perfis podem conter registros de Perfis, registros ExperienceEvent ou ambos. Perfis sem registros de Perfis e somente registros ExperienceEvent são chamados de &quot;emptyProfiles&quot;. Para exportar todos os perfis no repositório de Perfis, incluindo &quot;emptyProfiles&quot;, defina o valor de `emptyProfiles` como `true`. Se `emptyProfiles` estiver definido como `false`, somente perfis com registros de Perfis na loja serão exportados. Por padrão, se `emptyProfiles` o atributo não estiver incluído, somente os perfis que contêm registros de Perfis serão exportados. |
| `additionalFields.eventList` | *(Opcional)* Controla os campos de evento da série de tempo exportados para objetos filhos ou associados, fornecendo uma ou mais das seguintes configurações:<ul><li>`eventList.fields`: Controle os campos a serem exportados.</li><li>`eventList.filter`: Especifica critérios que limitam os resultados incluídos dos objetos associados. Espera um valor mínimo necessário para exportação, geralmente uma data.</li><li>`eventList.filter.fromIngestTimestamp`: Filtros eventos de séries cronológicas para os que foram ingeridos após o carimbo de data e hora fornecido. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos.</li></ul> |
| `destination` | **(Obrigatório)** Informações de destino para os dados exportados:<ul><li>`destination.datasetId`: **(Obrigatório)** A ID do conjunto de dados no qual os dados devem ser exportados.</li><li>`destination.segmentPerBatch`: *(Opcional)* Um valor booliano que, se não fornecido, assumirá o padrão `false`. Um valor de `false` exporta todas as IDs de segmento para uma única ID de lote. Um valor de `true` exporta uma ID de segmento para uma ID de lote. Observe que a configuração do valor a ser `true` pode afetar o desempenho da exportação em lote.</li></ul> |
| `schema.name` | **(Obrigatório)** O nome do schema associado ao conjunto de dados no qual os dados devem ser exportados. |
| `evaluationInfo.segmentation` | *(Opcional)* Um valor booliano que, se não fornecido, assumirá o padrão `false`. Um valor de `true` indica que a segmentação precisa ser feita no trabalho de exportação. |

>[!NOTE]
>
>Para exportar apenas dados de Perfil, e não incluir dados relacionados do ExperienceEvent, remova o objeto &quot;additionalFields&quot; da solicitação.

**Resposta**

Uma resposta bem-sucedida retorna um conjunto de dados preenchido com dados de Perfil, conforme especificado na solicitação.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Se não `destination.segmentPerBatch` tivesse sido incluído na solicitação (se não estiver presente, o padrão é `false`) ou o valor tiver sido definido como `false`, o `destination` objeto na resposta acima não teria uma `batches` matriz e, em vez disso, incluiria apenas uma `batchId`, como mostrado abaixo. Esse único lote incluiria todas as IDs de segmento, enquanto a resposta acima mostra uma única ID de segmento por ID de lote.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## Lista de todos os trabalhos de exportação

Você pode retornar uma lista de todos os trabalhos de exportação para uma Organização IMS específica, executando uma solicitação GET para o `export/jobs` endpoint. A solicitação também suporta os parâmetros de query `limit` e `offset`, como mostrado abaixo.

**Formato da API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propriedade | Descrição |
| -------- | ----------- |
| `limit` | Especifique o número de registros a serem retornados. |
| `offset` | Deslocar a página de resultados a ser retornada pelo número fornecido. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

A resposta inclui um `records` objeto que contém os trabalhos de exportação criados pela Organização IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
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
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
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
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Monitorar progresso de exportação

Para visualização dos detalhes de uma tarefa de exportação específica ou monitoramento de seu status enquanto é processada, é possível fazer uma solicitação GET ao `/export/jobs` endpoint e incluir o `id` da tarefa de exportação no caminho. A tarefa de exportação é concluída assim que o `status` campo retorna o valor &quot;SUCEDIDO&quot;.

**Formato da API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` da tarefa de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `batchId` | O identificador dos lotes criados a partir de uma exportação bem-sucedida, a ser usado para fins de pesquisa ao ler os dados do Perfil. |

## Cancelar uma tarefa de exportação

O Experience Platform permite cancelar um trabalho de exportação existente, o que pode ser útil por vários motivos, incluindo se o trabalho de exportação não foi concluído ou ficou preso no estágio de processamento. Para cancelar um trabalho de exportação, você pode executar uma solicitação DELETE para o `/export/jobs` ponto de extremidade e incluir o trabalho `id` de exportação que deseja cancelar no caminho da solicitação.

**Formato da API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` da tarefa de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio, indicando que a operação de cancelamento foi bem-sucedida.

## Próximas etapas

Quando a exportação for concluída com êxito, seus dados estarão disponíveis no Data Lake, no Experience Platform. Em seguida, você pode usar a API [de acesso a](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dados para acessar os dados usando a API `batchId` associada à exportação. Dependendo do tamanho da exportação, os dados podem estar em pedaços e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar a API de acesso a dados para acessar e baixar arquivos em lote, siga o tutorial [de acesso a](../../data-access/tutorials/dataset-data.md)dados.

Você também pode acessar os dados exportados com êxito do Perfil do cliente em tempo real usando o Serviço de Query do Adobe Experience Platform. Usando a interface do usuário ou RESTful API, o Serviço de Query permite que você grave, valide e execute query em dados dentro do Data Lake.

Para obter mais informações sobre como query dados de audiência, consulte a documentação [do serviço de](../../query-service/home.md)Query.