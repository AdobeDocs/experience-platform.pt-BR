---
keywords: Experience Platform; home; tópicos populares;
solution: Experience Platform
title: Conectar a zona de aterrissagem de dados ao Adobe Experience Platform usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform à zona de aterrissagem de dados usando a API do Serviço de fluxo.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 4%

---

# Conecte [!DNL Data Landing Zone] ao Adobe Experience Platform usando a API do Serviço de Fluxo

[!DNL Data Landing Zone] é um recurso de armazenamento de dados baseado em nuvem para armazenamento temporário de arquivos provisionado com o Adobe Experience Platform. Os dados são excluídos automaticamente do [!DNL Data Landing Zone] após sete dias.

Este tutorial o orienta pelas etapas sobre como criar uma conexão de origem [!DNL Data Landing Zone] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Este tutorial também fornece instruções sobre como recuperar [!DNL Data Landing Zone], bem como visualizar e atualizar suas credenciais.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito uma conexão de origem [!DNL Data Landing Zone] usando a API [!DNL Flow Service].

Este tutorial também requer a leitura do guia sobre a [introdução às APIs da plataforma](../../../../../landing/api-guide.md) para saber como autenticar para APIs da plataforma e interpretar as chamadas de exemplo fornecidas na documentação.

## Recuperar uma zona de aterrissagem utilizável

A primeira etapa no uso de APIs para acessar [!DNL Data Landing Zone] é fazer uma solicitação GET para o endpoint `/landingzone` da API [!DNL Connectors], fornecendo `type=user_drop_zone` como parte do cabeçalho da solicitação.

**Formato da API**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Cabeçalhos | Descrição |
| --- | --- |
| `user_drop_zone` | O tipo `user_drop_zone` permite que a API diferencie um contêiner de zona de aterrissagem dos outros tipos de contêineres que estão disponíveis para você. |

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

A resposta a seguir retorna informações em uma zona de aterrissagem, incluindo seus `containerName` e `containerTTL` correspondentes.

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

## Recuperar credenciais [!DNL Data Landing Zone]

Para recuperar credenciais para um [!DNL Data Landing Zone], faça uma solicitação GET ao endpoint `/credentials` da API [!DNL Connectors].

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

A resposta a seguir retorna as informações de credenciais para sua zona de aterrissagem, incluindo seus `SASToken` e `SASUri` atuais, bem como os `storageAccountName` que correspondem ao contêiner da zona de aterrissagem.

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


## Atualizar credenciais [!DNL Data Landing Zone]

Você pode atualizar seu `SASToken` fazendo uma solicitação de POST ao terminal `/credentials` da API [!DNL Connectors].

**Formato da API**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Cabeçalhos | Descrição |
| --- | --- |
| `user_drop_zone` | O tipo `user_drop_zone` permite que a API diferencie um contêiner de zona de aterrissagem dos outros tipos de contêineres que estão disponíveis para você. |
| `refresh` | A ação `refresh` permite redefinir as credenciais da zona de aterrissagem e gerar automaticamente um novo `SASToken`. |

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

A resposta a seguir retorna valores atualizados para seus `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Explorar a estrutura e o conteúdo do arquivo da zona de aterrissagem

Você pode explorar a estrutura de arquivos e o conteúdo de sua zona de aterrissagem fazendo uma solicitação GET para o terminal `connectionSpecs` da API [!DNL Flow Service].

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

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote a propriedade `path` do arquivo que deseja fazer upload, pois é necessário fornecê-lo na próxima etapa para inspecionar sua estrutura.

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

Uma resposta bem-sucedida retorna a estrutura do arquivo consultado, incluindo nomes de tabela e tipos de dados.

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

## Criar uma conexão de origem

Uma conexão de origem cria e gerencia a conexão com a fonte externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e ID de conexão de origem necessárias para criar um fluxo de dados. Uma instância de conexão de origem é específica de um locatário e da Organização IMS.

Para criar uma conexão de origem, faça uma solicitação de POST ao endpoint `/sourceConnections` da API [!DNL Flow Service].


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
| `name` | O nome da conexão de origem [!DNL Data Landing Zone]. |
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

Ao seguir este tutorial, você recuperou suas credenciais [!DNL Data Landing Zone], explorou sua estrutura de arquivos para localizar o arquivo que deseja trazer para a Plataforma e criou uma conexão de origem para começar a trazer seus dados para a Plataforma. Agora é possível prosseguir para o próximo tutorial, onde você aprenderá a [criar um fluxo de dados para trazer dados de armazenamento de nuvem para a plataforma usando a [!DNL Flow Service] API](../../collect/cloud-storage.md).
