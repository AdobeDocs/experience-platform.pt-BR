---
title: Endpoint de consultas aceleradas
description: Saiba como acessar o armazenamento acelerado de consultas de maneira sem estado para retornar resultados rapidamente com base em dados agregados. Este documento fornece um exemplo de solicitação HTTP e resposta para o endpoint de consultas aceleradas do Serviço de consulta.
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ea2a1cddf299bec750875c4a9125cdd065f18d8b
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Endpoint de consultas aceleradas

Como parte do SKU do Data Distiller, a variável [API do serviço de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/) O permite fazer consultas sem estado ao repositório acelerado. Os resultados retornados são baseados em dados agregados. A redução da latência dos resultados permite uma troca de informações mais interativa. As APIs de queries aceleradas também são usadas para potencializar [painéis definidos pelo usuário](../../dashboards/user-defined-dashboards.md).

Antes de continuar com este guia, verifique se você leu e compreendeu as [Guia da API do Serviço de consulta](./getting-started.md) para usar com êxito a API do Serviço de consulta.

## Introdução

O SKU do Data Distiller é necessário para usar o armazenamento acelerado de consulta. Consulte a [empacotamento](../packaging.md) e [grades de proteção](../guardrails.md#query-accelerated-store), e [licenciamento](../data-distiller/license-usage.md) Documentação relacionada ao Data Distiller SKU. Se você não tiver o Data Distiller SKU, entre em contato com o representante do serviço de atendimento ao cliente da Adobe para obter mais informações.

As seções a seguir detalham as chamadas de API necessárias para acessar o armazenamento acelerado de consulta de forma sem estado por meio da API do Serviço de consulta. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

## Executar uma consulta acelerada {#run-accelerated-query}

Faça uma solicitação POST para o `/accelerated-queries` para executar uma consulta acelerada. A consulta está contida diretamente na carga da solicitação ou é referenciada com uma ID de modelo.

**Formato da API**

```shell
POST /accelerated-queries
```

### Solicitação

>[!IMPORTANT]
>
>Solicitações para o `/accelerated-queries` O endpoint requer uma instrução SQL OU uma ID de modelo, mas não ambas. O envio de ambos em uma solicitação causa um erro.

A solicitação a seguir envia uma consulta SQL no corpo da solicitação para o armazenamento acelerado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Essa solicitação alternativa envia uma ID de modelo no corpo da solicitação para o armazenamento acelerado. O SQL do modelo correspondente é usado para consultar o armazenamento acelerado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Propriedade | Descrição |
|---|---|
| `dbName` | O nome do banco de dados para o qual você está fazendo uma consulta acelerada. O valor de `dbName` deve ter o formato de `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. O banco de dados fornecido deve existir no repositório acelerado ou a solicitação resultará em um erro. Você também deve garantir que a variável `x-sandbox-name` cabeçalho e nome da sandbox no `dbName` consulte a mesma sandbox. |
| `sql` | Uma string de instrução SQL. O tamanho máximo permitido é de 1000000 caracteres. |
| `templateId` | O identificador exclusivo de uma consulta criada e salva como modelo quando uma solicitação POST é feita ao `/templates` terminal. |
| `name` | Um nome descritivo opcional amigável para o usuário para a consulta acelerada. |
| `description` | Um comentário opcional sobre a intenção do query para ajudar outros usuários a entender sua finalidade. O tamanho máximo permitido é de 1000 bytes. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com o esquema ad hoc criado pela consulta.

>[!NOTE]
>
>A resposta a seguir foi truncada por motivos de brevidade.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Propriedade | Descrição |
|---|---|
| `queryId` | O valor de ID da consulta criada. |
| `resultsMeta` | Esse objeto contém os metadados de cada coluna retornada nos resultados para que os usuários saibam o nome e o tipo de cada coluna. |
| `resultsMeta._adhoc` | Um esquema ad-hoc do Experience Data Model (XDM) com campos com namespace para uso somente por um único conjunto de dados. |
| `resultsMeta._adhoc.type` | O tipo de dados do esquema ad hoc. |
| `resultsMeta._adhoc.meta:xdmType` | É um valor gerado pelo sistema para o tipo de campo XDM. Para obter mais informações sobre os tipos disponíveis, consulte a documentação em [tipos XDM disponíveis](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | Esses são os nomes das colunas do conjunto de dados consultado. |
| `resultsMeta._adhoc.results` | Esses são os nomes das linhas do conjunto de dados consultado. Elas refletem cada uma das colunas retornadas. |
