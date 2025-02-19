---
keywords: Experience Platform;página inicial;tópicos populares;catálogo;api;atualizar um objeto
solution: Experience Platform
title: Atualizar um objeto de catálogo
description: Você pode atualizar parte de um objeto de Catálogo incluindo a respectiva ID no caminho de uma solicitação PATCH. Este documento aborda o uso de campos e a utilização da notação JSON Patch para executar operações do PATCH em objetos de catálogo.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Atualizar um objeto de Catálogo

Você pode atualizar parte de um objeto [!DNL Catalog] incluindo a respectiva ID no caminho de uma solicitação PATCH. Este documento aborda os dois métodos para executar operações do PATCH em objetos de catálogo:

* Uso de campos
* Uso da notação de patch de JSON

>[!NOTE]
>
>As operações do PATCH em um objeto não podem modificar seus campos expansíveis, que representam objetos inter-relacionados. As modificações em objetos inter-relacionados devem ser feitas diretamente.

## Atualizar usando campos

O exemplo de chamada a seguir demonstra como atualizar um objeto usando campos e valores.

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser atualizado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os campos `name` e `description` de um conjunto de dados para os valores fornecidos na carga. Os campos de objeto que não devem ser atualizados podem ser excluídos da carga.

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

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A execução de uma solicitação GET para esse conjunto de dados agora mostra que apenas `name` e `description` foram atualizados, enquanto todos os outros valores permanecem inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Atualizar usando a notação JSON Patch {#patch-notation}

O exemplo de chamada a seguir demonstra como atualizar um objeto usando o JSON Patch, conforme descrito em [RFC-6902](https://tools.ietf.org/html/rfc6902).

Para obter mais informações sobre a sintaxe do patch de JSON, consulte o [guia de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

**Formato da API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser atualizado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | O identificador do objeto específico que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os campos `name` e `description` de um conjunto de dados para os valores fornecidos em cada objeto de patch JSON. Ao usar o patch de JSON, você também deve definir o cabeçalho Content-Type como `application/json-patch+json`.

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

Uma resposta bem-sucedida retorna uma matriz que contém a ID do objeto atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A execução de uma solicitação GET para este objeto agora mostra que apenas o `name` e `description` foram atualizados, enquanto todos os outros valores permanecem inalterados.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Atualizar usando a notação PATCH v2 {#patch-v2-notation}

O ponto de extremidade `/v2/dataSets/{DATASET_ID}` fornece uma maneira mais flexível de atualizar atributos de conjunto de dados complexos ou profundamente aninhados.

Normalmente, quando você atualiza um campo profundamente aninhado (como `a.b.c.d`), cada nível no caminho já deve existir. Se qualquer nível estiver ausente, você deverá criar manualmente cada um antes de definir o valor final. Isso geralmente requer várias operações, o que adiciona complexidade e aumenta a chance de erros.

O ponto de extremidade `/v2/dataSets/{DATASET_ID}` cria automaticamente todos os níveis ausentes no caminho. Em vez de verificar e adicionar manualmente `b` e `c` antes de configurar `d`, a operação `v2` do PATCH faz isso para você.

Ao enviar uma solicitação PATCH para o ponto de extremidade `/v2/dataSets/{DATASET_ID}`, você só precisará enviar a estrutura final, e o sistema preencherá as partes ausentes antes de aplicar a atualização.

>[!NOTE]
>
>`If-Match` e `If-None-Match` cabeçalhos são opcionais para o ponto de extremidade `/v2/dataSets/{id}`. As solicitações do PATCH para esse endpoint mesclam dinamicamente as atualizações, permitindo modificações sem recuperar a versão mais recente do conjunto de dados. Embora isso reduza o risco de perda de dados devido a atualizações simultâneas, você pode usar o `If-Match` com o `etag` mais recente para garantir que as alterações se apliquem apenas a uma versão específica. Como alternativa, `If-None-Match` impede atualizações se o conjunto de dados não tiver sido alterado desde a última versão conhecida.

**Formato da API**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O identificador do conjunto de dados a ser atualizado. |

**Solicitação**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados atualizado, que deve corresponder à ID enviada na solicitação do PATCH. A execução de uma solicitação GET para este objeto agora mostra que o objeto `extensions.adobe_lakeHouse.rowExpiration` foi criado sem a necessidade de etapas anteriores de criação manual.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### Um exemplo de conjunto de dados antes e depois da atualização

O exemplo de JSON abaixo ilustra a estrutura do conjunto de dados **antes** da solicitação PATCH, em que o objeto `extensions.adobe_lakeHouse.rowExpiration` não está presente no conjunto de dados.

+++Selecione para exibir o exemplo

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

O JSON a seguir mostra a estrutura do conjunto de dados **após** a solicitação do PATCH. A atualização cria automaticamente o objeto `extensions.adobe_lakeHouse.rowExpiration` ausente sem etapas de criação manual anteriores. Este exemplo demonstra como a solicitação do PATCH `/v2/` elimina a necessidade de várias operações, tornando as atualizações mais simples e eficientes.


+++Selecione para exibir o exemplo

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
