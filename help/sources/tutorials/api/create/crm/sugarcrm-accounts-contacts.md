---
title: Crie uma conexão de origem e um fluxo de dados para Contas e Contatos do SugarCRM usando a API do Serviço de Fluxo
description: Saiba como conectar o Adobe Experience Platform a contas e contatos do SugarCRM usando a API de serviço de fluxo.
exl-id: 2b422b39-5b86-4313-a214-725044d9812c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 2%

---

# Crie uma conexão de origem e um fluxo de dados para [!DNL SugarCRM Accounts & Contacts] usando a API de Serviço de Fluxo

O tutorial a seguir orienta você pelas etapas para criar uma conexão de origem [!DNL SugarCRM Accounts & Contacts] e criar um fluxo de dados para trazer dados de contas e contatos do [[!DNL SugarCRM]](https://www.sugarcrm.com/) para a Adobe Experience Platform usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL SugarCRM] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para conectar [!DNL SugarCRM Accounts & Contacts] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `host` | O ponto de extremidade da API do SugarCRM ao qual a origem se conecta. | `developer.salesfusion.com` |
| `username` | Seu nome de usuário da conta de desenvolvedor do SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | A senha da sua conta de desenvolvedor do SugarCRM. | `123456789` |

## Conectar o [!DNL SugarCRM Accounts & Contacts] ao Experience Platform usando a API [!DNL Flow Service]

A seguir estão descritas as etapas que você precisa realizar para autenticar sua origem do [!DNL SugarCRM], criar uma conexão de origem e criar um fluxo de dados para trazer seus dados de contas e contatos para a Experience Platform.

### Criar uma conexão básica {#base-connection}

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação do [!DNL SugarCRM Accounts & Contacts] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL SugarCRM Accounts & Contacts]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Accounts & Contacts base connection",
      "description": "Create a live inbound connection to your SugarCRM Accounts & Contacts instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "59a4b493-a615-40f9-bd38-f823d0909a2b",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "host": "developer.salesfusion.com",
              "username": "{SUGARCRM_DEVELOPER_ACCOUNT_USERNAME}",
              "password": "{SUGARCRM_DEVELOPER_ACCOUNT_PASSWORD}"
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
| `auth.params.host` | O host da API do SugarCRM: *developer.salesfusion.com* |
| `auth.params.username` | Seu nome de usuário da conta de desenvolvedor do SugarCRM. |
| `auth.params.password` | A senha da sua conta de desenvolvedor do SugarCRM. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura de arquivos e o conteúdo da fonte na próxima etapa.

