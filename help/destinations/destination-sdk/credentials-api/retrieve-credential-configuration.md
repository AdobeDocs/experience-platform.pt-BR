---
description: Esta página exemplifica a chamada da API usada para recuperar uma configuração de credencial por meio do Adobe Experience Platform Destination SDK.
title: Recuperar uma configuração de credencial
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---


# Recuperar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para recuperar uma configuração de credencial usando o `/authoring/credentials` Ponto de extremidade da API.

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

## Recuperar uma configuração de credencial {#retrieve}

Você pode recuperar um [existente](create-credential-configuration.md) configuração de credencial ao criar uma `GET` à `/authoring/credentials` endpoint .

**Formato da API**

Use o seguinte formato de API para recuperar todas as configurações de credenciais da sua conta.

```http
GET /authoring/credentials
```

Use o seguinte formato de API para recuperar uma configuração de credencial específica, definida pela variável `{INSTANCE_ID}` parâmetro.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

As duas solicitações a seguir recuperam todas as configurações de credenciais para a Organização IMS ou uma configuração de credencial específica, dependendo se você passa a variável `INSTANCE_ID` na solicitação.

Selecione cada guia abaixo para visualizar a carga correspondente.

>[!BEGINTABS]

>[!TAB Recuperar todas as configurações de credenciais]

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

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de configurações de credenciais às quais você tem acesso, com base no [!DNL IMS Org ID] e o nome da sandbox que você usou. One `instanceId` corresponde a uma configuração de credencial.

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
| `{INSTANCE_ID}` | A ID da configuração da credencial que você deseja recuperar. |

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração da credencial correspondente à variável `instanceId` , desde que solicitado.

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

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como recuperar detalhes sobre suas configurações de credenciais usando o `/authoring/credentials` Ponto de extremidade da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
