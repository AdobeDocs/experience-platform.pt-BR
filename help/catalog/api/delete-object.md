---
keywords: Experience Platform;home;popular topics;excluir um objeto;serviço de catálogo;api
solution: Experience Platform
title: Excluir um objeto na API
topic: developer guide
description: É possível excluir um objeto de Catálogo fornecendo sua ID no caminho de uma solicitação de DELETE.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---


# Excluir um objeto na API

Você pode excluir um objeto [!DNL Catalog] fornecendo sua ID no caminho de uma solicitação de DELETE.

>[!WARNING]
>
>Tenha cuidado extra ao excluir objetos, pois isso não pode ser desfeito e pode produzir alterações de quebra em [!DNL Experience Platform].

**Formato da API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>O ponto de extremidade `DELETE /batches/{ID}` foi substituído. Para excluir um lote, você deve estar usando a [API de ingestão em lote](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser excluído. Objetos válidos são: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir exclui um conjunto de dados cuja ID é especificada no caminho da solicitação.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma matriz que contém a ID do conjunto de dados excluído. Essa ID deve corresponder àquela enviada na solicitação de DELETE. A execução de uma solicitação de GET no objeto excluído retorna o status HTTP 404 (Não encontrado), confirmando que o conjunto de dados foi excluído com êxito.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Se nenhum objeto [!DNL Catalog] corresponder à ID fornecida em sua solicitação, você ainda poderá receber um Código de status HTTP 200, mas a matriz de resposta ficará vazia.