```json
{
     "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
     "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### Explorar sua fonte {#explore}

Usando a ID de conexão básica gerada na etapa anterior, você pode explorar arquivos e diretórios executando solicitações do GET.
Use as chamadas a seguir para localizar o caminho do arquivo que deseja trazer para o Experience Platform:

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
| `{SOURCE_PARAMS}` | Define parâmetros para o arquivo de origem que você deseja trazer para a Experience Platform. Para recuperar o tipo de formato aceito para `{SOURCE_PARAMS}`, você deve codificar a cadeia inteira em base64. <br> [!DNL SugarCRM Accounts & Contacts] dá suporte a várias APIs. Dependendo do tipo de objeto que você estiver utilizando, passe uma das opções abaixo: <ul><li>`accounts` : empresas com as quais sua organização tem um relacionamento.</li><li>`contacts` : pessoas com as quais sua organização tem uma relação estabelecida.</li></ul> |

O [!DNL SugarCRM Accounts & Contacts] dá suporte a várias APIs. Dependendo do tipo de objeto que você está usando, a solicitação a ser enviada é como a seguir:

**Solicitação**

>[!BEGINTABS]

>[!TAB Contas]

Para a API de contas [!DNL SugarCRM], o valor de `{SOURCE_PARAMS}` é passado como `{"object_type":"accounts"}`. Quando codificado em base64, ele equivale a `eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=`, como mostrado abaixo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB Contatos]

Para a API de Contatos [!DNL SugarCRM], o valor de `{SOURCE_PARAMS}` é passado como `{"object_type":"contacts"}`. Quando codificado em base64, ele equivale a `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=`, como mostrado abaixo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**Resposta**

Da mesma forma, dependendo do tipo de objeto que você está usando a resposta recebida, veja abaixo:

>[!NOTE]
>
>Alguns registros foram truncados para permitir uma apresentação melhor.

>[!BEGINTABS]

>[!TAB Contas]

Uma resposta bem-sucedida retorna uma estrutura, como abaixo.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "owner": {
                        "type": "string"
                    },
                    "key_account": {
                        "type": "boolean"
                    },
                    "owner_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_score_field": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "billing_city": {
                        "type": "string"
                    },
                    "account_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "account_name": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "created_date": {
                        "type": "string"
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account_score": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account": {
                        "type": "string"
                    },
                    "contacts": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 1,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/1/",
                "account_name": "No Company",
                "owner_id": 1,
                "owner": "https://developer.salesfusion.com/api/2.0/users/1/",
                "created_date": "2022-06-22T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/1/",
                "updated_date": "2019-08-29T15:18:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/1/",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/1/contacts/",
                "created_by_id": 1,
                "updated_by_id": 1,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 2,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/2/",
                "account_name": "360 Vacations",
                "owner_id": 45,
                "owner": "https://developer.salesfusion.com/api/2.0/users/45/",
                "phone": "+1 - 384 - 735 - 3844",
                "created_date": "2022-09-22T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "billing_city": "New York City",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/2/contacts/",
                "created_by_id": 45,
                "updated_by_id": 45,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 50,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/50/",
                "account_name": "Waverly Trading House",
                "owner_id": 40,
                "owner": "https://developer.salesfusion.com/api/2.0/users/40/",
                "phone": "+1 - 964 - 226 - 4552",
                "created_date": "2022-09-18T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/40/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/40/",
                "billing_city": "Minneapolis",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/50/contacts/",
                "created_by_id": 40,
                "updated_by_id": 40,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        }
    ]
}
```

>[!TAB Contatos]

Uma resposta bem-sucedida retorna uma estrutura, como abaixo.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "opt_out": {
                        "type": "string"
                    },
                    "custom_score_field": {
                        "type": "string"
                    },
                    "contact_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "title": {
                        "type": "string"
                    },
                    "deleted_date": {},
                    "contact": {
                        "type": "string"
                    },
                    "account_name": {
                        "type": "string"
                    },
                    "first_name": {
                        "type": "string"
                    },
                    "del_date": {},
                    "email": {
                        "type": "string"
                    },
                    "delivered_date": {},
                    "owner": {
                        "type": "string"
                    },
                    "owner_name": {
                        "type": "string"
                    },
                    "last_name": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "account_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "opt_out_date": {},
                    "phone": {
                        "type": "string"
                    },
                    "crm_id": {
                        "type": "string"
                    },
                    "crm_type": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "deliverability_status": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "deliverability_message": {},
                    "created_date": {
                        "type": "string"
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account": {
                        "type": "string"
                    },
                    "status": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 1,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/1/",
                "first_name": "Cynthia",
                "last_name": "Rose",
                "phone": "+1 - 000 - 000 - 000",
                "email": "test.user@hotmail.com",
                "account_id": 10,
                "account_name": "Sunyvale Reporting Ltd",
                "account": "https://developer.salesfusion.com/api/2.0/accounts/10/",
                "owner_name": "Sarah Smith",
                "owner": "https://developer.salesfusion.com/api/2.0/users/41/",
                "created_date": "2022-06-23T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/41/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/41/",
                "created_by_id": 41,
                "updated_by_id": 41,
                "crm_id": "f53c3982-84ea-11ec-874a-06a1e215b98e",
                "opt_out": "N",
                "crm_type": "Lead",
                "status": "Assigned",
                "title": "Director Operations",
                "custom_score_field": "0",
                "deliverability_status": 0
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 2,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/2/",
                "email": "test.user@outlook.com",
                "created_date": "2022-06-21T23:35:00Z",
                "updated_date": "2022-02-03T21:55:00Z",
                "opt_out": "N",
                "crm_type": "Contact",
                "deliverability_status": 0
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 3,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/3/",
                "first_name": "Jonathan",
                "last_name": "Ryan",
                "phone": "+1 - 000 - 000 - 0000",
                "email": "test.user@yahoo.com",
                "account_id": 52,
                "account_name": "Q3 ARVRO III PR",
                "account": "https://developer.salesfusion.com/api/2.0/accounts/52/",
                "owner_name": "Max Jensen",
                "owner": "https://developer.salesfusion.com/api/2.0/users/45/",
                "created_date": "2022-07-02T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "created_by_id": 45,
                "updated_by_id": 45,
                "crm_id": "f54a1840-84ea-11ec-9546-06a1e215b98e",
                "opt_out": "N",
                "crm_type": "Lead",
                "status": "New",
                "title": "Director Sales",
                "custom_score_field": "0",
                "deliverability_status": 0
            },
            "page_size": 100
    ]
}
```

>[!ENDTABS]

### Criar uma conexão de origem {#source-connection}

Você pode criar uma conexão de origem fazendo uma solicitação POST para a API [!DNL Flow Service]. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

**Formato da API**

```https
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para [!DNL SugarCRM Accounts & Contacts]:

