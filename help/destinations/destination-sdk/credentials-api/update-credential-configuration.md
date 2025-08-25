---
description: Esta página exemplifica a chamada à API usada para atualizar uma configuração de credencial existente por meio do Adobe Experience Platform Destination SDK.
title: Atualizar uma configuração de credencial
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 7%

---

# Atualizar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação de API e a carga que você pode usar para atualizar uma configuração de credencial existente, usando o ponto de extremidade de API `/authoring/credentials`.

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
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de credenciais {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Atualizar uma configuração de credencial {#update}

Você pode atualizar uma configuração de credencial [existente](create-credential-configuration.md) fazendo uma solicitação `PUT` para o ponto de extremidade `/authoring/credentials` com a carga atualizada.

Para obter uma configuração de credencial existente e sua `{INSTANCE_ID}` correspondente, consulte o artigo sobre [recuperação de uma configuração de credencial](retrieve-credential-configuration.md).

**Formato da API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de credencial que você deseja atualizar. Para obter uma configuração de credencial existente e sua `{INSTANCE_ID}` correspondente, consulte [Recuperar uma configuração de credencial](retrieve-credential-configuration.md). |

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

**Atualizar uma configuração de credencial [!DNL Amazon S3]**

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
| `accessId` | String | ID de acesso [!DNL Amazon S3] |
| `secretKey` | String | [!DNL Amazon S3] chave secreta |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB SSH]

**Atualizar uma configuração de credencial [!DNL SSH]**

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
| `sshKey` | String | Chave [!DNL SSH] para [!DNL SFTP] com autenticação [!DNL SSH] |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB Armazenamento do Azure Data Lake]

**Atualizar uma configuração de credencial [!DNL Azure Data Lake Storage]**

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
| `servicePrincipalKey` | String | [!DNL Azure Service Principal Key] para [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial atualizada.

+++

>[!TAB Armazenamento Azure Blob]

**Atualizar uma configuração de credencial [!DNL Azure Blob]**

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

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como atualizar uma configuração de credencial usando o ponto de extremidade da API `/authoring/credentials`. Leia [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
