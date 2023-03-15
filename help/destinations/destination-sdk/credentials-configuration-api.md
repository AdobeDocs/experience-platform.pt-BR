---
description: Esta página descreve todas as operações de API que você pode executar usando o endpoint da API `/authoring/credentials`.
title: Operações de API do endpoint de credenciais
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# Operações de API do endpoint de credenciais {#credentials}

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/credentials` Endpoint da API.

Para obter uma descrição da funcionalidade compatível com esse endpoint, leia:

* [Configuração de destino de transmissão](destination-configuration.md) para a funcionalidade que você pode configurar para destinos de transmissão.
* [Configuração de destino baseada em arquivo](file-based-destination-configuration.md) para a funcionalidade que você pode configurar para destinos baseados em arquivo.

## Quando usar a variável `/credentials` Endpoint da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você *não* necessidade de usar o `/credentials` Endpoint da API. Em vez disso, você poderá configurar as informações de autenticação para seu destino por meio da `customerAuthenticationConfigurations` parâmetros do `/destinations` terminal. Ler [Configuração de autenticação](./authentication-configuration.md#when-to-use) para obter mais informações.

Use este endpoint de API e selecione `PLATFORM_AUTHENTICATION` no [configuração de destino](./destination-configuration.md#destination-delivery) se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o `/credentials` Endpoint da API.

## Introdução às operações de API de configuração de credenciais {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Criar uma configuração de credenciais {#create}

Você pode criar uma nova configuração de credenciais fazendo uma solicitação POST para o `/authoring/credentials` terminal.

**Formato da API**

```http
POST /authoring/credentials
```

**Solicitação**

A solicitação a seguir cria uma nova configuração de credenciais, configurada pelos parâmetros fornecidos na carga. A carga abaixo inclui todos os parâmetros aceitos pelo `/authoring/credentials` terminal. Observe que não é necessário adicionar todos os parâmetros na chamada e que o modelo é personalizável, de acordo com os requisitos da API.

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
| `username` | String | Nome de usuário para logon na configuração de credenciais |
| `password` | String | Senha de logon da configuração de credenciais |
| `url` | String | URL do provedor de autorização |
| `clientId` | String | ID do cliente da credencial do cliente/aplicativo |
| `clientSecret` | String | Segredo do cliente da credencial Cliente/Aplicativo |
| `accessToken` | String | Token de acesso fornecido pelo provedor de autorização |
| `expiration` | String | A vida útil do token de acesso |
| `refreshToken` | String | Token de atualização fornecido pelo provedor de autorização |
| `header` | String | Qualquer cabeçalho necessário para autorização |
| `accessId` | String | ID de acesso do Amazon S3 |
| `secretKey` | String | Chave secreta do Amazon S3 |
| `sshKey` | String | Chave SSH para SFTP com autenticação SSH |
| `tenant` | String | Locatário do Armazenamento Azure Data Lake |
| `servicePrincipalId` | String | ID da Entidade de Serviço do Azure para Armazenamento do Azure Data Lake |
| `servicePrincipalKey` | String | Chave da Entidade de Serviço do Azure para Armazenamento do Azure Data Lake |
| `connectionString` | String | Cadeia de conexão do Armazenamento Azure Blob |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

## Listar configurações de credenciais {#retrieve-list}

Você pode recuperar uma lista de todas as configurações de credenciais para sua Organização IMS fazendo uma solicitação GET para o `/authoring/credentials` terminal.

**Formato da API**


```http
GET /authoring/credentials
```

**Solicitação**

A solicitação a seguir recuperará a lista de configurações de credenciais às quais você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de configurações de credenciais às quais você tem acesso, com base na ID da organização IMS e no nome da sandbox usados. Um `instanceId` corresponde ao modelo de uma configuração de credenciais. A resposta é truncada por brevidade.

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

Você pode atualizar uma configuração de credenciais existente fazendo uma solicitação PUT para o `/authoring/credentials` e fornecendo a ID da instância da configuração de credenciais que você deseja atualizar. No corpo da chamada, forneça a configuração de credenciais atualizadas.

**Formato da API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de credenciais que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza uma configuração de credenciais existente, configurada pelos parâmetros fornecidos na carga.

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

Você pode recuperar informações detalhadas sobre uma configuração de credenciais específica fazendo uma solicitação do GET para o `/authoring/credentials` e fornecendo a ID da instância da configuração de credenciais que você deseja atualizar.

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

Você pode excluir a configuração de credenciais especificadas fazendo uma solicitação DELETE para a `/authoring/credentials` e fornecendo a ID da configuração de credenciais que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | A variável `id` da configuração de credenciais que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta HTTP vazia.

## Manipulação de erros de API

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe quando usar o endpoint de credenciais e como definir uma configuração de credenciais usando o `/authoring/credentials` Endpoint da API ou o `/authoring/destinations` terminal. Ler [como usar o Destination SDK para configurar seu destino](./configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
