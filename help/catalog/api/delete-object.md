---
keywords: Experience Platform;página inicial;tópicos populares;excluir um objeto;serviço de catálogo;api
solution: Experience Platform
title: Excluir um objeto na API
description: Você pode excluir um objeto de Catálogo fornecendo a respectiva ID no caminho de uma solicitação DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 2%

---

# Excluir um objeto na API

Você pode excluir um objeto [!DNL Catalog] fornecendo a respectiva ID no caminho de uma solicitação DELETE.

>[!WARNING]
>
>Tenha cuidado extra ao excluir objetos, pois essa ação não pode ser desfeita e pode produzir alterações de quebra em outro lugar no [!DNL Experience Platform].

**Formato da API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>O ponto de extremidade `DELETE /batches/{ID}` foi substituído. Para excluir um lote, você deve usar a [API de assimilação de lote](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser excluído. Os objetos válidos são: <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir exclui um conjunto de dados cuja ID está especificada no caminho da solicitação.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados excluído. Essa ID deve corresponder à enviada na solicitação DELETE. A execução de uma solicitação GET no objeto excluído retorna o status HTTP 404 (Não encontrado), confirmando que o conjunto de dados foi excluído com sucesso.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Se nenhum objeto [!DNL Catalog] corresponder à ID fornecida em sua solicitação, você ainda poderá receber um Código de status HTTP 200, mas a matriz de resposta estará vazia.