Dependendo do tipo de objeto que você estiver utilizando, selecione uma das guias abaixo:

>[!BEGINTABS]

>[!TAB Contas]

Para a API de contas [!DNL SugarCRM], o valor da propriedade `object_type` deve ser `accounts`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "accounts",
          "path": "accounts"
      }
  }'
```

>[!TAB Contatos]

Para a API de Contatos [!DNL SugarCRM], o valor da propriedade `object_type` deve ser `contacts`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts",
          "path": "contacts"
      }
  }'
```

>[!ENDTABS]

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão base de [!DNL SugarCRM Accounts & Contacts]. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato dos dados [!DNL SugarCRM Accounts & Contacts] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |
| `object_type` | [!DNL SugarCRM Accounts & Contacts] dá suporte a várias APIs. Dependendo do tipo de objeto que você estiver utilizando, passe uma das opções abaixo: <ul><li>`accounts` : empresas com as quais sua organização tem um relacionamento.</li><li>`contacts` : pessoas com as quais sua organização tem uma relação estabelecida.</li></ul> |
| `path` | Isso terá o mesmo valor que você selecionar para *`object_type`*. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

### Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados no Experience Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados do Experience Platform no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornecendo a ID do esquema de destino na carga.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino em que os dados assimilados devem ser armazenados. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa que corresponde ao data lake. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o data lake. Usando esses identificadores, você pode criar uma conexão de destino usando a API [!DNL Flow Service] para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de destino para [!DNL SugarCRM Accounts & Contacts]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Target Connection Generic Rest",
      "description": "SugarCRM Target Connection Generic Rest",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "version": "1.22"
          }
      },
      "params": {
          "dataSetId": "6365389d1d37d01c077a81da"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da sua conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação da conexão que corresponde ao data lake. Esta ID fixa é: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | O formato dos dados [!DNL SugarCRM Accounts & Contacts] que você deseja assimilar. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão de destino. Essa ID é necessária nas etapas posteriores.

```json
{
    "id": "6b137bf6-d2a0-48c8-914b-d50f4942eb85",
    "etag": "\"8405a268-0000-0200-0000-6368b8c30000\""
}
```

### Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere. Isso é feito executando uma solicitação POST para [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```http
POST /conversion/mappingSets
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
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account",
          "destination": "_extconndev.account"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account_id",
          "destination": "_extconndev.account_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.acount_name",
          "destination": "_extconndev.account_name"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account_score",
          "destination": "_extconndev.account_score"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.billing_city",
          "destination": "_extconndev.billing_city"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.contacts",
          "destination": "_extconndev.contacts"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by",
          "destination": "_extconndev.created_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by_id",
          "destination": "_extconndev.created_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_date",
          "destination": "_extconndev.created_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.custom_score_field",
          "destination": "_extconndev.custom_score_field"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.key_account",
          "destination": "_extconndev.key_account"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.owner",
          "destination": "_extconndev.owner"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.owner_id",
          "destination": "_extconndev.owner_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.phone",
          "destination": "_extconndev.phone_no"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by",
          "destination": "_extconndev.updated_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by_id",
          "destination": "_extconndev.updated_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "_extconndev.updated_date"
      }
      ]
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `outputSchema.schemaRef.id` | A ID do [esquema XDM de destino](#target-schema) gerada em uma etapa anterior. |
| `mappings.sourceType` | O tipo de atributo de origem que está sendo mapeado. |
| `mappings.source` | O atributo de origem que precisa ser mapeado para um caminho XDM de destino. |
| `mappings.destination` | O caminho XDM de destino para o qual o atributo de origem está sendo mapeado. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "059c69f7207b4d7e9b48c47e2fd966a6",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Criar um fluxo {#flow}

A última etapa para trazer dados de [!DNL SugarCRM Accounts & Contacts] para a Experience Platform é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

* [ID de conexão do Source](#source-connection)
* [ID da conexão de destino](#target-connection)
* [ID de mapeamento](#mapping)

Um fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga.

Para agendar uma assimilação, primeiro defina o valor da hora inicial como a época em segundos. Em seguida, você deve definir o valor de frequência como um de `hour` ou `day`. O valor do intervalo designa o período entre duas assimilações consecutivas. O valor do intervalo deve ser definido como `1` ou `24`, dependendo da seleção `scheduleParams.frequency` de `hour` ou `day`.

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
      "name": "SugarCRM Connector Description Flow Generic Rest",
      "description": "SugarCRM Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
      ],
      "targetConnectionIds": [
          "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "059c69f7207b4d7e9b48c47e2fd966a6",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "hour",
          "interval": 1
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
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `hour` ou `day`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções de fluxo consecutivas. O valor do intervalo deve ser um inteiro diferente de zero. O valor do intervalo deve ser definido como `1` ou `24`, dependendo da seleção `scheduleParams.frequency` de `hour` ou `day`. |

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

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos de API, leia o guia em [monitorando seus fluxos de dados de fontes usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Atualizar seu fluxo de dados

Atualize os detalhes do seu fluxo de dados, como seu nome e descrição, bem como seu agendamento de execução e conjuntos de mapeamento associados fazendo uma solicitação PATCH para o ponto de extremidade `/flows` da API [!DNL Flow Service], ao mesmo tempo em que fornece a ID do seu fluxo de dados. Ao fazer uma solicitação PATCH, você deve fornecer o `etag` exclusivo do fluxo de dados no cabeçalho `If-Match`. Para obter exemplos completos de API, leia o guia em [atualizando fluxos de dados de fontes usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Atualizar sua conta

Atualize o nome, a descrição e as credenciais da conta de origem executando uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID da conexão base como um parâmetro de consulta. Ao fazer uma solicitação PATCH, você deve fornecer o `etag` exclusivo da sua conta de origem no cabeçalho `If-Match`. Para obter exemplos completos de API, leia o guia em [atualizando a conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Excluir seu fluxo de dados

Exclua seu fluxo de dados executando uma solicitação DELETE para a API [!DNL Flow Service] enquanto fornece a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos de API, leia o guia em [excluindo seus fluxos de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Excluir sua conta

Exclua sua conta executando uma solicitação DELETE para a API [!DNL Flow Service] enquanto fornece a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos de API, leia o guia em [excluindo sua conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
