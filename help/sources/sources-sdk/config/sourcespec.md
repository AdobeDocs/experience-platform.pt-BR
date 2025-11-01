---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Configurar especificações de origem para Origens de Autoatendimento (SDK em Lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Origens de Autoatendimento (SDK em Lote).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 1%

---

# Configurar especificação de origem para Origens de Autoatendimento (SDK em Lote)

As especificações do Source contêm informações específicas de uma origem, incluindo atributos pertencentes à categoria de uma origem, status beta e ícone de catálogo. Eles também contêm informações úteis, como parâmetros de URL, conteúdo, cabeçalho e agendamento. As especificações do Source também descrevem o esquema dos parâmetros necessários para criar uma conexão de origem a partir de uma conexão de base. O esquema é necessário para criar uma conexão de origem.

Consulte o [apêndice](#source-spec) para obter um exemplo de uma especificação de origem totalmente preenchida.


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
| `sourceSpec.attributes` | Contém informações sobre a fonte específica da interface do usuário ou da API. |  |
| `sourceSpec.attributes.uiAttributes` | Exibe informações sobre a origem específica da interface do usuário. |  |
| `sourceSpec.attributes.uiAttributes.isBeta` | Um atributo booleano que indica se a fonte requer mais feedback dos clientes para ser adicionada à funcionalidade. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Define a categoria da origem. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Define o ícone usado para a renderização da origem na interface do usuário do Experience Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Exibe uma breve descrição da origem. |  |
| `sourceSpec.attributes.uiAttributes.label` | Exibe o rótulo a ser usado para a renderização da origem na interface do Experience Platform. |  |
| `sourceSpec.attributes.spec.properties.urlParams` | Contém informações sobre o caminho de recurso do URL, o método e os parâmetros de consulta compatíveis. |  |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Define o caminho do recurso do qual buscar os dados. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Define o método HTTP a ser usado para fazer a solicitação ao recurso para buscar dados. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Define os parâmetros de consulta compatíveis que podem ser usados para anexar o URL de origem ao fazer uma solicitação para buscar dados. **Observação**: qualquer valor de parâmetro fornecido pelo usuário deve ser formatado como um espaço reservado. Por exemplo: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` será anexado à URL de origem como: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Define cabeçalhos que precisam ser fornecidos na solicitação HTTP para o URL de origem ao buscar dados. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Esse atributo pode ser configurado para enviar o corpo HTTP por meio de uma solicitação POST. |  |
| `sourceSpec.attributes.spec.properties.contentPath` | Define o nó que contém a lista de itens que devem ser assimilados na Experience Platform. Esse atributo deve seguir a sintaxe de caminho JSON válida e apontar para uma matriz específica. | Exiba a [seção de recursos adicionais](#content-path) para obter um exemplo do recurso contido em um caminho de conteúdo. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | O caminho que aponta para os registros de coleção a serem assimilados na Experience Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Essa propriedade permite identificar itens específicos do recurso identificado no caminho do conteúdo que devem ser excluídos de serem assimilados. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Essa propriedade permite especificar explicitamente os atributos individuais que você deseja manter. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Esta propriedade permite que você substitua o valor do nome de atributo especificado em `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Essa propriedade permite nivelar duas matrizes e transformar dados de recursos em recursos do Experience Platform. |  |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | O caminho que aponta para os registros de coleção que você deseja nivelar. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Essa propriedade permite identificar itens específicos do recurso identificado no caminho da entidade que devem ser excluídos da assimilação. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Essa propriedade permite especificar explicitamente os atributos individuais que você deseja manter. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Esta propriedade permite que você substitua o valor do nome de atributo especificado em `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Define os parâmetros ou campos que devem ser fornecidos para obter um link para a próxima página da resposta da página atual do usuário ou ao criar um URL da próxima página. |  |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Exibe o tipo de paginação suportada para a sua origem. | <ul><li>`OFFSET`: esse tipo de paginação permite analisar os resultados especificando um índice de onde iniciar a matriz resultante e um limite para quantos resultados são retornados.</li><li>`POINTER`: Esse tipo de paginação permite que você use uma variável `pointer` para apontar para um item específico que precisa ser enviado com uma solicitação. A paginação de tipo de ponteiro requer um caminho na carga que aponte para a próxima página.</li><li>`CONTINUATION_TOKEN`: esse tipo de paginação permite anexar seus parâmetros de consulta ou cabeçalho a um token de continuação para recuperar os dados de retorno restantes de sua origem, que não foram retornados inicialmente devido a um máximo predeterminado.</li><li>`PAGE`: esse tipo de paginação permite que você anexe seu parâmetro de consulta com um parâmetro de paginação para percorrer os dados de retorno por páginas, começando da página zero.</li><li>`NONE`: Esse tipo de paginação pode ser usado para fontes que não oferecem suporte a nenhum dos tipos de paginação disponíveis. O tipo de paginação `NONE` retorna todos os dados de resposta após uma solicitação.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. | `limit` ou `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | O número de registros a serem buscados em uma página. | `limit=10` ou `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | O nome do atributo offset. Isso é necessário se o tipo de paginação for definido como `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | O nome do atributo de ponteiro. Isso requer o caminho json para o atributo que apontará para a próxima página. Isso é necessário se o tipo de paginação for definido como `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contém parâmetros que definem formatos de agendamento compatíveis com a sua origem. Os parâmetros de agendamento incluem `startTime` e `endTime`, que permitem definir intervalos de tempo específicos para execuções em lote, o que garante que os registros buscados em uma execução em lote anterior não sejam buscados novamente. |  |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Define o nome do parâmetro da hora inicial | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Define o nome do parâmetro da hora final | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Define o formato com suporte para o `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Define o formato com suporte para o `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Define os parâmetros fornecidos pelo usuário para buscar valores do recurso. | Consulte os [recursos adicionais](#user-input) para obter um exemplo de parâmetros inseridos pelo usuário para `spec.properties`. |

{style="table-layout:auto"}

## Recursos adicionais {#appendix}

As seções a seguir fornecem informações sobre as configurações adicionais que você pode fazer no `sourceSpec`, incluindo o agendamento avançado e esquemas personalizados.

### Exemplo de caminho de conteúdo {#content-path}

Este é um exemplo do conteúdo da propriedade `contentPath` em uma especificação de conexão [!DNL MailChimp Members].

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

### `spec.properties` exemplo de entrada de usuário {#user-input}

Veja a seguir um exemplo de um `spec.properties` fornecido pelo usuário usando uma especificação de conexão [!DNL MailChimp Members].

Neste exemplo, `listId` é fornecido como parte de `urlParams.path`. Se você precisar recuperar `listId` de um cliente, defina-o também como parte de `spec.properties`.


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

### Exemplo de especificação do Source {#source-spec}

Esta é uma especificação de origem concluída usando [!DNL MailChimp Members]:

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

### Configurar tipos de paginação diferentes para a origem {#pagination}

A seguir estão exemplos de outros tipos de paginação compatíveis com Origens de Autoatendimento (SDK em Lote):

>[!BEGINTABS]

>[!TAB Deslocamento]

Esse tipo de paginação permite analisar os resultados especificando um índice de onde iniciar o array resultante e um limite para quantos resultados são retornados. Por exemplo:

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de paginação usado para retornar dados. |
| `limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. |
| `limitValue` | O número de registros a serem buscados em uma página. |
| `offSetName` | O nome do atributo offset. Isso é necessário se o tipo de paginação for definido como `offset`. |
| `endConditionName` | Um valor definido pelo usuário que indica a condição que encerrará o loop de paginação na próxima solicitação HTTP. Você deve fornecer o nome do atributo no qual deseja colocar a condição final. |
| `endConditionValue` | O valor do atributo no qual você deseja colocar a condição final. |

>[!TAB Ponteiro]

Esse tipo de paginação permite usar uma variável `pointer` para apontar para um item específico que precisa ser enviado com uma solicitação. A paginação de tipo de ponteiro requer um caminho na carga que aponte para a próxima página. Por exemplo:

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de paginação usado para retornar dados. |
| `limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. |
| `limitValue` | O número de registros a serem buscados em uma página. |
| `pointerPath` | O nome do atributo de ponteiro. Isso requer o caminho json para o atributo que apontará para a próxima página. |

>[!TAB Token de continuação]

Um tipo de token de continuação de paginação retorna um token de sequência de caracteres que significa a existência de mais itens que não puderam ser retornados, devido a um número máximo predeterminado de itens que podem ser retornados em uma única resposta.

Uma origem que oferece suporte ao tipo de paginação de token de continuação pode ter um parâmetro de paginação semelhante a:

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
| `continuationTokenPath` | O valor que deve ser anexado aos parâmetros de consulta para passar para a próxima página dos resultados retornados. |
| `parameterType` | A propriedade `parameterType` define onde `parameterName` deve ser adicionado. O tipo `QUERYPARAM` permite anexar sua consulta com o `parameterName`. O `HEADERPARAM` permite que você adicione o `parameterName` à sua solicitação de cabeçalho. |
| `parameterName` | O nome do parâmetro usado para incorporar o token de continuação. O formato é: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | A propriedade `delayRequestMillis` na paginação permite controlar a taxa de solicitações feitas na origem. Algumas origens podem ter um limite para o número de solicitações que podem ser feitas por minuto. Por exemplo, [!DNL Zendesk] tem um limite de 100 solicitações por minuto e definir `delayRequestMillis` como `850` permite que você configure a fonte para fazer chamadas a apenas 80 solicitações por minuto, bem abaixo do limite de 100 solicitações por minuto. |

Este é um exemplo de uma resposta retornada usando o tipo de token de continuação de paginação:

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

>[!TAB Página]

O tipo de paginação `PAGE` permite percorrer os dados de retorno pelo número de páginas começando de zero. Ao usar a paginação do tipo `PAGE`, você deve fornecer o número de registros fornecidos em uma única página.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de paginação usado para retornar dados. |
| `limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. |
| `limitValue` | O número de registros a serem buscados em uma página. |
| `initialPageIndex` | (Opcional) O índice da página inicial define o número da página a partir da qual a paginação iniciará. Esse campo pode ser usado para fontes nas quais a paginação não começa em 0. Se não for fornecido, o índice da página inicial será padrão de 0. Este campo espera um número inteiro. |
| `endPageIndex` | (Opcional) O índice da página final permite estabelecer uma condição final e parar a paginação. Esse campo pode ser usado quando as condições finais padrão para interromper a paginação não estiverem disponíveis. Este campo também pode ser usado se o número de páginas que serão assimiladas ou o número da última página for fornecido por meio do cabeçalho de resposta, o que é comum ao usar a paginação do tipo `PAGE`. O valor do índice da página final pode ser o número da última página ou um valor de expressão do tipo string do cabeçalho de resposta. Por exemplo, você pode usar `headers.x-pagecount` para atribuir um índice de página final ao valor `x-pagecount` dos cabeçalhos de resposta. **Observação**: `x-pagecount` é um cabeçalho de resposta obrigatório para algumas fontes e contém o número de valor de páginas a serem assimiladas. |
| `pageParamName` | O nome do parâmetro que você deve anexar aos parâmetros de consulta para percorrer diferentes páginas dos dados de retorno. Por exemplo, `https://abc.com?pageIndex=1` retornaria a segunda página de uma carga de retorno de API. |
| `maximumRequest` | O número máximo de solicitações que uma origem pode fazer para uma determinada execução incremental. O limite padrão atual é 10000. |

{style="table-layout:auto"}


>[!TAB Nenhum]

O tipo de paginação `NONE` pode ser usado para fontes que não oferecem suporte a nenhum dos tipos de paginação disponíveis. As fontes que usam o tipo de paginação de `NONE` simplesmente retornam todos os registros recuperáveis quando uma solicitação GET é feita.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### Programação avançada para Origens de Autoatendimento (SDK em Lote)

Configure a programação incremental e de preenchimento retroativo da origem usando a programação avançada. A propriedade `incremental` permite configurar um agendamento no qual sua origem assimilará somente registros novos ou modificados, enquanto a propriedade `backfill` permite criar um agendamento para assimilar dados históricos.

Com a programação avançada, você pode usar expressões e funções específicas da origem para configurar programações incrementais e de preenchimento retroativo. No exemplo abaixo, a origem [!DNL Zendesk] requer que o agendamento incremental seja formatado como `type:user updated > {START_TIME} updated < {END_TIME}` e o preenchimento retroativo como `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | O tipo de agendamento que sua origem usará. Defina este valor como `ADVANCE` para usar o tipo de agendamento avançado. |
| `scheduleParams.paramFormat` | O formato definido do seu parâmetro de agendamento. Este valor pode ser igual aos valores de `scheduleStartParamFormat` e `scheduleEndParamFormat` da sua origem. |
| `scheduleParams.incremental` | O query incremental da sua origem. Incremental refere-se a um método de assimilação em que somente dados novos ou modificados são assimilados. |
| `scheduleParams.backfill` | A consulta de preenchimento retroativo da origem. O preenchimento retroativo se refere a um método de assimilação no qual os dados históricos são assimilados. |

Depois de configurar o agendamento avançado, consulte `scheduleParams` na seção URL, corpo ou parâmetros de cabeçalho, dependendo do que a sua fonte específica suporta. No exemplo abaixo, `{SCHEDULE_QUERY}` é um espaço reservado usado para especificar onde as expressões de agendamento de preenchimento retroativo e incremental serão usadas. No caso de uma origem [!DNL Zendesk], `query` é usado em `queryParams` para especificar o agendamento avançado.

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

### Adicione um esquema personalizado para definir os atributos dinâmicos de sua fonte

Você pode incluir um esquema personalizado em seu `sourceSpec` para definir todos os atributos necessários para sua origem, inclusive os atributos dinâmicos que você possa precisar. Você pode atualizar a especificação de conexão correspondente da sua origem fazendo uma solicitação PUT para o ponto de extremidade `/connectionSpecs` da API [!DNL Flow Service] e, ao mesmo tempo, fornecendo seu esquema personalizado na seção `sourceSpec` da sua especificação de conexão.

Este é um exemplo de um esquema personalizado que você pode adicionar à especificação de conexão da origem:

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

Com as especificações de origem preenchidas, você pode continuar a configurar as especificações de exploração para a origem que deseja integrar ao Experience Platform. Consulte o documento sobre [configuração das especificações de exploração](./explorespec.md) para obter mais informações.
