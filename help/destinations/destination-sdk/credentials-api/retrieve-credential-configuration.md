---
description: Esta página exemplifica a chamada à API usada para recuperar uma configuração de credencial por meio do Adobe Experience Platform Destination SDK.
title: Recuperar uma configuração de credencial
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---

# Recuperar uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação de API e a carga que você pode usar para recuperar uma configuração de credencial usando o `/authoring/credentials` Endpoint da API.

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

## Recuperar uma configuração de credencial {#retrieve}

Você pode recuperar um [existente](create-credential-configuration.md) configuração de credencial fazendo um `GET` solicitação à `/authoring/credentials` terminal.

**Formato da API**

Use o formato de API a seguir para recuperar todas as configurações de credencial da sua conta.

```http
GET /authoring/credentials
```

Use o formato de API a seguir para recuperar uma configuração de credencial específica, definida pelo `{INSTANCE_ID}` parâmetro.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

As duas solicitações a seguir recuperam todas as configurações de credenciais para sua Organização IMS ou uma configuração de credencial específica, dependendo se você passa a `INSTANCE_ID` parâmetro na solicitação.

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

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de configurações de credencial às quais você tem acesso, com base no [!DNL IMS Org ID] e o nome da sandbox que você usou. Um `instanceId` corresponde a uma configuração de credencial.

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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de credencial correspondentes ao `instanceId` informações fornecidas no pedido.

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

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como recuperar detalhes sobre as configurações de credencial usando o `/authoring/credentials` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
