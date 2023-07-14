---
description: Use modelos de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo no destino de forma programática. O Adobe fornece um modelo extensível de metadados de público-alvo, que pode ser configurado com base nas especificações da API de marketing. Depois de definir, testar e enviar o modelo, ele será usado pelo Adobe para estruturar as chamadas de API para o seu destino.
title: Gerenciamento de metadados de público
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---


# Gerenciamento de metadados de público

Use modelos de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo no destino de forma programática. O Adobe fornece um modelo extensível de metadados de público-alvo, que pode ser configurado com base nas especificações da API de marketing. Depois de definir, testar e enviar a configuração, ela será usada pelo Adobe para estruturar as chamadas de API para o seu destino.

Você pode configurar a funcionalidade descrita neste documento usando o `/authoring/audience-templates` Endpoint da API. Ler [criar um modelo de metadados](../metadata-api/create-audience-template.md) para obter uma lista completa de operações que podem ser executadas no endpoint.

## Quando usar o endpoint de gerenciamento de metadados de público-alvo {#when-to-use}

Dependendo da configuração da API, pode ser ou não necessário usar o endpoint de gerenciamento de metadados de público-alvo ao configurar o destino no Experience Platform. Use o diagrama de árvore decisória abaixo para entender quando usar o endpoint de metadados de público-alvo e como configurar um template de metadados de público-alvo para seu destino.

![Diagrama de árvore de decisão](../assets/functionality/audience-metadata-decision-tree.png)

## Casos de uso compatíveis com o gerenciamento de metadados de público-alvo {#use-cases}

Com o suporte aos metadados de público no Destination SDK, ao configurar o destino do Experience Platform, você pode fornecer aos usuários da Platform uma das várias opções quando eles mapeiam e ativam públicos para o seu destino. É possível controlar as opções disponíveis para o usuário por meio dos parâmetros em [Configuração de metadados de público](../functionality/destination-configuration/audience-metadata-configuration.md) seção da configuração de destino.

### Caso de uso 1 - Você tem uma API de terceiros e os usuários não precisam inserir IDs de mapeamento

Se você tiver um terminal de API para criar/atualizar/excluir públicos ou públicos, poderá usar modelos de metadados de público para configurar o Destination SDK para corresponder às especificações do terminal de criação/atualização/exclusão de público. O Experience Platform pode criar/atualizar/excluir públicos de maneira programática e sincronizar metadados de volta ao Experience Platform.

Ao ativar públicos-alvo para o seu destino na interface do usuário (UI) do Experience Platform, os usuários não precisam preencher manualmente um campo de ID de mapeamento de público-alvo no fluxo de trabalho de ativação.

### Caso de uso 2 - Os usuários precisam criar um público-alvo em seu destino primeiro e são solicitados a inserir manualmente a ID do mapeamento

Se os públicos-alvo e outros metadados precisarem ser criados manualmente por parceiros ou usuários no destino, os usuários deverão preencher manualmente o campo de ID de mapeamento de público-alvo no fluxo de trabalho de ativação para sincronizar os metadados do público-alvo entre o destino e o Experience Platform.

![ID do mapeamento de entrada](../assets/functionality/input-mapping-id.png)

### Caso de uso 3: seu destino aceita a ID de público-alvo do Experience Platform, os usuários não precisam inserir a ID de mapeamento manualmente

Se o sistema de destino aceitar a ID de público-alvo do Experience Platform, você poderá configurá-la no modelo de metadados de público-alvo. Os usuários não precisam preencher uma ID de mapeamento de público-alvo ao ativar um segmento.

## Modelo de público-alvo genérico e extensível {#generic-and-extensible}

Para dar suporte aos casos de uso listados acima, o Adobe fornece um modelo genérico que pode ser personalizado para ajustar-se às especificações da API.

É possível usar o modelo genérico para [criar um novo modelo de público](../metadata-api/create-audience-template.md) se sua API suportar:

