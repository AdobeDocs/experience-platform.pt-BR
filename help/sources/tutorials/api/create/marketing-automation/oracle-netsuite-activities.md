---
title: Criar uma conexão de origem e um fluxo de dados para atividades do NetSuite do Oracle usando a API do Serviço de fluxo
description: Saiba como criar uma conexão de origem e um fluxo de dados para trazer dados de eventos do NetSuite do Oracle para o Experience Platform usando a API do Serviço de fluxo.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 053cf0af327b39830f025686e0f8f67c27f1c45c
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 2%

---

# Criar uma conexão de origem e um fluxo de dados para [!DNL Oracle NetSuite Activities] uso da API do Serviço de fluxo

>[!NOTE]
>
>A variável [!DNL Oracle NetSuite Activities] a fonte está na versão beta. Consulte a [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Leia o tutorial a seguir para saber como trazer dados de eventos de sua [!DNL Oracle NetSuite Activities] para a Adobe Experience Platform usando a variável [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer entendimento prático dos seguintes componentes do Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Oracle NetSuite Activities] usando o [!DNL Flow Service] API.

### Autenticação

Leia o [[!DNL Oracle NetSuite] visão geral](../../../../connectors/marketing-automation/oracle-netsuite.md) para obter informações sobre como recuperar suas credenciais de autenticação.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL Oracle NetSuite Activities] para a Platform usando o [!DNL Flow Service] API

Siga o guia abaixo para saber como autenticar seu [!DNL Oracle NetSuite Activities] , crie uma conexão de origem e um fluxo de dados para trazer seus dados de eventos para o Experience Platform.

### Criar uma conexão básica {#base-connection}

Uma conexão base retém informações entre sua origem e Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Oracle NetSuite Activities] credenciais de autenticação como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Oracle NetSuite Activities]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NeSuite Activities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Activities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão básica seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão básica. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre sua conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão da sua origem. Essa ID pode ser recuperada depois que a origem é registrada e aprovada por meio do [!DNL Flow Service] API. |
| `auth.specName` | O tipo de autenticação que você está usando para autenticar sua origem na Platform. |
| `auth.params.clientId` | O valor da ID do cliente ao criar o registro de integração. O processo para criar um registro de integração pode ser encontrado [aqui](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). O valor é uma string de 64 caracteres semelhante a `7fce.....b42f`. |
| `auth.params.clientSecret` | O valor da ID do cliente ao criar o registro de integração. O processo para criar um registro de integração pode ser encontrado [aqui](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). O valor é uma string de 64 caracteres semelhante a `5c98.....1b46`. |
| `auth.params.accessTokenUrl` | A variável [!DNL NetSuite] URL do token de acesso, semelhante a `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token` onde você substituirá ACCOUNT_ID pela sua [!DNL NetSuite] ID da conta. |
| `auth.params.accessToken` | O valor do token de acesso é gerado no final de [Etapa dois](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint) do [Fluxo de concessão de código de autorização OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) tutorial. Os tokens de acesso expiram e são válidos somente por 60 minutos. o valor é uma string de 1024 caracteres formatada como um JWT (JSON Web Token) semelhante a `eyJr......f4V0`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura de arquivos e o conteúdo da fonte na próxima etapa.

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### Explorar sua fonte {#explore}

Depois de ter a ID de conexão básica, agora é possível explorar o conteúdo e a estrutura dos dados de origem executando uma solicitação GET para a `/connections` ao fornecer a ID de conexão básica como parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Solicitação**

Ao executar solicitações do GET para explorar a estrutura e o conteúdo do arquivo de origem, você deve incluir os parâmetros de consulta listados na tabela abaixo:

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica gerada na etapa anterior. |
| `objectType=rest` | O tipo de objeto que você deseja explorar. No momento, esse valor está sempre definido como `rest`. |
| `{OBJECT}` | Esse parâmetro é necessário somente ao visualizar um diretório específico. Seu valor representa o caminho do diretório que você deseja explorar. Para essa fonte, o valor seria `json`. |
| `fileType=json` | O tipo do arquivo que você deseja trazer para a Platform. Atualmente, `json` é o único tipo de arquivo compatível. |
| `{PREVIEW}` | Um valor booliano que define se o conteúdo da conexão oferece suporte à visualização. |
| `{SOURCE_PARAMS}` | Define parâmetros para o arquivo de origem que você deseja trazer para a Platform. Para recuperar o tipo de formato aceito para `{SOURCE_PARAMS}`, você deve codificar toda a cadeia de caracteres em base64. <br> O valor está vazio para [!DNL Oracle NetSuite Activities].</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma estrutura JSON como a seguinte:

+++Selecione para exibir a carga JSON

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "owner": {
                        "type": "string"
                    },
                    "createddate": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "accesslevel": {
                        "type": "string"
                    },
                    "alldayevent": {
                        "type": "string"
                    },
                    "message": {
                        "type": "string"
                    },
                    "startdate": {
                        "type": "string"
                    },
                    "title": {
                        "type": "string"
                    },
                    "organizer": {
                        "type": "string"
                    },
                    "response": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "location": {
                        "type": "string"
                    },
                    "timedevent": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "status": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2022-12-15",
                "id": "5",
                "lastmodifieddate": "2022-12-15",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-02-01",
                "id": "103",
                "lastmodifieddate": "2023-02-01",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-11-09",
                "id": "204",
                "lastmodifieddate": "2023-11-09",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2023-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
    ]
}
```

+++

### Criar uma conexão de origem {#source-connection}

Você pode criar uma conexão de origem fazendo uma solicitação POST para o `/sourceConnections` endpoint do [!DNL Flow Service] API. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

**Formato da API**

```https
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para [!DNL Oracle NetSuite Activities].

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Source Connection",
      "description": "Oracle NetSuite Activities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão base de [!DNL Oracle NetSuite Activities]. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato do [!DNL Oracle NetSuite Activities] dados que você deseja assimilar. No momento, o único formato de dados compatível é `json`. |

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados da Platform no qual os dados de origem estão contidos.

