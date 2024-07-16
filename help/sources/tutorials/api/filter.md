---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;API de serviço de fluxo;fontes;Fontes
title: Filtrar dados em nível de linha para uma Source usando a API do serviço de fluxo
description: Este tutorial aborda as etapas sobre como filtrar dados no nível da origem usando a API do Serviço de fluxo
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: b0e2fc4767fb6fbc90bcdd3350b3add965988f8f
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# Filtrar dados em nível de linha para uma origem usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>Atualmente, o suporte para filtragem de dados em nível de linha está disponível apenas para as seguintes fontes:
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Snowflake](../../connectors/databases/snowflake.md)

Este tutorial fornece etapas sobre como filtrar dados de nível de linha para uma origem usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Platform].
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../landing/api-guide.md).

## Filtrar dados de origem

As etapas a seguir descrevem as etapas a serem seguidas para filtrar os dados no nível de linha para sua origem.

### Pesquisar especificações de conexão

Antes de usar a API para filtrar dados em nível de linha para uma origem, primeiro você deve recuperar os detalhes de especificação da conexão da origem para determinar os operadores e o idioma compatíveis com uma origem específica.

Para recuperar a especificação de conexão de uma determinada origem, faça uma solicitação GET para o ponto de extremidade `/connectionSpecs` da API [!DNL Flow Service] enquanto fornece o nome da propriedade da origem como parte dos parâmetros de consulta.

**Formato da API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMS}` | Os parâmetros de consulta opcionais para filtrar os resultados. Você pode recuperar a especificação de conexão [!DNL Google BigQuery] aplicando a propriedade `name` e especificando `"google-big-query"` em sua pesquisa. |

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

Uma resposta bem-sucedida retorna as especificações de conexão para [!DNL Google BigQuery], incluindo informações sobre seu idioma de consulta com suporte e operadores lógicos.

>[!NOTE]
>
>A resposta da API abaixo está truncada por motivos de brevidade.

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
| `attributes.filterAtSource.enabled` | Determina se a origem consultada oferece suporte à filtragem de dados em nível de linha. |
| `attributes.filterAtSource.queryLanguage` | Determina o idioma da consulta que a fonte consultada aceita. |
| `attributes.filterAtSource.logicalOperators` | Determina os operadores lógicos que você pode usar para filtrar dados em nível de linha para a origem. |
| `attributes.filterAtSource.comparisonOperators` | Determina operadores de comparação que você pode usar para filtrar dados em nível de linha para sua origem. Consulte a tabela abaixo para obter mais informações sobre operadores de comparação. |
| `attributes.filterAtSource.columnNameEscapeChar` | Determina o caractere a ser usado para colunas de escape. |
| `attributes.filterAtSource.valueEscapeChar` | Determina como os valores serão cercados ao gravar uma consulta SQL. |

{style="table-layout:auto"}

#### Operadores de comparação

| Operador | Descrição |
| --- | --- |
| `==` | Define se a propriedade é igual ao valor fornecido. |
| `!=` | Define se a propriedade não é igual ao valor fornecido. |
| `<` | Define se a propriedade é menor que o valor fornecido. |
| `>` | Filtra especificando se a propriedade é maior que o valor fornecido. |
| `<=` | Filtra se a propriedade é menor ou igual ao valor fornecido. |
| `>=` | Filtra se a propriedade é maior ou igual ao valor fornecido. |
| `like` | Filtros sendo usados em uma cláusula `WHERE` para procurar um padrão especificado. |
| `in` | Define se a propriedade está dentro de um intervalo especificado. |

{style="table-layout:auto"}

### Especificar condições de filtragem para assimilação

Depois de identificar os operadores lógicos e o idioma de consulta compatíveis com sua origem, você pode usar o Profile Query Language (PQL) para especificar as condições de filtragem que deseja aplicar aos dados de origem.

No exemplo abaixo, as condições são aplicadas apenas a dados de seleção que sejam iguais aos valores fornecidos para os tipos de nó listados como parâmetros.

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

### Pré-visualizar seus dados

Você pode visualizar seus dados fazendo uma solicitação GET para o ponto de extremidade `/explore` da API [!DNL Flow Service] enquanto fornece `filters` como parte de seus parâmetros de consulta e especifica suas condições de entrada do PQL em [!DNL Base64].

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da sua origem. |
| `{TABLE_PATH}` | A propriedade de caminho da tabela que você deseja inspecionar. |
| `{FILTERS}` | As condições de filtragem do PQL estão codificadas em [!DNL Base64]. |

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

Para criar uma conexão de origem e assimilar dados filtrados, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` enquanto fornece as condições de filtragem como parte dos parâmetros do corpo.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para assimilar dados de `test1.fasTestTable` onde `city` = `DDN`.

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

Esta seção fornece mais exemplos de diferentes payloads para filtragem.

### Condições peculiares

Você pode omitir a `fnApply` inicial em cenários que exigem apenas uma condição.

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

### Usando o operador `in`

Consulte a carga abaixo para obter um exemplo do operador `in`.

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

### Usando o operador `isNull`

Consulte a carga abaixo para obter um exemplo do operador `isNull`.

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

### Usando o operador `NOT`

Consulte a carga abaixo para obter um exemplo do operador `NOT`.

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
