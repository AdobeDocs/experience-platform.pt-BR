---
keywords: Experience Platform;página inicial;tópicos populares;catálogo;api;atualizar um objeto
solution: Experience Platform
title: Atualizar um objeto de catálogo
description: Você pode atualizar parte de um objeto de Catálogo incluindo a respectiva ID no caminho de uma solicitação PATCH. Este documento aborda o uso de campos e a utilização da notação JSON Patch para executar operações PATCH em objetos de Catálogo.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---

# Atualizar um objeto de Catálogo

Você pode atualizar parte de um [!DNL Catalog] incluindo a respectiva ID no caminho de uma solicitação PATCH. Este documento aborda os dois métodos para executar operações de PATCH em objetos de Catálogo:

* Uso de campos
* Uso da notação de patch de JSON

>[!NOTE]
>
>as operações de PATCH em um objeto não podem modificar seus campos expansíveis, que representam objetos inter-relacionados. As modificações em objetos inter-relacionados devem ser feitas diretamente.

## Atualizar usando campos

O exemplo de chamada a seguir demonstra como atualizar um objeto usando campos e valores.

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser atualizado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza o `name` e `description` de um conjunto de dados aos valores fornecidos na carga. Os campos de objeto que não devem ser atualizados podem ser excluídos da carga.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A execução de uma solicitação GET para esse conjunto de dados agora mostra que somente o `name` e `description` foram atualizadas, enquanto todos os outros valores permanecem inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Atualizar usando a notação JSON Patch

O exemplo de chamada a seguir demonstra como atualizar um objeto usando o JSON Patch, conforme descrito em [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser atualizado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza o `name` e `description` de um conjunto de dados aos valores fornecidos em cada objeto JSON Patch. Ao usar o patch de JSON, você também deve definir o cabeçalho Content-Type como `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do objeto atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A execução de uma solicitação GET para esse objeto agora mostra que somente o `name` e `description` foram atualizadas, enquanto todos os outros valores permanecem inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
