---
keywords: Experience Platform;início;tópicos populares;conexão de transmissão;criar conexão de transmissão;guia de api;tutorial;criar uma conexão de transmissão;assimilação de transmissão;assimilação;
title: Criar uma conexão de transmissão da API HTTP usando a API do serviço de fluxo
description: Este tutorial fornece etapas sobre como criar uma conexão de transmissão usando a fonte de API HTTP para dados brutos e XDM usando a API do serviço de fluxo
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 6ea5eaf28f260f974d168db2bed9bc95fcfa52af
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 4%

---


# Criar uma conexão de transmissão da API HTTP usando a API [!DNL Flow Service]

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de diferentes fontes na Adobe Experience Platform. O serviço fornece uma interface de usuário e a API RESTful a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) para orientá-lo nas etapas de criação de uma conexão de streaming usando a API [!DNL Flow Service].

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): A estrutura padronizada pela qual o [!DNL Platform] organiza os dados de experiência.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de múltiplas fontes.

Além disso, a criação de uma conexão de transmissão exige que você tenha um esquema XDM de destino e um conjunto de dados. Para aprender a criar essas séries, leia o tutorial em [streaming de dados de registro](../../../../../ingestion/tutorials/streaming-record-data.md) ou o tutorial em [streaming de dados de série temporal](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base especifica a origem e contém as informações necessárias para tornar o fluxo compatível com as APIs de assimilação de streaming. Ao criar uma conexão básica, você tem a opção de criar uma conexão não autenticada e autenticada.

### Conexão não autenticada

Conexões não autenticadas são a conexão de transmissão padrão que você pode criar quando quiser transmitir dados para a Platform.

Para criar uma conexão base não autenticada, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece um nome para a conexão, o tipo de dados e a ID de especificação da conexão da API HTTP. Esta ID é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para a API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Dados brutos]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome seja descritivo, pois você pode usá-lo para pesquisar informações sobre sua conexão básica. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer mais informações sobre sua conexão básica. |
| `connectionSpec.id` | A ID da especificação de conexão que corresponde à API HTTP. Esta ID é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | O tipo de dados da conexão de streaming. Os valores suportados incluem: `xdm` e `raw`. |
| `auth.params.name` | O nome da conexão de streaming que você deseja criar. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O `id` da sua conexão base recém-criada. |
| `etag` | Um identificador atribuído à conexão, especificando a versão da conexão base. |

### Conexão autenticada

As conexões autenticadas devem ser usadas quando for necessário diferenciar entre registros provenientes de fontes confiáveis e não confiáveis. Os usuários que desejam enviar informações com Informações de identificação pessoal (PII) devem criar uma conexão autenticada ao transmitir informações para a Platform.

Para criar uma conexão de base autenticada, você deve incluir o parâmetro `authenticationRequired` em sua solicitação e especificar seu valor como `true`. Durante essa etapa, também é possível fornecer uma ID de origem para a conexão de base autenticada. Este parâmetro é opcional e usará o mesmo valor que o atributo `name`, se ele não for fornecido.


**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica autenticada para a API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Dados brutos]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.sourceId` | Um identificador adicional que pode ser usado ao criar uma conexão de base autenticada. Este parâmetro é opcional e usará o mesmo valor que o atributo `name`, se ele não for fornecido. |
| `auth.params.authenticationRequired` | Esse parâmetro especifica se a conexão de streaming requer ou não autenticação. Se `authenticationRequired` estiver definido como `true`, a autenticação deverá ser fornecida para a conexão de streaming. Se `authenticationRequired` estiver definido como `false`, a autenticação não será necessária. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Obter URL de ponto de extremidade de streaming

Com a conexão base criada, agora é possível recuperar o URL do ponto de extremidade de streaming.

**Formato da API**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | O valor `id` da conexão criada anteriormente. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a conexão solicitada. A URL da extremidade de streaming é criada automaticamente com a conexão e pode ser recuperada usando o valor `inletUrl`.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Criar uma conexão de origem {#source}

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` enquanto fornece a ID da conexão base.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
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
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados da Platform no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](../../../../../xdm/api/schemas.md).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado por meio de uma solicitação POST para a [API de Serviço de Catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do esquema de destino na carga.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../../../catalog/api/create-dataset.md).

## Criar uma conexão de destino {#target}

