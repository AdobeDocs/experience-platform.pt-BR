---
keywords: Experience Platform, home, tópicos populares, catálogo, pesquisa de objeto, api
solution: Experience Platform
title: Pesquisar um objeto de catálogo
topic-legacy: developer guide
description: Se você souber o identificador exclusivo de um objeto de Catálogo específico, poderá executar uma solicitação de GET para exibir os detalhes desse objeto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# Pesquisar um objeto de catálogo

Se você souber o identificador exclusivo de um objeto [!DNL Catalog] específico, poderá executar uma solicitação GET para exibir os detalhes desse objeto.

>[!NOTE]
>
>Ao visualizar objetos específicos, ainda é uma prática recomendada [filtrar por propriedades](filter-data.md) e retornar somente as propriedades em que você está interessado.

**Formato da API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera um conjunto de dados por sua ID, retornando suas propriedades `name`, `description`, `state`, `tags` e `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o conjunto de dados especificado com apenas o `properties` solicitado no corpo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>As propriedades cujos valores têm o prefixo `@` representam objetos inter-relacionados. Consulte a seção do apêndice em [visualizar objetos interrelacionados](appendix.md#view-interrelated-objects) para obter etapas sobre como visualizar os detalhes desses objetos.
