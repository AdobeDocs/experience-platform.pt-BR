---
keywords: Experience Platform, home, tópicos populares, conjunto de dados, conjunto de dados, criar um conjunto de dados, criar conjunto de dados, ativar conjunto de dados
solution: Experience Platform
title: Criar um conjunto de dados na API
topic-legacy: developer guide
description: Este documento aborda como criar um objeto de conjunto de dados na API do Serviço de catálogo.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 75426b1ddc16af39eb6c423027fac7d4d0e21c6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 2%

---

# Criar um conjunto de dados na API

Para criar um conjunto de dados usando o [!DNL Catalog] Você deve conhecer a API do `$id` do [!DNL Experience Data Model] (XDM) no qual o conjunto de dados será baseado. Depois de ter a ID do esquema, você pode criar um conjunto de dados, fazendo uma solicitação de POST para a `/datasets` endpoint no [!DNL Catalog] API.

>[!NOTE]
>
>Este documento aborda apenas como criar um objeto de conjunto de dados em [!DNL Catalog]. Para obter as etapas completas sobre como criar, preencher e monitorar um conjunto de dados, consulte o seguinte [tutorial](../datasets/create.md).

**Formato da API**

```HTTP
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um conjunto de dados que faz referência a um esquema definido anteriormente.

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
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do conjunto de dados a ser criado. |
| `schemaRef.id` | O URI `$id` para o esquema XDM, o conjunto de dados será baseado. |
| `schemaRef.contentType` | Indica o formato e a versão do esquema. Consulte a seção sobre [versão do schema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações. |

>[!NOTE]
>
>Esse exemplo usa a variável [Apache Parquet](https://parquet.apache.org/docs/) formato de arquivo para `containerFormat` propriedade. Um exemplo que usa o formato de arquivo JSON pode ser encontrado no [guia do desenvolvedor de ingestão em lote](../../ingestion/batch-ingestion/api-overview.md).

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta que consiste em uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma string gerada pelo sistema e somente leitura, usada para fazer referência ao conjunto de dados nas chamadas de API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
