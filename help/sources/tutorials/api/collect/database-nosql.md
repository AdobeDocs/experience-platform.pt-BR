---
title: Criar um Fluxo de Dados para Origens de Banco de Dados Usando a API de Serviço de Fluxo
type: Tutorial
description: Saiba como usar a API do Serviço de fluxo para criar um fluxo de dados e assimilar dados do banco de dados na Experience Platform.
exl-id: 1e1f9bbe-eb5e-40fb-a03c-52df957cb683
source-git-commit: 2ad0ffba128e8c51f173d24d4dd2404b9cbbb59a
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 3%

---

# Criar um fluxo de dados para fontes de banco de dados usando a API [!DNL Flow Service]

Leia este tutorial para saber como criar um fluxo de dados e assimilar dados do seu banco de dados na Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>* Para criar um fluxo de dados, você já deve ter uma ID de conexão base válida com uma origem de banco de dados. Se você não tiver essa ID, visite o [catálogo de fontes](../../../home.md#database) para exibir uma lista de fontes de banco de dados com as quais você pode criar uma conexão base.
>* Para que o Experience Platform assimile dados, os fusos horários de todas as fontes de lote baseadas em tabela devem ser configurados como UTC. O único carimbo de data/hora com suporte para [[!DNL Snowflake] origem](../../../connectors/databases/snowflake.md) é TIMESTAMP_NTZ com hora UTC.

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Guia do desenvolvedor do Registro de Esquema](../../../../xdm/api/getting-started.md): inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro de Esquema. Isso inclui o `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Aceitar e seus valores possíveis).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo é o sistema de registro para localização e linhagem de dados no Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): a API de assimilação em lote permite assimilar dados na Experience Platform como arquivos em lote.
* [Sandboxes](../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../landing/api-guide.md).

## Criar uma conexão de origem {#source}

Você pode criar uma conexão de origem fazendo uma solicitação POST para a API [!DNL Flow Service]. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

Para criar uma conexão de origem, você também deve definir um valor de enumeração para o atributo de formato de dados.

Use os seguintes valores de enumeração para conectores baseados em arquivo:

| Formato dos dados | Valor de enumeração |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todos os conectores baseados em tabela, defina o valor como `tabular`.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Database source connection",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "description": "Database source connection",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "test1.Mytable",
      "columns": [
        {
          "name": "TestID",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Name",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Datefield",
          "type": "string",
          "meta:xdmType": "date-time",
          "xdm": {
            "type": "string",
            "format": "date-time"
          }
        }
      ],
      "cdcEnabled": true
    },
    "connectionSpec": {
      "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
      "version": "1.0"
    }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `baseConnectionId` | A ID de conexão da origem do banco de dados. |
| `params.tableName` | O caminho do arquivo de origem. |
| `params.cdcEnabled` | Um valor booleano que indica se a captura do histórico de alterações está ativada. Quando usado com esquemas relacionais, a captura de dados de alteração rastreia inserções, atualizações e exclusões para manter o conjunto de dados de destino sincronizado com a origem. Esta propriedade é suportada pelas seguintes fontes de banco de dados: <ul><li>[!DNL Azure Databricks]</li><li>[!DNL Google BigQuery]</li><li>[!DNL Snowflake]</li></ul> Para obter uma visão geral desse recurso, consulte a [visão geral do Data Mirror](../../../../xdm/data-mirror/overview.md). Para obter detalhes sobre a implementação, consulte [alterar captura de dados no guia de origens](../change-data-capture.md) e [referência técnica de esquemas relacionais](../../../../xdm/schema/relational.md). |
| `connectionSpec.id` | A ID da especificação de conexão da origem do banco de dados. Consulte o [Apêndice](#appendix) para obter uma lista de IDs de especificação do banco de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária nas etapas posteriores para criar uma conexão de destino.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados no Experience Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados do Experience Platform no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](../../../../xdm/api/schemas.md).

## Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornecendo a ID do esquema de destino na carga.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../../catalog/api/create-dataset.md).

## Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação da conexão fixa associada ao Data Lake. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o data lake. Usando a API [!DNL Flow Service], você pode criar uma conexão de destino especificando esses identificadores junto com o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```http
POST /targetConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Database target connection",
        "description": "Database target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "6019e0e7c5dcf718db5ebc71"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.schema.id` | O `$id` do esquema XDM de destino. |
