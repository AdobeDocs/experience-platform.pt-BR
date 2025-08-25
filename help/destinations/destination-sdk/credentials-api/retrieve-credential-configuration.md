---
description: Esta página exemplifica a chamada à API usada para recuperar uma configuração de credencial por meio do Adobe Experience Platform Destination SDK.
title: Recuperar uma configuração de credencial
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 2%

---

# Recuperar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação de API e a carga que você pode usar para recuperar uma configuração de credencial usando o ponto de extremidade de API `/authoring/credentials`.

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

## Recuperar uma configuração de credencial {#retrieve}

Você pode recuperar uma configuração de credencial [existente](create-credential-configuration.md) fazendo uma solicitação `GET` para o ponto de extremidade `/authoring/credentials`.

**Formato da API**

Use o formato de API a seguir para recuperar todas as configurações de credencial da sua conta.

```http
GET /authoring/credentials
```

Use o formato de API a seguir para recuperar uma configuração de credencial específica, definida pelo parâmetro `{INSTANCE_ID}`.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

As duas solicitações a seguir recuperam todas as configurações de credenciais para sua Organização IMS ou uma configuração de credencial específica, dependendo se você passa o parâmetro `INSTANCE_ID` na solicitação.

Selecione cada guia abaixo para visualizar o conteúdo correspondente.

>[!BEGINTABS]

>[!TAB Recuperar todas as configurações de credencial]

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de configurações de credencial às quais você tem acesso, com base no [!DNL IMS Org ID] e no nome da sandbox que você usou. Um `instanceId` corresponde a uma configuração de credencial.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Recuperar uma configuração de credencial específica]

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de credencial que você deseja recuperar. |

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial correspondente ao `instanceId` fornecido na solicitação.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## Manipulação de erros de API {#error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como recuperar detalhes sobre as configurações de credencial usando o ponto de extremidade da API `/authoring/credentials`. Leia [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
