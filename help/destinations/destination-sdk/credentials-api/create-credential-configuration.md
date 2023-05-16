---
description: Esta página exemplifica a chamada da API usada para criar um Adobe Experience Platform Destination SDK de configuração de credencial.
title: Criar uma configuração de credencial
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 8%

---


# Criar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para criar uma configuração de credencial usando o `/authoring/credentials` Ponto de extremidade da API.

## Quando usar a variável `/credentials` Ponto de extremidade da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você ***não*** precisam usar o `/credentials` Ponto de extremidade da API. Em vez disso, você pode configurar as informações de autenticação para o seu destino por meio do `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint .
> 
>Ler [Configuração de autenticação do cliente](../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação suportados.

Use esse ponto de extremidade de API para criar uma configuração de credencial somente se houver um sistema de autenticação global entre o Adobe e a plataforma de destino, e [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar uma configuração de credencial usando o `/credentials` Ponto de extremidade da API.

Ao usar um sistema de autenticação global, você deve definir `"authenticationRule":"PLATFORM_AUTHENTICATION"` no [entrega de destino](../functionality/destination-configuration/destination-delivery.md) configuração, quando [criação de uma nova configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API de credenciais {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar uma configuração de credenciais {#create}

Você pode criar uma nova configuração de credenciais fazendo uma `POST` à `/authoring/credentials` endpoint .

**Formato da API**

```http
POST /authoring/credentials
```

As solicitações a seguir criam novas configurações de credenciais, definidas pelos parâmetros fornecidos no payload.

Selecione cada guia abaixo para visualizar a carga correspondente.

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
| `url` | String | URL do fornecedor de autorização |
| `username` | String | Nome de usuário de logon da configuração de credenciais |
| `password` | String | Senha de logon da configuração de credenciais |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB Amazon S3]

**Crie um [!DNL Amazon S3] configuração de credencial**

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
| `accessId` | String | [!DNL Amazon S3] ID de acesso |
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
| `username` | String | Nome de usuário de logon da configuração de credenciais |
| `sshKey` | String | Chave SSH para SFTP com autenticação SSH |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB Armazenamento Azure Data Lake]

**Crie um [!DNL Azure Data Lake Storage] configuração de credencial**

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
| `url` | String | URL do fornecedor de autorização |
| `tenant` | String | Alocador do Armazenamento Azure Data Lake |
| `servicePrincipalId` | String | ID Principal do Serviço Azure para o Armazenamento Azure Data Lake |
| `servicePrincipalKey` | String | Chave Principal do Serviço Azure para Armazenamento Azure Data Lake |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!TAB Armazenamento Azure Blob]

**Crie um [!DNL Azure Blob Storage] configuração de credencial**

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
| `connectionString` | String | [!DNL Azure Blob Storage] string de conexão |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de credenciais recém-criadas.

+++

>[!ENDTABS]

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe quando usar o ponto de extremidade de credenciais e como configurar uma configuração de credenciais usando o `/authoring/credentials` Leitura do ponto de extremidade da API [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
