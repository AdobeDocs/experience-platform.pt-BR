---
title: Criar Um Fluxo De Dados Para Assimilar Dados Do Source Na Experience Platform
description: Saiba como usar a API de serviço de fluxo para criar um fluxo de dados e assimilar dados de origem na Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 4e9448170a6c3eb378e003bcd7520cb0e573e408
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 3%

---

# Criar um fluxo de dados para assimilar dados de uma origem

Leia este guia para saber como criar um fluxo de dados e assimilar dados na Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Assimilação em lote](../../../../ingestion/batch-ingestion/overview.md): descubra como você pode carregar grandes volumes de dados com eficiência em lotes.
* [Serviço de catálogo](../../../../catalog/datasets/overview.md): organize e acompanhe seus conjuntos de dados no Experience Platform.
* [Preparo de dados](../../../../data-prep/home.md): transforme e mapeie seus dados de entrada para corresponder aos requisitos do esquema.
* [Fluxos de dados](../../../../dataflows/home.md): configure e gerencie os pipelines que movem seus dados das fontes para os destinos.
* [Esquemas do Experience Data Model (XDM)](../../../../xdm/home.md): estruture seus dados usando esquemas XDM para que estejam prontos para uso no Experience Platform.
* [Sandboxes](../../../../sandboxes/home.md): testar e desenvolver com segurança em ambientes isolados, sem afetar os dados de produção.
* [Fontes](../../../home.md): saiba como conectar suas fontes de dados externas à Experience Platform.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas com êxito para APIs do Experience Platform, leia o manual sobre a [introdução às APIs do Experience Platform](../../../../landing/api-guide.md).

### Criar conexão básica

Você deve ter uma conta de origem totalmente autenticada e sua ID de conexão base correspondente para criar com êxito um fluxo de dados para sua origem. Se você não tiver essa ID, visite o [catálogo de fontes](../../../home.md) para obter uma lista de fontes com as quais você pode criar uma conexão base.

### Criar um esquema XDM de destino {#target-schema}

Um esquema do Experience Data Model (XDM) fornece uma maneira padronizada para organizar e descrever os dados de experiência do cliente no Experience Platform. Para assimilar os dados de origem na Experience Platform, primeiro você deve criar um esquema XDM de destino que defina a estrutura e os tipos de dados que deseja assimilar. Esse esquema serve de blueprint para o conjunto de dados do Experience Platform em que seus dados assimilados residirão.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Leia os guias a seguir para obter detalhes sobre as etapas de criação de um esquema XDM do Target:

* [Criar um esquema usando a API](../../../../xdm/api/schemas.md).
* [Criar um esquema usando a interface](../../../../xdm/tutorials/create-schema-ui.md).

Depois de criado, o esquema XDM de destino `$id` será necessário posteriormente para o conjunto de dados e o mapeamento de destino.

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os dados assimilados com sucesso na Experience Platform são armazenados no data lake como conjuntos de dados. Durante essa etapa, você pode criar um novo conjunto de dados ou usar um conjunto de dados existente.

Você pode criar um conjunto de dados de destino fazendo uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/) e, ao mesmo tempo, fornecendo a ID do esquema de destino na carga. Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, leia o manual sobre [criação de um conjunto de dados usando a API](../../../../catalog/api/create-dataset.md).

>[!TIP]
>
>Se desejar assimilar seus dados no Perfil de cliente em tempo real, certifique-se de que ambos os esquemas XDM de destino e o conjunto de dados de destino estejam ativados para Perfil.

+++Selecione para exibir o exemplo

**Formato da API**

```HTTP
POST /dataSets
```

**Solicitação**