| `data.schema.version` | A versão do esquema. Este valor deve ser definido como `application/vnd.adobe.xed-full+json;version=1`, que retorna a versão secundária mais recente do esquema. |
| `params.dataSetId` | A ID do conjunto de dados de destino gerado na etapa anterior. **Observação**: você deve fornecer uma ID de conjunto de dados válida ao criar uma conexão de destino. Uma ID de conjunto de dados inválida resultará em um erro. |
| `connectionSpec.id` | A ID da especificação de conexão usada para conectar ao data lake. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão de destino. Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
    "etag": "\"c0038936-0000-0200-0000-6019e1190000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere.

Para criar um conjunto de mapeamento, faça uma solicitação POST para o ponto de extremidade `mappingSets` da [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/) enquanto fornece o esquema XDM de destino `$id` e os detalhes dos conjuntos de mapeamento que deseja criar.

**Formato da API**

```http
POST /mappingSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "TestID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.birthDate",
                "sourceAttribute": "Datefield",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `xdmSchema` | O `$id` do esquema XDM de destino. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "0b090130b58b4819afc78b6dc98b484d",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificações de fluxo de dados {#specs}

Um fluxo de dados é responsável por coletar dados de fontes e trazê-los para o Experience Platform. Para criar um fluxo de dados, primeiro obtenha as especificações do fluxo de dados executando uma solicitação GET para a API [!DNL Flow Service]. As especificações de fluxo de dados são responsáveis pela coleta de dados de um banco de dados externo ou sistema NoSQL.

**Formato da API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação do fluxo de dados responsáveis por trazer os dados de sua origem para a Experience Platform. A resposta inclui a especificação de fluxo exclusiva `id` necessária para criar um novo fluxo de dados.

>[!NOTE]
>
>A carga de resposta JSON abaixo está oculta por brevidade. Selecione &quot;carga&quot; para ver a carga de resposta.

+++ Exibir conteúdo

```json
{
  "id": "14518937-270c-4525-bdec-c2ba7cce3860",
  "name": "CRMToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "3416976c-a9ca-4bba-901a-1f08f66978ff",
    "38ad80fe-8b06-4938-94f4-d4ee80266b07",
    "d771e9c1-4f26-40dc-8617-ce58c4b53702",
    "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
    "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
    "3000eb99-cd47-43f3-827c-43caf170f015",
    "26d738e0-8963-47ea-aadf-c60de735468a",
    "74a1c565-4e59-48d7-9d67-7c03b8a13137",
    "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
    "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
    "cb66ab34-8619-49cb-96d1-39b37ede86ea",
    "eb13cb25-47ab-407f-ba89-c0125281c563",
    "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
    "37b6bf40-d318-4655-90be-5cd6f65d334b",
    "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
    "221c7626-58f6-4eec-8ee2-042b0226f03b",
    "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
    "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
    "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
    "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
    "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
    "102706fb-a5cd-42ee-afe0-bc42f017ff43",
    "09182899-b429-40c9-a15a-bf3ddbc8ced7",
    "0479cc14-7651-4354-b233-7480606c2ac3",
    "d6b52d86-f0f8-475f-89d4-ce54c8527328",
    "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
    "1fe283f6-9bec-11ea-bb37-0242ac130002",
    "fcad62f3-09b0-41d3-be11-449d5a621b69",
    "ea1c2a08-b722-11eb-8529-0242ac130003",
    "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
    "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
    "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
    "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
    "929e4450-0237-4ed2-9404-b7e1e0a00309",
    "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
    "2fa8af9c-2d1a-43ea-a253-f00a00c74412"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
  "permissionsInfo": {
    "view": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "optionSpec": {
    "name": "OptionSpec",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "errorDiagnosticsEnabled": {
          "title": "Error diagnostics.",
          "description": "Flag to enable detailed and sample error diagnostics summary.",
          "type": "boolean",
          "default": false
        },
        "partialIngestionPercent": {
          "title": "Partial ingestion threshold.",
          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
          "type": "number",
          "exclusiveMinimum": 0
        }
      }
    }
  },
  "scheduleSpec": {
    "name": "PeriodicSchedule",
    "type": "Periodic",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "startTime": {
          "description": "epoch time",
          "type": "integer"
        },
        "frequency": {
          "type": "string",
          "enum": [
            "once",
            "minute",
            "hour",
            "day",
            "week"
          ]
        },
        "interval": {
          "type": "integer"
        },
        "backfill": {
          "type": "boolean",
          "default": true
        }
      },
      "required": [
        "startTime",
        "frequency"
      ],
      "if": {
        "properties": {
          "frequency": {
            "const": "once"
          }
        }
      },
      "then": {
        "allOf": [
          {
            "not": {
              "required": [
                "interval"
              ]
            }
          },
          {
            "not": {
              "required": [
                "backfill"
              ]
            }
          }
        ]
      },
      "else": {
        "required": [
          "interval"
        ],
        "if": {
          "properties": {
            "frequency": {
              "const": "minute"
            }
          }
        },
        "then": {
          "properties": {
            "interval": {
              "minimum": 15
            }
          }
        },
        "else": {
          "properties": {
            "interval": {
              "minimum": 1
            }
          }
        }
      }
    }
  },
  "transformationSpec": [
    {
      "name": "Copy",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "properties": {
          "deltaColumn": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "dateFormat": {
                "type": "string"
              },
              "timezone": {
                "type": "string"
              }
            },
            "required": [
              "name"
            ]
          }
        },
        "required": [
          "deltaColumn"
        ]
      }
    },
    {
      "name": "Mapping",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for different mapping from source to target",
        "properties": {
          "mappingId": {
            "type": "string"
          },
          "mappingVersion": {
            "type": "string"
          }
        }
      }
    }
  ],
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "deltaColumn": {
            "type": "object",
            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
            "properties": {
              "name": {
                "type": "string"
              },
              "dateFormat": {
                "type": "string"
              },
              "timezone": {
                "type": "string"
              }
            },
            "required": [
              "name"
            ]
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime",
          "deltaColumn"
        ]
      }
    }
}
```

+++

## Criar um fluxo de dados

A última etapa para coletar dados é criar um fluxo de dados. Nesse ponto, os seguintes valores obrigatórios devem ser preparados:

* [ID de conexão do Source](#source)
* [ID da conexão de destino](#target)
* [ID de mapeamento](#mapping)
* [ID da especificação do fluxo de dados](#specs)

Um fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga da solicitação.

Para agendar uma assimilação, primeiro defina o valor da hora inicial como a época em segundos. Em seguida, defina o valor de frequência para uma das cinco opções: `once`, `minute`, `hour`, `day` ou `week`. O valor do intervalo designa o período entre duas assimilações consecutivas e a criação de uma assimilação única não requer que um intervalo seja definido. Para todas as outras frequências, o valor do intervalo deve ser definido como igual ou maior que `15`.

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Database dataflow using BigQuery",
        "description": "collecting test1.Mytable",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "b7581b59-c603-4df1-a689-d23d7ac440f3"
        ],
        "targetConnectionIds": [
            "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "Datefield",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1612310466",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

+++

| Propriedade | Descrição |
| -------- | ----------- |
| `flowSpec.id` | A [ID de especificação de fluxo](#specs) recuperou na etapa anterior. |
| `sourceConnectionIds` | A [ID da conexão de origem](#source) recuperou em uma etapa anterior. |
| `targetConnectionIds` | A [ID da conexão de destino](#target-connection) recuperou em uma etapa anterior. |
| `transformations.params.mappingId` | A [ID de mapeamento](#mapping) recuperou em uma etapa anterior. |
| `transformations.params.deltaColum` | A coluna designada usada para diferenciar entre dados novos e existentes. Os dados incrementais serão assimilados com base no carimbo de data e hora da coluna selecionada. O formato de data com suporte para `deltaColumn` é `yyyy-MM-dd HH:mm:ss`. Se você estiver usando o Armazenamento de Tabelas do Azure, o formato com suporte para `deltaColumn` é `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | A ID de mapeamento associada ao banco de dados. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções de fluxo consecutivas. O valor do intervalo deve ser um inteiro diferente de zero. O valor mínimo de intervalo aceito para cada frequência é o seguinte:<ul><li>**Uma vez**: n/d</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Dia**: 1</li><li>**Semana**: 1</li></ul> |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial sobre [monitoramento de fluxos de dados na API](../monitor.md)

## Próximas etapas

Seguindo este tutorial, você criou um conector de origem para coletar dados de um banco de dados de forma programada. Os dados de entrada agora podem ser usados por serviços downstream do Experience Platform, como [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
* [Visão geral do Espaço de trabalho de ciência de dados](../../../../data-science-workspace/home.md)

## Apêndice

A seção a seguir lista os diferentes conectores de origem de armazenamento na nuvem e suas especificações de conexão.

### Especificação de conexão

| Nome do conector | ID de especificação da conexão |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] em [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] em [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL Greenplum] | `37b6bf40-d318-4655-90be-5cd6f65d334b` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |
