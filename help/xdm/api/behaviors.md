---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro de esquema, Registro de esquema, comportamento, comportamentos, comportamentos, comportamentos, comportamentos;
solution: Experience Platform
title: Comportamento do ponto de extremidade da API
description: O endpoint /comporors na API do Registro de Schema permite recuperar todos os comportamentos disponíveis no contêiner global.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 6%

---

# Ponto de extremidade de comportamentos

No Experience Data Model (XDM), os comportamentos definem a natureza dos dados que um esquema descreve. Cada classe XDM deve referenciar um comportamento específico, que todos os esquemas que empregam essa classe herdarão. Para quase todos os casos de uso na Platform, há dois comportamentos disponíveis:

* **[!UICONTROL Registro]**: Fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.
* **[!UICONTROL Série cronológica]**: Fornece um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de registro.

>[!NOTE]
>
>Há alguns casos de uso na Platform que exigem o uso de um esquema que não emprega nenhum dos comportamentos acima. Nesses casos, um terceiro comportamento &quot;ad-hoc&quot; está disponível. Veja o tutorial em [criação de um schema ad hoc](../tutorials/ad-hoc.md) para obter mais informações.
>
>Para obter informações mais gerais sobre comportamentos de dados em termos de como eles afetam a composição do schema, consulte o guia no [noções básicas da composição do schema](../schema/composition.md).

O `/behaviors` endpoint no [!DNL Schema Registry] A API permite exibir os comportamentos disponíveis na variável `global` contêiner.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de comportamentos {#list}

Você pode recuperar uma lista de todos os comportamentos disponíveis, fazendo uma solicitação do GET para o `/behaviors` endpoint .

**Formato da API**

```http
GET /global/behaviors
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Resposta**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Pesquisar um comportamento {#lookup}

Você pode pesquisar um comportamento específico fornecendo a ID no caminho de uma solicitação do GET para o `/behaviors` endpoint .

**Formato da API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BEHAVIOR_ID}` | O `meta:altId` ou codificado por URL `$id` do comportamento que você deseja procurar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera os detalhes do comportamento do registro fornecendo `meta:altId` no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do comportamento, incluindo sua versão, descrição e os atributos que o comportamento fornece às classes que o utilizam.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Próximas etapas

Este guia cobriu o uso do `/behaviors` endpoint no [!DNL Schema Registry] API. Para saber como atribuir um comportamento a uma classe usando a API, consulte [guia de endpoint de classes](./classes.md).
