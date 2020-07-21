---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Pesquisar um objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Pesquisar um objeto

Se você souber o identificador exclusivo de um [!DNL Catalog] objeto específico, poderá executar uma solicitação GET para visualização dos detalhes desse objeto.

>[!NOTE]
>
>Ao exibir objetos específicos, ainda é prática recomendada [filtrar por propriedades](filter-data.md) e retornar somente as propriedades que lhe interessam.

**Formato da API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera um conjunto de dados por sua ID, retornando suas propriedades `name`, `description`, `state`e `tags``files` .

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o conjunto de dados especificado somente com o solicitado `properties` no corpo.

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
>Propriedades cujos valores recebem o prefixo `@` representam objetos interrelacionados. Consulte a seção do apêndice sobre como [visualizar objetos](appendix.md#view-interrelated-objects) interrelacionados para obter etapas sobre como visualização os detalhes desses objetos.
