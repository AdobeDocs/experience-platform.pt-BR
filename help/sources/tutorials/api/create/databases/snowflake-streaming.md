---
title: Conecte sua conta de streaming do Snowflake à Adobe Experience Platform
description: Saiba como conectar o Adobe Experience Platform à transmissão Snowflake usando a API do serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: a4a464f1f3b61311754a39f2a6e6a4ef21af3ab0
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 5%

---

# Transmitir dados do [!DNL Snowflake] para o Experience Platform usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>
> A fonte de transmissão [!DNL Snowflake] está disponível na API para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Este tutorial fornece etapas sobre como conectar e transmitir dados da sua conta do [!DNL Snowflake] para a Adobe Experience Platform usando a [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

### Coletar credenciais necessárias

Leia a [[!DNL Snowflake] visão geral](../../../../connectors/databases/snowflake-streaming.md#prerequisites) para obter informações sobre autenticação.

## Criar uma conexão básica {#create-a-base-connection}

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação do [!DNL Snowflake] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Snowflake]:

>[!TIP]
>
>O valor `auth.specName` deve ser inserido exatamente como o exemplo abaixo, incluindo os espaços em branco.

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
| `auth.params.account` | O nome da sua conta de streaming [!DNL Snowflake]. |
| `auth.params.database` | O nome do banco de dados [!DNL Snowflake] do qual os dados serão extraídos. |
| `auth.params.warehouse` | O nome do warehouse [!DNL Snowflake]. O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse é independente um do outro e deve ser acessado individualmente ao trazer dados para o Experience Platform. |
| `auth.params.username` | O nome de usuário da sua conta de streaming [!DNL Snowflake]. |
| `auth.params.schema` | (Opcional) O esquema de banco de dados associado à sua conta de streaming [!DNL Snowflake]. |
| `auth.params.password` | A senha da sua conta de streaming [!DNL Snowflake]. |
| `auth.params.role` | (Opcional) A função do usuário para esta conexão [!DNL Snowflake]. Se não for fornecido, o padrão será `public`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Snowflake]: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada e sua tag correspondente.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Explore suas tabelas de dados {#explore-your-data-tables}

Em seguida, use a ID de conexão básica para explorar e navegar pelas tabelas de dados da sua origem, fazendo uma solicitação GET para o ponto de extremidade `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` e fornecendo a ID de conexão básica como um parâmetro.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão base da sua fonte de streaming [!DNL Snowflake]. |


**Solicitação**

A solicitação a seguir recupera a estrutura e o conteúdo da sua conta de streaming [!DNL Snowflake].

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

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service].

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
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `baseConnectionId` | A ID da conexão base autenticada para sua fonte de streaming [!DNL Snowflake]. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID de especificação da conexão para a fonte de streaming [!DNL Snowflake]. |
| `params.tableName` | O nome da tabela no banco de dados [!DNL Snowflake] que você deseja trazer para a Experience Platform. |
| `params.timestampColumn` | O nome da coluna de carimbo de data e hora que será usada para buscar valores incrementais. |
| `params.backfill` | Um sinalizador booleano que determina se os dados são obtidos do início (época 0) ou do momento em que a origem é iniciada. Para obter mais informações sobre esse valor, leia a [[!DNL Snowflake] visão geral da fonte de streaming](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | O valor do fuso horário indica qual hora atual do fuso horário deve ser buscada ao consultar o banco de dados [!DNL Snowflake]. Esse parâmetro deve ser fornecido se a coluna de carimbo de data/hora na configuração estiver definida como `TIMESTAMP_NTZ`. Se não for fornecido, `timezoneValue` assumirá como padrão UTC. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de origem e a tag correspondente. A ID da conexão de origem será usada em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Criar um fluxo de dados

>[!NOTE]
>
>Depois de criar ou atualizar um fluxo de dados de transmissão, é necessária uma breve pausa de 5 minutos na assimilação de dados para evitar possíveis instâncias de perda ou perda de dados.

Para criar um fluxo de dados para transmitir dados da conta do tour [!DNL Snowflake] para a Experience Platform, você deve fazer uma solicitação POST para o ponto de extremidade `/flows` e fornecer os seguintes valores:

>[!TIP]
>
>Siga os links abaixo para obter guias passo a passo sobre como recuperar as seguintes IDs.

* [ID de conexão do Source](#create-a-source-connection)
* [ID da conexão de destino](../../collect/database-nosql.md#create-a-target-connection)
* [ID de especificação de fluxo](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID de mapeamento](../../collect/database-nosql.md#create-a-mapping)

**Formato da API**

```http
POST /flows
```

**Solicitação**

A solicitação a seguir cria um fluxo de dados de streaming para sua conta [!DNL Snowflake].

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
| `sourceConnectionIds` | A ID da conexão de origem da sua fonte de streaming [!DNL Snowflake]. |
| `targetConnectionIds` | A ID da conexão de destino para sua fonte de streaming [!DNL Snowflake]. |
| `flowSpec.id` | A ID de especificação do fluxo para criar um fluxo de dados para uma fonte de streaming [!DNL Snowflake]. Essa ID de especificação de fluxo permite criar um fluxo de dados de transmissão com transformações de mapeamento. Essa ID é fixa e é: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
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

Seguindo este tutorial, você criou um fluxo de dados de transmissão para seus dados do [!DNL Snowflake] usando a API [!DNL Flow Service]. Consulte a documentação a seguir para obter informações adicionais sobre origens na Adobe Experience Platform:

* [Visão geral das fontes](../../../../home.md)
* [Monitorar seu fluxo de dados usando APIs](../../monitor.md)
