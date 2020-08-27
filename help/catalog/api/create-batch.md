---
keywords: Experience Platform;home;popular topics;create batch;catalog service;api
solution: Experience Platform
title: Criar um conjunto de dados
topic: developer guide
description: Para que um conjunto de dados ingira dados, ele deve ter um lote associado a ele. Usando o valor de id de um conjunto de dados existente, é possível criar um lote, fazendo uma solicitação de POST para o ponto de extremidade /lotes na API de catálogo.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 3%

---


# Criar um lote

Para que um conjunto de dados ingira dados, ele deve ter um lote associado a ele. Usando o `id` valor de um conjunto de dados existente, é possível criar um lote, fazendo uma solicitação de POST para o `/batches` endpoint na [!DNL Catalog] API.

**Formato da API**

```HTTP
POST /batches
```

**Solicitação**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `datasetId` | O conjunto `id` de dados ao qual o lote será associado. |

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta que contém detalhes do lote recém-criado, incluindo `id`uma sequência de caracteres gerada pelo sistema, somente leitura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
