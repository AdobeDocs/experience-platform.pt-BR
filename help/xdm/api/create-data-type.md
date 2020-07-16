---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um tipo de dados
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---


# Criar um tipo de dados

Quando existem estruturas de dados comuns que sua organização deseja usar de várias formas, você pode definir um tipo de dados. Os tipos de dados permitem o uso consistente de estruturas de vários campos, com mais flexibilidade do que combinações, pois eles podem ser incluídos em qualquer lugar de um schema adicionando-os como o campo `type` .

Em outras palavras, os tipos de dados permitem que você defina uma hierarquia de objetos uma vez, e faça referência a ela em um campo da mesma maneira que qualquer outro tipo escalar.

**Formato da API**

```http
POST /tenant/datatypes
```

**Solicitação**

A definição de um tipo de dados não exige campos `meta:extends` ou `meta:intendedToExtend` , nem campos precisam ser aninhados para evitar colisões.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga que contém os detalhes do tipo de dados recém-criado, incluindo o `$id`, `meta:altId`e `version`. Esses três valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

A execução de uma solicitação GET para lista de todos os tipos de dados no container locatário agora inclui o tipo de dados Construção da propriedade. Você também pode executar uma solicitação de pesquisa (GET) usando o `$id` URI codificado por URL para visualização o novo tipo de dados diretamente. Certifique-se de incluir o `version` no cabeçalho Aceitar para uma solicitação de pesquisa.
