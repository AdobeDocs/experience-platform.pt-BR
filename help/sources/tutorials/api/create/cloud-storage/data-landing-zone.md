---
title: Conectar a zona de aterrissagem de dados à Adobe Experience Platform usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform à Data Landing Zone usando a API do serviço de fluxo.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 4%

---

# Conectar [!DNL Data Landing Zone] ao Adobe Experience Platform usando a API do Serviço de Fluxo

>[!IMPORTANT]
>
>Esta página é específica para o conector de [!DNL Data Landing Zone] *origem* na Experience Platform. Para obter informações sobre como se conectar ao conector de [!DNL Data Landing Zone] *destino*, consulte a [[!DNL Data Landing Zone] página de documentação de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

O [!DNL Data Landing Zone] é um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Adobe Experience Platform. Os dados são excluídos automaticamente do [!DNL Data Landing Zone] após sete dias.

Este tutorial o guiará pelas etapas sobre como criar uma conexão de origem [!DNL Data Landing Zone] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Este tutorial também fornece instruções sobre como recuperar o [!DNL Data Landing Zone], bem como visualizar e atualizar suas credenciais.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Este tutorial também requer que você leia o guia sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md) para saber como autenticar em APIs do Experience Platform e interpretar as chamadas de exemplo fornecidas na documentação.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito uma conexão de origem do [!DNL Data Landing Zone] usando a API [!DNL Flow Service].

## Recuperar uma zona de destino utilizável

>[!IMPORTANT]
>
>Você deve ter a permissão de controle de acesso **[!UICONTROL Manage Sources]** para usar as APIs [!DNL Data Landing Zone] e recuperar `type=user_drop_zone`. Para obter mais informações, leia a [visão geral do controle de acesso](../../../../../access-control/home.md) ou contate o administrador do produto para obter as permissões necessárias.

A primeira etapa no uso de APIs para acessar o [!DNL Data Landing Zone] é fazer uma solicitação GET para o ponto de extremidade `/landingzone` da API [!DNL Connectors] e, ao mesmo tempo, fornecer `type=user_drop_zone` como parte do cabeçalho da sua solicitação.

**Formato da API**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Cabeçalhos | Descrição |
| --- | --- |
| `user_drop_zone` | O tipo `user_drop_zone` permite que a API diferencie um contêiner de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |

**Solicitação**

A solicitação a seguir recupera uma zona de aterrissagem existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Resposta**

Dependendo do seu provedor, uma solicitação bem-sucedida retorna o seguinte:

>[!BEGINTABS]

>[!TAB Resposta no Azure]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome da zona de aterrissagem recuperada. |
| `containerTTL` | O tempo de expiração (em dias) aplicado aos seus dados na zona de aterrissagem. Qualquer item em uma determinada zona de aterrissagem é excluído após sete dias. |


>[!TAB Resposta no AWS]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## Recuperar credenciais de [!DNL Data Landing Zone]

Para recuperar credenciais para [!DNL Data Landing Zone], faça uma solicitação GET para o ponto de extremidade `/credentials` da API [!DNL Connectors].

**Formato da API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Solicitação**

O exemplo de solicitação a seguir recupera credenciais para uma zona de aterrissagem existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

Dependendo do seu provedor, uma solicitação bem-sucedida retorna o seguinte:

>[!BEGINTABS]

>[!TAB Resposta no Azure]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome de seu [!DNL Data Landing Zone]. |
| `SASToken` | O token de assinatura de acesso compartilhado para o seu [!DNL Data Landing Zone]. Esta cadeia de caracteres contém todas as informações necessárias para autorizar uma solicitação. |
| `storageAccountName` | O nome da sua conta de armazenamento. |
| `SASUri` | O URI de assinatura de acesso compartilhado para o seu [!DNL Data Landing Zone]. Esta cadeia de caracteres é uma combinação do URI para o [!DNL Data Landing Zone] para o qual você está sendo autenticado e seu token SAS correspondente. |
| `expiryDate` | A data em que o token SAS expirará. Você deve atualizar seu token antes da data de expiração para continuar usando-o em seu aplicativo para carregar dados para o [!DNL Data Landing Zone]. Se você não atualizar manualmente o token antes da data de expiração declarada, ele será atualizado automaticamente e fornecerá um novo token quando a chamada de credenciais do GET for executada. |

>[!TAB Resposta no AWS]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| Propriedade | Descrição |
| --- | --- |
| `credentials.clientId` | A ID do cliente do seu [!DNL Data Landing Zone] no AWS. |
| `credentials.awsAccessKeyId` | A ID da chave de acesso do [!DNL Data Landing Zone] no AWS. |
| `credentials.awsSecretAccessKey` | A chave de acesso secreta de seu [!DNL Data Landing Zone] no AWS. |
| `credentials.awsSessionToken` | Seu token de sessão do AWS. |
| `dlzPath.bucketName` | O nome do seu bucket do AWS. |
| `dlzPath.dlzFolder` | A pasta [!DNL Data Landing Zone] que você está acessando. |
| `dlzProvider` | O provedor [!DNL Data Landing Zone] que você está usando. Para o Amazon, será [!DNL Amazon S3]. |
| `expiryTime` | A hora de expiração em unix time. |

>[!ENDTABS]

### Recuperar os campos obrigatórios usando APIs

Após gerar o token, é possível recuperar os campos obrigatórios programaticamente usando os exemplos de solicitação abaixo:

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## Atualizar credenciais de [!DNL Data Landing Zone]

