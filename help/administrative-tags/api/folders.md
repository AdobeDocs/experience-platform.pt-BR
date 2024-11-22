---
title: Ponto de Extremidade de Pastas
description: Saiba como criar, atualizar, gerenciar e excluir pastas usando as APIs do Adobe Experience Platform.
role: Developer
exl-id: ee43d699-725d-4ffd-a71b-049eeb3b4d7c
source-git-commit: 78aa48701abaadea963b25e390aa96d7b31386f4
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 5%

---

# Ponto de extremidade de pastas

>[!IMPORTANT]
>
>A URL do ponto de extremidade para este conjunto de pontos de extremidade é `https://experience.adobe.io`.

As pastas são um recurso que permite organizar melhor os objetos de negócios para facilitar a navegação e a categorização.

Este guia fornece informações para ajudar você a entender melhor as pastas e inclui chamadas de API de exemplo para executar ações básicas usando a API.

## Introdução

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo da API.

## Recuperar uma lista de pastas {#list}

Você pode recuperar uma lista de pastas que pertencem à sua organização fazendo uma solicitação GET para o ponto de extremidade `/folder` e especificando o tipo de pasta e a ID da pasta pai.

**Formato da API**

```http
GET /folders/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FOLDER_TYPE}` | O tipo de objetos contidos na pasta. Os valores suportados incluem `segment` e `dataset`. |
| `{PARENT_FOLDER_ID}` | A ID da pasta pai da qual você está recuperando a lista de pastas. Para exibir uma lista de todas as pastas pai, use a ID de pasta `root`. |

**Solicitação**

+++Uma solicitação de amostra para listar todas as pastas de conjunto de dados de nível superior

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de todas as pastas de nível superior para o conjunto de dados na organização.

+++Uma resposta de amostra que contém uma lista de todas as pastas de nível superior para o conjunto de dados na organização.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Criar uma nova pasta {#create}

Você pode criar uma nova pasta fazendo uma solicitação POST para o ponto de extremidade `/folder` e especificando o tipo de pasta.

**Formato da API**

```http
POST /folders/{FOLDER_TYPE}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FOLDER_TYPE}` | O tipo de objetos contidos na pasta. Os valores suportados incluem `segment` e `dataset`. |

**Solicitação**

+++Uma solicitação de exemplo para criar uma nova pasta.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folders/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da pasta que você deseja criar. |
| `parentId` | A ID da pasta pai. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da pasta recém-criada.

+++Uma resposta de amostra que contém detalhes da pasta recém-criada.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID da pasta recém-criada. |
| `createdBy` | A ID do usuário que criou a pasta. |
| `createdAt` | O carimbo de data e hora de quando a pasta foi criada. |
| `modifiedBy` | A ID do usuário que modificou a pasta pela última vez. |
| `modifiedAt` | O carimbo de data e hora de quando a pasta foi atualizada pela última vez. |

+++

## Recuperar uma pasta específica {#get}

Você pode recuperar uma pasta específica que pertença à sua organização fazendo uma solicitação GET para o ponto de extremidade `/folder` e especificando o tipo de pasta e a ID da pasta.

**Formato da API**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FOLDER_TYPE}` | O tipo de objetos contidos na pasta. Os valores suportados incluem `segment` e `dataset`. |
| `{FOLDER_ID}` | A ID da pasta que você está recuperando. |

**Solicitação**

+++Uma solicitação de amostra para recuperar uma pasta específica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da pasta solicitada.

+++Uma resposta de amostra que contém detalhes da pasta solicitada.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID da pasta solicitada. |
| `name` | O nome da pasta solicitada. |
| `parentId` | A ID da pasta pai. |
| `createdBy` | A ID do usuário que criou a pasta. |
| `createdAt` | O carimbo de data e hora de quando a pasta foi criada. |
| `modifiedBy` | A ID do usuário que atualizou a pasta pela última vez. |
| `modifiedAt` | O carimbo de data e hora de quando a pasta foi atualizada pela última vez. |
| `status` | O status da pasta solicitada. Os valores suportados incluem `IN_USE` e `ARCHIVED`. |

+++

## Validar uma pasta especificada {#validate}

Você pode validar se uma pasta está qualificada para ter objetos fazendo uma solicitação GET para o ponto de extremidade `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` e fornecer o tipo e a ID da pasta.

**Formato da API**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FOLDER_TYPE}` | O tipo de objetos contidos na pasta. Os valores suportados incluem `segment` e `dataset`. |
| `{FOLDER_ID}` | A ID da pasta que você está validando. |

**Solicitação**

+++Uma solicitação de exemplo para validar uma pasta específica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Um status bem-sucedido retorna o status HTTP 200 com detalhes da pasta que você está validando.

+++Uma resposta de amostra contém detalhes da pasta validada

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Atualizar uma pasta específica {#update}

Você pode atualizar os detalhes de uma pasta específica que pertence à sua organização fazendo uma solicitação PATCH para o ponto de extremidade `/folder` e especificando o tipo de pasta e a ID da pasta.

**Formato da API**

```http
PATCH /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FOLDER_TYPE}` | O tipo de objetos contidos na pasta. Os valores suportados incluem `segment` e `dataset`. |
| `{FOLDER_ID}` | A ID da pasta que você está atualizando. |

**Solicitação**

+++Uma solicitação de amostra para atualizar uma pasta específica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre a pasta recém-atualizada.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Excluir uma pasta específica {#delete}

Você pode excluir uma pasta específica que pertence à sua organização fazendo uma solicitação DELETE para o `/folder` e especificando o tipo de pasta e a ID da pasta.

***Formato de API**

```http
DELETE /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FOLDER_TYPE}` | O tipo de objetos contidos na pasta. Os valores suportados incluem `segment` e `dataset`. |
| `{FOLDER_ID}` | A ID da pasta que você está excluindo. |

**Solicitação**

+++Uma solicitação de amostra para excluir uma pasta específica

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com um corpo de mensagem que informa sobre a exclusão da pasta.

```json
{
    "message": "delete request accepted successfully"
}
```

## Próximas etapas

Depois de ler este guia, você compreenderá melhor como criar, gerenciar e excluir pastas usando a API do Adobe Experience Platform.
