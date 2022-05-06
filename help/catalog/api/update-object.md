---
keywords: Experience Platform, home, tópicos populares, catálogo, api, atualizar um objeto
solution: Experience Platform
title: Atualizar um objeto de catálogo
topic-legacy: developer guide
description: Você pode atualizar parte de um objeto de Catálogo incluindo sua ID no caminho de uma solicitação de PATCH. Este documento aborda o uso de campos e a notação de Patch JSON para executar operações de PATCH em objetos do catálogo.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---

# Atualizar um objeto de catálogo

Você pode atualizar parte de um [!DNL Catalog] ao incluir sua ID no caminho de uma solicitação de PATCH. Este documento aborda os dois métodos para executar operações de PATCH em objetos do catálogo:

* Uso de campos
* Uso da notação de patch JSON

>[!NOTE]
>
>As operações de PATCH em um objeto não podem modificar seus campos expansíveis, que representam objetos inter-relacionados. As modificações em objetos interrelacionados devem ser feitas diretamente.

## Atualizar usando campos

A chamada de exemplo a seguir demonstra como atualizar um objeto usando campos e valores.

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser atualizado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza o `name` e `description` campos de um conjunto de dados para os valores fornecidos no payload. Os campos de objeto que não devem ser atualizados podem ser excluídos da carga útil.

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

Uma resposta bem-sucedida retorna uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A execução de uma solicitação do GET para esse conjunto de dados agora mostra que somente a variável `name` e `description` foram atualizados enquanto todos os outros valores permaneciam inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Atualizar usando a notação de patch JSON

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
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser atualizado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza o `name` e `description` campos de um conjunto de dados para os valores fornecidos em cada objeto de patch JSON. Ao usar o Patch JSON, você também deve definir o cabeçalho Content-Type como `application/json-patch+json`.

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

Uma resposta bem-sucedida retorna uma matriz contendo a ID do objeto atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A execução de uma solicitação de GET para esse objeto agora mostra que somente a variável `name` e `description` foram atualizados enquanto todos os outros valores permaneciam inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
