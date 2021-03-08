---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, modelo de dados de experiência, Modelo de dados da experiência, modelo de dados, Modelo de dados, sampledata, dados de amostra, rpc;
solution: Experience Platform
title: Endpoint da API de dados de exemplo
description: O endpoint /sampledata na API do Registro de Schema permite gerar dados de amostra mapeados para a estrutura de qualquer esquema XDM existente.
topic: guia do desenvolvedor
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---


# Ponto de extremidade de dados de amostra

Para assimilar dados na Adobe Experience Platform, o formato e a estrutura dos dados devem estar em conformidade com um esquema do Experience Data Model (XDM) existente. Dependendo da complexidade do esquema para um conjunto de dados específico, pode ser difícil determinar a forma exata dos dados que o conjunto de dados espera ao assimilar.

Usando o endpoint `/sampledata` na API [!DNL Schema Registry], é possível gerar um objeto de assimilação de exemplo para qualquer schema criado anteriormente.

## Introdução

O endpoint usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da Experience Platform.

O ponto de extremidade de dados de amostra faz parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Ao contrário de outros endpoints na API [!DNL Schema Registry], os endpoints RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type` e não usam um `CONTAINER_ID`. Em vez disso, eles devem usar o namespace `/rpc`, conforme demonstrado na chamada de API abaixo.

## Recuperar dados de amostra de um esquema

Você pode recuperar dados de amostra de qualquer esquema na Biblioteca de esquemas especificando a ID do esquema no caminho de uma solicitação GET para o endpoint.

**Formato da API**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou `$id` codificado por URL do esquema para o qual você deseja gerar dados de amostra. |

**Solicitação**

A solicitação a seguir gera dados de amostra para um esquema de Membros de Fidelidade.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna um objeto de dados de amostra para o esquema especificado.

```json
{
    "@id": "/uri-reference",
    "_{TENANT_ID}": {
        "favoriteHotel": "string",
        "loyalty": {
            "loyaltyId": "string",
            "loyaltyLevel": "string",
            "loyaltyPoints": 4862,
            "memberSince": "2018-11-12T20:20:39+00:00"
        }
    },
    "repo:createDate": "2004-10-23T12:00:00-06:00",
    "repo:modifyDate": "2004-10-23T12:00:00-06:00",
    "xdm:createdByBatchID": "/uri-reference",
    "xdm:faxPhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:homeAddress": {
        "@id": "/uri-reference",
        "repo:createDate": "2004-10-23T12:00:00-06:00",
        "repo:modifyDate": "2004-10-23T12:00:00-06:00",
        "schema:description": "string",
        "schema:elevation": 31148.05,
        "schema:latitude": 29.25,
        "schema:longitude": -145.42,
        "xdm:city": "string",
        "xdm:country": "string",
        "xdm:countryCode": "US",
        "xdm:createdByBatchID": "/uri-reference",
        "xdm:dmaID": 1612,
        "xdm:label": "string",
        "xdm:lastVerifiedDate": "2018-01-12",
        "xdm:modifiedByBatchID": "/uri-reference",
        "xdm:msaID": 26375,
        "xdm:postOfficeBox": "string",
        "xdm:postalCode": "string",
        "xdm:primary": false,
        "xdm:region": "string",
        "xdm:repositoryCreatedBy": "string",
        "xdm:repositoryLastModifiedBy": "string",
        "xdm:state": "string",
        "xdm:stateProvince": "US-CA",
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:street1": "string",
        "xdm:street2": "string",
        "xdm:street3": "string",
        "xdm:street4": "string"
    },
    "xdm:homePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:identityMap": {
        "key": [
            {
                "xdm:authenticatedState": "ambiguous",
                "xdm:id": "string",
                "xdm:primary": false
            }
        ]
    },
    "xdm:mobilePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:modifiedByBatchID": "/uri-reference",
    "xdm:person": {
        "xdm:birthDate": "2018-01-12",
        "xdm:birthDayAndMonth": "01-23",
        "xdm:birthYear": 6427,
        "xdm:gender": "not_specified",
        "xdm:maritalStatus": "not_specified",
        "xdm:name": {
            "xdm:courtesyTitle": "string",
            "xdm:firstName": "string",
            "xdm:fullName": "string",
            "xdm:lastName": "string",
            "xdm:middleName": "string",
            "xdm:suffix": "string"
        },
        "xdm:nationality": "US",
        "xdm:taxId": "string"
    },
    "xdm:personalEmail": {
        "xdm:address": "john.smith@abc.com",
        "xdm:label": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:type": "unknown"
    },
    "xdm:repositoryCreatedBy": "string",
    "xdm:repositoryLastModifiedBy": "string"
}
```
