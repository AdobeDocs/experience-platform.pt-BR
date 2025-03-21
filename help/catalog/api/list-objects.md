---
keywords: Experience Platform;página inicial;tópicos populares;filtro;Filtrar;filtrar dados;Filtrar dados
solution: Experience Platform
title: Listar Objetos de Catálogo
description: Você pode recuperar uma lista de todos os objetos disponíveis de um tipo específico por meio de uma única chamada de API, com a prática recomendada de incluir filtros que limitam o tamanho da resposta.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 2%

---

# Listar objetos do Catálogo

Você pode recuperar uma lista de todos os objetos disponíveis de um tipo específico por meio de uma única chamada de API, com a prática recomendada de incluir filtros que limitam o tamanho da resposta.

**Formato da API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser listado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | Um parâmetro de consulta usado para filtrar os resultados retornados na resposta. Vários parâmetros são separados por &quot;E&quot; comercial (`&`). Consulte o guia em [filtrando dados do catálogo](filter-data.md) para obter mais informações. |

**Solicitação**

A solicitação de amostra abaixo recupera uma lista de conjuntos de dados, com um filtro `limit` reduzindo a resposta a cinco resultados e um filtro `properties` que limita as propriedades exibidas para cada conjunto de dados.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de objetos [!DNL Catalog] na forma de pares de valor chave, filtrados pelos parâmetros de consulta fornecidos na solicitação. Para cada par de valor-chave, a chave representa um identificador exclusivo para o objeto [!DNL Catalog] em questão, que pode ser usado em outra chamada para [exibir esse objeto específico](look-up-object.md) para obter mais detalhes.

>[!NOTE]
>
>Se um objeto retornado não contiver uma ou mais das propriedades solicitadas indicadas pela consulta `properties`, a resposta retornará apenas as propriedades solicitadas que ela não inclui, conforme mostrado em ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** abaixo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
