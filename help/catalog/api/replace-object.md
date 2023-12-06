---
keywords: Experience Platform;página inicial;tópicos populares;catálogo;api;substituir um objeto
solution: Experience Platform
title: Substituir um objeto de catálogo
description: Você pode substituir o conteúdo de um objeto de Catálogo usando uma solicitação PUT, em que o recurso inteiro é substituído pela carga da solicitação.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 3%

---

# Substituir um objeto de catálogo

É possível substituir o conteúdo de um [!DNL Catalog] objeto usando uma solicitação PUT, em que todo o recurso é substituído pela carga da solicitação.

>[!NOTE]
>
>Se você precisar apenas atualizar alguns campos específicos em um [!DNL Catalog] objeto, o uso de uma solicitação PATCH pode ser mais eficiente.

**Formato da API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser substituído. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir substitui um conjunto de dados pelos valores fornecidos na carga.

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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do objeto substituído. Essa ID deve corresponder à enviada na solicitação PUT. A execução de uma solicitação GET para esse objeto agora mostra que seus detalhes foram substituídos pelos fornecidos na carga da solicitação PUT anterior.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
