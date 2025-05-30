---
keywords: Experience Platform;página inicial;tópicos populares;catálogo;pesquisa de objeto;api
solution: Experience Platform
title: Pesquisar um objeto de catálogo
description: Se você souber o identificador exclusivo de um objeto de Catálogo específico, poderá executar uma solicitação do GET para exibir os detalhes desse objeto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Pesquisar um objeto de Catálogo

Se você souber o identificador exclusivo de um objeto [!DNL Catalog] específico, poderá executar uma solicitação GET para exibir os detalhes desse objeto.

>[!NOTE]
>
>Ao exibir objetos específicos, ainda é prática recomendada [filtrar por propriedades](filter-data.md) e retornar somente as propriedades em que está interessado.

**Formato da API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera um conjunto de dados por sua ID, retornando suas propriedades `name`, `description`, `tags` e `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o conjunto de dados especificado com apenas o `properties` solicitado no corpo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Propriedades cujos valores têm o prefixo `@` representam objetos inter-relacionados. Consulte a seção do apêndice em [exibindo objetos inter-relacionados](appendix.md#view-interrelated-objects) para obter etapas sobre como exibir os detalhes desses objetos.