Você pode atualizar seu `SASToken` fazendo uma solicitação POST para o ponto de extremidade `/credentials` da API [!DNL Connectors].

**Formato da API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Cabeçalhos | Descrição |
| --- | --- |
| `user_drop_zone` | O tipo `user_drop_zone` permite que a API diferencie um contêiner de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |
| `refresh` | A ação `refresh` permite redefinir suas credenciais de zona de aterrissagem e gerar automaticamente um novo `SASToken`. |

**Solicitação**

A solicitação a seguir atualiza suas credenciais de zona de aterrissagem.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

A resposta a seguir retorna valores atualizados para o(a) `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Explorar a estrutura e o conteúdo do arquivo de zona de aterrissagem

Você pode explorar a estrutura de arquivos e o conteúdo da sua zona de destino fazendo uma solicitação GET para o ponto de extremidade `connectionSpecs` da API [!DNL Flow Service].

**Formato da API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | A ID da especificação de conexão que corresponde a [!DNL Data Landing Zone]. Esta ID fixa é: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote a propriedade `path` do arquivo que deseja carregar, pois você deverá fornecê-la na próxima etapa para inspecionar sua estrutura.

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

## Visualizar estrutura e conteúdo do arquivo de zona de aterrissagem

Para inspecionar a estrutura de um arquivo na zona de destino, execute uma solicitação GET enquanto fornece o caminho e o tipo do arquivo como um parâmetro de consulta.

**Formato da API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | A ID da especificação de conexão que corresponde a [!DNL Data Landing Zone]. Esta ID fixa é: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |  |
| `{OBJECT_TYPE}` | O tipo do objeto que você deseja acessar. | `file` |
| `{OBJECT}` | O caminho e o nome do objeto que você deseja acessar. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | O tipo do arquivo. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Um valor booleano que define se a visualização do arquivo é suportada. | </ul><li>`true`</li><li>`false`</li></ul> |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

### Use `determineProperties` para detectar automaticamente informações de propriedade de arquivo de um [!DNL Data Landing Zone]

Você pode usar o parâmetro `determineProperties` para detectar automaticamente informações de propriedade do conteúdo do arquivo de seu [!DNL Data Landing Zone] ao fazer uma chamada do GET para explorar o conteúdo e a estrutura de sua origem.

#### `determineProperties` casos de uso

A tabela a seguir descreve os diferentes cenários que você pode encontrar ao usar o parâmetro de consulta `determineProperties` ou ao fornecer informações manualmente sobre o arquivo.

| `determineProperties` | `queryParams` | Resposta |
| --- | --- | --- |
| Verdadeiro | N/D | Se `determineProperties` for fornecido como um parâmetro de consulta, ocorrerá a detecção das propriedades do arquivo e a resposta retornará uma nova chave `properties` que inclui informações sobre tipo de arquivo, tipo de compactação e delimitador de coluna. |
| N/D | Verdadeiro | Se os valores para tipo de arquivo, tipo de compactação e delimitador de coluna forem fornecidos manualmente como parte de `queryParams`, eles serão usados para gerar o esquema e as mesmas propriedades serão retornadas como parte da resposta. |
| Verdadeiro | Verdadeiro | Se ambas as opções forem executadas simultaneamente, um erro será retornado. |
| N/D | N/D | Se nenhuma das duas opções for fornecida, um erro será retornado, pois não há como obter propriedades para a resposta. |

**Formato da API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `determineProperties` | Esse parâmetro de consulta permite que a API [!DNL Flow Service] detecte informações relacionadas às propriedades do arquivo, incluindo informações sobre o tipo de arquivo, o tipo de compactação e o delimitador de coluna. | `true` |

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura do arquivo consultado, incluindo nomes de arquivos e tipos de dados, bem como uma chave `properties`, contendo informações sobre `fileType`, `compressionType` e `columnDelimiter`.

+++Clique em mim

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
| `properties.fileType` | O tipo de arquivo correspondente do arquivo consultado. Os tipos de arquivos suportados são: `delimited`, `json` e `parquet`. |
| `properties.compressionType` | O tipo de compactação correspondente usado para o arquivo consultado. Os tipos de compactação compatíveis são: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | O delimitador de coluna correspondente usado para o arquivo consultado. Qualquer valor de caractere único é um delimitador de coluna permitido. O valor padrão é uma vírgula `(,)`. |


## Criar uma conexão de origem

Uma conexão de origem cria e gerencia a conexão com a origem externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e a ID da conexão de origem necessária para criar um fluxo de dados. Uma instância de conexão de origem é específica para um locatário e uma organização.

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service].


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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | O nome da sua conexão de origem [!DNL Data Landing Zone]. |
| `data.format` | O formato dos dados que você deseja trazer para o Experience Platform. |
| `params.path` | O caminho para o arquivo que você deseja trazer para o Experience Platform. |
| `connectionSpec.id` | A ID da especificação de conexão que corresponde a [!DNL Data Landing Zone]. Esta ID fixa é: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária no próximo tutorial para criar um fluxo de dados.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Próximas etapas

Seguindo este tutorial, você recuperou as credenciais do [!DNL Data Landing Zone], explorou a estrutura do arquivo para encontrar o arquivo que deseja trazer para a Experience Platform e criou uma conexão de origem para começar a trazer seus dados para a Experience Platform. Agora você pode prosseguir para o próximo tutorial, onde aprenderá a [criar um fluxo de dados para trazer dados de armazenamento na nuvem para a Experience Platform usando a [!DNL Flow Service] API](../../collect/cloud-storage.md).
