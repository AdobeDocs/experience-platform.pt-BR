---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Configurar especificações de origem para fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Fontes de autoatendimento (SDK em lote).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# Configurar especificação de origem para fontes de autoatendimento (SDK em lote)

As especificações de origem contêm informações específicas de uma fonte, incluindo atributos pertencentes à categoria de uma fonte, ao status beta e ao ícone de catálogo. Eles também contêm informações úteis, como parâmetros de URL, conteúdo, cabeçalho e agendamento. As especificações de origem também descrevem o esquema dos parâmetros necessários para criar uma conexão de origem a partir de uma conexão base. O schema é necessário para criar uma conexão de origem.

Consulte a [apêndice](#source-spec) para obter um exemplo de especificação de origem totalmente preenchida.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `sourceSpec.attributes` | Contém informações sobre a fonte específica para a interface do usuário ou a API. |
| `sourceSpec.attributes.uiAttributes` | Exibe informações sobre a fonte específica para a interface do usuário. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Um atributo booleano que indica se a fonte requer mais feedback dos clientes para adicionar a funcionalidade. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Define a categoria da origem. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Define o ícone usado para a renderização da fonte na interface do usuário da plataforma. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Exibe uma breve descrição da origem. |
| `sourceSpec.attributes.uiAttributes.label` | Exibe o rótulo a ser usado para a renderização da origem na interface do usuário da plataforma. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contém informações sobre o caminho do recurso de URL, o método e os parâmetros de consulta compatíveis. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Define o caminho do recurso de onde buscar os dados. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Define o método HTTP a ser usado para fazer a solicitação ao recurso para buscar dados. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Define os parâmetros de consulta compatíveis que podem ser usados para anexar o URL de origem ao fazer uma solicitação para buscar dados. **Observação**: Qualquer valor de parâmetro fornecido pelo usuário deve ser formatado como um espaço reservado. Por exemplo: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` será anexado ao URL de origem como: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Define cabeçalhos que precisam ser fornecidos na solicitação HTTP para o URL de origem ao buscar dados. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Esse atributo pode ser configurado para enviar corpo HTTP por meio de uma solicitação POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Define o nó que contém a lista de itens necessários para ser assimilado na Platform. Esse atributo deve seguir a sintaxe de caminho JSON válida e deve apontar para uma matriz específica. | Visualize o [seção recursos adicionais](#content-path) para obter um exemplo do recurso contido em um caminho de conteúdo. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | O caminho que aponta para os registros da coleção que serão assimilados na Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Essa propriedade permite identificar itens específicos do recurso identificado no caminho do conteúdo que devem ser excluídos da assimilação. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Essa propriedade permite especificar explicitamente os atributos individuais que você deseja manter. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Essa propriedade permite que você substitua o valor do nome do atributo especificado em `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Essa propriedade permite nivelar duas matrizes e transformar dados de recursos no recurso Plataforma . |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | O caminho que aponta para os registros de coleção que você deseja nivelar. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Essa propriedade permite identificar itens específicos do recurso identificado no caminho da entidade que devem ser excluídos da assimilação. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Essa propriedade permite especificar explicitamente os atributos individuais que você deseja manter. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Essa propriedade permite que você substitua o valor do nome do atributo especificado em `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Define os parâmetros ou campos que devem ser fornecidos para obter um link para a próxima página da resposta da página atual do usuário ou ao criar um URL da próxima página. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Exibe o tipo de paginação suportada para a sua origem. | <ul><li>`OFFSET`: Esse tipo de paginação permite analisar os resultados especificando um índice de onde iniciar a matriz resultante e um limite de quantos resultados são retornados.</li><li>`POINTER`: Esse tipo de paginação permite usar um `pointer` para apontar para um item específico que precisa ser enviado com uma solicitação. A paginação do tipo de ponteiro requer um caminho na carga que aponte para a próxima página.</li><li>`CONTINUATION_TOKEN`: Esse tipo de paginação permite anexar seus parâmetros de query ou cabeçalho com um token de continuação para recuperar os dados de retorno restantes da sua origem, que não foram retornados inicialmente devido a um máximo predeterminado.</li><li>`PAGE`: Esse tipo de paginação permite anexar seu parâmetro de consulta com um parâmetro de paginação para navegar pelos dados de retorno por páginas, começando da página zero.</li><li>`NONE`: Esse tipo de paginação pode ser usado para fontes que não oferecem suporte a nenhum dos tipos de paginação disponíveis. Tipo de paginação `NONE` retorna todos os dados de resposta após uma solicitação.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. | `limit` ou `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | O número de registros a serem buscados em uma página. | `limit=10` ou `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | O nome do atributo de deslocamento. Isso é necessário se o tipo de paginação estiver definido como `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | O nome do atributo do ponteiro. Isso requer o caminho json para o atributo que apontará para a próxima página. Isso é necessário se o tipo de paginação estiver definido como `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contém parâmetros que definem formatos de agendamento compatíveis para a sua origem. Os parâmetros de agendamento incluem `startTime` e `endTime`, que permitem definir intervalos de tempo específicos para execuções de lote, o que garante que os registros buscados em uma execução de lote anterior não sejam buscados novamente. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Define o nome do parâmetro de hora de início | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Define o nome do parâmetro de hora de término | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Define o formato compatível para a variável `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Define o formato compatível para a variável `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Define os parâmetros fornecidos pelo usuário para buscar valores de recursos. | Consulte a [recursos adicionais](#user-input) para um exemplo de parâmetros inseridos pelo usuário para `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Recursos adicionais {#appendix}

As seções a seguir fornecem informações sobre configurações adicionais que você pode fazer com o `sourceSpec`, incluindo agendamento avançado e esquemas personalizados.

### Exemplo de caminho de conteúdo {#content-path}

Este é um exemplo do conteúdo da variável `contentPath` em uma [!DNL MailChimp Members] especificação de conexão.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` exemplo de entrada do usuário {#user-input}

Este é um exemplo de um `spec.properties` usando um [!DNL MailChimp Members] especificação de conexão.

Neste exemplo, `listId` é fornecido como parte de `urlParams.path`. Se precisar recuperar `listId` de um cliente, você também deve defini-lo como parte de `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Exemplo de especificação de origem {#source-spec}

Veja a seguir uma especificação de fonte concluída usando [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### Configurar diferentes tipos de paginação para a sua origem {#pagination}

A seguir estão exemplos de outros tipos de paginação suportados por Fontes de Autoatendimento (SDK em lote):

#### `CONTINUATION_TOKEN`

Um tipo de token de continuação da paginação retorna um token de string que significa a existência de mais itens que não puderam ser retornados, devido a um número máximo predeterminado de itens que podem ser retornados em uma única resposta.

Uma fonte que suporta o tipo de token de continuação de paginação pode ter um parâmetro de paginação semelhante a:

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de paginação usado para retornar dados. |
| `continuationTokenPath` | O valor que deve ser anexado aos parâmetros de query para mover para a próxima página dos resultados retornados. |
| `parameterType` | O `parameterType` define onde a variável `parameterName` deve ser adicionado. O `QUERYPARAM` permite anexar sua consulta com a variável `parameterName`. O `HEADERPARAM` permite adicionar `parameterName` à solicitação do cabeçalho. |
| `parameterName` | O nome do parâmetro usado para incorporar o token de continuação. O formato é o seguinte: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | O `delayRequestMillis` na paginação permite controlar a taxa de solicitações feitas na origem. Algumas fontes podem ter um limite para o número de solicitações que podem ser feitas por minuto. Por exemplo, [!DNL Zendesk] tem um limite de 100 solicitações por minuto e define  `delayRequestMillis` para `850` O permite configurar a origem para fazer chamadas em cerca de 80 solicitações por minuto, bem abaixo do limite de 100 solicitações por minuto. |

Este é um exemplo de uma resposta retornada usando o tipo de token de continuação da paginação:

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

O `PAGE` O tipo de paginação permite percorrer os dados de retorno por número de páginas começando em zero. Ao usar `PAGE` do tipo paginação, você deve fornecer o número de registros fornecidos em uma única página.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de paginação usado para retornar dados. |
| `limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. |
| `limitValue` | O número de registros a serem buscados em uma página. |
| `pageParamName` | O nome do parâmetro que deve ser anexado aos parâmetros de consulta para percorrer páginas diferentes dos dados de retorno. Por exemplo, `https://abc.com?pageIndex=1` retornaria a segunda página do payload de retorno da API. |
| `maximumRequest` | O número máximo de solicitações que uma origem pode fazer para uma determinada execução incremental. O limite padrão atual é 10000. |

#### `NONE`

O `NONE` o tipo de paginação pode ser usado para fontes que não oferecem suporte para nenhum dos tipos de paginação disponíveis. Fontes que usam o tipo de paginação de `NONE` simplesmente retorne todos os registros recuperáveis quando uma solicitação do GET for feita.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Programação avançada de fontes de autoatendimento (SDK em lote)

Configure o agendamento incremental e de preenchimento retroativo da origem usando o agendamento avançado. O `incremental` permite configurar um agendamento no qual sua origem assimilará somente registros novos ou modificados, enquanto que a variável `backfill` permite criar um agendamento para assimilar dados históricos.

Com o agendamento avançado, você pode usar expressões e funções específicas para sua origem para configurar agendamentos incrementais e de preenchimento retroativo. No exemplo abaixo, a variável [!DNL Zendesk] a origem requer que o agendamento incremental seja formatado como `type:user updated > {START_TIME} updated < {END_TIME}` e preenchimento retroativo como `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Propriedade | Descrição |
| --- | --- |
| `scheduleParams.type` | O tipo de agendamento que sua origem usará. Defina esse valor como `ADVANCE` para usar o tipo de agendamento avançado. |
| `scheduleParams.paramFormat` | O formato definido do seu parâmetro de agendamento. Esse valor pode ser igual ao da origem `scheduleStartParamFormat` e `scheduleEndParamFormat` valores. |
| `scheduleParams.incremental` | O query incremental da sua origem. Incremental refere-se a um método de ingestão em que apenas dados novos ou modificados são assimilados. |
| `scheduleParams.backfill` | A consulta de preenchimento retroativo da origem. O preenchimento retroativo refere-se a um método de assimilação em que os dados históricos são assimilados. |

Depois de configurar o agendamento avançado, você deve consultar o `scheduleParams` na seção parâmetros de URL, corpo ou cabeçalho , dependendo do suporte a sua fonte específica. No exemplo abaixo, `{SCHEDULE_QUERY}` é um espaço reservado usado para especificar onde as expressões de agendamento incremental e de preenchimento retroativo serão usadas. No caso de um [!DNL Zendesk] fonte, `query` é usado no `queryParams` para especificar o agendamento avançado.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Adicione um esquema personalizado para definir os atributos dinâmicos de sua origem

Você pode incluir um esquema personalizado na `sourceSpec` para definir todos os atributos necessários para a sua fonte, incluindo quaisquer atributos dinâmicos que você possa precisar. Você pode atualizar a especificação de conexão correspondente da sua origem, fazendo uma solicitação de PUT para o `/connectionSpecs` endpoint da variável [!DNL Flow Service] API, enquanto fornece o esquema personalizado na variável `sourceSpec` seção da especificação de conexão.

A seguir encontra-se um exemplo de esquema personalizado que pode ser adicionado à especificação de conexão da origem:

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Próximas etapas

Com suas especificações de origem preenchidas, você pode continuar a configurar as especificações de exploração para a fonte que deseja integrar à Platform. Veja o documento em [configuração de especificações do explore](./explorespec.md) para obter mais informações.
