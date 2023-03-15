---
keywords: Experience Platform;página inicial;tópicos populares;criar lote;serviço de catálogo;api
solution: Experience Platform
title: Criar um lote na API
description: Você pode criar um lote fazendo uma solicitação POST para o endpoint /batches na API de catálogo.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 5%

---

# Criar um lote

Para que um conjunto de dados assimile dados, ele deve ter um lote associado a ele. Usar o `id` de um conjunto de dados existente, é possível criar um lote fazendo uma solicitação POST para o `/batches` endpoint na variável [!DNL Catalog] API.

**Formato da API**

```HTTP
POST /batches
```

**Solicitação**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `datasetId` | A variável `id` do conjunto de dados ao qual o lote será associado. |

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta contendo detalhes do lote recém-criado, incluindo seu `id`, uma sequência de caracteres gerada pelo sistema somente leitura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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
