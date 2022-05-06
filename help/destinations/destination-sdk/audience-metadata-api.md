---
description: Esta página descreve todas as operações da API que podem ser executadas usando o endpoint da API `/authoring/audience-templates`.
title: Operações da API de ponto de extremidade de metadados de público-alvo
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 5%

---

# Operações da API de ponto de extremidade de metadados de público-alvo

>[!IMPORTANT]
>
>**Ponto de extremidade da API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/audience-templates` Ponto de extremidade da API. Para obter uma descrição de quando usar este endpoint, leia [gerenciamento de metadados do público-alvo](./audience-metadata-management.md).

## Introdução às operações de API dos templates de público-alvo {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar um novo modelo de público-alvo {#create}

Você pode criar um novo modelo de público-alvo fazendo uma solicitação de POST para o `/authoring/audience-templates` endpoint .

**Formato da API**

```http
POST /authoring/audience-templates
```

**Solicitação**

A solicitação a seguir cria um novo modelo de metadados de público-alvo, configurado pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pela `/authoring/audience-templates` endpoint . Observe que não é necessário adicionar todos os parâmetros na chamada do e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Propriedade | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `name` | String | O nome do modelo de metadados do público-alvo para o seu destino. Esse nome aparecerá em qualquer mensagem de erro específica do parceiro na interface do usuário do Experience Platform, seguido da mensagem de erro analisada em `metadataTemplate.create.errorSchemaMap`. |
| `url` | String | O URL e o terminal da API, usado para criar, atualizar, excluir ou validar públicos/segmentos na plataforma. Dois exemplos do setor são: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | String | O método usado no terminal para criar, atualizar, excluir ou validar programaticamente o segmento/público-alvo no destino. Por exemplo: `POST`, `PUT`, `DELETE` |
| `headers.header` | String | Especifica todos os cabeçalhos HTTP que devem ser adicionados à chamada para sua API. Por exemplo, `"Content-Type"` |
| `headers.value` | String | Especifica o valor dos cabeçalhos HTTP que devem ser adicionados à chamada para sua API. Por exemplo, `"application/x-www-form-urlencoded"` |
| `requestBody` | String | Especifica o conteúdo do corpo da mensagem que deve ser enviado para sua API. Os parâmetros que devem ser adicionados à variável `requestBody` dependem dos campos aceitos pela API. Para obter um exemplo, consulte a [primeiro exemplo de modelo](./audience-metadata-management.md#example-1) no documento de funcionalidade Metadados de público-alvo . |
| `responseFields.name` | String | Especifique quaisquer campos de resposta que sua API retorne quando chamada. Para obter um exemplo, consulte a [exemplos de modelo](./audience-metadata-management.md#examples) no documento de funcionalidade Metadados de público-alvo . |
| `responseFields.value` | String | Especifique o valor de qualquer campo de resposta que sua API retorna quando chamada. |
| `responseErrorFields.name` | String | Especifique quaisquer campos de resposta que sua API retorne quando chamada. Para obter um exemplo, consulte a [ exemplos de modelo](./audience-metadata-management.md#examples) no documento de funcionalidade Metadados de público-alvo . |
| `responseErrorFields.value` | String | Analisa todas as mensagens de erro retornadas nas respostas de chamada da API do seu destino. Essas mensagens de erro serão exibidas para os usuários na interface do usuário do Experience Platform. |
| `validations.field` | String | Indica se as validações devem ser executadas para qualquer campo antes que as chamadas de API sejam feitas ao seu destino. Por exemplo, você pode usar `{{validations.accountId}}` para validar a ID da conta do usuário. |
| `validations.regex` | String | Indica como o campo deve ser estruturado para que a validação seja aprovada. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do modelo de público-alvo recém-criado.

## Atualizar modelo de público-alvo {#update}

Você pode atualizar um modelo de público-alvo existente fazendo uma solicitação de PUT para a variável `/authoring/audience-templates` endpoint e fornecer a ID da instância do modelo de público-alvo que deseja atualizar. No corpo da chamada , forneça o template atualizado.

**Formato da API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID do modelo de metadados do público-alvo que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza um modelo de metadados de público-alvo existente, configurado pelos parâmetros fornecidos no payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
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
}
```

## Recuperar uma lista de modelos de público-alvo {#retrieve-list}

Você pode recuperar uma lista de todos os modelos de público-alvo para sua Organização IMS fazendo uma solicitação ao `/authoring/audience-templates` endpoint .

**Formato da API**


```http
GET /authoring/audience-templates
```

**Solicitação**

A solicitação a seguir recuperará a lista de modelos de público-alvo aos quais você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de modelos de metadados de público-alvo aos quais você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. One `instanceId` corresponde ao modelo para um destino. A resposta é truncada por brevidade.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Recuperar um modelo de público-alvo específico {#get}

Você pode recuperar informações detalhadas sobre um modelo de público-alvo específico fazendo uma solicitação do GET para a `/authoring/audience-templates` endpoint e fornecer a ID da instância do modelo de público-alvo que deseja recuperar.

**Formato da API**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID do modelo de metadados de público-alvo que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o modelo de público-alvo especificado.

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


## Excluir um modelo de público-alvo específico {#delete}

Você pode excluir o modelo de público-alvo especificado, fazendo uma solicitação de DELETE para a variável `/authoring/audience-templates` endpoint e fornecer a ID do modelo de público-alvo que você deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `id` do modelo de público-alvo que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.

## Tratamento de erros da API

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe quando usar modelos de metadados de público-alvo e como configurar um modelo de metadados de público-alvo usando o `/authoring/audience-templates` Ponto de extremidade da API. Ler [como usar o Destination SDK para configurar seu destino](./configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
