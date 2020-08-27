---
keywords: Experience Platform;home;popular topics;catalog;api;replace an object
solution: Experience Platform
title: Substituir um objeto
topic: developer guide
description: É possível substituir o conteúdo de um objeto de Catálogo usando uma solicitação PUT, onde todo o recurso é substituído pela carga da solicitação.
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---


# Substituir um objeto

É possível substituir o conteúdo de um [!DNL Catalog] objeto usando uma solicitação PUT, onde todo o recurso é substituído pela carga da solicitação.

>[!NOTE]
>
>Se for necessário atualizar apenas alguns campos específicos em um [!DNL Catalog] objeto, o uso de uma solicitação de PATCH pode ser mais eficiente.

**Formato da API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser substituído. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir substitui um conjunto de dados pelos valores fornecidos na carga.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Uma resposta bem-sucedida retorna uma matriz que contém a ID do objeto substituído. Essa ID deve corresponder àquela enviada na solicitação de PUT. Executar uma solicitação de GET para esse objeto agora mostra que seus detalhes foram substituídos pelos fornecidos na carga da solicitação de PUT anterior.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
