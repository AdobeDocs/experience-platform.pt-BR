---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;modelo de dados de experiência;Modelo de dados de experiência;Modelo de dados;Modelo de dados;Modelo de dados;Registro do schema;comportamento;comportamentos;comportamentos;comportamentos;comportamento;comportamentos;comportamento;comportamento;comportamento;comportamento;Schema;home;popular topics;api;API;XDM;system;experience data model;Experience Data Model;data model;
solution: Experience Platform
title: Comportamento do Ponto Final da API
description: O endpoint /comporors na API do Registro de Schemas permite recuperar todos os comportamentos disponíveis no container global.
topic: developer guide
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


# Ponto de extremidade de comportamento

No Experience Data Model (XDM), os comportamentos definem a natureza dos dados que um schema descreve. Cada classe XDM deve fazer referência a um comportamento específico, que todos os schemas que empregam essa classe herdarão. Para quase todos os casos de uso na Plataforma, há dois comportamentos disponíveis:

* **[!UICONTROL Registro]**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **[!UICONTROL Séries]** cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

>[!NOTE]
>
>Há alguns casos de uso na Plataforma que exigem o uso de schema que não emprega nenhum dos comportamentos acima. Para esses casos, um terceiro comportamento &quot;ad-hoc&quot; está disponível. Consulte o tutorial em [criar um schema ad-hoc](../tutorials/ad-hoc.md) para obter mais informações.
>
>Para obter informações mais gerais sobre os comportamentos de dados em termos de como eles afetam a composição do schema, consulte o guia sobre [noções básicas de composição do schema](../schema/composition.md).

O endpoint `/behaviors` na API [!DNL Schema Registry] permite que você visualização os comportamentos disponíveis no container `global`.

## Introdução

O endpoint usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de comportamentos {#list}

Você pode recuperar uma lista de todos os comportamentos disponíveis, fazendo uma solicitação de GET para o terminal `/behaviors`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Procure um comportamento {#lookup}

Você pode procurar um comportamento específico fornecendo sua ID no caminho de uma solicitação de GET para o terminal `/behaviors`.

**Formato da API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BEHAVIOR_ID}` | O `meta:altId` ou `$id` codificado por URL do comportamento que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera os detalhes do comportamento do registro fornecendo seu `meta:altId` no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do comportamento, incluindo sua versão, descrição e os atributos que o comportamento fornece às classes que o empregam.

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

Este guia cobriu o uso do terminal `/behaviors` na API [!DNL Schema Registry]. Para saber como atribuir um comportamento a uma classe usando a API, consulte o [guia de ponto de extremidade de classes](./classes.md).