---
keywords: Experience Platform;home;popular topics;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: Criar um conjunto de dados
topic: developer guide
description: Este documento aborda como criar um objeto de conjunto de dados no Catálogo.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---


# Criar um conjunto de dados

Para criar um conjunto de dados usando a [!DNL Catalog] API, é necessário saber o `$id` valor do schema [!DNL Experience Data Model] (XDM) no qual o conjunto de dados será baseado. Depois de ter a ID do schema, você pode criar um conjunto de dados, solicitando um POST para o `/datasets` endpoint na [!DNL Catalog] API.

>[!NOTE]
>
>Este documento só aborda como criar um objeto de conjunto de dados no [!DNL Catalog]. Para obter as etapas completas sobre como criar, preencher e monitorar um conjunto de dados, consulte o [tutorial](../datasets/create.md)a seguir.

**Formato da API**

```HTTP
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um conjunto de dados que faz referência a um schema definido anteriormente.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do conjunto de dados a ser criado. |
| `schemaRef.id` | O `$id` valor de URI para o schema XDM no qual o conjunto de dados será baseado. |

>[!NOTE]
>
>Este exemplo usa o formato de arquivo [parquet](https://parquet.apache.org/documentation/latest/) para sua `containerFormat` propriedade. Um exemplo que usa o formato de arquivo JSON pode ser encontrado no guia [do desenvolvedor de ingestão em](../../ingestion/batch-ingestion/api-overview.md)lote.

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta que consiste em uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma sequência de caracteres somente leitura, gerada pelo sistema, usada para fazer referência ao conjunto de dados em chamadas de API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
