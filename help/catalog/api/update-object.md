---
keywords: Experience Platform;home;popular topics;catalog;api;update an object
solution: Experience Platform
title: Atualizar um objeto
topic: developer guide
description: 'É possível atualizar parte de um objeto de Catálogo incluindo sua ID no caminho de uma solicitação de PATCH. Este documento aborda o uso de campos e a notação de Patch JSON para executar operações de PATCH em objetos de Catálogo. '
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 3%

---


# Atualizar um objeto

É possível atualizar parte de um [!DNL Catalog] objeto incluindo sua ID no caminho de uma solicitação de PATCH. Este documento aborda os dois métodos para executar operações de PATCH em objetos do Catálogo:

* Uso de campos
* Uso da notação de Patch JSON

>[!NOTE]
>
>As operações de PATCH em um objeto não podem modificar seus campos expansíveis, que representam objetos inter-relacionados. As modificações a objetos interrelacionados devem ser feitas diretamente.

## Atualizar usando campos

A chamada de exemplo a seguir demonstra como atualizar um objeto usando campos e valores.

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser atualizado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os campos `name` e `description` de um conjunto de dados para os valores fornecidos na carga. Campos de objeto que não devem ser atualizados podem ser excluídos da carga.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados atualizado. Essa ID deve corresponder àquela enviada na solicitação de PATCH. A execução de uma solicitação de GET para este conjunto de dados agora mostra que somente os valores `name` e `description` foram atualizados enquanto todos os outros valores permanecem inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Atualizar usando notação de Patch JSON

A chamada de exemplo a seguir demonstra como atualizar um objeto usando o Patch JSON, conforme descrito em [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser atualizado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os campos `name` e `description` de um conjunto de dados para os valores fornecidos em cada objeto de Patch JSON. Ao usar o Patch JSON, você também deve definir o cabeçalho Content-Type como `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do objeto atualizado. Essa ID deve corresponder àquela enviada na solicitação de PATCH. A execução de uma solicitação de GET para esse objeto agora mostra que somente os valores `name` e `description` foram atualizados enquanto todos os outros valores permanecem inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
