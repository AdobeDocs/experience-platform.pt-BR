---
description: Esta página descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/credentials`.
title: Operações da API do endpoint de credenciais
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 6%

---

# Operações da API do endpoint de credenciais {#credentials}

>[!IMPORTANT]
>
>**Ponto de extremidade da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/credentials` Ponto de extremidade da API.

Para obter uma descrição da funcionalidade suportada por este ponto de extremidade, leia:

* [Configuração de destino de transmissão](destination-configuration.md) para a funcionalidade que você pode configurar para destinos de transmissão.
* [Configuração de destino baseada em arquivo](file-based-destination-configuration.md) para a funcionalidade que você pode configurar para destinos com base em arquivo.

## Quando usar a variável `/credentials` Ponto de extremidade da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você *não* precisam usar o `/credentials` Ponto de extremidade da API. Em vez disso, você pode configurar as informações de autenticação para o seu destino por meio do `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint . Ler [Configuração de autenticação](./authentication-configuration.md#when-to-use) para obter mais informações.

Use esse ponto de extremidade de API e selecione `PLATFORM_AUTHENTICATION` no [configuração de destino](./destination-configuration.md#destination-delivery) se houver um sistema de autenticação global entre o Adobe e seu destino e o [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o `/credentials` Ponto de extremidade da API.

## Introdução às operações da API de configuração de credenciais {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar uma configuração de credenciais {#create}

Você pode criar uma nova configuração de credenciais, fazendo uma solicitação de POST para o `/authoring/credentials` endpoint .

**Formato da API**

```http
POST /authoring/credentials
```

**Solicitação**

A solicitação a seguir cria uma nova configuração de credenciais, configurada pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pela `/authoring/credentials` endpoint . Observe que não é necessário adicionar todos os parâmetros na chamada do e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `username` | String | Nome de usuário de logon da configuração de credenciais |
| `password` | String | Senha de logon da configuração de credenciais |
| `url` | String | URL do fornecedor de autorização |
| `clientId` | String | ID do cliente da credencial do cliente/aplicativo |
| `clientSecret` | String | Segredo do cliente da credencial do cliente/aplicativo |
| `accessToken` | String | Token de acesso fornecido pelo provedor de autorização |
| `expiration` | String | O tempo de vida do token de acesso |
| `refreshToken` | String | Token de atualização fornecido pelo provedor de autorização |
| `header` | String | Qualquer cabeçalho necessário para autorização |
| `accessId` | String | ID de acesso do Amazon S3 |
| `secretKey` | String | Chave secreta do Amazon S3 |
| `sshKey` | String | Chave SSH para SFTP com autenticação SSH |
| `tenant` | String | Alocador do Armazenamento Azure Data Lake |
| `servicePrincipalId` | String | ID Principal do Serviço Azure para o Armazenamento Azure Data Lake |
| `servicePrincipalKey` | String | Chave Principal do Serviço Azure para Armazenamento Azure Data Lake |
| `connectionString` | String | Cadeia de conexão do Armazenamento Azure Blob |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

## Listar configurações de credenciais {#retrieve-list}

Você pode recuperar uma lista de todas as configurações de credenciais para sua Organização IMS fazendo uma solicitação de GET para a `/authoring/credentials` endpoint .

**Formato da API**


```http
GET /authoring/credentials
```

**Solicitação**

A solicitação a seguir recuperará a lista de configurações de credenciais que você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de configurações de credenciais que você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. One `instanceId` corresponde ao template para uma configuração de credenciais. A resposta é truncada por brevidade.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Atualizar uma configuração de credenciais existente {#update}

Você pode atualizar uma configuração de credenciais existente, fazendo uma solicitação de PUT para o `/authoring/credentials` endpoint e fornecendo a ID da instância da configuração de credenciais que deseja atualizar. No corpo da chamada , forneça a configuração de credenciais atualizada.

**Formato da API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de credenciais que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza uma configuração de credenciais existente, configurada pelos parâmetros fornecidos no payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## Recuperar uma configuração de credenciais específica {#get}

Você pode recuperar informações detalhadas sobre uma configuração de credenciais específica fazendo uma solicitação do GET para a `/authoring/credentials` endpoint e fornecendo a ID da instância da configuração de credenciais que deseja atualizar.

**Formato da API**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de credenciais que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a configuração de credenciais especificadas.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## Excluir uma configuração de credenciais específica {#delete}

Você pode excluir a configuração de credenciais especificada, fazendo uma solicitação de DELETE para a `/authoring/credentials` endpoint e fornecendo a ID da configuração de credenciais que você deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `id` da configuração de credenciais que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.

## Tratamento de erros da API

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe quando usar o ponto de extremidade de credenciais e como configurar uma configuração de credenciais usando o `/authoring/credentials` Ponto de extremidade da API ou o `/authoring/destinations` endpoint . Ler [como usar o Destination SDK para configurar seu destino](./configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
