---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;criar um conjunto de dados;criar conjunto de dados;habilitar conjunto de dados
solution: Experience Platform
title: Criar um conjunto de dados na API
description: Este documento aborda como criar um objeto de conjunto de dados na API de serviço de catálogo.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# Criar um conjunto de dados na API

Para criar um conjunto de dados usando a API [!DNL Catalog], você deve saber o valor `$id` do esquema [!DNL Experience Data Model] (XDM) no qual o conjunto de dados será baseado. Depois de ter a ID do esquema, você pode criar um conjunto de dados fazendo uma solicitação POST para o ponto de extremidade `/datasets` na API [!DNL Catalog].

>[!NOTE]
>
>Este documento aborda apenas como criar um objeto de conjunto de dados no [!DNL Catalog]. Para obter etapas completas sobre como criar, preencher e monitorar um conjunto de dados, consulte este [tutorial](../datasets/create.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schemaRef.id` | O valor do URI `$id` para o esquema XDM no qual o conjunto de dados será baseado. |
| `schemaRef.contentType` | Indica o formato e a versão do esquema. Consulte a seção sobre [controle de versão do esquema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações. |

>[!NOTE]
>
>Este exemplo usa o formato de arquivo [Apache Parquet](https://parquet.apache.org/docs/) para sua propriedade `containerFormat`. Um exemplo que usa o formato de arquivo JSON pode ser encontrado no [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md).

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta que consiste em uma matriz contendo a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma cadeia de caracteres gerada pelo sistema e somente leitura usada para fazer referência ao conjunto de dados em chamadas de API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
