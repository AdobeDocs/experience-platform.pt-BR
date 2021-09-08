---
description: Esta página descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/credentials`.
title: Operações da API do endpoint de credenciais
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 5%

---

# Operações da API do endpoint de credenciais {#credentials}

>[!IMPORTANT]
>
>**Ponto de extremidade** da API:  `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página lista e descreve todas as operações de API que podem ser executadas usando o endpoint da API `/authoring/credentials`.

## Quando usar o endpoint da API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, *não* precisa usar o endpoint da API `/credentials`. Em vez disso, você pode configurar as informações de autenticação para seu destino por meio dos parâmetros `customerAuthenticationConfigurations` do endpoint `/destinations`. Leia [Configuração de credenciais](./credentials-configuration.md) para obter mais informações.

Use esse ponto de extremidade de API e selecione `PLATFORM_AUTHENTICATION` na [configuração de destino](./destination-configuration.md#destination-delivery) se houver um sistema de autenticação global entre o Adobe e seu destino e o cliente [!DNL Platform] não precisar fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o ponto de extremidade da API `/credentials`.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Introdução às operações da API de configuração de credenciais {#get-started}

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar uma configuração de credenciais {#create}

Você pode criar uma nova configuração de credenciais fazendo uma solicitação de POST ao endpoint `/authoring/credentials`.

**Formato da API**


```http
POST /authoring/credentials
```

**Solicitação**

A solicitação a seguir cria uma nova configuração de credenciais, configurada pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pelo ponto de extremidade `/authoring/credentials`. Observe que não é necessário adicionar todos os parâmetros na chamada do e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `username` | String | nome de usuário de logon da configuração de credenciais |
| `password` | String | senha de logon da configuração de credenciais |
| `url` | String | URL do fornecedor de autorização |
| `clientId` | String | ID do cliente da credencial do cliente/aplicativo |
| `clientSecret` | String | Segredo do cliente da credencial do cliente/aplicativo |
| `accessToken` | String | Token de acesso fornecido pelo provedor de autorização |
| `expiration` | String | O tempo de vida do token de acesso |
| `refreshToken` | String | Token de atualização fornecido pelo provedor de autorização |
| `header` | String | Qualquer cabeçalho necessário para autorização |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

## Listar configurações de credenciais {#retrieve-list}

Você pode recuperar uma lista de todas as configurações de credenciais para sua Organização IMS fazendo uma solicitação de GET para o endpoint `/authoring/credentials`.

**Formato da API**


```http
GET /authoring/credentials
```

**Solicitação**

A solicitação a seguir recuperará a lista de configurações de credenciais que você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de configurações de credenciais que você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. Um `instanceId` corresponde ao modelo para uma configuração de credenciais. A resposta é truncada por brevidade.

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

Você pode atualizar uma configuração de credenciais existente, fazendo uma solicitação de PUT para o endpoint `/authoring/credentials` e fornecendo a ID da instância da configuração de credenciais que deseja atualizar. No corpo da chamada , forneça a configuração de credenciais atualizada.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Você pode recuperar informações detalhadas sobre uma configuração de credenciais específica fazendo uma solicitação de GET para o endpoint `/authoring/credentials` e fornecendo a ID da instância da configuração de credenciais que deseja atualizar.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Você pode excluir a configuração de credenciais especificada, fazendo uma solicitação de DELETE ao endpoint `/authoring/credentials` e fornecendo a ID da configuração de credenciais que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `id` da configuração de credenciais que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.

## Tratamento de erros da API

Os pontos de extremidade da API do SDK de destino seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [erros do cabeçalho da solicitação](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe quando usar o ponto de extremidade de credenciais e como configurar uma configuração de credenciais usando o ponto de extremidade da API `/authoring/credentials` ou o ponto de extremidade `/authoring/destinations`. Leia [como usar o SDK de destino para configurar seu destino](./configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
