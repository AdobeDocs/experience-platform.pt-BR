---
description: Esta página exemplifica a chamada à API usada para atualizar um modelo de público-alvo por meio do Adobe Experience Platform Destination SDK.
title: Atualizar um modelo de público
exl-id: 8185a015-256d-46a7-af33-8475832fb6c1
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 3%

---

# Atualizar um modelo de público

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página exemplifica a solicitação de API e a carga que você pode usar para atualizar um modelo de público-alvo usando o `/authoring/audience-templates` Endpoint da API.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio desse endpoint, consulte [gerenciamento de metadados de público](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do modelo de público-alvo {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Atualizar um modelo de público {#create}

Você pode atualizar um [existente](create-audience-template.md) modelo de público fazendo um `PUT` solicitação à `/authoring/audience-templates` terminal com a carga atualizada.

Para obter um template de público-alvo existente e seu correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperação de um template de público](retrieve-audience-template.md).

**Formato da API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID do modelo de público-alvo que você deseja atualizar. Para obter um template de público-alvo existente e seu correspondente `{INSTANCE_ID}`, consulte [Recuperar um modelo de público-alvo](retrieve-audience-template.md). |

A solicitação a seguir atualiza um modelo existente de metadados de público-alvo, configurado pelos parâmetros fornecidos na carga.

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do seu modelo de público-alvo atualizado.

+++

## Manipulação de erros de API

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe quando usar modelos de público-alvo e como atualizar um modelo de público usando o `/authoring/audience-templates` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
