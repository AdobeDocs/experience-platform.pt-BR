---
description: Esta página exemplifica a chamada à API usada para recuperar um modelo de público-alvo por meio do Adobe Experience Platform Destination SDK.
title: Recuperar um modelo de público-alvo
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 2%

---


# Recuperar um modelo de público-alvo

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página exemplifica a solicitação de API e a carga que você pode usar para recuperar um modelo de metadados de público-alvo usando o `/authoring/audience-templates` Endpoint da API.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio desse endpoint, consulte [gerenciamento de metadados de público](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do modelo de público-alvo {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Recuperar um modelo de público-alvo {#retrieve}

É possível recuperar um template de público-alvo fazendo um `GET` solicitação à `/authoring/audience-templates` terminal.

**Formato da API**

Use o formato de API a seguir para recuperar todos os modelos de público-alvo da sua conta.

```http
GET /authoring/audience-templates
```

Use o formato de API a seguir para recuperar um template de público-alvo específico, definido pelo `{INSTANCE_ID}` parâmetro.

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

As duas solicitações a seguir recuperam todos os modelos de público-alvo para sua Organização IMS ou um modelo de público-alvo específico, dependendo se você passa a variável `INSTANCE_ID` parâmetro na solicitação.

Selecione cada guia abaixo para visualizar o conteúdo correspondente.

>[!BEGINTABS]

>[!TAB Recuperar todos os modelos de público]

A solicitação a seguir recuperará a lista de modelos de público-alvo aos quais você tem acesso com base [!DNL IMS Org ID] e a configuração da sandbox.

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de templates de público-alvo aos quais você tem acesso, com base na variável [!DNL IMS Org ID] e o nome da sandbox que você usou. Um `instanceId` corresponde a um template de público.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

+++

>[!TAB Recuperar um modelo de público-alvo específico]

A solicitação a seguir recuperará a lista de modelos de público-alvo aos quais você tem acesso com base [!DNL IMS Org ID] e a configuração da sandbox.

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID do modelo de público-alvo que você deseja recuperar. |

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes do modelo de público-alvo correspondentes à variável `{INSTANCE_ID}` fornecido na chamada.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

+++

>[!ENDTABS]

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como recuperar detalhes sobre a configuração do servidor de destino usando o `/authoring/destination-servers` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.