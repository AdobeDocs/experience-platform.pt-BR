---
keywords: Experience Platform, home, tópicos populares, conexão de transmissão, criar conexão de transmissão, guia de api, tutorial, criar uma conexão de transmissão, assimilação de transmissão, ingestão;
solution: Experience Platform
title: Criar uma conexão de transmissão usando a API
topic-legacy: tutorial
type: Tutorial
description: Este tutorial ajudará você a começar a usar APIs de assimilação de streaming, parte das APIs do serviço de assimilação de dados da Adobe Experience Platform.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 42b8710cf6c04fabf7df1f005fae6b3828eeee49
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 3%

---


# Criação de uma conexão de transmissão usando a API

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para criar uma conexão de transmissão usando a API do Serviço de fluxo.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): O quadro normalizado pelo qual  [!DNL Platform] organiza os dados de experiência.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Além disso, a criação de uma conexão de transmissão exige um esquema XDM de destino e um conjunto de dados. Para saber como criá-los, leia o tutorial em [dados de registro de transmissão](../../../../../ingestion/tutorials/streaming-record-data.md) ou o tutorial em [dados da série de tempo de transmissão](../../../../../ingestion/tutorials/streaming-time-series-data.md).

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de assimilação de streaming.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../../../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão base

Uma conexão base especifica a fonte e contém as informações necessárias para tornar o fluxo compatível com as APIs de assimilação de streaming. Ao criar uma conexão base, você tem a opção de criar uma conexão não autenticada e autenticada.

### Conexão não autenticada

As conexões não autenticadas são a conexão de transmissão padrão que pode ser criada quando você deseja transmitir dados na Plataforma.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

Para criar uma conexão de transmissão, a ID do provedor e a ID de especificação de conexão devem ser fornecidas como parte da solicitação do POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.sourceId` | A ID da conexão de transmissão que você deseja criar. |
| `auth.params.dataType` | O tipo de dados para a conexão de transmissão. Esse valor deve ser `xdm`. |
| `auth.params.name` | O nome da conexão de transmissão que deseja criar. |
| `connectionSpec.id` | A especificação de conexão `id` para conexões de transmissão. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O `id` da conexão recém-criada. Isso será chamado de `{CONNECTION_ID}`. |
| `etag` | Um identificador atribuído à conexão, especificando a revisão da conexão. |

### Conexão autenticada

As conexões autenticadas devem ser usadas quando for necessário diferenciar entre registros provenientes de fontes confiáveis e não confiáveis. Os usuários que desejam enviar informações com informações de identificação pessoal (PII) devem criar uma conexão autenticada ao transmitir informações para a plataforma.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

Para criar uma conexão de transmissão, a ID do provedor e a ID de especificação de conexão devem ser fornecidas como parte da solicitação do POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.sourceId` | A ID da conexão de transmissão que você deseja criar. |
| `auth.params.dataType` | O tipo de dados para a conexão de transmissão. Esse valor deve ser `xdm`. |
| `auth.params.name` | O nome da conexão de transmissão que deseja criar. |
| `auth.params.authenticationRequired` | O parâmetro que especifica a conexão de transmissão criada |
| `connectionSpec.id` | A especificação de conexão `id` para conexões de transmissão. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O `id` da conexão recém-criada. Isso será chamado de `{CONNECTION_ID}`. |
| `etag` | Um identificador atribuído à conexão, especificando a revisão da conexão. |

## Obter URL de ponto de extremidade de fluxo

Com a conexão básica criada, agora é possível recuperar o URL do terminal de transmissão.

**Formato da API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão criada anteriormente. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a conexão solicitada. O URL do ponto de extremidade de transmissão é criado automaticamente com a conexão e pode ser recuperado usando o valor `inletUrl` .

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Criar uma conexão de origem

Depois de criar a conexão básica, será necessário criar uma conexão de origem. Ao criar uma conexão de origem, você precisará do valor `id` da conexão de base criada.

**Formato da API**

```http
POST /flowservice/sourceConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão de origem recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## Criar uma conexão de destino

Depois de criar a conexão de origem, você pode criar uma conexão de destino. Ao criar a conexão de destino, você precisará do valor `id` do conjunto de dados criado anteriormente.

**Formato da API**

```http
POST /flowservice/targetConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão de destino recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## Criar um fluxo de dados

Com as conexões de origem e de destino criadas, agora é possível criar um fluxo de dados. O fluxo de dados é responsável por agendar e coletar dados de uma fonte. Você pode criar um fluxo de dados executando uma solicitação POST para o ponto de extremidade `/flows`.

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes do fluxo de dados recém-criado, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HTTP de transmissão, permitindo usar o endpoint de transmissão para assimilar dados na plataforma. Para obter instruções para criar uma conexão de transmissão na interface do usuário, leia o [tutorial de conexão de transmissão](../../../ui/create/streaming/http.md).

Para saber como transmitir dados para a Platform, leia o tutorial em [dados da série de tempo de transmissão](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou o tutorial em [dados de registro de transmissão](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apêndice

Esta seção fornece informações complementares sobre como criar conexões de transmissão usando a API.

### Envio de mensagens para uma conexão de transmissão autenticada

Se uma conexão de transmissão tiver a autenticação ativada, o cliente deverá adicionar o cabeçalho `Authorization` à solicitação.

Se o cabeçalho `Authorization` não estiver presente ou um token de acesso inválido/expirado for enviado, uma resposta HTTP 401 Não autorizado será retornada, com uma resposta semelhante como abaixo:

**Resposta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

### Postar dados brutos a serem assimilados na plataforma {#ingest-data}

Depois de criar o fluxo, é possível enviar a mensagem JSON para o endpoint de transmissão criado anteriormente.

**Formato da API**

```http
POST /collection/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão de transmissão recém-criada. |

**Solicitação**

A solicitação de exemplo assimila dados brutos no endpoint de transmissão que foi criado anteriormente.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das informações recém-assimiladas.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{CONNECTION_ID}` | A ID da conexão de transmissão criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerou no lado do servidor para o registro que você acabou de enviar. Essa ID ajuda o Adobe a rastrear o ciclo de vida desse registro em vários sistemas e com a depuração. |
| `receivedTimeMs` | Um carimbo de data e hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |
