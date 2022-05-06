---
keywords: Experience Platform, home, tópicos populares, catálogo, pesquisa de objeto, api
solution: Experience Platform
title: Pesquisar um objeto de catálogo
topic-legacy: developer guide
description: Se você souber o identificador exclusivo de um objeto de Catálogo específico, poderá executar uma solicitação de GET para exibir os detalhes desse objeto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Pesquisar um objeto de catálogo

Se você sabe o identificador exclusivo de um [!DNL Catalog] , é possível executar uma solicitação do GET para exibir os detalhes desse objeto.

>[!NOTE]
>
>Ao exibir objetos específicos, a prática recomendada é [filtrar por propriedades](filter-data.md) e retornam somente as propriedades em que está interessado.

**Formato da API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera um conjunto de dados por sua ID, retornando seu `name`, `description`, `state`, `tags`e `files` propriedades.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o conjunto de dados especificado somente com o `properties` no corpo.

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
>Propriedades cujos valores recebem o prefixo `@` representam objetos interrelacionados. Consulte a seção do apêndice em [como visualizar objetos interrelacionados](appendix.md#view-interrelated-objects) para obter etapas sobre como visualizar os detalhes desses objetos.
