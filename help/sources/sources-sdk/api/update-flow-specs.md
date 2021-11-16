---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Atualizar especificações de fluxo usando a API do Serviço de Fluxo (Beta)
topic-legacy: developer guide
description: O documento a seguir fornece etapas sobre como recuperar e atualizar especificações de fluxo usando a API de Serviço de Fluxo para SDK de Fontes.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 2%

---

# Atualize as especificações de fluxo usando o [!DNL Flow Service] API (Beta)

>[!IMPORTANT]
>
>O SDK das Fontes está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. A funcionalidade descrita nesta documentação está sujeita a alterações.

Depois de gerar uma nova ID de especificação de conexão, você deve adicionar essa ID a uma especificação de fluxo para criar um fluxo de dados.

As especificações de fluxo contêm informações que definem um fluxo, incluindo as IDs de conexão de origem e de destino que ele suporta, as especificações de transformação que precisam ser aplicadas aos dados e os parâmetros de agendamento necessários para gerar um fluxo. É possível editar as especificações de fluxo usando o `/flowSpecs` endpoint .

O documento a seguir fornece etapas sobre como recuperar e atualizar especificações de fluxo usando o [!DNL Flow Service] API para SDK de fontes.

## Introdução

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Pesquisar uma especificação de fluxo {#lookup}

Fontes criadas com o `generic-rest-extension` usar o modelo `RestStorageToAEP` especificação do fluxo. Essa especificação de fluxo pode ser recuperada fazendo uma solicitação de GET para o `/flowSpecs/` endpoint e fornecer a variável `flowSpec.id` de `6499120c-0b15-42dc-936e-847ea3c24d72`.

**Formato da API**

```http
GET /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Solicitação**

A solicitação a seguir recupera o `6499120c-0b15-42dc-936e-847ea3c24d72` especificação de conexão.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação do fluxo consultado.

```json
{
  "items": [
      {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "createdAt": 1633080822911,
          "updatedAt": 1633080822911,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "{SANDBOX_ID}",
          "sandboxName": "{SANDBOX_NAME}",
          "imsOrgId": "{IMS_ORG}",
          "name": "RestStorageToAEP",
          "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
          "version": "1.0",
          "sourceConnectionSpecIds": [
              "2d46966e-4fcc-4015-9f9e-a67594e395a3"
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
      },
  ]
}
```

## Atualizar uma especificação de fluxo {#update}

Você pode atualizar os campos de uma especificação de conexão por meio de uma operação PUT. Ao atualizar uma especificação de conexão por meio de uma solicitação de PUT, o corpo deve incluir todos os campos que seriam necessários ao criar uma nova especificação de conexão em uma solicitação de POST.

>[!IMPORTANT]
>
>Você deve atualizar a lista de `sourceConnectionSpecIds` da especificação de fluxo que corresponde a uma nova fonte sempre que uma nova fonte é criada. Isso garante que sua nova fonte seja compatível com uma especificação de fluxo existente, permitindo concluir o processo de criação do fluxo de dados com a nova fonte.

**Formato da API**

```http
PUT /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Solicitação**

A solicitação a seguir atualiza a especificação do fluxo de `6499120c-0b15-42dc-936e-847ea3c24d72` para incluir a ID da especificação de conexão `f6c0de0c-0a42-4cd9-9139-8768bf2f1b55`.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
`     "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "name": "RestStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
      ]
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação do fluxo consultado, incluindo sua lista atualizada de `sourceConnectionSpecIds`.

```json
{
    "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{IMS_ORG}",
    "name": "RestStorageToAEP",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
```

## Próximas etapas

Com sua nova especificação de conexão adicionada à especificação de fluxo apropriada, agora você pode continuar testando e enviando sua nova fonte. Consulte o guia sobre [teste e envio de uma nova fonte](./submit.md) para obter mais informações.