---
description: Use modelos de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo de forma programática no seu destino. O Adobe fornece um modelo de metadados de público-alvo extensível, que pode ser configurado com base nas especificações da sua API de marketing. Após definir, testar e enviar o modelo, ele será usado pelo Adobe para estruturar as chamadas da API para seu destino.
title: Gerenciamento de metadados do público-alvo
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: 397c49284c30c648695a7a186d3f3e76a2675807
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 1%

---

# Gerenciamento de metadados do público-alvo {#audience-metadata-management}

## Visão geral {#overview}

Use modelos de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo de forma programática no seu destino. O Adobe fornece um modelo de metadados de público-alvo extensível, que pode ser configurado com base nas especificações da sua API de marketing. Após definir, testar e enviar a configuração, ela será usada pelo Adobe para estruturar as chamadas da API para seu destino.

Você pode configurar a funcionalidade descrita neste documento usando o ponto de extremidade da API `/authoring/audience-templates`. Leia [Audience metadata endpoint API operations](./audience-metadata-api.md) para obter uma lista completa de operações que você pode executar no endpoint.

## Quando usar o endpoint de gerenciamento de metadados do público-alvo {#when-to-use}

Dependendo da configuração da sua API, talvez seja necessário usar ou não o endpoint de gerenciamento de metadados de público-alvo ao configurar o destino no Experience Platform. Use o diagrama de árvore de decisão abaixo para entender quando usar o endpoint de metadados de público-alvo e como configurar um template de metadados de público-alvo para seu destino.

![Diagrama da árvore de decisão](./assets/audience-metadata-decision-tree.png)

## Casos de uso compatíveis com o gerenciamento de metadados do público-alvo {#use-cases}

Com o suporte a metadados de público-alvo no SDK de destino, ao configurar o destino do Experience Platform, você pode oferecer uma das várias opções aos usuários da plataforma ao mapear e ativar segmentos no seu destino. Você pode controlar as opções disponíveis para o usuário por meio dos parâmetros na seção de mapeamento de segmento da [configuração de destino](./destination-configuration.md#segment-mapping).

### Caso de uso 1 - Você tem uma API de terceiros e os usuários não precisam inserir IDs de mapeamento

Se você tiver um endpoint de API para criar/atualizar/excluir segmentos ou públicos-alvo, poderá usar modelos de metadados de público-alvo para configurar o SDK de destino para corresponder às especificações do endpoint de criação/atualização/exclusão de segmento. O Experience Platform pode criar/atualizar/excluir segmentos de maneira programática e sincronizar os metadados de volta ao Experience Platform.

Ao ativar segmentos no seu destino na interface do usuário do Experience Platform (UI), os usuários não precisam preencher manualmente um campo de ID de mapeamento de segmento no fluxo de trabalho de ativação.

### Caso de uso 2 - Os usuários precisam criar um segmento em seu destino primeiro e precisam inserir manualmente a ID de mapeamento

Se os segmentos e outros metadados precisarem ser criados por parceiros ou usuários manualmente no destino, os usuários deverão preencher manualmente o campo de ID de mapeamento de segmento no fluxo de trabalho de ativação para sincronizar os metadados de segmento entre o destino e o Experience Platform.

![ID de mapeamento de entrada](./assets/input-mapping-id.png)

### Caso de uso 3 - Seu destino aceita a ID de segmento do Experience Platform, os usuários não precisam inserir manualmente a ID de mapeamento

Se o sistema de destino aceitar a ID de segmento do Experience Platform, é possível configurar isso no modelo de metadados do público-alvo. Os usuários não precisam preencher uma ID de mapeamento de segmento ao ativar um segmento.

## Modelo de público-alvo genérico e extensível {#generic-and-extensible}

Para ser compatível com os casos de uso listados acima, o Adobe fornece um modelo genérico que pode ser personalizado para se ajustar às especificações da API.

Você pode usar o modelo genérico para [criar um novo modelo de público-alvo](./audience-metadata-api.md#create) se a API suportar:

* Os métodos HTTP: POST, GET, PUT, DELETE, PATCH
* Os tipos de autenticação: OAuth 1, OAuth 2 com token de atualização, OAuth 2 com token portador
* As funções: criar um público-alvo, atualizar um público-alvo, obter um público-alvo, excluir um público-alvo, validar credenciais

A equipe de engenharia do Adobe pode trabalhar com você para expandir o modelo genérico com campos personalizados, se seus casos de uso exigirem isso.

## Exemplos de configuração {#configuration-examples}

Esta seção inclui três exemplos de configurações genéricas de metadados de público-alvo, para sua referência, juntamente com descrições das seções principais da configuração. Observe como o url, os cabeçalhos, a solicitação e o corpo da resposta diferem entre as três configurações de exemplo. Isso se deve às diferentes especificações da API de marketing das três plataformas de amostra.

Observe que em alguns exemplos, campos de macro como `{{authData.accessToken}}` ou `{{segment.name}}` são usados no URL e em outros exemplos são usados nos cabeçalhos ou no corpo da solicitação. Isso realmente depende de suas especificações da API de marketing.

| Seção Modelo | Descrição |
|--- |--- |
| `create` | Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, solicitação e corpo de resposta) para fazer uma chamada HTTP para sua API, criar segmentos/públicos-alvo de forma programática em sua plataforma e sincronizar as informações de volta ao Adobe Experience Platform. |
| `update` | Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, solicitação e corpo de resposta) para fazer uma chamada HTTP para sua API, para atualizar programaticamente segmentos/públicos na plataforma e sincronizar as informações de volta ao Adobe Experience Platform. |
| `delete` | Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, solicitação e corpo de resposta) para fazer uma chamada HTTP para sua API, para excluir segmentos/públicos-alvo de forma programática em sua plataforma. |
| `validations` | Executa validações para qualquer campo na configuração do modelo antes de chamar a API do parceiro. Por exemplo, você pode validar se a ID da conta do usuário está inserida corretamente. |

