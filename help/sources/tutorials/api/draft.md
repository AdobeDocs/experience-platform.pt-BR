---
title: Criar rascunhos da API de entidades do serviço de fluxo
description: Saiba como criar rascunhos de sua conexão base, conexão de origem, conexão de destino e fluxo de dados usando a API do Serviço de fluxo
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: ebd650355a5a4c2a949739384bfd5c8df9577075
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 5%

---

# Criar rascunhos de entidades [!DNL Flow Service] usando a API

Você pode usar o parâmetro de consulta `mode=draft` na [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) para definir suas entidades [!DNL Flow Service], como conexões base, conexões de origem, conexões de destino e fluxos de dados, para um estado de rascunho.

Os rascunhos podem ser atualizados posteriormente com novas informações e publicados quando prontos, usando o parâmetro de consulta `op=publish`.

Este tutorial fornece etapas sobre como definir entidades do [!DNL Flow Service] para um estado de rascunho e permite pausar e salvar seus fluxos de trabalho para conclusão posterior.

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../landing/api-guide.md).

### Verificar suporte para modo de rascunho

Você também deve verificar se a ID de especificação da conexão e a ID de especificação de fluxo correspondente da origem que você está usando estão ativadas para o modo de rascunho.

>[!BEGINTABS]

>[!TAB Pesquisar detalhes de especificação da conexão]

+++Solicitação
A solicitação a seguir recupera as informações de especificação da conexão para [!DNL Azure File Storage]:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna as informações de especificação da conexão para a sua origem. Para verificar se há suporte para o modo de rascunho na sua origem, verifique se `items[0].attributes.isDraftModeSupported` tem um valor de `true`.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
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

>[!TAB Pesquisar detalhes de especificação de fluxo]

+++Solicitação
A solicitação a seguir recupera os detalhes da especificação do fluxo para uma fonte de armazenamento na nuvem:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna as informações de especificação de fluxo da origem. Para verificar se há suporte para o modo de rascunho na sua origem, verifique se `items[0].attributes.isDraftModeSupported` tem um valor de `true`.

