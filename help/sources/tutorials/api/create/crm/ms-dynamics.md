---
title: Criar uma conexão básica do Microsoft Dynamics usando a API do serviço de fluxo
description: Saiba como conectar o Experience Platform a uma conta do Microsoft Dynamics usando a API do serviço de fluxo.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 5%

---

# Conectar o [!DNL Microsoft Dynamics] ao Experience Platform usando a API [!DNL Flow Service]

Leia este guia para saber como você pode conectar sua origem do [!DNL Microsoft Dynamics] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

As seções a seguir fornecem informações adicionais que você precisará saber para conectar com êxito o Experience Platform a uma conta do Dynamics usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Dynamics], você deve fornecer valores para as seguintes propriedades de conexão:

>[!BEGINTABS]

>[!TAB Autenticação básica]

| Credencial | Descrição |
| --- | --- |
| `serviceUri` | A URL de serviço da instância [!DNL Dynamics]. |
| `username` | O nome de usuário da sua conta de usuário [!DNL Dynamics]. |
| `password` | A senha da sua conta [!DNL Dynamics]. |

>[!TAB Autenticação da entidade de serviço e da chave]

| Credencial | Descrição |
| --- | --- |
| `servicePrincipalId` | A ID de cliente da sua conta [!DNL Dynamics]. Essa ID é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

>[!ENDTABS]

Para obter mais informações sobre a introdução, consulte [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Criar uma conexão básica

>[!TIP]
>
>Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL Dynamics]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Dynamics] como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para criar uma conexão base do [!DNL Dynamics] usando autenticação básica, faça uma solicitação POST para a API [!DNL Flow Service] enquanto fornece valores para os `serviceUri`, `username` e `password` da sua conexão.

**Solicitação**

A solicitação a seguir cria uma conexão base para uma origem [!DNL Dynamics] usando autenticação básica.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.serviceUri` | O URI de serviço associado à sua instância [!DNL Dynamics]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Dynamics]. |
| `auth.params.password` | A senha associada à sua conta [!DNL Dynamics]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Selecione para exibir o exemplo de resposta

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Autenticação baseada na chave da entidade de serviço]

Para criar uma conexão base [!DNL Dynamics] usando a autenticação baseada em chave da entidade de serviço, faça uma solicitação POST para a API [!DNL Flow Service] enquanto fornece valores para os `serviceUri`, `servicePrincipalId` e `servicePrincipalKey` da sua conexão.

**Solicitação**

A solicitação a seguir cria uma conexão base para uma origem [!DNL Dynamics] usando a autenticação básica baseada em chave de entidade de serviço.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.serviceUri` | O URI de serviço associado à sua instância [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | A ID de cliente da sua conta [!DNL Dynamics]. Essa ID é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `auth.params.servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`).

+++Selecione para exibir o exemplo de resposta

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Explore suas tabelas de dados

Para explorar suas tabelas de dados do [!DNL Dynamics], faça uma solicitação GET para o ponto de extremidade `/connections/{BASE_CONNECTION_ID}/explore` e forneça sua ID de conexão básica como parte dos parâmetros de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão base. Use essa ID para explorar o conteúdo e a estrutura da fonte. |

**Solicitação**

A solicitação a seguir recupera a lista de tabelas e exibições disponíveis para uma origem [!DNL Dynamics] com a ID de conexão base: `dd668808-25da-493f-8782-f3433b976d1e`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o diretório de tabelas e exibições [!DNL Dynamics] no nível raiz.

+++Selecione para exibir o exemplo de resposta

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### Usar a chave primária para otimizar a exploração de dados

>[!NOTE]
>
>Você só pode usar atributos que não sejam de pesquisa ao usar a abordagem de chave primária para otimização.

