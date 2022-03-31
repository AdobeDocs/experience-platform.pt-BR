---
keywords: Experience Platform; home; tópicos populares;
solution: Experience Platform
title: Conectar a zona de aterrissagem de dados ao Adobe Experience Platform usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform à zona de aterrissagem de dados usando a API do Serviço de fluxo.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 5829b50a81741cc4883dfa8f4d7d7891b791caf5
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 5%

---

# Connect [!DNL Data Landing Zone] à Adobe Experience Platform usando a API do Serviço de Fluxo

[!DNL Data Landing Zone] é um recurso de armazenamento de dados baseado em nuvem para armazenamento temporário de arquivos provisionado com o Adobe Experience Platform. Os dados são excluídos automaticamente do [!DNL Data Landing Zone] após sete dias.

Este tutorial o orienta pelas etapas sobre como criar um [!DNL Data Landing Zone] conexão de origem usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Este tutorial também fornece instruções sobre como recuperar [!DNL Data Landing Zone], bem como exibir e atualizar suas credenciais.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com sucesso um [!DNL Data Landing Zone] conexão de origem usando o [!DNL Flow Service] API.

Este tutorial também requer a leitura do guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md) para saber como autenticar nas APIs da plataforma e interpretar os exemplos de chamadas fornecidos na documentação.

## Recuperar uma zona de aterrissagem utilizável

A primeira etapa do uso de APIs para acessar o [!DNL Data Landing Zone] é fazer uma solicitação GET para `/landingzone` endpoint da variável [!DNL Connectors] API ao fornecer `type=user_drop_zone` como parte do cabeçalho da solicitação.

**Formato da API**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Cabeçalhos | Descrição |
| --- | --- |
| `user_drop_zone` | O `user_drop_zone` permite que a API diferencie um contêiner de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |

**Solicitação**

A solicitação a seguir recupera uma zona de aterrissagem existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Resposta**

A resposta a seguir retorna informações sobre uma zona de aterrissagem, incluindo as correspondentes `containerName` e `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome da zona de aterrissagem recuperada. |
| `containerTTL` | A configuração de tempo de vida útil aplicada aos seus dados dentro da zona de aterrissagem. Os produtos de uma determinada zona de aterrissagem são eliminados após sete dias. |

## Recuperar [!DNL Data Landing Zone] credenciais

Para recuperar credenciais para um [!DNL Data Landing Zone], faça uma solicitação GET para `/credentials` endpoint da variável [!DNL Connectors] API.

**Formato da API**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Solicitação**

O exemplo de solicitação a seguir recupera credenciais para uma zona de aterrissagem existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

A resposta a seguir retorna as informações de credenciais para a zona de aterrissagem, incluindo a `SASToken` e `SASUri`, bem como a `storageAccountName` que corresponde ao contêiner da zona de aterrissagem.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome da sua zona de aterrissagem. |
| `SASToken` | O token de assinatura de acesso compartilhado para sua zona de aterrissagem. Essa cadeia de caracteres contém todas as informações necessárias para autorizar uma solicitação. |
| `SASUri` | O URI da assinatura de acesso compartilhado para sua zona de aterrissagem. Essa string é uma combinação do URI à zona de aterrissagem para a qual você está sendo autenticado e seu token SAS correspondente, |


## Atualizar [!DNL Data Landing Zone] credenciais

Você pode atualizar seu `SASToken` ao fazer uma solicitação de POST à `/credentials` endpoint da variável [!DNL Connectors] API.

**Formato da API**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Cabeçalhos | Descrição |
| --- | --- |
| `user_drop_zone` | O `user_drop_zone` permite que a API diferencie um contêiner de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |
| `refresh` | O `refresh` permite redefinir as credenciais da zona de aterrissagem e gerar automaticamente um novo `SASToken`. |

**Solicitação**

A solicitação a seguir atualiza suas credenciais da zona de aterrissagem.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

A resposta a seguir retorna valores atualizados para seu `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Explorar a estrutura e o conteúdo do arquivo da zona de aterrissagem

Você pode explorar a estrutura de arquivos e o conteúdo de sua zona de aterrissagem fazendo uma solicitação de GET para a `connectionSpecs` endpoint da variável [!DNL Flow Service] API.

**Formato da API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | A ID da especificação de conexão que corresponde a [!DNL Data Landing Zone]. Essa ID fixa é: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote o `path` propriedade do arquivo que deseja fazer upload, pois é necessário fornecê-lo na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Visualizar a estrutura e o conteúdo do arquivo da zona de aterrissagem