```json {line-numbers="true" start-line="1" highlight="167"}
{
  "items": [
    {
      "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
      "name": "CloudStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "ecadc60c-7455-4d87-84dc-2a0e293d997b",
        "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
        "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
        "32e8f412-cdf7-464c-9885-78184cb113fd",
        "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
        "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
        "54e221aa-d342-4707-bcff-7a4bceef0001",
        "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
        "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
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
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
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
      "attributes": {
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

>[!ENDTABS]



## Criar uma conexão de base de rascunho {#create-a-draft-base-connection}

Para criar uma conexão base de rascunho, faça uma solicitação POST para o ponto de extremidade `/connections` da API [!DNL Flow Service] e forneça `mode=draft` como um parâmetro de consulta.

**Formato da API**

```http
POST /connections?mode=draft
```

| Parâmetro | Descrição |
| --- | --- |
| `mode` | Um parâmetro de consulta fornecido pelo usuário que decide o estado da conexão base. Para definir uma conexão base como rascunho, defina `mode` como `draft`. |

**Solicitação**

A solicitação a seguir cria uma conexão base de rascunho para a origem [!DNL Azure File Storage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão básica e a tag correspondente para a conexão básica de rascunho. Você pode usar essa ID posteriormente para atualizar e publicar sua conexão base.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Publish sua conexão de base de rascunho {#publish-your-draft-base-connection}

Quando o rascunho estiver pronto para ser publicado, faça uma solicitação POST ao ponto de extremidade `/connections` e forneça a ID da conexão base de rascunho que você deseja publicar, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `op` | Uma operação de ação que atualiza o estado da conexão base consultada. Para publicar uma conexão de base de rascunho, defina `op` como `publish`. |

**Solicitação**

A solicitação a seguir publica a conexão base de rascunho para [!DNL Azure File Storage] que foi criada em uma etapa anterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna a ID e a tag correspondente da conexão base publicada.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Criar uma conexão de origem de rascunho {#create-a-draft-source-connection}

Para criar uma conexão de origem de rascunho, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service] e forneça `mode=draft` como um parâmetro de consulta.

**Formato da API**

```http
POST /sourceConnections?mode=draft
```

| Parâmetro | Descrição |
| --- | --- |
| `mode` | Um parâmetro de consulta fornecido pelo usuário que decide o estado da conexão de origem. Para definir uma conexão de origem como rascunho, defina `mode` como `draft`. |

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna a ID da conexão de origem e a tag correspondente para a conexão de origem de rascunho. Você pode usar essa ID posteriormente para atualizar e publicar sua conexão de origem.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Publish sua conexão de origem de rascunho {#publish-your-draft-source-connection}

>[!NOTE]
>
>Não é possível publicar uma conexão de origem se a conexão base associada ainda estiver em estado de rascunho. Certifique-se de que a conexão base seja publicada primeiro, antes de publicar sua conexão de origem.

Quando o rascunho estiver pronto para ser publicado, faça uma solicitação POST ao ponto de extremidade `/sourceConnections` e forneça a ID da conexão de origem de rascunho que você deseja publicar, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `op` | Uma operação de ação que atualiza o estado da conexão de origem consultada. Para publicar uma conexão de origem de rascunho, defina `op` como `publish`. |

**Solicitação**

A solicitação a seguir publica a conexão de origem de rascunho para [!DNL Azure File Storage] que foi criada em uma etapa anterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna a ID e a tag correspondente da conexão de origem publicada.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Criar uma conexão de destino de rascunho {#create-a-draft-target-connection}

Para criar uma conexão de destino de rascunho, faça uma solicitação POST para o ponto de extremidade `/targetConnections` da API [!DNL Flow Service] e forneça `mode=draft` como um parâmetro de consulta.

**Formato da API**

```http
POST /targetConnections?mode=draft
```

| Parâmetro | Descrição |
| --- | --- |
| `mode` | Um parâmetro de consulta fornecido pelo usuário que decide o estado da conexão de destino. Para definir uma conexão como rascunho, defina `mode` como `draft`. |

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão do público-alvo e a tag correspondente para a conexão do público-alvo de rascunho. Você pode usar essa ID posteriormente para atualizar e publicar sua conexão de destino.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Publish sua conexão de destino de rascunho {#publish-your-draft-target-connection}

>[!NOTE]
>
>Não é possível publicar uma conexão de destino se a conexão base associada ainda estiver em estado de rascunho. Certifique-se de que sua conexão base seja publicada primeiro, antes de publicar sua conexão de destino.

Quando o rascunho estiver pronto para ser publicado, faça uma solicitação POST ao ponto de extremidade `/targetConnections` e forneça a ID da conexão de destino de rascunho que você deseja publicar, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `op` | Uma operação de ação que atualiza o estado da conexão de destino consultada. Para publicar uma conexão de destino de rascunho, defina `op` como `publish`. |

**Solicitação**

A solicitação a seguir publica a conexão de destino de rascunho para [!DNL Azure File Storage] que foi criada em uma etapa anterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna a ID e a tag correspondente da conexão de destino publicada.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Criar um fluxo de dados de rascunho {#create-a-draft-dataflow}

Para definir um fluxo de dados como rascunho, faça uma solicitação POST para o ponto de extremidade `/flows` ao adicionar `mode=draft` como parâmetro de consulta. Isso permite criar um fluxo de dados e salvá-lo como rascunho.

**Formato da API**

```http
POST /flows?mode=draft
```

| Parâmetro | Descrição |
| --- | --- |
| `mode` | Um parâmetro de consulta fornecido pelo usuário que decide o estado do fluxo de dados. Para definir um fluxo de dados como rascunho, defina `mode` como `draft`. |

**Solicitação**

A solicitação a seguir cria um fluxo de dados de rascunho.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e a tag correspondente para o fluxo de dados de rascunho. Você pode usar essa ID posteriormente para atualizar e publicar seu fluxo de dados.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Publish seu fluxo de dados de rascunho {#publish-your-draft-dataflow}

>[!NOTE]
>
>Não é possível publicar um fluxo de dados se as conexões de origem e de destino associadas ainda estiverem em estado de rascunho. Verifique se suas conexões de origem e de destino foram publicadas primeiro, antes de publicar seu fluxo de dados.

Quando o rascunho estiver pronto para ser publicado, faça uma solicitação POST para o ponto de extremidade `/flows` enquanto fornece a ID do fluxo de dados de rascunho que você deseja publicar, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `op` | Uma operação de ação que atualiza o estado do fluxo de dados consultado. Para publicar um fluxo de dados de rascunho, defina `op` como `publish`. |

**Solicitação**

A solicitação a seguir publica o fluxo de dados de rascunho.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna a ID e o `etag` correspondente do fluxo de dados.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Próximas etapas

Seguindo este tutorial, você aprendeu a criar rascunhos das entidades [!DNL Flow Service], bem como a publicá-los. Para obter mais informações sobre origens, leia a [visão geral de origens](../../home.md).