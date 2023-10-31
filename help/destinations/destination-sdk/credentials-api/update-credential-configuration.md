---
description: Esta página exemplifica a chamada à API usada para atualizar uma configuração de credencial existente por meio do Adobe Experience Platform Destination SDK.
title: Atualizar uma configuração de credencial
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 8%

---

# Atualizar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação de API e a carga que você pode usar para atualizar uma configuração de credencial existente, usando o `/authoring/credentials` Endpoint da API.

## Quando usar a variável `/credentials` Endpoint da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você ***não*** necessidade de usar o `/credentials` Endpoint da API. Em vez disso, você poderá configurar as informações de autenticação para seu destino por meio da `customerAuthenticationConfigurations` parâmetros do `/destinations` terminal.
> 
>Ler [Configuração de autenticação do cliente](../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação compatíveis.

Use esse endpoint de API para criar uma configuração de credencial somente se houver um sistema de autenticação global entre o Adobe e sua plataforma de destino e o [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar uma configuração de credencial usando o `/credentials` Endpoint da API.

Ao usar um sistema de autenticação global, você deve definir `"authenticationRule":"PLATFORM_AUTHENTICATION"` no [entrega de destino](../functionality/destination-configuration/destination-delivery.md) configuração, quando [criação de uma nova configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de credenciais {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Atualizar uma configuração de credencial {#update}

Você pode atualizar um [existente](create-credential-configuration.md) configuração de credencial fazendo um `PUT` solicitação à `/authoring/credentials` terminal com a carga atualizada.

Para obter uma configuração de credencial existente e sua configuração correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperação de uma configuração de credencial](retrieve-credential-configuration.md).

**Formato da API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de credencial que você deseja atualizar. Para obter uma configuração de credencial existente e sua configuração correspondente `{INSTANCE_ID}`, consulte [Recuperar uma configuração de credencial](retrieve-credential-configuration.md). |

As solicitações a seguir atualizam as configurações de credencial existentes, definidas pelos parâmetros fornecidos na carga.

Selecione cada guia abaixo para visualizar o conteúdo correspondente.

>[!BEGINTABS]

>[!TAB Básico]

**Atualizar uma configuração básica de credencial**

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB Amazon S3]

**Atualizar um [!DNL Amazon S3] configuração de credencial**

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB SSH]

**Atualizar um [!DNL SSH] configuração de credencial**

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `sshKey` | String | [!DNL SSH] chave para [!DNL SFTP] com [!DNL SSH] autenticação |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB Armazenamento Azure Data Lake]

**Atualizar um [!DNL Azure Data Lake Storage] configuração de credencial**

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `servicePrincipalId` | String | [!DNL Azure Service Principal] ID para [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | String | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB Armazenamento Azure Blob]

**Atualizar um [!DNL Azure Blob] configuração de credencial**

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!ENDTABS]

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como atualizar uma configuração de credencial usando o `/authoring/credentials` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