O exemplo a seguir mostra como criar um conjunto de dados de destino que esteja ativado para assimilação de Perfil do cliente em tempo real. Nesta solicitação, a propriedade `unifiedProfile` está definida como `true` (no objeto `tags`), o que instrui a Experience Platform a incluir esse conjunto de dados no Perfil de Cliente em Tempo Real.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | Um nome descritivo para o conjunto de dados de destino. Use um nome claro e exclusivo para facilitar a identificação e o gerenciamento do conjunto de dados em operações futuras. |
| `schemaRef.id` | A ID do esquema XDM do público-alvo. |
| `tags.unifiedProfile` | Um valor booleano que informa à Experience Platform se os dados devem ser assimilados no Perfil do cliente em tempo real. |

**Resposta**

Uma resposta bem-sucedida retorna a ID do conjunto de dados de destino. Essa ID é necessária posteriormente para criar uma conexão de destino.

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## Criar uma conexão de origem

Uma conexão de origem define como os dados são trazidos para a Experience Platform a partir de uma origem externa. Ele especifica o sistema de origem e o formato dos dados recebidos e faz referência a uma conexão base que contém detalhes de autenticação. Cada conexão de origem é exclusiva de sua organização.

* Para fontes baseadas em arquivos (como armazenamentos em nuvem), uma conexão de origem pode incluir configurações como delimitador de coluna, tipo de codificação, tipo de compactação, expressões regulares para seleção de arquivos e se os arquivos devem ser assimilados recursivamente.
* Para fontes baseadas em tabela (como bancos de dados, CRMs e provedores de automação de marketing), uma conexão de origem pode especificar detalhes como o nome da tabela e os mapeamentos de coluna.

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service] e forneça a ID da conexão base, a ID da especificação da conexão e o caminho para o arquivo de dados de origem.

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
    "name": "ACME source connection",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "description": "A source connection for ACME contact data",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
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
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | Um nome descritivo para a conexão de origem. Use um nome claro e exclusivo para facilitar a identificação e o gerenciamento da conexão em operações futuras. |
| `description` | Uma descrição opcional que pode ser adicionada para fornecer mais informações sobre a conexão de origem. |
| `baseConnectionId` | O `id` da sua conexão base. Você pode recuperar essa ID autenticando sua origem no Experience Platform usando a API [!DNL Flow Service]. |
| `data.format` | O formato dos dados. Defina esse valor como `tabular` para fontes baseadas em tabela (como bancos de dados, CRMs e provedores de automação de marketing). |
| `params.tableName` | O nome da tabela na conta de origem que você deseja assimilar na Experience Platform. |
| `params.columns` | As colunas de dados da tabela específica que você deseja assimilar na Experience Platform. |
| `params.cdcEnabled` | Um valor booleano que indica se a captura do histórico de alterações está ativada ou não. Esta propriedade é suportada pelas seguintes fontes de banco de dados: <ul><li>[!DNL Azure Databricks]</li><li>[!DNL Google BigQuery]</li><li>[!DNL Snowflake]</li></ul> Para obter mais informações, leia o manual sobre como usar a [captura de dados de alteração nas fontes](../change-data-capture.md). |
| `connectionSpec.id` | A ID de especificação de conexão da origem que você está usando. |

**Resposta**

Uma resposta bem-sucedida retorna a ID da conexão de origem. Essa ID é necessária para criar um fluxo de dados e assimilar seus dados.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação da conexão fixa associada ao Data Lake. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | Um nome descritivo para a conexão de destino. Use um nome claro e exclusivo para facilitar a identificação e o gerenciamento da conexão em operações futuras. |
| `description` | Uma descrição opcional que pode ser adicionada para fornecer mais informações sobre a conexão de destino. |
| `data.schema.id` | A ID do esquema XDM do público-alvo. |
| `params.dataSetId` | A ID do conjunto de dados de destino. |
| `connectionSpec.id` | A ID de especificação de conexão do data lake. Esta ID foi corrigida: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

## Mapeamento {#mapping}

Em seguida, você deve mapear os dados de origem para o esquema de destino ao qual o conjunto de dados de destino adere. Para criar um mapeamento, faça uma solicitação POST para o ponto de extremidade `mappingSets` da [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/), forneça a ID do esquema XDM de destino e os detalhes dos conjuntos de mapeamento que deseja criar.

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
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificações de fluxo de dados

