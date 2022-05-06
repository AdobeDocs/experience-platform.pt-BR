---
keywords: Experience Platform, home, tópicos populares, excluir um objeto, serviço de catálogo, api
solution: Experience Platform
title: Excluir um objeto na API
topic-legacy: developer guide
description: Você pode excluir um objeto de Catálogo fornecendo sua ID no caminho de uma solicitação de DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 2%

---

# Excluir um objeto na API

Você pode excluir um [!DNL Catalog] ao fornecer a ID no caminho de uma solicitação de DELETE.

>[!WARNING]
>
>Tenha cuidado extra ao excluir objetos, pois isso não pode ser desfeito e pode produzir alterações de quebra em outro local do [!DNL Experience Platform].

**Formato da API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>O `DELETE /batches/{ID}` endpoint foi descontinuado. Para excluir um lote, você deve usar a variável [API de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser excluído. Os objetos válidos são: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir exclui um conjunto de dados cuja ID esteja especificada no caminho da solicitação.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados excluído. Essa ID deve corresponder à enviada na solicitação DELETE. A execução de uma solicitação do GET no objeto excluído retorna o status HTTP 404 (Não encontrado), confirmando que o conjunto de dados foi excluído com êxito.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Se não [!DNL Catalog] objetos que correspondem à ID fornecida em sua solicitação, você ainda pode receber um Código de status HTTP 200, mas a matriz de resposta estará vazia.
