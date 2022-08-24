---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Criar uma nova especificação de conexão usando a API do Serviço de fluxo
topic-legacy: tutorial
description: O documento a seguir fornece etapas sobre como criar uma especificação de conexão usando a API do Serviço de Fluxo e integrar uma nova fonte por meio de Fontes de Autoatendimento.
exl-id: 0b0278f5-c64d-4802-a6b4-37557f714a97
source-git-commit: ae5bb475bca90b31d8eb7cf6b66d4d191d36ac5c
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 2%

---

# Crie uma nova especificação de conexão usando o [!DNL Flow Service] API

Uma especificação de conexão representa a estrutura de uma fonte. Ele contém informações sobre os requisitos de autenticação de uma fonte, define como os dados da fonte podem ser explorados e inspecionados e fornece informações sobre os atributos de uma fonte específica. O `/connectionSpecs` endpoint no [!DNL Flow Service] A API permite gerenciar programaticamente as especificações de conexão em sua organização.

O documento a seguir fornece etapas sobre como criar uma especificação de conexão usando o [!DNL Flow Service] API e integre uma nova fonte por meio de Fontes de autoatendimento (SDK em lote).

## Introdução

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Coletar artefatos

Para criar uma nova fonte de lote usando Fontes de Autoatendimento, você deve primeiro coordenar com o Adobe, solicitar um repositório Git privado e alinhar com o Adobe nos detalhes sobre o rótulo, descrição, categoria e ícone da sua fonte.

Depois de fornecido, você deve estruturar seu repositório Git privado da seguinte maneira:

