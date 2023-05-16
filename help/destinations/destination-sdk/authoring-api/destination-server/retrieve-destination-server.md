---
description: Esta página exemplifica a chamada da API usada para recuperar uma configuração de servidor de destino por meio do Adobe Experience Platform Destination SDK.
title: Recuperar uma configuração do servidor de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---


# Recuperar uma configuração do servidor de destino

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para recuperar informações sobre uma configuração de servidor de destino existente usando o `/authoring/destination-servers` Ponto de extremidade da API.

Para obter uma descrição detalhada dos recursos usados pelos servidores de destino, leia os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Especificações de modelo para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato de mensagem](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuração de formatação de arquivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do servidor de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Recuperar uma configuração do servidor de destino {#retrieve}

Você pode recuperar uma configuração de servidor de destino existente fazendo uma `GET` à `/authoring/destination-servers` endpoint .

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato da API**

Use o seguinte formato de API para recuperar todas as configurações do servidor de destino para sua conta.

```http
GET /authoring/destination-servers
```

Use o seguinte formato de API para recuperar uma configuração específica do servidor de destino, definida pela variável `{INSTANCE_ID}` parâmetro.

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

As duas solicitações a seguir recuperam todas as configurações do servidor de destino para sua Organização IMS ou uma configuração específica do servidor de destino, dependendo se você passa a variável `INSTANCE_ID` na solicitação.

Selecione cada guia abaixo para exibir a carga correspondente e suas respostas.

>[!BEGINTABS]

>[!TAB Recuperar todas as configurações do servidor de destino]

A solicitação a seguir recuperará a lista de configurações do servidor de destino às quais você tem acesso, com base em [!DNL IMS Org ID] e configuração de sandbox.

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de configurações do servidor de destino às quais você tem acesso, com base no [!DNL IMS Org ID] e o nome da sandbox que você usou. One `instanceId` corresponde a um servidor de destino. A resposta de exemplo abaixo inclui duas configurações de servidor de destino.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
```

+++

>[!TAB Recuperar uma configuração específica do servidor de destino]

A solicitação a seguir recuperará configurações específicas do servidor de destino definidas pelo `{INSTANCE_ID}` parâmetro.

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração do servidor de destino que você deseja recuperar. |

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com a configuração do servidor de destino correspondente ao `{INSTANCE_ID}` você forneceu.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
```

+++

>[!ENDTABS]

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como recuperar uma configuração de servidor de destino por meio do Destination SDK `/authoring/destination-servers` Ponto de extremidade da API.

Para saber mais sobre o que você pode fazer com esse terminal, consulte os seguintes artigos:

* [Criar uma configuração de servidor de destino](create-destination-server.md)
* [Atualizar uma configuração de servidor de destino](update-destination-server.md)
* [Excluir uma configuração de servidor de destino](delete-destination-server.md)