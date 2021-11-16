---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Configurar especificações de autenticação para o SDK do SDK do SDK do SDK do Sources
topic-legacy: overview
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar o SDK das Fontes.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 1%

---


# Configurar especificação de origem para o SDK do SDK do SDK do SDK do SDK do SDK do SDK do SDK do SDK do Forms

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
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `sourceSpec.attributes` | Contém informações sobre a fonte específica para a interface do usuário ou a API. |
| `sourceSpec.attributes.uiAttributes` | Exibe informações sobre a fonte específica para a interface do usuário. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Um atributo booleano que indica se a fonte requer mais feedback dos clientes para adicionar a funcionalidade. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Define a categoria da origem. | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Define o ícone usado para a renderização da fonte na interface do usuário da plataforma. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Exibe uma breve descrição da origem. |
| `sourceSpec.attributes.uiAttributes.label` | Exibe o rótulo a ser usado para a renderização da origem na interface do usuário da plataforma. |
| `sourceSpec.attributes.urlParams` | Contém informações sobre o caminho do recurso de URL, o método e os parâmetros de consulta compatíveis. |
| `sourceSpec.attributes.urlParams.path` | Define o caminho do recurso de onde buscar os dados. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | Define o método HTTP a ser usado para fazer a solicitação ao recurso para buscar dados. | `GET`, `POST` |
| `sourceSpec.attributes.urlParams.queryParams` | Define os parâmetros de consulta compatíveis que podem ser usados para anexar o URL de origem ao fazer uma solicitação para buscar dados. Os parâmetros de consulta devem ser vírgulas (`,`) pares de valores-chave separados. **Observação**: Qualquer valor de parâmetro fornecido pelo usuário deve ser formatado como um espaço reservado. Por exemplo: `${USER_PARAMETER}`. | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | Define a vírgula (`,`) cabeçalhos separados que precisam ser fornecidos na solicitação HTTP para o URL de origem ao buscar dados. | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | Define os parâmetros de corpo necessários. Essa propriedade só será usada se `urlParams.method` está definida como `POST`. |
| `sourceSpec.attributes.contentPath` | Define o nó que contém a lista de itens necessários para ser assimilado na Platform. Esse atributo deve seguir a sintaxe de caminho JSON válida e deve apontar para uma matriz específica. | Consulte a [apêndice](#content-path) para obter um exemplo do recurso contido em um caminho de conteúdo. |
| `sourceSpec.attributes.contentPath.path` | O caminho que aponta para os registros da coleção que serão assimilados na Platform. | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | Essa propriedade permite identificar itens específicos do recurso identificado no caminho do conteúdo que devem ser excluídos da assimilação. |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | Essa propriedade permite que você substitua o valor do nome do atributo especificado em `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | Essa propriedade permite especificar explicitamente os atributos individuais que você deseja mapear. |
| `sourceSpec.attributes.explodeEntityPath` | Essa propriedade permite nivelar duas matrizes e transformar dados de recursos no recurso Plataforma . |
| `sourceSpec.attributes.explodeEntityPath.path` | O caminho que aponta para os registros de coleção que você deseja nivelar. | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | Essa propriedade permite identificar itens específicos do recurso identificado no caminho da entidade que devem ser excluídos da assimilação. |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | Essa propriedade permite que você substitua o valor do nome do atributo especificado em `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | Essa propriedade permite especificar explicitamente os atributos individuais que você deseja mapear. |
| `sourceSpec.attributes.paginationParams` | Define os parâmetros ou campos que devem ser fornecidos para obter um link para a próxima página da resposta da página atual do usuário ou ao criar um URL da próxima página. |
| `sourceSpec.attributes.paginationParams.type` | Exibe o tipo de paginação suportada para a sua origem. | <ul><li>`offset`: Esse tipo de paginação permite analisar os resultados especificando um índice de onde iniciar a matriz resultante e um limite de quantos resultados são retornados.</li><li>`pointer`: Esse tipo de paginação permite usar um `pointer` para apontar para um item específico que precisa ser enviado com uma solicitação. A paginação do tipo de ponteiro requer um caminho na carga que aponte para a próxima página</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | O nome do limite pelo qual a API pode especificar o número de registros a serem buscados em uma página. | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | O número de registros a serem buscados em uma página. | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | O nome do atributo de deslocamento. Isso é necessário se o tipo de paginação estiver definido como `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | O nome do atributo do ponteiro. Isso requer o caminho json para o atributo que apontará para a próxima página. Isso é necessário se o tipo de paginação estiver definido como `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | Contém parâmetros que definem formatos de agendamento compatíveis para a sua origem. Os parâmetros de agendamento incluem `startTime` e `endTime`, que permitem definir intervalos de tempo específicos para execuções de lote, o que garante que os registros buscados em uma execução de lote anterior não sejam buscados novamente. |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | Define o nome do parâmetro de hora de início | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | Define o nome do parâmetro de hora de término | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | Define o formato compatível para a variável `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | Define o formato compatível para a variável `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Define os parâmetros fornecidos pelo usuário para buscar valores de recursos. | Consulte a [apêndice](#user-input) para um exemplo de parâmetros inseridos pelo usuário para `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Apêndice {#appendix}

### Exemplo de caminho de conteúdo {#content-path}

Este é um exemplo do conteúdo da variável `contentPath` em uma [!DNL MailChimp Campaigns] especificação de conexão.

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

## Próximas etapas

Com suas especificações de origem preenchidas, você pode continuar a configurar as especificações de exploração para a fonte que deseja integrar à Platform. Veja o documento em [configuração de especificações do explore](./explorespec.md) para obter mais informações.