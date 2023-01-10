---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Criar um fluxo de dados para a Campanha Mailchimp usando a API do Serviço de Fluxo
description: Saiba como conectar o Adobe Experience Platform ao MailChimp Campaign usando a API do Serviço de Fluxo.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 2%

---

# Criar um fluxo de dados para [!DNL Mailchimp Campaign] usando a API do Serviço de Fluxo

O tutorial a seguir o orienta pelas etapas para criar uma conexão de origem e um fluxo de dados para trazer [!DNL Mailchimp Campaign] dados para a plataforma usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Pré-requisitos

Antes de se conectar [!DNL Mailchimp] para o Adobe Experience Platform usando o código de atualização do OAuth 2, você deve primeiro recuperar o token de acesso para [!DNL MailChimp.] Consulte a [[!DNL Mailchimp] Guia OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) para obter instruções detalhadas sobre como encontrar o token de acesso.

## Criar uma conexão base {#base-connection}

Depois de recuperar o [!DNL Mailchimp] credenciais de autenticação, agora você pode iniciar o processo de criação do fluxo de dados para trazer [!DNL Mailchimp Campaign] para a plataforma. A primeira etapa na criação de um fluxo de dados é criar uma conexão base.

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

[!DNL Mailchimp] O suporta autenticação básica e código de atualização OAuth 2. Consulte os exemplos a seguir para obter orientação sobre como autenticar com qualquer um dos tipos de autenticação.

### Crie um [!DNL Mailchimp] conexão básica usando autenticação básica

Para criar um [!DNL Mailchimp] conexão básica usando autenticação básica, faça uma solicitação de POST para `/connections` ponto final de [!DNL Flow Service] API , fornecendo credenciais para `authorizationTestUrl`, `username`e `password`.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão base seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão base. |
| `description` | (Opcional) Uma propriedade que pode ser incluída para fornecer mais informações sobre a conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão da sua origem. Essa ID pode ser recuperada depois que a fonte é registrada e aprovada por meio do [!DNL Flow Service] API. |
| `auth.specName` | O tipo de autenticação que você está usando para conectar sua fonte à Platform. |
| `auth.params.authorizationTestUrl` | (Opcional) O URL do teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |
| `auth.params.username` | O nome de usuário que corresponde a sua [!DNL Mailchimp] conta. Isso é necessário para a autenticação básica. |
| `auth.params.password` | A senha que corresponde ao seu [!DNL Mailchimp] conta. Isso é necessário para a autenticação básica. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura e o conteúdo do arquivo da sua origem na próxima etapa.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### Crie um [!DNL Mailchimp] conexão base usando o código de atualização OAuth 2

Para criar um [!DNL Mailchimp] conexão base usando o código de atualização OAuth 2, faça uma solicitação de POST para a `/connections` endpoint , ao fornecer credenciais para `authorizationTestUrl`e `accessToken`.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with OAuth 2 refresh code",
      "description": "Mailchimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão base seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão base. |