Antes de criar um fluxo de dados, primeiro recupere as especificações do fluxo de dados que correspondem à origem. Para recuperar essas informações, faça uma solicitação do GET para o ponto de extremidade `/flowSpecs` da API [!DNL Flow Service].

**Formato da API**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| Parâmetro da consulta | Descrição |
| --- | --- |
| `property=name=="{NAME}"` | O nome da especificação do fluxo de dados. <ul><li>Para fontes baseadas em arquivo (como armazenamento na nuvem), defina esse valor como `CloudStorageToAEP`.</li><li>Para fontes baseadas em tabela (como bancos de dados, CRMs e provedores de automação de marketing), defina esse valor como `CRMToAEP`.</li></ul> |

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

Para garantir que você esteja usando a especificação de fluxo de dados correta, verifique a matriz `items.sourceConnectionSpecIds` na resposta. Confirme se a ID de especificação da conexão para sua origem está incluída nesta lista.

+++Selecionar para exibir

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
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
            "transformationSpecs": [
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
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## Criar um fluxo de dados

Um fluxo de dados é um pipeline configurado que transfere dados entre os serviços da Experience Platform. Ele define como os dados são assimilados de fontes externas (como bancos de dados, armazenamento em nuvem ou APIs), processados e roteados para conjuntos de dados de destino. Esses conjuntos de dados são usados por serviços como o Serviço de identidade, Perfil do cliente em tempo real e Destinos para ativação e análise.

Para criar um fluxo de dados, você deve ter valores para os seguintes itens:

* ID de conexão do Source
* ID da conexão de destino
* ID de mapeamento
* ID da especificação do fluxo de dados

Durante essa etapa, você pode usar os seguintes parâmetros no `scheduleParams` para configurar um agendamento de assimilação para seu fluxo de dados:

| Parâmetro de agendamento | Descrição |
| --- | --- |
| `startTime` | O tempo da época (em segundos) em que o fluxo de dados deve começar. |
| `frequency` | A frequência da ingestão. Configure a frequência para indicar a frequência de execução do fluxo de dados. Você pode definir a frequência como: <ul><li>`once`: Defina sua frequência como `once` para criar uma assimilação única. As configurações para intervalo e preenchimento retroativo não estão disponíveis ao criar um fluxo de dados de assimilação única. Por padrão, a frequência de agendamento é definida como uma vez.</li><li>`minute`: Defina sua frequência como `minute` para agendar seu fluxo de dados para assimilar dados por minuto.</li><li>`hour`: Defina sua frequência como `hour` para agendar seu fluxo de dados para assimilar dados por hora.</li><li>`day`: Defina sua frequência como `day` para agendar seu fluxo de dados para assimilar dados por dia.</li><li>`week`: Defina sua frequência como `week` para agendar seu fluxo de dados para assimilar dados por semana.</li></ul> |
| `interval` | O intervalo entre as assimilações consecutivas (necessário para todas as frequências, exceto `once`). Defina a configuração de intervalo para estabelecer o intervalo de tempo entre cada assimilação. Por exemplo, se você definir a frequência como dia e configurar o intervalo como 15, o fluxo de dados será executado a cada 15 dias. Você não pode definir o intervalo como zero. O valor mínimo de intervalo aceito para cada frequência é o seguinte:<ul><li>`once`: n/d</li><li>`minute`: 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | Indica se os dados históricos devem ser assimilados antes de `startTime`. |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
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
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
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

| Propriedade | Descrição |
| --- | --- |
| `name` | Um nome descritivo para o fluxo de dados. Use um nome claro e exclusivo para facilitar a identificação e o gerenciamento do fluxo de dados em operações futuras. |
| `description` | Uma descrição opcional que pode ser adicionada para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID da especificação de fluxo que corresponde à sua origem. |
| `sourceConnectionIds` | A ID da conexão de origem gerada em uma etapa anterior. |
| `targetConnectionIds` | A ID de conexão de destino gerada em uma etapa anterior. |
| `transformations.params.deltaColum` | A coluna designada usada para diferenciar entre dados novos e existentes. Os dados incrementais serão assimilados com base no carimbo de data e hora da coluna selecionada. O formato com suporte para `deltaColumn` é `yyyy-MM-dd HH:mm:ss`. Para [!DNL Microsoft Dynamics], o formato com suporte para `deltaColumn` é `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.deltaColumn.dateFormat` | O formato de data a ser seguido para a coluna delta. |
| `transformations.params.deltaColumn.timeZone` | O fuso horário a ser usado ao interpretar os valores na coluna delta. |
| `transformations.params.mappingId` | A ID de mapeamento que foi gerada em uma etapa anterior. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época (segundos desde a época Unix). Determina quando o fluxo de dados iniciará sua primeira execução. |
| `scheduleParams.frequency` | A frequência na qual o fluxo de dados será executado. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | O intervalo entre execuções consecutivas de fluxo de dados, com base na frequência selecionada. Deve ser um inteiro diferente de zero. Por exemplo, um intervalo de `15` com frequência `minute` significa que o fluxo de dados é executado a cada 15 minutos. |
| `scheduleParams.backfill` | Um valor booliano (`true` ou `false`) que determina se os dados históricos devem ser assimilados (preenchimento retroativo) quando o fluxo de dados é criado pela primeira vez. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### Use a interface do para validar o fluxo de trabalho da API

É possível usar a interface do usuário do Experience Platform para validar a criação do fluxo de dados. Navegue até o catálogo *[!UICONTROL Fontes]* na interface do usuário do Experience Platform e selecione **[!UICONTROL Fluxos de Dados]** nas guias do cabeçalho. Em seguida, use a coluna [!UICONTROL Nome do Fluxo de Dados] e localize o fluxo de dados criado usando a API [!DNL Flow Service].

![A interface de fluxos de dados do espaço de trabalho de origens na interface do usuário do Experience Platform](../../../images/tutorials/validations/dataflows-interface.png)

Você pode validar ainda mais seu fluxo de dados por meio da interface [!UICONTROL Atividade de fluxo de dados]. Use o painel direito para exibir as informações de [!UICONTROL uso da API] do seu fluxo de dados. Esta seção exibe a mesma ID de fluxo de dados, ID de conjunto de dados e ID de mapeamento que foi gerada durante o processo de criação do fluxo de dados em [!DNL Flow Service].

![A página de exibição do fluxo de dados do espaço de trabalho de fontes.](../../../images/tutorials/validations/api-usage.png)

## Próximas etapas

Este tutorial guiou você pelo processo de criação de um fluxo de dados no Experience Platform usando a API [!DNL Flow Service]. Você aprendeu a criar e configurar os componentes necessários, incluindo o esquema XDM do destino, o conjunto de dados, a conexão de origem, a conexão de destino e o próprio fluxo de dados. Seguindo essas etapas, é possível automatizar a assimilação de dados de fontes externas na Experience Platform, permitindo que serviços downstream, como Perfil do cliente em tempo real e Destinos, aproveitem os dados assimilados para casos de uso avançados.

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para exibir informações sobre taxas de assimilação, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, visite o tutorial em [monitoramento de contas e fluxos de dados](../../../../dataflows/ui/monitor-sources.md).

### Atualizar seu fluxo de dados

Para atualizar as configurações do agendamento de fluxos de dados, mapeamento e informações gerais, visite o tutorial em [atualizando fluxos de dados de fontes](../../api/update-dataflows.md).

## Excluir seu fluxo de dados

Você pode excluir fluxos de dados que não são mais necessários ou que foram criados incorretamente usando a função **[!UICONTROL Excluir]** disponível no espaço de trabalho **[!UICONTROL Fluxos de Dados]**. Para obter mais informações sobre como excluir fluxos de dados, visite o tutorial em [excluindo fluxos de dados](../../api/delete.md).