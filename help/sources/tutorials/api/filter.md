---
title: Filtrar dados em nível de linha para uma Source usando a API do serviço de fluxo
description: Este tutorial aborda as etapas sobre como filtrar dados no nível da origem usando a API do Serviço de fluxo
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: 544bb7b5aff437fd49c30ac3d6261f103a609cac
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 5%

---

# Filtrar dados em nível de linha para uma origem usando a API [!DNL Flow Service]

>[!AVAILABILITY]
>
>Atualmente, o suporte para filtragem de dados em nível de linha está disponível apenas para as seguintes fontes:
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] atividades padrão](../../connectors/adobe-applications/marketo/marketo.md)

Leia este guia para obter as etapas sobre como filtrar dados de nível de linha para uma fonte usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Platform].
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../landing/api-guide.md).

## Filtrar dados de origem {#filter-source-data}

As etapas a seguir descrevem as etapas a serem seguidas para filtrar os dados no nível de linha para sua origem.

### Recupere as especificações da conexão {#retrieve-your-connection-specs}

A primeira etapa na filtragem de dados em nível de linha para a origem é recuperar as especificações de conexão da origem e determinar os operadores e o idioma compatíveis com a origem.

Para recuperar a especificação de conexão de uma determinada origem, faça uma solicitação GET para o ponto de extremidade `/connectionSpecs` da API [!DNL Flow Service] e forneça o nome da propriedade da origem como parte dos parâmetros de consulta.

**Formato da API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMS}` | Os parâmetros de consulta opcionais para filtrar os resultados. Você pode recuperar a especificação de conexão [!DNL Google BigQuery] aplicando a propriedade `name` e especificando `"google-big-query"` em sua pesquisa. |

+++Solicitação

A solicitação a seguir recupera as especificações de conexão para [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o código de status 200 e as especificações de conexão para [!DNL Google BigQuery], incluindo informações sobre o idioma de consulta e operadores lógicos com suporte.

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

+++

#### Operadores de comparação {#comparison-operators}

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

### Especificar condições de filtragem para assimilação {#specify-filtering-conditions-for-ingestion}

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

### Pré-visualizar seus dados {#preview-your-data}

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

+++Solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o conteúdo e a estrutura dos dados.

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

+++

### Criar uma conexão de origem para dados filtrados

Para criar uma conexão de origem e assimilar dados filtrados, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` e forneça suas condições de filtragem nos parâmetros do corpo da solicitação.

**Formato da API**

```http
POST /sourceConnections
```

+++Solicitação

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

+++