Um schema XDM de destino pode ser criado executando uma solicitação POST para o [API do registro de esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um schema usando a API](../../../../../xdm/api/schemas.md#create-a-schema).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para o [API do serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do schema de destino na carga útil.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../../../catalog/api/create-dataset.md).

### Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino em que os dados assimilados devem ser armazenados. Para criar uma conexão de destino, você deve fornecer a ID de especificação da conexão fixa que corresponde ao data lake. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o data lake. Usando esses identificadores, você pode criar uma conexão de destino usando o [!DNL Flow Service] API para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de destino para [!DNL Oracle NetSuite Activities]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Target Connection Generic Rest",
      "description": "Oracle NetSuite Activities Target Connection Generic Rest",
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
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da sua conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação da conexão que corresponde ao data lake. Essa ID fixa é: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | O formato do [!DNL Oracle NetSuite Activities] dados que você deseja assimilar. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Essa ID é necessária nas etapas posteriores.

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere. Isso é feito executando uma solicitação POST para [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```http
POST /conversion/mappingSets
```

**Solicitação**

A solicitação a seguir cria um mapeamento para [!DNL DNL NetSuite Activities]

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
            "source": "items.id",
            "destination": "_extconndev.NSA_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.title",
            "destination": "_extconndev.NSA_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.createddate",
            "destination": "_extconndev.NSA_createddate"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.location",
            "destination": "_extconndev.NSA_location"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NSA_lastmodifieddate"
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
| `outputSchema.schemaRef.id` | A ID do [esquema XDM do público-alvo](#target-schema) gerada em uma etapa anterior. |
| `mappings.sourceType` | O tipo de atributo de origem que está sendo mapeado. |
| `mappings.source` | O atributo de origem que precisa ser mapeado para um caminho XDM de destino. |
| `mappings.destination` | O caminho XDM de destino para o qual o atributo de origem está sendo mapeado. |

**Resposta**

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

### Criar um fluxo {#flow}

O último passo para trazer dados de [!DNL Oracle NetSuite Activities] para a Platform é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

* [ID da conexão de origem](#source-connection)
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
    "name": "Oracle NetSuite Activities connector Flow Generic Rest",
    "description": "Oracle NetSuite Activities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do fluxo de dados. Verifique se o nome do fluxo de dados é descritivo, pois você pode usá-lo para pesquisar informações sobre o fluxo de dados. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID de especificação de fluxo necessária para criar um fluxo de dados. Essa ID fixa é: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | A versão correspondente da ID de especificação de fluxo. Esse valor é padronizado como `1.0`. |
| `sourceConnectionIds` | A variável [ID da conexão de origem](#source-connection) gerada em uma etapa anterior. |
| `targetConnectionIds` | A variável [ID da conexão de destino](#target-connection) gerada em uma etapa anterior. |
| `transformations` | Essa propriedade contém as várias transformações necessárias para serem aplicadas aos seus dados. Essa propriedade é necessária ao trazer dados não compatíveis com XDM para a Platform. |
| `transformations.name` | O nome atribuído à transformação. |
| `transformations.params.mappingId` | A variável [ID do mapeamento](#mapping) gerada em uma etapa anterior. |
| `transformations.params.mappingVersion` | A versão correspondente da ID de mapeamento. Esse valor é padronizado como `0`. |
| `scheduleParams.startTime` | Essa propriedade contém informações sobre o agendamento de assimilação do fluxo de dados. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções de fluxo consecutivas. O valor do intervalo deve ser um inteiro diferente de zero. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado. Você pode usar essa ID para monitorar, atualizar ou excluir seu fluxo de dados.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## Apêndice

A seção a seguir fornece informações sobre as etapas que podem ser seguidas para monitorar, atualizar e excluir o fluxo de dados.

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos de API, leia o guia em [monitoramento de fluxos de dados de origens usando a API](../../monitor.md).

### Atualizar seu fluxo de dados

Atualize os detalhes do seu fluxo de dados, como nome e descrição, bem como o agendamento de execução e os conjuntos de mapeamento associados fazendo uma solicitação PATCH para o `/flows` endpoint de [!DNL Flow Service] ao fornecer a ID do fluxo de dados. Ao fazer uma solicitação PATCH, você deve fornecer os atributos exclusivos de seu fluxo de dados `etag` no `If-Match` cabeçalho. Para obter exemplos completos de API, leia o guia em [atualização de fluxos de dados de origens usando a API](../../update-dataflows.md).

### Atualizar sua conta

Atualize o nome, a descrição e as credenciais da sua conta de origem executando uma solicitação PATCH para a [!DNL Flow Service] ao fornecer a ID de conexão básica como um parâmetro de consulta. Ao fazer uma solicitação PATCH, você deve fornecer as informações exclusivas de sua conta de origem `etag` no `If-Match` cabeçalho. Para obter exemplos completos de API, leia o guia em [atualização da conta de origem usando a API](../../update.md).

### Excluir seu fluxo de dados

Exclua seu fluxo de dados executando uma solicitação DELETE para o [!DNL Flow Service] ao fornecer a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos de API, leia o guia em [exclusão de fluxos de dados usando a API](../../delete-dataflows.md).

### Excluir sua conta

Exclua sua conta executando uma solicitação DELETE para o [!DNL Flow Service] ao fornecer a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos de API, leia o guia em [exclusão da conta de origem usando a API](../../delete.md).
