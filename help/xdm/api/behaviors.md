---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;comportamento;comportamento;comportamentos;comportamentos;
solution: Experience Platform
title: Endpoint da API de comportamentos
description: O ponto de extremidade /behavior na API do Registro de esquema permite recuperar todos os comportamentos disponíveis no contêiner global.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 3%

---

# Endpoint de comportamentos

No Experience Data Model (XDM), os comportamentos definem a natureza dos dados que um esquema descreve. Cada classe XDM deve fazer referência a um comportamento específico, que todos os esquemas que empregam essa classe herdarão. Para quase todos os casos de uso na Platform, há dois comportamentos disponíveis:

* **[!UICONTROL Registro]**: fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.
* **[!UICONTROL Série temporal]**: fornece um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um assunto do registro.

>[!NOTE]
>
>Há alguns casos de uso na Platform que exigem o uso de um esquema que não emprega nenhum dos comportamentos acima. Para esses casos, um terceiro comportamento &quot;ad-hoc&quot; está disponível. Consulte o tutorial sobre [criação de um esquema ad-hoc](../tutorials/ad-hoc.md) para obter mais informações.
>
>Para obter informações mais gerais sobre comportamentos de dados em termos de como eles afetam a composição do esquema, consulte o manual sobre as [noções básicas da composição do esquema](../schema/composition.md).

O ponto de extremidade `/behaviors` na API [!DNL Schema Registry] permite exibir os comportamentos disponíveis no contêiner `global`.

## Introdução

O ponto de extremidade usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas para qualquer API Experience Platform com êxito.

## Recuperar uma lista de comportamentos {#list}

Você pode recuperar uma lista de todos os comportamentos disponíveis fazendo uma solicitação GET para o ponto de extremidade `/behaviors`.

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

Você pode pesquisar um comportamento específico fornecendo a respectiva ID no caminho de uma solicitação GET para o ponto de extremidade `/behaviors`.

**Formato da API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BEHAVIOR_ID}` | O `meta:altId` ou o `$id` codificado na URL do comportamento que você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera os detalhes do comportamento do registro fornecendo seu `meta:altId` no caminho da solicitação.

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

Este guia abordou o uso do ponto de extremidade `/behaviors` na API [!DNL Schema Registry]. Para saber como atribuir um comportamento a uma classe usando a API, consulte o [manual de ponto de extremidade de classes](./classes.md).