Para inspecionar a estrutura de um arquivo na zona de aterrissagem, execute uma solicitação de GET enquanto fornece o caminho do arquivo e digite como um parâmetro de consulta.

**Formato da API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | A ID da especificação de conexão que corresponde a [!DNL Data Landing Zone]. Essa ID fixa é: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | O tipo do objeto que você deseja acessar. | `file` |
| `{OBJECT}` | O caminho e o nome do objeto que você deseja acessar. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | O tipo do arquivo. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Um valor booleano que define se a visualização de arquivo é compatível. | </ul><li>`true`</li><li>`false`</li></ul> |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura do arquivo consultado, incluindo nomes de arquivo e tipos de dados.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### Use `determineProperties` para detectar automaticamente as informações de propriedade do arquivo de um [!DNL Data Landing Zone]

Você pode usar o `determineProperties` para detectar automaticamente as informações de propriedade do conteúdo do arquivo de sua [!DNL Data Landing Zone] ao fazer uma chamada GET para explorar o conteúdo e a estrutura de sua fonte.

#### `determineProperties` casos de uso

A tabela a seguir descreve cenários diferentes que podem ser encontrados ao usar o `determineProperties` ou forneça manualmente informações sobre seu arquivo.

| `determineProperties` | `queryParams` | Resposta |
| --- | --- | --- |
| Verdadeiro | N/D | If `determineProperties` é fornecido como um parâmetro de consulta, então a detecção de propriedades de arquivo ocorre e a resposta retorna um novo `properties` chave que inclui informações sobre tipo de arquivo, tipo de compactação e delimitador de coluna. |
| N/D | Verdadeiro | Se os valores para tipo de arquivo, tipo de compactação e delimitador de coluna forem fornecidos manualmente como parte de `queryParams`, são usadas para gerar o schema e as mesmas propriedades são retornadas como parte da resposta. |
| Verdadeiro | Verdadeiro | Se ambas as opções forem feitas simultaneamente, um erro será retornado. |
| N/D | N/D | Se nenhuma das duas opções for fornecida, um erro será retornado porque não há como obter propriedades para a resposta. |

**Formato da API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `determineProperties` | Esse parâmetro de consulta permite [!DNL Flow Service] API para detectar informações relacionadas às propriedades do arquivo, incluindo informações sobre tipo de arquivo, tipo de compactação e delimitador de coluna. | `true` |

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura do arquivo consultado, incluindo nomes de arquivo e tipos de dados, bem como uma `properties` chave, contendo informações sobre `fileType`, `compressionType`e `columnDelimiter`.

+++Clique

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Propriedade | Descrição |
| --- | --- |
| `properties.fileType` | O tipo de arquivo correspondente do arquivo consultado. Os tipos de arquivos compatíveis são: `delimited`, `json`e `parquet`. |
| `properties.compressionType` | O tipo de compactação correspondente usado para o arquivo consultado. Os tipos de compactação compatíveis são: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | O delimitador de coluna correspondente usado para o arquivo consultado. Qualquer valor de caractere único é um delimitador de coluna permitido. O valor padrão é uma vírgula `(,)`. |


## Criar uma conexão de origem

Uma conexão de origem cria e gerencia a conexão com a fonte externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e ID de conexão de origem necessárias para criar um fluxo de dados. Uma instância de conexão de origem é específica de um locatário e da Organização IMS.

Para criar uma conexão de origem, faça uma solicitação de POST para a variável `/sourceConnections` endpoint da variável [!DNL Flow Service] API.


**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua [!DNL Data Landing Zone] conexão de origem. |
| `data.format` | O formato dos dados que você deseja trazer para a plataforma. |
| `params.path` | O caminho para o arquivo que você deseja trazer para a plataforma. |
| `connectionSpec.id` | A ID da especificação de conexão que corresponde a [!DNL Data Landing Zone]. Essa ID fixa é: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária no próximo tutorial para criar um fluxo de dados.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você recuperou seu [!DNL Data Landing Zone] credenciais, explorou sua estrutura de arquivos para encontrar o arquivo que deseja trazer para a plataforma e criou uma conexão de origem para começar a trazer seus dados para a plataforma. Agora você pode prosseguir para o próximo tutorial, onde você aprenderá a usar [crie um fluxo de dados para trazer os dados de armazenamento em nuvem para a plataforma usando o [!DNL Flow Service] API](../../collect/cloud-storage.md).
