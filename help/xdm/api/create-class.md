---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar uma classe
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Criar uma classe

O principal bloco de construção de um schema é uma classe. A classe contém o conjunto mínimo de campos que devem ser definidos para capturar os dados principais de um schema. Por exemplo, se você estivesse projetando um schema para carros e caminhões eles provavelmente usariam uma classe chamada Veículo que descrevia as propriedades comuns básicas de todos os veículos.

Há várias classes padrão fornecidas pela Adobe e outros [!DNL Experience Platform] parceiros, mas você também pode definir suas próprias classes e salvá-las no [!DNL Schema Registry]. Em seguida, é possível compor um schema que implementa a classe criada e definir combinações compatíveis com a classe recém-definida.

>[!NOTE]
>
>Ao compor um schema com base em uma classe definida, você não poderá usar as mixagens padrão. Cada mixin define as classes com as quais são compatíveis em seus `meta:intendedToExtend` atributos. Depois de começar a definir misturas compatíveis com sua nova classe (usando o `$id` da nova classe no `meta:intendedToExtend` campo da mistura), você poderá reutilizar essas misturas toda vez que definir um schema que implemente a classe definida. Consulte as seções sobre como [criar misturas](create-mixin.md) e [criar schemas](create-schema.md) para obter mais informações.

**Formato da API**

```http
POST /tenant/classes
```

**Solicitação**

A solicitação para criar (POST) uma classe deve incluir um `allOf` atributo que contenha um `$ref` para um de dois valores: `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Esses valores representam o comportamento no qual a classe se baseia (registro ou série de tempo, respectivamente). Para obter mais informações sobre as diferenças entre os dados de registro e os dados de série de tempo, consulte a seção sobre tipos de comportamento dentro dos [fundamentos da composição](../schema/composition.md)do schema.

Ao definir uma classe, você também pode incluir combinações ou campos personalizados na definição da classe. Isso faria com que as combinações e os campos adicionados fossem incluídos em todos os schemas que implementam a classe. A solicitação de exemplo a seguir define uma classe chamada &quot;Propriedade&quot;, que captura informações relacionadas a diferentes propriedades pertencentes e operadas por uma empresa. Inclui um `propertyId` campo a ser incluído toda vez que a classe é usada.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `_{TENANT_ID}` | A `TENANT_ID` namespace de sua organização. Todos os recursos criados pela sua organização devem incluir essa propriedade para evitar colisões com outros recursos no [!DNL Schema Registry]. |
| `allOf` | Uma lista de recursos cujas propriedades devem ser herdadas pela nova classe. Um dos `$ref` objetos dentro da matriz define o comportamento da classe. Neste exemplo, a classe herda o comportamento &quot;record&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga que contém os detalhes da classe recém-criada, incluindo `$id`, `meta:altId`e `version`. Esses três valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
    "title": "Property",
    "description": "Properties owned and operated by the company.",
    "type": "object",
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "property": {
                            "title": "Property Information",
                            "type": "object",
                            "description": "Information about different owned and operated properties.",
                            "properties": {
                                "propertyId": {
                                    "title": "Property Identification Number",
                                    "type": "string",
                                    "description": "Unique Property identification number",
                                    "meta:xdmType": "string"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/record"
        },
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "version": "1.0",
    "meta:resourceType": "classes",
    "meta:registryMetadata": {
        "repo:createDate": 1552086405448,
        "repo:lastModifiedDate": 1552086405448,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

A execução de uma solicitação GET para lista de todas as classes no container locatário agora inclui a classe Property. Você também pode executar uma solicitação de pesquisa (GET) usando o `$id` URI codificado por URL para visualização a nova classe diretamente. Certifique-se de incluir o `version` no cabeçalho Aceitar ao executar uma solicitação de pesquisa.
