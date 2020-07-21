---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Pesquisar vários objetos
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 1%

---


# Pesquisar vários objetos

Se você desejar visualização em vários objetos específicos, em vez de fazer uma solicitação por objeto, [!DNL Catalog] fornecer um atalho simples para solicitar vários objetos do mesmo tipo. Você pode usar uma única solicitação GET para retornar vários objetos específicos, incluindo uma lista separada por vírgulas de IDs.

>[!NOTE]
>
>Mesmo ao solicitar [!DNL Catalog] objetos específicos, ainda é prática recomendada o parâmetro `properties` query para retornar somente as propriedades necessárias.

**Formato da API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a recuperar. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Um identificador para um dos objetos específicos que você deseja recuperar. |

**Solicitação**

A solicitação a seguir inclui uma lista separada por vírgulas de IDs de conjunto de dados, bem como uma lista separada por vírgulas de propriedades a serem retornadas para cada conjunto de dados.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista dos conjuntos de dados especificados, contendo apenas as propriedades solicitadas (`name`, `description`e `files`) para cada um.

>[!NOTE]
>
>Se um objeto retornado não contiver mais uma ou mais das propriedades solicitadas indicadas pelo `properties` query, a resposta retornará somente as propriedades solicitadas que ela inclui, conforme mostrado em ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** abaixo.

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
