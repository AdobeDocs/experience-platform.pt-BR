---
keywords: Experience Platform;home;popular topics;filter;Filter;filter data;Filter data
solution: Experience Platform
title: objetos de lista
topic: developer guide
description: É possível recuperar uma lista de todos os objetos disponíveis de um tipo específico por meio de uma única chamada de API, com a prática recomendada de incluir filtros que limitam o tamanho da resposta.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 1%

---


# objetos de lista

É possível recuperar uma lista de todos os objetos disponíveis de um tipo específico por meio de uma única chamada de API, com a prática recomendada de incluir filtros que limitam o tamanho da resposta.

**Formato da API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser listado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Um parâmetro de query usado para filtrar os resultados retornados na resposta. Vários parâmetros são separados por E comercial (`&`). Consulte o guia sobre como [filtrar dados](filter-data.md) do catálogo para obter mais informações. |

**Solicitação**

A solicitação de amostra abaixo recupera uma lista de conjuntos de dados, com um `limit` filtro reduzindo a resposta a cinco resultados, e um `properties` filtro que limita as propriedades exibidas para cada conjunto de dados.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de [!DNL Catalog] objetos na forma de pares de valores chave, filtrados pelos parâmetros de query fornecidos na solicitação. Para cada par de valores-chave, a chave representa um identificador exclusivo para o [!DNL Catalog] objeto em questão, que pode ser usado em outra chamada para [visualização desse objeto](look-up-object.md) específico para obter mais detalhes.

>[!NOTE]
>
>Se um objeto retornado não contiver uma ou mais das propriedades solicitadas indicadas pelo `properties` query, a resposta retornará somente as propriedades solicitadas que ela inclui, conforme mostrado em ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** abaixo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