| `description` | (Opcional) Uma propriedade que pode ser incluída para fornecer mais informações sobre a conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão da sua origem. Essa ID pode ser recuperada depois de registrar sua fonte usando o [!DNL Flow Service] API. |
| `auth.specName` | O tipo de autenticação que você está usando para autenticar sua origem na Plataforma. |
| `auth.params.authorizationTestUrl` | (Opcional) O URL de teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |
| `auth.params.accessToken` | O token de acesso correspondente usado para autenticar sua fonte. Isso é necessário para a autenticação baseada em OAuth. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura e o conteúdo do arquivo da sua origem na próxima etapa.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Explorar sua fonte {#explore}

Usando a ID de conexão básica gerada na etapa anterior, você pode explorar arquivos e diretórios executando solicitações do GET. Ao executar solicitações do GET para explorar a estrutura de arquivos e o conteúdo de sua origem, você deve incluir os parâmetros de consulta listados na tabela abaixo:

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica gerada na etapa anterior. |
| `{OBJECT_TYPE}` | O tipo do objeto que você deseja explorar. Para fontes REST, esse valor assume como padrão `rest`. |
| `{OBJECT}` | O objeto que você deseja explorar. |
| `{FILE_TYPE}` | Esse parâmetro é necessário somente ao visualizar um diretório específico. Seu valor representa o caminho do diretório que você deseja explorar. |
| `{PREVIEW}` | Um valor booleano que define se o conteúdo da conexão suporta pré-visualização. |
| `{SOURCE_PARAMS}` | Uma string codificada em base64 de seu `campaign_id`. |

>[!TIP]
>
>Para recuperar o tipo de formato aceito para `{SOURCE_PARAMS}`, você deve codificar o todo `campaignId` string em base64. Por exemplo, `{"campaignId": "c66a200cda"}` codificado em base64 é igual a `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura do arquivo consultado.

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## Criar uma conexão de origem {#source-connection}

Você pode criar uma conexão de origem fazendo uma solicitação de POST para o [!DNL Flow Service] API. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

Para criar uma conexão de origem, você também deve definir um valor enum para o atributo de formato de dados.

Use os seguintes valores enum para fontes baseadas em arquivo:

| Formato dos dados | Valor de enumeração |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todas as fontes baseadas em tabela, defina o valor como `tabular`.

**Formato da API**

```https
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão básica de [!DNL Mailchimp]. Essa ID foi gerada em uma etapa anterior. |
| `connectionSpec.id` | A ID da especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato do [!DNL Mailchimp] dados que você deseja assimilar. |
| `params.campaignId` | O [!DNL Mailchimp] a ID da campanha identifica um [!DNL Mailchimp] campanha, que permite enviar emails para suas listas/públicos. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um schema de target deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema de destino é usado para criar um conjunto de dados da plataforma no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando-se uma solicitação de POST para a [API do Registro de Schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial em [criação de um schema usando a API](../../../../../xdm/api/schemas.md).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação de POST para a [API do Serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do schema do target no payload.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial em [criação de um conjunto de dados usando a API](../../../../../catalog/api/create-dataset.md).

## Criar uma conexão de destino {#target-connection}

Uma conexão target representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa que corresponde ao [!DNL Data Lake]. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos em um esquema de destino em um conjunto de dados de destino e a ID de especificação de conexão com o [!DNL Data Lake]. Usando esses identificadores, você pode criar uma conexão de target usando o [!DNL Flow Service] API para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de destino para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação de conexão que corresponde a [!DNL Data Lake]. Essa ID fixa é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | O formato do [!DNL Mailchimp] dados que você deseja trazer para a plataforma. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |


**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Essa ID é necessária em etapas posteriores.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>Atualmente, as funções de preparação de dados não são compatíveis com o [!DNL Mailchimp Campaign].

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## Criar um fluxo {#flow}

O último passo para trazer [!DNL Mailchimp] Os dados para a Platform são para criar um fluxo de dados. Por enquanto, você terá os seguintes valores obrigatórios preparados:

* [ID de conexão de origem](#source-connection)
* [ID de conexão do Target](#target-connection)

Um fluxo de dados é responsável por agendar e coletar dados de uma fonte. Você pode criar um fluxo de dados executando uma solicitação de POST e, ao mesmo tempo, fornecendo os valores mencionados anteriormente dentro da carga útil.

Para agendar uma assimilação, primeiro defina o valor de hora de início como época em segundos. Em seguida, você deve definir o valor de frequência para uma das cinco opções: `once`, `minute`, `hour`, `day`ou `week`. O valor do intervalo designa o período entre duas assimilações consecutivas e cria uma ingestão única (`once`) não requer que um intervalo seja definido. Para todas as outras frequências, o valor do intervalo deve ser definido como igual ou superior a `15`.


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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do seu fluxo de dados. Certifique-se de que o nome do seu fluxo de dados seja descritivo, pois você pode usá-lo para pesquisar informações no seu fluxo de dados. |
| `description` | (Opcional) Uma propriedade que pode ser incluída para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID de especificação de fluxo necessária para criar um fluxo de dados. Essa ID fixa é: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | A versão correspondente da ID de especificação de fluxo. Esse valor assume como padrão `1.0`. |
| `sourceConnectionIds` | O [ID de conexão de origem](#source-connection) gerado em uma etapa anterior. |
| `targetConnectionIds` | O [target connection ID](#target-connection) gerado em uma etapa anterior. |
| `scheduleParams.startTime` | A hora de início designada para o início da primeira assimilação de dados. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero. O intervalo não é necessário quando a frequência é definida como `once` e deve ser maior que ou igual a `15` para outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado. Você pode usar essa ID para monitorar, atualizar ou excluir seu fluxo de dados.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## Apêndice

A seção a seguir fornece informações sobre as etapas possíveis para monitorar, atualizar e excluir seu fluxo de dados.

### Monitorar o fluxo de dados

Depois que o fluxo de dados tiver sido criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos da API, leia o guia em [monitorar os fluxos de dados de fontes usando a API](../../monitor.md).

### Atualizar o fluxo de dados

Atualize os detalhes do seu fluxo de dados, como o nome e a descrição, bem como o cronograma de execução e os conjuntos de mapeamento associados, fazendo uma solicitação de PATCH para a `/flows` ponto final de [!DNL Flow Service] API, enquanto fornece a ID do fluxo de dados. Ao fazer uma solicitação do PATCH, você deve fornecer dados exclusivos de seu fluxo de dados `etag` no `If-Match` cabeçalho. Para obter exemplos completos da API, leia o guia em [atualização de fluxos de dados de fontes usando a API](../../update-dataflows.md).

### Atualize sua conta

Atualize o nome, a descrição e as credenciais da conta de origem executando uma solicitação de PATCH para a [!DNL Flow Service] API ao fornecer a ID de conexão básica como parâmetro de consulta. Ao fazer uma solicitação de PATCH, você deve fornecer a conta de origem exclusiva `etag` no `If-Match` cabeçalho. Para obter exemplos completos da API, leia o guia em [atualização da conta de origem usando a API](../../update.md).

### Excluir seu fluxo de dados

Exclua seu fluxo de dados executando uma solicitação de DELETE para [!DNL Flow Service] Ao fornecer a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos da API, leia o guia em [excluir seus fluxos de dados usando a API](../../delete-dataflows.md).

### Excluir sua conta

Exclua sua conta executando uma solicitação de DELETE para [!DNL Flow Service] API ao fornecer a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos da API, leia o guia em [excluir sua conta de origem usando a API](../../delete.md).