+++Resposta

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Filtrar entidades de atividade para [!DNL Marketo Engage] {#filter-for-marketo}

Você pode usar a filtragem em nível de linha para filtrar entidades de atividade ao usar o [[!DNL Marketo Engage] conector de origem](../../connectors/adobe-applications/marketo/marketo.md). Atualmente, você só pode filtrar por entidades de atividade e tipos de atividade padrão. As atividades personalizadas permanecem controladas em [[!DNL Marketo] mapeamentos de campo](../../connectors/adobe-applications/mapping/marketo.md).

### [!DNL Marketo] tipos de atividades padrão {#marketo-standard-activity-types}

A tabela a seguir descreve os tipos de atividade padrão para [!DNL Marketo]. Use essa tabela como referência para seus critérios de filtragem.

| ID do tipo de atividade | Nome do tipo de atividade |
| --- | --- |
| 1 | Visitar página da Web |
| 2 | Preencher formulário |
| 3 | Clique em Link |
| 6 | Enviar e-mail |
| 7 | Email entregue |
| 8 | Email rejeitado |
| 9 | Cancelar assinatura de email |
| 10 | Abrir e-mail |
| 11 | Clique em Email |
| 12 | Novo lead |
| 21 | Converter lead |
| 22 | Alterar pontuação |
| 24 | Adicionar à lista |
| 25 | Remover da lista |
| 27 | Email rejeitado temporariamente |
| 32 | Mesclar leads |
| 34 | Adicionar à oportunidade |
| 35 | Remover da oportunidade |
| 36 | Atualizar oportunidade |
| 46 | Momento interessante |
| 101 | Alterar estágio de receita |
| 104 | Alterar status na progressão |
| 110 | Chamar Webhook |
| 113 | Adicionar à criação |
| 114 | Alterar Faixa de Criação |
| 115 | Alterar cadência de criação |

{style="table-layout:auto"}

Siga as etapas abaixo para filtrar suas entidades de atividade padrão ao usar o conector de origem [!DNL Marketo].

### Criar um fluxo de dados de rascunho

Primeiro, crie um [[!DNL Marketo] fluxo de dados](../ui/create/adobe-applications/marketo.md) e salve-o como rascunho. Consulte a documentação a seguir para obter as etapas detalhadas sobre como criar um fluxo de dados de rascunho:

* [Salvar um fluxo de dados como rascunho usando a interface](../ui/draft.md)
* [Salvar um fluxo de dados como rascunho usando a API](../api/draft.md)

### Recuperar a ID do fluxo de dados

Depois de ter um fluxo de dados em rascunho, você deve recuperar a ID correspondente.

Na interface, navegue até o catálogo de fontes e selecione **[!UICONTROL Fluxos de Dados]** no cabeçalho superior. Use a coluna de status para identificar todos os fluxos de dados que foram salvos no modo de rascunho e, em seguida, selecione o nome do fluxo de dados. Em seguida, use o painel **[!UICONTROL Propriedades]** à direita para localizar sua ID de fluxo de dados.

### Recuperar detalhes do fluxo de dados

Em seguida, você deve recuperar os detalhes do fluxo de dados, especialmente a ID da conexão de origem associada ao fluxo de dados. Para recuperar os detalhes do fluxo de dados, faça uma solicitação GET para o ponto de extremidade `/flows` e forneça sua ID de fluxo de dados como um parâmetro de caminho.

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{FLOW_ID}` | A ID do fluxo de dados que você deseja recuperar. |

+++Solicitação

A solicitação a seguir recupera informações sobre a ID do fluxo de dados: `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna os detalhes do fluxo de dados, incluindo informações sobre as conexões de origem e de destino correspondentes. Você deve anotar suas IDs de conexão de origem e destino, pois esses valores são necessários posteriormente, para publicar seu fluxo de dados.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### Recuperar detalhes da conexão de origem

Em seguida, use sua ID de conexão de origem e faça uma solicitação GET ao ponto de extremidade `/sourceConnections` para recuperar os detalhes da conexão de origem.

**Formato da API**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | A ID da conexão de origem que você deseja recuperar. |

+++Solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna os detalhes da conexão de origem. Anote a versão, pois você precisará desse valor na próxima etapa para atualizar sua conexão de origem.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### Atualizar sua conexão de origem com condições de filtragem

Agora que você tem a ID de conexão de origem e a versão correspondente, é possível fazer uma solicitação de PATCH com as condições de filtro que especificam os tipos de atividade padrão.

Para atualizar sua conexão de origem, faça uma solicitação PATCH para o ponto de extremidade `/sourceConnections` e forneça sua ID de conexão de origem como um parâmetro de consulta. Além disso, você deve fornecer um parâmetro de cabeçalho `If-Match`, com a versão correspondente da conexão de origem.

>[!TIP]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação PATCH. O valor desse cabeçalho é a versão/tag exclusiva do fluxo de dados que você deseja atualizar. O valor da versão/tag é atualizado com cada atualização bem-sucedida de um fluxo de dados.

**Formato da API**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | A ID da conexão de origem que você deseja recuperar. |

+++Solicitação

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna a ID de conexão de origem e a tag (versão).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Publish sua conexão de origem

Com sua conexão de origem atualizada com suas condições de filtragem, agora é possível seguir do estado de rascunho e publicar sua conexão de origem. Para fazer isso, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` e forneça a ID da sua conexão de origem de rascunho, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | A ID da conexão de origem que você deseja publicar. |
| `op` | Uma operação de ação que atualiza o estado da conexão de origem consultada. Para publicar uma conexão de origem de rascunho, defina `op` como `publish`. |

+++Solicitação

A solicitação a seguir publica uma conexão de origem de rascunho.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna a ID de conexão de origem e a tag (versão).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Publish sua conexão de destino

Semelhante à etapa anterior, você também deve publicar sua conexão de destino para continuar e publicar seu fluxo de dados de rascunho. Faça uma solicitação POST para o ponto de extremidade `/targetConnections` e forneça a ID da conexão de destino de rascunho que você deseja publicar, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | A ID da conexão de destino que você deseja publicar. |
| `op` | Uma operação de ação que atualiza o estado da conexão de destino consultada. Para publicar uma conexão de destino de rascunho, defina `op` como `publish`. |

+++Solicitação

A solicitação a seguir publica a conexão de destino com ID: `7e53e6e8-b432-4134-bb29-21fc6e8532e5`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna a ID e a tag correspondente da conexão de destino publicada.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Publish seu fluxo de dados

Com suas conexões de origem e de destino publicadas, agora é possível prosseguir para a etapa final e publicar seu fluxo de dados. Para publicar seu fluxo de dados, faça uma solicitação POST para o ponto de extremidade `/flows` e forneça sua ID de fluxo de dados e uma operação de ação para publicação.

**Formato da API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `{FLOW_ID}` | A ID do fluxo de dados que você deseja publicar. |
| `op` | Uma operação de ação que atualiza o estado do fluxo de dados consultado. Para publicar um fluxo de dados de rascunho, defina `op` como `publish`. |

+++Solicitação

A solicitação a seguir publica o fluxo de dados de rascunho.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna a ID e o `etag` correspondente do fluxo de dados.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Você pode usar a interface do usuário do Experience Platform para verificar se o fluxo de dados de rascunho foi publicado. Navegue até a página de fluxos de dados no catálogo de fontes e faça referência ao **[!UICONTROL Status]** do seu fluxo de dados. Se for bem-sucedido, o status agora deve ser definido como **Habilitado**.

>[!TIP]
>
>* Um fluxo de dados com filtragem ativada será preenchido retroativamente apenas uma vez. Quaisquer alterações no que você fizer nos critérios de filtragem (seja uma adição ou remoção) só poderão ter efeito para dados incrementais.
>* Se precisar assimilar dados históricos para qualquer novo tipo de atividade, é recomendável criar um novo fluxo de dados e definir os critérios de filtragem com os tipos de atividade apropriados na condição de filtro.
>* Não é possível filtrar tipos de atividades personalizadas.
>* Não é possível visualizar dados filtrados.

## Apêndice

Esta seção fornece mais exemplos de diferentes payloads para filtragem.

### Condições peculiares

Você pode omitir a `fnApply` inicial em cenários que exigem apenas uma condição.

+++Selecione para exibir o exemplo

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

+++

### Usando o operador `in`

Consulte a carga abaixo para obter um exemplo do operador `in`.

+++Selecione para exibir o exemplo

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

+++

### Usando o operador `isNull`

+++Selecione para exibir o exemplo

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

+++

### Usando o operador `NOT`

Consulte a carga abaixo para obter um exemplo do operador `NOT`.


+++Selecione para exibir o exemplo

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

+++

### Exemplo com condições aninhadas

Consulte a carga de amostra abaixo para obter um exemplo de condições aninhadas complexas.

+++Selecione para exibir o exemplo

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

+++