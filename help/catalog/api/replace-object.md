---
keywords: Experience Platform, home, tópicos populares, catálogo, api, substituir um objeto
solution: Experience Platform
title: Substituir um objeto de catálogo
topic-legacy: developer guide
description: Você pode substituir o conteúdo de um objeto de Catálogo usando uma solicitação de PUT, onde todo o recurso é substituído pela carga da solicitação.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 3%

---

# Substituir um objeto de catálogo

Você pode substituir o conteúdo de um [!DNL Catalog] objeto que usa uma solicitação PUT, onde todo o recurso é substituído pela carga da solicitação.

>[!NOTE]
>
>Se você precisar apenas atualizar alguns campos específicos em um [!DNL Catalog] , o uso de uma solicitação PATCH pode ser mais eficiente.

**Formato da API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser substituído. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir substitui um conjunto de dados pelos valores fornecidos no payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID do objeto substituído. Essa ID deve corresponder à enviada na solicitação PUT. Executar uma solicitação de GET para esse objeto agora mostra que seus detalhes foram substituídos pelos fornecidos na carga da solicitação de PUT anterior.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