Uma conexão de destino representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, faça uma solicitação POST para `/targetConnections` enquanto fornece IDs para o conjunto de dados de destino e o esquema XDM de destino. Durante essa etapa, você também deve fornecer a ID de especificação da conexão do data lake. Esta ID é `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão de destino recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere.

Para criar um conjunto de mapeamento, faça uma solicitação POST para o ponto de extremidade `mappingSets` da [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) enquanto fornece o esquema XDM de destino `$id` e os detalhes dos conjuntos de mapeamento que deseja criar.

**Formato da API**

```http
POST /mappingSets
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `xdmSchema` | O `$id` do esquema XDM de destino. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

## Criar um fluxo de dados

Com as conexões de origem e de destino criadas, agora é possível criar um fluxo de dados. O fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST para o ponto de extremidade `/flows`.

**Formato da API**

```http
POST /flows
```

**Solicitação**

>[!BEGINTABS]

>[!TAB XDM]

A solicitação a seguir cria um fluxo de dados de transmissão para dados XDM.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB BRUTO]

As solicitações a seguir criam um fluxo de dados de transmissão para dados brutos.

Ao criar um fluxo de dados com transformações, o parâmetro `name` não pode ser alterado. Este valor deve ser sempre configurado para `Mapping`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do fluxo de dados. Verifique se o nome do fluxo de dados é descritivo, pois você pode usá-lo para pesquisar informações sobre o fluxo de dados. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID da especificação de fluxo para [!DNL HTTP API]. Para criar um fluxo de dados com transformações, você deve usar `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Para criar um fluxo de dados sem transformações, use `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | A [ID da conexão de origem](#source) recuperou em uma etapa anterior. |
| `targetConnectionIds` | A [ID da conexão de destino](#target) recuperou em uma etapa anterior. |
| `transformations.params.mappingId` | A [ID de mapeamento](#mapping) recuperou em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes do fluxo de dados recém-criado, incluindo o identificador exclusivo (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## Dados da publicação a serem assimilados na plataforma {#ingest-data}

>[!NOTE]
>
>Você deve adicionar um atraso de pelo menos ~5 minutos entre a criação do fluxo de dados e a assimilação de quaisquer dados de transmissão. Isso permite que o fluxo de dados seja totalmente ativado, antes que quaisquer dados sejam assimilados.

Agora que você criou o fluxo, é possível enviar a mensagem JSON para o ponto de extremidade de streaming criado anteriormente.

**Formato da API**

```http
POST /collection/{INLET_URL}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INLET_URL}` | O URL do ponto de extremidade de streaming. Você pode recuperar esta URL fazendo uma solicitação GET para o ponto de extremidade `/connections` enquanto fornece sua ID de conexão base. |
| `{FLOW_ID}` | A ID do fluxo de dados de transmissão da API HTTP. Essa ID é necessária para dados XDM e RAW. |

**Solicitação**

>[!BEGINTABS]

>[!TAB Enviar dados XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Enviar dados brutos com identificação de fluxo como um cabeçalho HTTP]

Ao enviar dados brutos, você pode especificar sua ID de fluxo como um parâmetro de consulta ou como parte de seu cabeçalho HTTP. O exemplo a seguir especifica a ID do fluxo como um cabeçalho HTTP.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
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

>[!TAB Enviar dados brutos com a ID de fluxo como um parâmetro de consulta]

Ao enviar dados brutos, você pode especificar sua ID de fluxo como um parâmetro de consulta ou como um cabeçalho HTTP. O exemplo a seguir especifica a ID de fluxo como um parâmetro de consulta.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
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

>[!ENDTABS]

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das informações recém-assimiladas.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | A ID da conexão de streaming criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerado no lado do servidor para o registro que você acabou de enviar. Essa ID ajuda o Adobe a rastrear o ciclo de vida desse registro por vários sistemas e com depuração. |
| `receivedTimeMs` | Um carimbo de data e hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |


## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HTTP de transmissão, permitindo usar o endpoint de transmissão para assimilar dados na Platform. Para obter instruções sobre como criar uma conexão de streaming na interface, leia o [tutorial sobre criação de uma conexão de streaming](../../../ui/create/streaming/http.md).

Para saber como transmitir dados para a Platform, leia o tutorial sobre [dados de série temporal de transmissão](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou o tutorial sobre [dados de registro de transmissão](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apêndice

Esta seção fornece informações adicionais sobre como criar conexões de transmissão usando a API.

### Envio de mensagens a uma conexão de streaming autenticada

Se uma conexão de streaming tiver autenticação habilitada, o cliente precisará adicionar o cabeçalho `Authorization` à solicitação.

Se o cabeçalho `Authorization` não estiver presente ou um token de acesso inválido/expirado for enviado, uma resposta HTTP 401 Não autorizado será retornada, com uma resposta semelhante à abaixo:

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

