---
title: Criar uma conexão de origem e um fluxo de dados para o SAP Commerce usando a API do Serviço de Fluxo
description: Saiba como criar uma conexão de origem e um fluxo de dados para trazer dados do SAP Commerce para a Experience Platform usando a API do Serviço de Fluxo.
badge: Beta
exl-id: 580731b9-0c04-4f83-a475-c1890ac5b7cd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# Crie uma conexão de origem e um fluxo de dados para [!DNL SAP Commerce] usando a API de Serviço de Fluxo

>[!NOTE]
>
>A origem [!DNL SAP Commerce] está na versão beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O tutorial a seguir orienta você pelas etapas para criar uma conexão de origem [!DNL SAP Commerce] e um fluxo de dados para trazer contatos de [[!DNL SAP] Cobrança de assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) e dados do cliente para a Adobe Experience Platform usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL SAP Commerce] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para conectar [!DNL SAP Commerce] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `clientId` | O valor de `clientId` da chave de serviço. |
| `clientSecret` | O valor de `clientSecret` da chave de serviço. |
| `tokenEndpoint` | O valor de `url` da chave de serviço será semelhante a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| `region` | O local do data center. A região está presente no `url` e tem um valor semelhante a `eu10` ou `us10`. Por exemplo, se o `url` for `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`, então você precisará de `eu10`. |