* Fontes
   * {your_source}
      * Artefatos
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefatos (nomes de arquivo) | Descrição | Exemplo |
| --- | --- | --- |
| {your_source} | O nome da sua fonte. Essa pasta deve conter todos os artefatos relacionados à sua origem, dentro do repositório Git privado. | `mailchimp-members` |
| {your_source}-category.txt | A categoria à qual a fonte pertence, formatada como um arquivo de texto. A lista de categorias de origem disponíveis suportadas pelas Fontes de Autoatendimento (SDK em lote) inclui: <ul><li>Advertising</li><li>Analytics</li><li>Consentimento e preferências</li><li>CRM</li><li>Sucesso do cliente</li><li>Banco de dados</li><li>comércio eletrônico</li><li>Automação de marketing</li><li>Pagamentos</li><li>Protocolos</li></ul> **Observação**: Se você achar que sua fonte não se encaixa em nenhuma das categorias acima, entre em contato com o representante do Adobe para discutir. | `mailchimp-members-category.txt` Dentro do arquivo, especifique a categoria da fonte, como: `marketingAutomation`. |
| {your_source}-description.txt | Uma breve descrição da sua fonte. | [!DNL Mailchimp Members] é a fonte de automação de marketing que você pode usar para trazer [!DNL Mailchimp Members] dados para o Experience Platform. |
| {your_source}-icon.svg | A imagem a ser usada para representar sua fonte no catálogo de fontes do Experience Platform. Este ícone deve ser um SVG file. |
| {your_source}-label.txt | O nome da origem como deve aparecer no catálogo de fontes do Experience Platform. | Membros do Mailchimp |
| {your_source}-connectionSpec.json | Um arquivo JSON que contém a especificação de conexão de sua fonte. Inicialmente, esse arquivo não é necessário, pois você preencherá a especificação da conexão ao concluir este guia. | `mailchimp-members-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Durante o período de teste da especificação da conexão, em vez de valores-chave, você pode usar `text` na especificação da conexão.

Depois de ter adicionado os arquivos necessários ao repositório Git privado, você deve criar uma solicitação de pull (PR) para o Adobe ser revisado. Quando a PR for aprovada e mesclada, você receberá uma ID que poderá ser usada para a especificação da conexão se referir ao rótulo, descrição e ícone da fonte.

Em seguida, siga as etapas descritas abaixo para configurar sua especificação de conexão. Para obter orientação adicional sobre as diferentes funcionalidades que você pode adicionar à sua origem, como agendamento avançado, esquema personalizado ou tipos de paginação diferentes, consulte o guia em [configuração de especificações de origem](../config/sourcespec.md).

## Copiar modelo de especificação de conexão

Depois de coletar os artefatos necessários, copie e cole o modelo de especificação de conexão abaixo para o editor de texto de sua escolha e, em seguida, atualize os atributos entre colchetes `{}` com informações relevantes para sua fonte específica.

```json
{
  "name": "generic-rest-extension",
  "type": "generic-rest",
  "description": "{DESCRIPTION}",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "uiAttributes": {
      "apiFeatures": {
        "explorePaginationSupported": false
      }
    }
  },
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "clientId": {
            "description": "Client id of user account.",
            "type": "string"
          },
          "clientSecret": {
            "description": "Client secret of user account.",
            "type": "string",
            "format": "password"
          },
          "accessToken": {
            "description": "Access Token",
            "type": "string",
            "format": "password"
          },
          "refreshToken": {
            "description": "Refresh Token",
            "type": "string",
            "format": "password"
          },
          "expirationDate": {
            "description": "Date of token expiry.",
            "type": "string",
            "format": "date",
            "uiAttributes": {
              "hidden": true
            }
          },
          "accessTokenUrl": {
            "description": "Access token url to fetch access token.",
            "type": "string"
          },
          "requestParameterOverride": {
            "type": "object",
            "description": "Specify parameter to override.",
            "properties": {
              "accessTokenField": {
                "description": "Access token field name to override.",
                "type": "string"
              },
              "refreshTokenField": {
                "description": "Refresh token field name to override.",
                "type": "string"
              },
              "expireInField": {
                "description": "ExpireIn field name to override.",
                "type": "string"
              },
              "authenticationMethod": {
                "description": "Authentication method override.",
                "type": "string",
                "enum": [
                  "GET",
                  "POST"
                ]
              },
              "clientId": {
                "description": "ClientId field name override.",
                "type": "string"
              },
              "clientSecret": {
                "description": "ClientSecret field name override.",
                "type": "string"
              }
            }
          }
        },
        "required": [
          "host",
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
          "username": {
            "description": "Username to connect rest endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect rest endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "protocols"
        },
        "icon": {
          "key": "genericRestIcon"
        },
        "description": {
          "key": "genericRestDescription"
        },
        "label": {
          "key": "genericRestLabel"
        }
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "Http method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "query parameters in json format",
              "example": "{'key':'value','key1':'value1'} in JSON format"
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "header parameters in json format",
          "example": "{'user':'c26f50c88dc035610e6753f807e28e9','x-api-key':'apiKey'}"
        },
        "contentPath": {
          "type": "object",
          "description": "Params required for main collection content.",
          "properties": {
            "path": {
              "description": "path to main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "Params required for sub-array content.",
          "properties": {
            "path": {
              "description": "path to sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "Params required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "Pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "number of records per page to fetch.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "pointer property name",
              "example": "pointer"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "Params required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
  "exploreSpec": {
    "name": "Resource",
    "type": "Resource",
    "requestSpec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object"
    },
    "responseSpec": {
      "$schema": "http: //json-schema.org/draft-07/schema#",
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
```

## Criar uma especificação de conexão {#create}

Depois de adquirir o modelo de especificação de conexão, agora é possível começar a criar uma nova especificação de conexão preenchendo os valores apropriados que correspondem à sua origem.

Uma especificação de conexão pode ser dividida em três partes distintas: as especificações de autenticação, as especificações de origem e as especificações de exploração.

Consulte os seguintes documentos para obter instruções sobre como preencher os valores de cada parte de uma especificação de conexão:

* [Configurar a especificação de autenticação](../config/authspec.md)
* [Configurar a especificação de origem](../config/sourcespec.md)
* [Configurar a especificação do explorador](../config/explorespec.md)

Com suas informações de especificação atualizadas, você pode enviar a nova especificação de conexão fazendo uma solicitação de POST para a `/connectionSpecs` endpoint da variável [!DNL Flow Service] API.

**Formato da API**

```http
POST /connectionSpecs
```

**Solicitação**

A solicitação a seguir é um exemplo de uma especificação de conexão totalmente criada para um [!DNL MailChimp] fonte:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MailChimp Members source",
      "description": "MailChimp Members source using generic-rest and SDK",
      "type": "generic-rest",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
          "uiAttributes": {
              "apiFeatures": {
                  "explorePaginationSupported": false
              }
          }
      },
      "authSpec": [
          {
              "name": "OAuth2 Refresh Code",
              "type": "OAuth2RefreshCode",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                  "properties": {
                      "domain": {
                        "type": "string",
                        "description": "Enter domain name for host url"
                      },
                      "authorizationTestUrl": {
                          "description": "Authorization test url to validate accessToken.",
                          "type": "string"
                      },
                      "accessToken": {
                          "description": "Access Token of mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "domain",
                      "accessToken"
                  ]
              }
          },
          {
              "name": "Basic Authentication",
              "type": "BasicAuthentication",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "defines auth params required for connecting to rest service.",
                  "properties": {
                      "domain": {
                        "type": "string",
                        "description": "Enter domain name for host url"
                      },
                      "username": {
                          "description": "Username to connect mailChimp endpoint.",
                          "type": "string"
                      },
                      "password": {
                          "description": "Password to connect mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "domain",
                      "username",
                      "password"
                  ]
              }
          }
      ],
      "sourceSpec": {
          "attributes": {
              "uiAttributes": {
                  "isSource": true,
                  "isPreview": true,
                  "isBeta": true,
                  "icon": {
                      "key": "mailchimpMembersIcon"
                  },
                  "description": {
                      "key": "mailchimpMembersDescription"
                  },
                  "label": {
                      "key": "mailchimpMembersLabel"
                  }
              },
              "urlParams": {
                  "host": "https://${domain}.api.mailchimp.com",
                  "path": "/3.0/lists/${listId}/members",
                  "method": "GET"
              },
              "contentPath": {
                  "path": "$.members",
                  "skipAttributes": [
                    "_links",
                    "total_items",
                    "list_id"
                  ],
                  "overrideWrapperAttribute": "member"
                },
              "paginationParams": {
                  "type": "OFFSET",
                  "limitName": "count",
                  "limitValue": "100",
                  "offSetName": "offset"
              },
              "scheduleParams": {
                  "scheduleStartParamName": "since_last_changed",
                  "scheduleEndParamName": "before_last_changed",
                  "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                  "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
              }
          },
          "spec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object",
              "description": "Define user input parameters to fetch resource values.",
              "properties": {
                  "listId": {
                      "type": "string",
                      "description": "listId for which members need to fetch."
                  }
              }
          }
      },
      "exploreSpec": {
          "name": "Resource",
          "type": "Resource",
          "requestSpec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object"
          },
          "responseSpec": {
              "$schema": "http: //json-schema.org/draft-07/schema#",
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
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna a especificação de conexão recém-criada, incluindo sua `id`.

```json
{
    "id": "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55",
    "createdAt": 1633388930134,
    "updatedAt": 1633388930134,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "MailChimp Members source",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "type": "generic-rest",
    "authSpec": [
        {
            "name": "OAuth2 Refresh Code",
            "type": "OAuth2RefreshCode",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path"
                    },
                    "authorizationTestUrl": {
                        "description": "Authorization test url to validate accessToken.",
                        "type": "string"
                    },
                    "accessToken": {
                        "description": "Access Token of mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "accessToken"
                ]
            }
        },
        {
            "name": "Basic Authentication",
            "type": "BasicAuthentication",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "defines auth params required for connecting to rest service.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path."
                    },
                    "username": {
                        "description": "Username to connect mailChimp endpoint.",
                        "type": "string"
                    },
                    "password": {
                        "description": "Password to connect mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "username",
                    "password"
                ]
            }
        }
    ],
    "sourceSpec": {
        "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "Define user input parameters to fetch resource values.",
            "properties": {
                "listId": {
                    "type": "string",
                    "description": "listId for which members need to fetch."
                }
            }
        },
        "attributes": {
            "uiAttributes": {
                "isSource": true,
                "isPreview": true,
                "isBeta": true,
                "icon": {
                    "key": "mailchimpMembersIcon"
                },
                "description": {
                    "key": "mailchimpMembersDescription"
                },
                "label": {
                    "key": "mailchimpMembersLabel"
                }
            },
            "urlParams": {
                "path": "/3.0/lists/${listId}/members",
                "method": "GET"
            },
            "contentPath": {
                    "path": "$.members",
                    "skipAttributes": [
                      "_links",
                      "total_items",
                      "list_id"
                    ],
                    "overrideWrapperAttribute": "member"
                  },
            "paginationParams": {
                "type": "OFFSET",
                "limitName": "count",
                "limitValue": "100",
                "offSetName": "offset"
            },
            "scheduleParams": {
                "scheduleStartParamName": "since_last_changed",
                "scheduleEndParamName": "before_last_changed",
                "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
            }
        }
    },
    "exploreSpec": {
        "name": "Resource",
        "type": "Resource",
        "requestSpec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object"
        },
        "responseSpec": {
            "$schema": "http: //json-schema.org/draft-07/schema#",
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
    },
    "attributes": {
        "uiAttributes": {
            "apiFeatures": {
                "explorePaginationSupported": false
            }
        }
    }
}
```

## Próximas etapas

Depois de criar uma nova especificação de conexão, é necessário adicionar a ID de especificação de conexão correspondente a uma especificação de fluxo existente. Veja o tutorial em [atualização das especificações de fluxo](./update-flow-specs.md) para obter mais informações.

Para fazer modificações na especificação de conexão criada, consulte o tutorial em [atualização das especificações de conexão](./update-connection-specs.md).
