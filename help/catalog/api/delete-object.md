---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Excluir um objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 85b497d87fcfb54f390302036ce24c98c6dba6ff

---


# Excluir um objeto

É possível excluir um objeto de Catálogo fornecendo sua ID no caminho de uma solicitação DELETE.

>[!WARNING] Tenha cuidado extra ao excluir objetos, pois isso não pode ser desfeito e pode produzir alterações de quebra em outro lugar na Experience Platform.

**Formato da API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto Catalog a ser excluído. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma matriz que contém a ID do conjunto de dados excluído. Essa ID deve corresponder àquela enviada na solicitação DELETE. A execução de uma solicitação GET no objeto excluído retorna o status HTTP 404 (Não encontrado), confirmando que o conjunto de dados foi excluído com êxito.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] Se nenhum objeto de Catálogo corresponder à ID fornecida em sua solicitação, você ainda poderá receber um Código de status HTTP 200, mas a matriz de respostas ficará vazia.