{style=&quot;table-layout:auto&quot;}

### Primeiro exemplo {#example-1}

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

### Segundo exemplo {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

### Terceiro exemplo {#example-3}

```json
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
```

Encontre descrições de todos os parâmetros no modelo na documentação de referência [Operações da API do ponto de extremidade de metadados de público-alvo](./audience-metadata-api.md).

## Macros usadas em modelos de metadados de público-alvo

Para transmitir informações como IDs de segmento, tokens de acesso, mensagens de erro e muito mais entre o Experience Platform e sua API, os modelos de público-alvo incluem macros que você pode usar. Leia abaixo uma descrição das macros usadas nos três exemplos de configuração nesta página:

| Macro | Descrição |
|--- |--- |
| `{{segment.alias}}` | Permite acessar o alias do segmento no Experience Platform. |
| `{{segment.name}}` | Permite acessar o nome do segmento no Experience Platform. |
| `{{segment.id}}` | Permite acessar a ID do segmento no Experience Platform. |
| `{{customerData.accountId}}` | Permite acessar o campo ID da conta que você configurou na configuração de destino. |
| `{{oauth2ServiceAccessToken}}` | Permite gerar um token de acesso dinamicamente com base na configuração do OAuth 2. |
| `{{authData.accessToken}}` | Permite que você passe o token de acesso para o endpoint da API. Use `{{authData.accessToken}}` se o Experience Platform deve usar tokens que não expiram para se conectar ao seu destino; caso contrário, use `{{oauth2ServiceAccessToken}}` para gerar um token de acesso. |
| `{{body.segments[0].segment.id}}` | Retorna o identificador exclusivo do público-alvo criado, como o valor da chave `externalAudienceId`. |
| `{{error.message}}` | Retorna uma mensagem de erro que será exibida para os usuários na interface do usuário do Experience Platform. |

{style=&quot;table-layout:auto&quot;}