Para obter mais informações sobre essas credenciais, consulte a [[!DNL SAP Commerce] documentação](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

## Conectar o [!DNL SAP Commerce] ao Experience Platform usando a API [!DNL Flow Service]

A seguir estão descritas as etapas que você precisa realizar para autenticar sua origem do [!DNL SAP Commerce], criar uma conexão de origem e criar um fluxo de dados para trazer seus dados de contas e contatos para a Experience Platform.

### Criar uma conexão básica {#base-connection}

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação do [!DNL SAP Commerce] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce base connection",
      "description": "Authenticated base connection for SAP Commerce",
      "connectionSpec": {
          "id": "d8ee38de-7ae9-4058-9610-c79ce75f8e92",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "region": "{REGION}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "tokenEndpoint": "{TOKEN_ENDPOINT}"
          }
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão básica seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão básica. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre sua conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão da sua origem. Essa ID pode ser recuperada depois que a origem é registrada e aprovada por meio da API [!DNL Flow Service]. |
| `auth.specName` | O tipo de autenticação que você está usando para autenticar sua origem na Experience Platform. |
| `auth.params.region` | O local do data center. A região está presente no `url` e tem um valor semelhante a `eu10` ou `us10`. Por exemplo, se o `url` for `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`, você precisará de `eu10`. |
| `auth.params.clientId` | O valor de `clientId` da chave de serviço. |
| `auth.params.clientSecret` | O valor de `clientSecret` da chave de serviço. |
| `auth.params.tokenEndpoint` | O valor de `url` da chave de serviço será semelhante a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura de arquivos e o conteúdo da fonte na próxima etapa.

```json
{
     "id": "5f6d6022-3f64-400c-ba01-d4010de2d8ff",
     "etag": "\"f8018de1-0000-0200-0000-6482d7210000\""
}
```

### Explorar sua fonte {#explore}

Depois de ter a ID de conexão básica, você pode explorar o conteúdo e a estrutura dos dados de origem executando uma solicitação GET para o ponto de extremidade `/connections` enquanto fornece a ID de conexão básica como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Ao executar solicitações do GET para explorar a estrutura e o conteúdo do arquivo de origem, você deve incluir os parâmetros de consulta listados na tabela abaixo:

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica gerada na etapa anterior. |
| `objectType=rest` | O tipo de objeto que você deseja explorar. Atualmente, este valor está sempre configurado para `rest`. |
| `{OBJECT}` | Esse parâmetro é necessário somente ao visualizar um diretório específico. Seu valor representa o caminho do diretório que você deseja explorar. Para esta fonte, o valor seria `json`. |
| `fileType=json` | O tipo do arquivo que você deseja trazer para a Experience Platform. Atualmente, `json` é o único tipo de arquivo com suporte. |
| `{PREVIEW}` | Um valor booliano que define se o conteúdo da conexão oferece suporte à visualização. |
| `{SOURCE_PARAMS}` | Define parâmetros para o arquivo de origem que você deseja trazer para a Experience Platform. Para recuperar o tipo de formato aceito para `{SOURCE_PARAMS}`, você deve codificar a cadeia inteira em base64. <br> [!DNL SAP Commerce] dá suporte a várias APIs. Dependendo do tipo de objeto que você estiver utilizando, passe uma das opções abaixo: <ul><li>`customers`</li><li>`contacts`</li></ul> |

A origem [!DNL SAP Commerce] dá suporte a várias APIs. Dependendo do tipo de objeto que você está usando, a solicitação a ser enviada é como a seguir:

>[!NOTE]
>
>Alguns registros de resposta foram truncados para permitir uma apresentação melhor.

>[!BEGINTABS]

>[!TAB Clientes]

+++Solicitação

Para a API de clientes [!DNL SAP Commerce], o valor de `{SOURCE_PARAMS}` é passado como `{"object_type":"customers"}`. Quando codificado em base64, ele equivale a `eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9`, como mostrado abaixo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna uma estrutura JSON como a seguinte:

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "addresses": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "isDefault": {
                            "type": "boolean"
                        },
                        "phone": {
                            "type": "string"
                        },
                        "city": {
                            "type": "string"
                        },
                        "street": {
                            "type": "string"
                        },
                        "postalCode": {
                            "type": "string"
                        },
                        "addressUUID": {
                            "type": "string"
                        },
                        "houseNumber": {
                            "type": "string"
                        },
                        "additionalAddressInfo": {
                            "type": "string"
                        },
                        "state": {
                            "type": "string"
                        },
                        "email": {
                            "type": "string"
                        }
                    }
                }
            },
            "customerNumber": {
                "type": "string"
            },
            "corporateInfo": {
                "type": "object",
                "properties": {}
            },
            "customReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "externalSystemId": {
                            "type": "string"
                        },
                        "externalId": {
                            "type": "string"
                        },
                        "externalIdTypeCode": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "customerType": {
                "type": "string"
            },
            "markets": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "salesArea": {
                            "type": "object",
                            "properties": {
                                "division": {
                                    "type": "string"
                                },
                                "distributionChannel": {
                                    "type": "string"
                                },
                                "salesOrganization": {
                                    "type": "string"
                                }
                            }
                        },
                        "priceType": {
                            "type": "string"
                        },
                        "active": {
                            "type": "boolean"
                        },
                        "currency": {
                            "type": "string"
                        },
                        "marketId": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            },
            "defaultAddress": {
                "type": "object",
                "properties": {
                    "country": {
                        "type": "string"
                    },
                    "isDefault": {
                        "type": "boolean"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "city": {
                        "type": "string"
                    },
                    "street": {
                        "type": "string"
                    },
                    "postalCode": {
                        "type": "string"
                    },
                    "addressUUID": {
                        "type": "string"
                    },
                    "houseNumber": {
                        "type": "string"
                    },
                    "additionalAddressInfo": {
                        "type": "string"
                    },
                    "state": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "addresses": [
                {
                    "email": "user1@test.com",
                    "phone": "123456890",
                    "houseNumber": "123",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                    "isDefault": true
                }
            ],
            "customerNumber": "2863620303",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t090000",
                    "externalId": "1324566",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.499Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedAt": "2023-05-31T06:39:28.499Z",
            "defaultAddress": {
                "email": "user1@test.com",
                "phone": "123456890",
                "houseNumber": "123",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                "isDefault": true
            }
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "addresses": [
                {
                    "email": "user2@test.com",
                    "phone": "1234567899",
                    "houseNumber": "876",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                    "isDefault": true
                }
            ],
            "customerNumber": "6776445404",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t089999",
                    "externalId": "1324565",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.142Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedAt": "2023-05-31T06:39:28.142Z",
            "defaultAddress": {
                "email": "user2@test.com",
                "phone": "1234567899",
                "houseNumber": "876",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                "isDefault": true
            }
        }
    ]
}
```

+++

>[!TAB Contatos]

+++Solicitação

Para a API de Contatos [!DNL SAP Commerce], o valor de `{SOURCE_PARAMS}` é passado como `{"object_type":"contacts"}`. Quando codificado em base64, ele equivale a `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=`, como mostrado abaixo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna uma estrutura JSON como a seguinte:

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "contactNumber": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "createdAt": "2023-05-31T13:33:52.689Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4365374130",
            "changedAt": "2023-05-31T13:33:52.689Z"
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "createdAt": "2023-05-31T13:33:52.37Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4075431868",
            "changedAt": "2023-05-31T13:33:52.37Z"
        }
    ]
}
```

+++

>[!ENDTABS]

### Criar uma conexão de origem {#source-connection}

Você pode criar uma conexão de origem fazendo uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service]. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

**Formato da API**

```https
POST /sourceConnections
```

Dependendo do tipo de objeto que você estiver utilizando, selecione uma das guias abaixo:

>[!BEGINTABS]

>[!TAB Clientes]

+++Solicitação

A solicitação a seguir cria uma conexão de origem para dados de clientes [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "customers"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão base de [!DNL SAP Commerce]. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato dos dados [!DNL SAP Commerce] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |
| `object_type` | [!DNL SAP Commerce] dá suporte a várias APIs. Para API de clientes, o parâmetro `object_type` deve ser definido como `customers`. |
| `path` | Isso terá o mesmo valor que você selecionar para `object_type`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!TAB Contatos]

+++Solicitação

A solicitação a seguir cria uma conexão de origem para dados de contatos de [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão base de [!DNL SAP Commerce]. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato dos dados [!DNL SAP Commerce] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |
| `object_type` | [!DNL SAP Commerce] dá suporte a várias APIs. Para a API de contatos, o parâmetro `object_type` deve ser definido como `contacts`. |
| `path` | Isso terá o mesmo valor que você selecionar para *`object_type`*. |

+++

+++Resposta

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!ENDTABS]

### Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados no Experience Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados do Experience Platform no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](../../../../../xdm/api/schemas.md#create-a-schema).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornecendo a ID do esquema de destino na carga.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../../../catalog/api/create-dataset.md).

### Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino em que os dados assimilados devem ser armazenados. Para criar uma conexão de destino, você deve fornecer a ID de especificação da conexão fixa que corresponde ao data lake. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o data lake. Usando esses identificadores, você pode criar uma conexão de destino usando a API [!DNL Flow Service] para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de destino para [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Target Connection Generic Rest",
      "description": "SAP Commerce Target Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "645923cd7aeeea1c06c5e92e"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da sua conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação da conexão que corresponde ao data lake. Esta ID fixa é: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | O formato dos dados [!DNL SAP Commerce] que você deseja assimilar. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão de destino. Essa ID é necessária nas etapas posteriores.

```json
{
    "id": "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c",
    "etag": "\"db00c6dc-0000-0200-0000-6482d8280000\""
}
```

### Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere. Isso é feito executando uma solicitação POST para [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```http
POST /conversion/mappingSets
```

>[!BEGINTABS]

>[!TAB Clientes]

+++Solicitação

A solicitação a seguir cria um mapeamento para os dados da API do cliente [!DNL SAP Commerce]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerNumber",
            "destination": "_extconndev.customerNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerType",
            "destination": "_extconndev.customerType"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].email",
            "destination": "_extconndev.addresses[*].email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].city",
            "destination": "_extconndev.addresses[*].city"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].addressUUID",
            "destination": "_extconndev.addresses[*].addressUUID"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].id",
            "destination": "_extconndev.customReferences[*].id"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].typeCode",
            "destination": "_extconndev.customReferences[*].typeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `outputSchema.schemaRef.id` | A ID do [esquema XDM de destino](#target-schema) gerada em uma etapa anterior. |
| `mappings.sourceType` | O tipo de atributo de origem que está sendo mapeado. |
| `mappings.source` | O atributo de origem que precisa ser mapeado para um caminho XDM de destino. |
| `mappings.destination` | O caminho XDM de destino para o qual o atributo de origem está sendo mapeado. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

+++

>[!TAB Contatos]

+++Solicitação

A solicitação a seguir cria um mapeamento para os dados da API de Contatos [!DNL SAP Commerce]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "contactNumber",
            "destination": "_extconndev.contactNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "createdAt",
            "destination": "_extconndev.createdAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.lastName",
            "destination": "_extconndev.personalInfo.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.firstName",
            "destination": "_extconndev.personalInfo.firstName"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectRefereneces[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/extconndev/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `outputSchema.schemaRef.id` | A ID do [esquema XDM de destino](#target-schema) gerada em uma etapa anterior. |
| `mappings.sourceType` | O tipo de atributo de origem que está sendo mapeado. |
| `mappings.source` | O atributo de origem que precisa ser mapeado para um caminho XDM de destino. |
| `mappings.destination` | O caminho XDM de destino para o qual o atributo de origem está sendo mapeado. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

+++

>[!ENDTABS]

### Criar um fluxo {#flow}

A última etapa para trazer dados de [!DNL SAP Commerce] para a Experience Platform é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

* [ID de conexão do Source](#source-connection)
* [ID da conexão de destino](#target-connection)
* [ID de mapeamento](#mapping)

Um fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga.

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
      "name": "SAP Commerce Connector Description Flow Generic Rest",
      "description": "SAP Commerce Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "2ef2e831-f4f1-4363-a0f7-08b4ea347164"
      ],
      "targetConnectionIds": [
          "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "ddf0592bcc9d4ac391803f15f2429f87",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "once",
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do fluxo de dados. Verifique se o nome do fluxo de dados é descritivo, pois você pode usá-lo para pesquisar informações sobre o fluxo de dados. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID de especificação de fluxo necessária para criar um fluxo de dados. Esta ID fixa é: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | A versão correspondente da ID de especificação de fluxo. O padrão deste valor é `1.0`. |
| `sourceConnectionIds` | A [ID da conexão de origem](#source-connection) gerada em uma etapa anterior. |
| `targetConnectionIds` | A [ID da conexão de destino](#target-connection) gerada em uma etapa anterior. |
| `transformations` | Essa propriedade contém as várias transformações necessárias para serem aplicadas aos seus dados. Essa propriedade é necessária ao trazer dados não compatíveis com XDM para a Experience Platform. |
| `transformations.name` | O nome atribuído à transformação. |
| `transformations.params.mappingId` | A [ID de mapeamento](#mapping) gerou em uma etapa anterior. |
| `transformations.params.mappingVersion` | A versão correspondente da ID de mapeamento. O padrão deste valor é `0`. |
| `scheduleParams.startTime` | Essa propriedade contém informações sobre o agendamento de assimilação do fluxo de dados. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções de fluxo consecutivas. O valor do intervalo deve ser um inteiro diferente de zero. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado. Você pode usar essa ID para monitorar, atualizar ou excluir seu fluxo de dados.

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## Apêndice

A seção a seguir fornece informações sobre as etapas que podem ser seguidas para monitorar, atualizar e excluir o fluxo de dados.

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos de API, leia o guia em [monitorando seus fluxos de dados de fontes usando a API](../../monitor.md).

### Atualizar seu fluxo de dados

Atualize os detalhes do seu fluxo de dados, como seu nome e descrição, bem como seu agendamento de execução e conjuntos de mapeamento associados fazendo uma solicitação PATCH para o ponto de extremidade `/flows` da API [!DNL Flow Service], ao mesmo tempo em que fornece a ID do seu fluxo de dados. Ao fazer uma solicitação PATCH, você deve fornecer o `etag` exclusivo do fluxo de dados no cabeçalho `If-Match`. Para obter exemplos completos de API, leia o guia em [atualizando fluxos de dados de fontes usando a API](../../update-dataflows.md).

### Atualizar sua conta

Atualize o nome, a descrição e as credenciais da conta de origem executando uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID da conexão base como um parâmetro de consulta. Ao fazer uma solicitação PATCH, você deve fornecer o `etag` exclusivo da sua conta de origem no cabeçalho `If-Match`. Para obter exemplos completos de API, leia o guia em [atualizando a conta de origem usando a API](../../update.md).

### Excluir seu fluxo de dados

Exclua seu fluxo de dados executando uma solicitação DELETE para a API [!DNL Flow Service] enquanto fornece a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos de API, leia o guia em [excluindo seus fluxos de dados usando a API](../../delete-dataflows.md).

### Excluir sua conta

Exclua sua conta executando uma solicitação DELETE para a API [!DNL Flow Service] enquanto fornece a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos de API, leia o guia em [excluindo sua conta de origem usando a API](../../delete.md).
