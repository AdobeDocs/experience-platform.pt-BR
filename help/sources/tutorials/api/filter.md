---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, API de Serviço de fluxo, fontes, fontes
title: Filtrar dados no nível da linha para uma fonte usando a API do Serviço de fluxo
description: Este tutorial aborda as etapas sobre como filtrar dados no nível da fonte usando a API do Serviço de Fluxo
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: da6f5a79b1ee16fb0d44a5c2990ed1b8be1f99e2
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 3%

---

# Filtrar dados em nível de linha para uma origem usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>Atualmente, o suporte para filtrar dados em nível de linha está disponível apenas para as seguintes fontes:
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Marketing Cloud Salesforce](../../connectors/marketing-automation/salesforce-marketing-cloud.md)
>* [Snowflake](../../connectors/databases/snowflake.md)


Este tutorial fornece etapas sobre como filtrar dados em nível de linha para uma fonte usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Filtrar dados de origem

O seguinte descreve as etapas a serem seguidas para filtrar dados no nível da linha para sua origem.

### Pesquisar especificações de conexão

Antes de usar a API para filtrar dados a nível de linha para uma fonte, primeiro recupere os detalhes da especificação de conexão da fonte para determinar os operadores e o idioma aceitos por uma fonte específica.

Para recuperar uma especificação de conexão de uma fonte específica, faça uma solicitação do GET para a variável `/connectionSpecs` endpoint da variável [!DNL Flow Service] API enquanto fornece o nome da propriedade da sua origem como parte dos parâmetros de consulta.

**Formato da API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMS}` | Os parâmetros de consulta opcionais para filtrar os resultados por. Você pode recuperar o [!DNL Google BigQuery] especificação de conexão aplicando `name` propriedade e especificação `"google-big-query"` em sua pesquisa. |

**Solicitação**

A solicitação a seguir recupera especificações de conexão para [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão para [!DNL Google BigQuery], incluindo informações sobre a linguagem de consulta e os operadores lógicos compatíveis.

>[!NOTE]
>
>A resposta da API abaixo é truncada por brevidade.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.filterAtSource.enabled` | Determina se a origem consultada suporta a filtragem de dados no nível da linha. |
| `attributes.filterAtSource.queryLanguage` | Determina o idioma da consulta que a origem consultada suporta. |
| `attributes.filterAtSource.logicalOperators` | Determina os operadores lógicos que podem ser usados para filtrar dados em nível de linha para sua origem. |
| `attributes.filterAtSource.comparisonOperators` | Determina operadores de comparação que podem ser usados para filtrar dados em nível de linha para sua origem. Consulte a tabela abaixo para obter mais informações sobre operadores de comparação. |
| `attributes.filterAtSource.columnNameEscapeChar` | Determina o caractere a ser usado para evitar colunas. |
| `attributes.filterAtSource.valueEscapeChar` | Determina como os valores serão arredondados ao gravar uma consulta SQL. |

{style="table-layout:auto"}

#### Operadores de comparação

| Operador | Descrição |
| --- | --- |
| `==` | Filtra se a propriedade é igual ao valor fornecido. |
| `!=` | Filtra se a propriedade não é igual ao valor fornecido. |
| `<` | Filtra se a propriedade é menor que o valor fornecido. |
| `>` | Filtra se a propriedade é maior que o valor fornecido. |
| `<=` | Filtra se a propriedade é menor ou igual ao valor fornecido. |
| `>=` | Filtra se a propriedade é maior ou igual ao valor fornecido. |
| `like` | Filtros sendo usados em um `WHERE` para procurar um padrão especificado. |
| `in` | Filtra se a propriedade está dentro de um intervalo especificado. |

{style="table-layout:auto"}

### Especificar condições de filtragem para assimilação

Depois de identificar os operadores lógicos e o idioma de consulta aceitos pela origem, você pode usar a Linguagem de consulta de perfil (PQL) para especificar as condições de filtragem que deseja aplicar aos dados de origem.

No exemplo abaixo, as condições são aplicadas para selecionar apenas dados que sejam iguais aos valores fornecidos para os tipos de nó listados como parâmetros.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Visualizar seus dados

É possível visualizar seus dados fazendo uma solicitação do GET para a `/explore` endpoint da variável [!DNL Flow Service] API ao fornecer `filters` como parte dos parâmetros de consulta e especificando as condições de entrada PQL em [!DNL Base64].

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da sua origem. |
| `{TABLE_PATH}` | A propriedade path da tabela que você deseja inspecionar. |
| `{FILTERS}` | Suas condições de filtragem PQL codificadas em [!DNL Base64]. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma solicitação bem-sucedida retorna a seguinte resposta.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### Criar uma conexão de origem para dados filtrados

Para criar uma conexão de origem e assimilar dados filtrados, faça uma solicitação de POST para a `/sourceConnections` endpoint , ao fornecer as condições de filtragem como parte dos parâmetros do corpo.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para assimilar dados de `test1.fasTestTable` em que `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Apêndice

Esta seção fornece mais exemplos de diferentes cargas para filtragem.

### Condições singulares

Você pode omitir a `fnApply` para cenários que exigem apenas uma condição.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### Usar o `in` operador

Consulte a carga de exemplo abaixo para obter um exemplo do operador `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### Usar o `isNull` operador

Consulte a carga de exemplo abaixo para obter um exemplo do operador `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### Usar o `NOT` operador

Consulte a carga de exemplo abaixo para obter um exemplo do operador `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### Exemplo com condições aninhadas

Consulte a carga de amostra abaixo para obter um exemplo de condições aninhadas complexas.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