* Os métodos HTTP: POST, GET, PUT, DELETE, PATCH
* Os tipos de autenticação: OAuth 1, OAuth 2 com token de atualização, OAuth 2 com token de portador
* As funções: criar um público, atualizar um público, obter um público, excluir um público, validar credenciais

A equipe de engenharia do Adobe pode trabalhar com você para expandir o modelo genérico com campos personalizados, se os casos de uso exigirem.

## Exemplos de configuração {#configuration-examples}

Esta seção inclui três exemplos de configurações genéricas de metadados de público-alvo, para sua referência, juntamente com descrições das seções principais da configuração. Observe como o url, os cabeçalhos, a solicitação e o corpo da resposta diferem entre as três configurações de exemplo. Isso se deve às diferentes especificações da API de marketing das três plataformas de amostra.

Observe que em alguns exemplos, campos de macro como `{{authData.accessToken}}` ou `{{segment.name}}` são usados no URL e em outros exemplos são usados nos cabeçalhos ou no corpo da solicitação. Isso realmente depende das especificações da sua API de marketing.

| Seção Modelo | Descrição |
|--- |--- |
| `create` | Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, corpo da solicitação e resposta) para fazer uma chamada HTTP para a API, criar segmentos/públicos-alvo de forma programática na plataforma e sincronizar as informações de volta para o Adobe Experience Platform. |
| `update` | Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, corpo da solicitação e resposta) para fazer uma chamada HTTP para a sua API, atualizar programaticamente segmentos/públicos-alvo na sua plataforma e sincronizar as informações de volta para o Adobe Experience Platform. |
| `delete` | Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, corpo da solicitação e resposta) para fazer uma chamada HTTP na API e excluir segmentos/públicos de forma programática na plataforma. |
| `validate` | Executa validações para qualquer campo na configuração do modelo antes de chamar a API do parceiro. Por exemplo, você pode validar se a ID da conta do usuário foi inserida corretamente. |
| `notify` | Aplica-se somente a destinos baseados em arquivo. Inclui todos os componentes necessários (URL, método HTTP, cabeçalhos, corpo da solicitação e resposta) para fazer uma chamada HTTP para sua API e notificá-lo de exportações de arquivos bem-sucedidas. |

{style="table-layout:auto"}

### Exemplo 1 de streaming {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

### Exemplo 2 de streaming {#example-2}

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

### Exemplo 3 de streaming {#example-3}

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


### Exemplo baseado em arquivo {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

Encontre descrições de todos os parâmetros no modelo na [Criar um modelo de público-alvo](../metadata-api/create-audience-template.md) Referência da API.

## Macros usadas em modelos de metadados de público

Para transmitir informações como IDs de público-alvo, tokens de acesso, mensagens de erro e muito mais entre o Experience Platform e a API, os modelos de público-alvo incluem macros que você pode usar. Leia abaixo uma descrição das macros usadas nos três exemplos de configuração desta página:

| Macro | Descrição |
|--- |--- |
| `{{segment.alias}}` | Permite acessar o alias de público-alvo no Experience Platform. |
| `{{segment.name}}` | Permite acessar o nome do público-alvo no Experience Platform. |
| `{{segment.id}}` | Permite acessar a ID de público-alvo no Experience Platform. |
| `{{customerData.accountId}}` | Permite acessar o campo de ID da conta que você configurou na configuração de destino. |
| `{{oauth2ServiceAccessToken}}` | Permite gerar dinamicamente um token de acesso com base na configuração do OAuth 2. |
| `{{authData.accessToken}}` | Permite passar o token de acesso para o endpoint da API. Uso `{{authData.accessToken}}` se o Experience Platform deve usar tokens sem expiração para se conectar ao seu destino, caso contrário, use `{{oauth2ServiceAccessToken}}` para gerar um token de acesso. |
| `{{body.segments[0].segment.id}}` | Retorna o identificador exclusivo do público-alvo criado, como o valor da chave `externalAudienceId`. |
| `{{error.message}}` | Retorna uma mensagem de erro que será exibida aos usuários na interface do usuário do Experience Platform. |

{style="table-layout:auto"}
