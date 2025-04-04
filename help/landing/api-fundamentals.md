---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Fundamentos da API do Experience Platform
description: Este documento fornece uma breve visão geral de algumas das tecnologias subjacentes e sintaxes envolvidas com as APIs do Experience Platform.
role: Developer
feature: API
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# Fundamentos da API do Experience Platform

As APIs do Adobe Experience Platform empregam várias tecnologias e sintaxes subjacentes que são importantes para gerenciar efetivamente os recursos do [!DNL Experience Platform] baseados em JSON. Este documento fornece uma breve visão geral dessas tecnologias, bem como links para documentação externa para obter mais informações.

## Ponteiro JSON {#json-pointer}

O ponteiro JSON é uma sintaxe de sequência de caracteres padronizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos em documentos JSON. Um ponteiro JSON é uma cadeia de tokens separada por `/` caracteres, que especifica chaves de objeto ou índices de matriz, e os tokens podem ser uma cadeia de caracteres ou um número. As cadeias de caracteres JSON Pointer são usadas em muitas operações do PATCH para APIs [!DNL Experience Platform], conforme descrito posteriormente neste documento. Para obter mais informações sobre o JSON Pointer, consulte a [documentação de visão geral do JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Exemplo de objeto de esquema JSON

O JSON a seguir representa um esquema XDM simplificado cujos campos podem ser referenciados usando cadeias de caracteres de ponteiro JSON. Observe que todos os campos que foram adicionados usando grupos de campos de esquema personalizados (como `loyaltyLevel`) têm namespace sob um objeto `_{TENANT_ID}`, enquanto os campos que foram adicionados usando grupos de campos principais (como `fullName`) não têm.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Exemplo de ponteiros JSON com base no objeto de esquema

| Ponteiro JSON | Resolve para |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Retorna uma referência ao campo `fullName`, fornecida por um grupo de campos principal.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Retorna uma referência ao campo `loyaltyLevel`, fornecida por um grupo de campos personalizado.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Ao lidar com os atributos `xdm:sourceProperty` e `xdm:destinationProperty` de [!DNL Experience Data Model] descritores (XDM), qualquer chave `properties` deve ser **excluída** da cadeia de caracteres JSON Pointer. Consulte o subguia do guia do desenvolvedor da API [!DNL Schema Registry] em [descritores](../xdm/api/descriptors.md) para obter mais informações.

## Patch JSON {#json-patch}

Há muitas operações do PATCH para APIs [!DNL Experience Platform] que aceitam objetos JSON Patch para suas cargas de solicitação. O Patch JSON é um formato padronizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para descrever alterações em um documento JSON. Ela permite definir atualizações parciais no JSON sem precisar enviar o documento inteiro em um corpo de solicitação.

### Exemplo de objeto de patch de JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: O tipo de operação de patch. Embora o JSON Patch ofereça suporte a vários tipos de operação diferentes, nem todas as operações do PATCH nas APIs [!DNL Experience Platform] são compatíveis com todos os tipos de operação. Os tipos de operação disponíveis são:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: a parte da estrutura JSON a ser atualizada, identificada com a notação [JSON Pointer](#json-pointer).

Dependendo do tipo de operação indicado em `op`, o objeto de Patch JSON pode exigir propriedades adicionais. Para obter mais informações sobre as diferentes operações de patch de JSON e sua sintaxe necessária, consulte a [documentação de patch de JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Esquema JSON {#json-schema}

O esquema JSON é um formato usado para descrever e validar a estrutura dos dados JSON. O [Experience Data Model (XDM)](../xdm/home.md) aproveita os recursos do Esquema JSON para impor restrições na estrutura e no formato dos dados de experiência do cliente assimilados. Para obter mais informações sobre o Esquema JSON, consulte a [documentação oficial](https://json-schema.org/).

## Próximas etapas

Este documento apresentou algumas das tecnologias e sintaxes envolvidas no gerenciamento de recursos baseados em JSON para [!DNL Experience Platform]. Consulte o [guia de introdução](api-guide.md) para obter mais informações sobre como trabalhar com APIs do Experience Platform, incluindo as práticas recomendadas. Para obter respostas para perguntas frequentes, consulte o [guia de solução de problemas do Experience Platform](troubleshooting.md).
