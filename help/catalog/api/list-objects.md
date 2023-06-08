---
keywords: Experience Platform;página inicial;tópicos populares;filtro;Filtrar;filtrar dados;Filtrar dados
solution: Experience Platform
title: Listar Objetos de Catálogo
description: Você pode recuperar uma lista de todos os objetos disponíveis de um tipo específico por meio de uma única chamada de API, com a prática recomendada de incluir filtros que limitam o tamanho da resposta.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
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
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser listado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Um parâmetro de consulta usado para filtrar os resultados retornados na resposta. Vários parâmetros são separados por &quot;E&quot; comercial (`&`). Consulte o guia sobre [filtragem de dados do catálogo](filter-data.md) para obter mais informações. |

**Solicitação**

A solicitação de amostra abaixo recupera uma lista de conjuntos de dados, com uma `limit` filtre reduzindo a resposta a cinco resultados, e um `properties` que limita as propriedades exibidas para cada conjunto de dados.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de [!DNL Catalog] objetos na forma de pares de valor chave, filtrados pelos parâmetros de consulta fornecidos na solicitação. Para cada par de valor-chave, a chave representa um identificador exclusivo do [!DNL Catalog] objeto em questão, que pode ser usado em outra chamada para [exibir esse objeto específico](look-up-object.md) para obter mais detalhes.

>[!NOTE]
>
>Se um objeto retornado não contiver uma ou mais das propriedades solicitadas indicadas pelo `properties` consulta, a resposta retorna somente as propriedades solicitadas que ela inclui, conforme mostrado na ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** abaixo.

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
