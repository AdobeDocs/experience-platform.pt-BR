---
title: Conecte sua conta de transmissão do Snowflake à Adobe Experience Platform
description: Saiba como conectar o Adobe Experience Platform ao Snowflake Streaming usando a API do Serviço de fluxo.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: 8bc232034301fa713f61bd3f11fbde122afcdcf9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# Fluxo [!DNL Snowflake] dados para Experience Platform usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>* A variável [!DNL Snowflake] a fonte da transmissão está na versão beta. Leia as [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.
>* Suporte de API para o [!DNL Snowflake] a fonte de transmissão está disponível somente para clientes que compraram o Real-Time CDP Ultimate.


Este tutorial fornece etapas sobre como conectar e transmitir dados de seu [!DNL Snowflake] para a Adobe Experience Platform usando a variável [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Para obter a configuração de pré-requisitos e informações sobre o [!DNL Snowflake] origem da transmissão. Leia as [[!DNL Snowflake] visão geral da fonte de transmissão](../../../../connectors/databases/snowflake-streaming.md).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica {#create-a-base-connection}

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Snowflake] credenciais de autenticação como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Snowflake]:

>[!TIP]
>
>A variável `auth.specName` deve ser inserido exatamente como no exemplo abaixo, incluindo os espaços em branco.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.account` | O nome do seu [!DNL Snowflake] conta de transmissão. |
| `auth.params.database` | O nome do seu [!DNL Snowflake] banco de dados de onde os dados serão extraídos. |
| `auth.params.warehouse` | O nome do seu [!DNL Snowflake] depósito. A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Cada warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a plataforma. |
| `auth.params.username` | O nome de usuário do seu [!DNL Snowflake] conta de transmissão. |
| `auth.params.schema` | (Opcional) O esquema de banco de dados associado à [!DNL Snowflake] conta de transmissão. |
| `auth.params.password` | A senha do [!DNL Snowflake] conta de transmissão. |
| `auth.params.role` | (Opcional) A função do usuário para este [!DNL Snowflake] conexão. Se não for fornecido, esse valor assumirá como padrão `public`. |
| `connectionSpec.id` | A variável [!DNL Snowflake] ID da especificação de conexão: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada e sua tag correspondente.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Explore suas tabelas de dados {#explore-your-data-tables}

Em seguida, use a ID de conexão básica para explorar e navegar pelas tabelas de dados da sua origem fazendo uma solicitação GET para o `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` ao fornecer a ID de conexão básica como parâmetro.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica de seu [!DNL Snowflake] origem da transmissão. |


**Solicitação**

A solicitação a seguir recupera a estrutura e o conteúdo do [!DNL Snowflake] conta de transmissão.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura e o conteúdo dos dados da origem no nível raiz.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `items.type` | O tipo da tabela. |
| `items.names` | O nome da tabela. |

## Criar uma conexão de origem {#create-a-source-connection}

Uma conexão de origem cria e gerencia a conexão com a origem externa de onde os dados são assimilados.

Para criar uma conexão de origem, faça uma solicitação POST ao `/sourceConnections` endpoint do [!DNL Flow Service] API.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `baseConnectionId` | A ID de conexão básica autenticada do seu [!DNL Snowflake] origem da transmissão. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID de especificação da conexão para o [!DNL Snowflake] origem da transmissão. |
| `params.tableName` | O nome da tabela no [!DNL Snowflake] banco de dados que você deseja trazer para a Platform. |
| `params.timestampColumn` | O nome da coluna de carimbo de data e hora que será usada para buscar valores incrementais. |
| `params.backfill` | Um sinalizador booleano que determina se os dados são obtidos do início (época 0) ou do momento em que a origem é iniciada. Para obter mais informações sobre esse valor, leia a [[!DNL Snowflake] visão geral da fonte de transmissão](../../../../connectors/databases/snowflake-streaming.md). |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de origem e a tag correspondente. A ID da conexão de origem será usada em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Criar um fluxo de dados

Para criar um fluxo de dados para transmitir dados de um tour [!DNL Snowflake] para a Platform, você deve fazer uma solicitação POST para a `/flows` ao fornecer os seguintes valores:

>[!TIP]
>
>Siga os links abaixo para obter guias passo a passo sobre como recuperar as seguintes IDs.

* [ID da conexão de origem](#create-a-source-connection)
* [ID da conexão de destino](../../collect/database-nosql.md#create-a-target-connection)
* [ID de especificação de fluxo](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID de mapeamento](../../collect/database-nosql.md#create-a-mapping)

**Formato da API**

```http
POST /flows
```

**Solicitação**

A solicitação a seguir cria um fluxo de dados de transmissão para o [!DNL Snowflake] conta.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `sourceConnectionIds` | A ID da conexão de origem para o [!DNL Snowflake] origem da transmissão. |
| `targetConnectionIds` | A ID de conexão de destino para o [!DNL Snowflake] origem da transmissão. |
| `flowSpec.id` | A ID de especificação de fluxo para criar um fluxo de dados para um [!DNL Snowflake] origem da transmissão. Essa ID de especificação de fluxo permite criar um fluxo de dados de transmissão com transformações de mapeamento. Essa ID é fixa e é: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | A ID de mapeamento do seu fluxo de dados. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e a tag correspondente.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um fluxo de dados de transmissão para seu [!DNL Snowflake] dados usando o [!DNL Flow Service] API. Consulte a documentação a seguir para obter informações adicionais sobre origens na Adobe Experience Platform:

* [Visão geral das fontes](../../../../home.md)
* [Monitorar seu fluxo de dados usando APIs](../../monitor.md)