---
description: Esta página exemplifica a chamada à API usada para criar uma Adobe Experience Platform Destination SDK de configuração de credencial.
title: Criar uma configuração de credencial
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 7%

---

# Criar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação de API e a carga que você pode usar para criar uma configuração de credencial usando o ponto de extremidade de API `/authoring/credentials`.

## Quando usar o ponto de extremidade de API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você ***não*** precisa usar o ponto de extremidade de API `/credentials`. Em vez disso, você pode configurar as informações de autenticação para o seu destino através dos parâmetros `customerAuthenticationConfigurations` do ponto de extremidade `/destinations`.
> 
>Leia a [Configuração de autenticação do cliente](../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação com suporte.

Use este ponto de extremidade de API para criar uma configuração de credencial somente se houver um sistema de autenticação global entre o Adobe e a plataforma de destino, e o cliente do [!DNL Experience Platform] não precisar fornecer credenciais de autenticação para se conectar ao destino. Nesse caso, você deve criar uma configuração de credencial usando o ponto de extremidade da API `/credentials`.

Ao usar um sistema de autenticação global, você deve definir `"authenticationRule":"PLATFORM_AUTHENTICATION"` na configuração de [entrega de destino](../functionality/destination-configuration/destination-delivery.md), ao [criar uma nova configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md). Em seguida, você deve criar uma [configuração de credenciais](../credentials-api/create-credential-configuration.md) e passar a ID do objeto de credencial no parâmetro `authenticationId` na configuração de [entrega de destino](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de credenciais {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Criar uma configuração de credenciais {#create}

Você pode criar uma nova configuração de credenciais fazendo uma solicitação `POST` para o ponto de extremidade `/authoring/credentials`.

**Formato da API**

```http
POST /authoring/credentials
```

As solicitações a seguir criam novas configurações de credencial, definidas pelos parâmetros fornecidos na carga.

Selecione cada guia abaixo para visualizar o conteúdo correspondente.

>[!BEGINTABS]

>[!TAB Básico]

**Criar uma configuração básica de credencial**

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `url` | String | URL do provedor de autorização |
| `username` | String | Nome de usuário para logon na configuração de credenciais |
| `password` | String | Senha de logon da configuração de credenciais |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB Amazon S3]

**Criar uma [!DNL Amazon S3] configuração de credencial**

+++**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `accessId` | String | ID de acesso [!DNL Amazon S3] |
| `secretKey` | String | [!DNL Amazon S3] chave secreta |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB SSH]

**Criar uma configuração de credencial SSH**

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `username` | String | Nome de usuário para logon na configuração de credenciais |
| `sshKey` | String | Chave SSH para SFTP com autenticação SSH |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB Armazenamento do Azure Data Lake]

**Criar uma [!DNL Azure Data Lake Storage] configuração de credencial**

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `url` | String | URL do provedor de autorização |
| `tenant` | String | Locatário do Armazenamento Azure Data Lake |
| `servicePrincipalId` | String | ID da Entidade de Serviço do Azure para Armazenamento do Azure Data Lake |
| `servicePrincipalKey` | String | Chave da Entidade de Serviço do Azure para Armazenamento do Azure Data Lake |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB Armazenamento Azure Blob]

**Criar uma [!DNL Azure Blob Storage] configuração de credencial**

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `connectionString` | String | [!DNL Azure Blob Storage] cadeia de conexão |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!ENDTABS]

## Manipulação de erros de API {#error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe quando usar o ponto de extremidade de credenciais e como definir uma configuração de credenciais usando o ponto de extremidade de API `/authoring/credentials` Leia [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde esta etapa se encaixa no processo de configuração do seu destino.