Você pode otimizar suas consultas de exploração fornecendo `primaryKey` como parte de seus parâmetros de consulta. Você deve especificar a chave primária da tabela [!DNL Dynamics] ao incluir `primaryKey` como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão base. Use essa ID para explorar o conteúdo e a estrutura da fonte. |
| `preview` | Um valor booleano que permite a visualização de dados. |
| `{OBJECT}` | O objeto [!DNL Dynamics] que você deseja explorar. |
| `{OBJECT_TYPE}` | O tipo do objeto. |
| `previewCount` | Uma restrição que limita a visualização retornada a apenas um determinado número de registros. |
| `{PRIMARY_KEY}` | A chave primária da tabela que você está recuperando para visualização. |

**Solicitação**

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## Inspecionar a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela específica, faça uma solicitação GET para `/connections/{BASE_CONNECTION_ID}/explore` e forneça o caminho para a tabela específica como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Parâmetro de consulta | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão base. Use essa ID para explorar o conteúdo e a estrutura da fonte. |
| `{TABLE_PATH}` | O caminho para a tabela específica que você deseja explorar. |

**Solicitação**

A solicitação a seguir recupera a estrutura e o conteúdo de uma tabela [!DNL Dynamics] com o caminho `workflowdependency`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o conteúdo do caminho `workflowdependency`.

+++Selecione para exibir o exemplo de resposta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## Inspecionar a estrutura de uma exibição

Em [!DNL Dynamics], uma exibição se refere às colunas a serem exibidas, à largura de cada coluna, ao sistema padrão no qual uma lista de registros é classificada e aos filtros padrão aplicados para restringir quais registros aparecerão na lista.

Para inspecionar a estrutura de um modo de exibição, faça uma solicitação GET para `/connections/{BASE_CONNECTION_ID}/explore` e especifique o caminho de modo de exibição nos parâmetros de consulta. Além disso, você deve especificar `objectType` como `view`.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Parâmetro de consulta | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão base. Use essa ID para explorar o conteúdo e a estrutura da fonte. |
| `{VIEW_PATH}` | O caminho para a exibição que você deseja inspecionar. |

**Solicitação**

A solicitação a seguir recupera `accountView1`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna a estrutura de `accountView1`.

+++Selecione para exibir o exemplo de resposta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Visualizar exibição de tipo de entidade

Para visualizar o conteúdo de um modo de exibição, faça uma solicitação do GET para `/connections/{BASE_CONNECTION_ID}/explore` e inclua o caminho de exibição e `preview=true` nos parâmetros de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Parâmetro de consulta | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão base. Use essa ID para explorar o conteúdo e a estrutura da fonte. |
| `{VIEW_PATH}` | O caminho para a exibição que você deseja inspecionar. |


**Solicitação**

A solicitação a seguir visualiza o conteúdo de `accountView1`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o conteúdo de `accountView1`.

+++Selecione para exibir o exemplo de resposta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Criar uma conexão de origem para assimilar a exibição

Para criar uma conexão de origem e assimilar uma exibição, faça uma solicitação POST para o ponto de extremidade `/sourceConnections`, forneça o nome da tabela e especifique `entityType` como `view` no corpo da solicitação.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem [!DNL Dynamics] e assimila exibições.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de origem recém-gerada e a tag correspondente.

+++Selecione para exibir o exemplo de resposta

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### Usar a chave primária para otimizar seu fluxo de dados

Você também pode otimizar o fluxo de dados do [!DNL Dynamics] especificando a chave primária como parte dos parâmetros do corpo da solicitação.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem [!DNL Dynamics] ao especificar a chave primária como `contactid`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `baseConnectionId` | A ID da conexão base. |
| `data.format` | O formato dos dados. |
| `params.tableName` | O nome da tabela em [!DNL Dynamics]. |
| `params.primaryKey` | A chave primária da tabela que otimizará as consultas. |
| `connectionSpec.id` | A ID de especificação da conexão que corresponde à origem [!DNL Dynamics]. |

+++

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de origem recém-gerada e a tag correspondente.

+++Selecione para exibir o exemplo de resposta

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Microsoft Dynamics] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para o Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/crm.md)
