---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Criar um schema
description: 'Um schema pode ser considerado como o modelo para os dados que você deseja assimilar no Experience Platform. Cada schema é composto de uma classe e zero ou mais combinações. Em outras palavras, você não precisa adicionar uma mixin para definir um schema, mas na maioria dos casos, pelo menos uma mixin será usada. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---


# Criar um schema

Um schema pode ser considerado o modelo para os dados que você deseja assimilar [!DNL Experience Platform]. Cada schema é composto de uma classe e zero ou mais combinações. Em outras palavras, você não precisa adicionar uma mixin para definir um schema, mas na maioria dos casos, pelo menos uma mixin será usada.

O processo de composição do schema começa atribuindo uma classe. A classe define os principais aspectos comportamentais dos dados (registro ou série cronológica), bem como os campos mínimos necessários para descrever os dados que serão assimilados.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação deve incluir um `allOf` atributo que faça referência ao `$id` de uma classe. Este atributo define a &quot;classe base&quot; que o schema implementará. Neste exemplo, a classe base é uma classe &quot;Informações de propriedade&quot; criada anteriormente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `allOf > $ref` | O `$id` valor da classe que o novo schema implementará. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga que contém os detalhes do schema recém-criado, incluindo o `$id`, `meta:altId`e `version`. Esses valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

A execução de uma solicitação de GET para lista de todos os schemas no container locatário agora inclui o schema Informações de propriedade ou você pode executar uma solicitação de pesquisa (GET) usando o `$id` URI codificado por URL para visualização direta do novo schema. Lembre-se de incluir o `version` no cabeçalho Aceitar para todas as solicitações de pesquisa.
