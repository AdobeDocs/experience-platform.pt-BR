---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Fundamentos da API do Experience Platform
topic-legacy: getting started
description: Este documento fornece uma breve visão geral de algumas tecnologias e sintaxes subjacentes envolvidas com APIs do Experience Platform.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# Fundamentos da API do Experience Platform

As APIs do Adobe Experience Platform empregam várias tecnologias e sintaxes subjacentes que são importantes para entender a fim de gerenciar com eficácia os recursos [!DNL Platform] baseados em JSON. Este documento fornece uma breve visão geral dessas tecnologias, bem como links para a documentação externa para obter mais informações.

## Ponteiro JSON {#json-pointer}

O Ponteiro JSON é uma sintaxe de sequência padronizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos em documentos JSON. Um ponteiro JSON é uma string de tokens separados por `/` caracteres, que especificam chaves de objeto ou índices de matriz, e os tokens podem ser uma string ou um número. As cadeias de caracteres JSON Pointer são usadas em muitas operações PATCH para [!DNL Platform] APIs, conforme descrito posteriormente neste documento. Para obter mais informações sobre o ponteiro JSON, consulte a [documentação de visão geral do ponteiro JSON](https://rapidjson.org/md_doc_pointer.html).

### Exemplo de objeto de esquema JSON

O JSON a seguir representa um esquema XDM simplificado cujos campos podem ser referenciados usando strings de ponteiro JSON. Observe que todos os campos que foram adicionados usando combinações personalizadas (como `loyaltyLevel`) são namespacados em um objeto `_{TENANT_ID}`, enquanto os campos que foram adicionados usando combinações principais (como `fullName`) não são.

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
| `"/properties/person/properties/name/properties/fullName"` | (Retorna uma referência ao campo `fullName` , fornecido por uma combinação principal.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Retorna uma referência ao campo `loyaltyLevel` , fornecido por um mixin personalizado.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Ao lidar com os atributos `xdm:sourceProperty` e `xdm:destinationProperty` de [!DNL Experience Data Model] (XDM) descritores, qualquer chave `properties` deve ser **excluída** da string do ponteiro JSON. Consulte o [!DNL Schema Registry] sub-guia do desenvolvedor de API em [descritores](../xdm/api/descriptors.md) para obter mais informações.

## Patch JSON {#json-patch}

Há muitas operações do PATCH para APIs [!DNL Platform] que aceitam objetos de patch JSON para suas cargas de solicitação. O Patch JSON é um formato padronizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para descrever alterações em um documento JSON. Ela permite definir atualizações parciais para o JSON sem precisar enviar o documento inteiro em um corpo da solicitação.

### Exemplo de objeto de patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: O tipo de operação de patch. Embora o Patch JSON seja compatível com vários tipos de operação diferentes, nem todas as operações do PATCH nas APIs [!DNL Platform] são compatíveis com cada tipo de operação. Os tipos de operação disponíveis são:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: A parte da estrutura JSON a ser atualizada, identificada usando a  [Pontuação ](#json-pointer) JSON.

Dependendo do tipo de operação indicado em `op`, o objeto Patch JSON pode exigir propriedades adicionais. Para obter mais informações sobre as diferentes operações do Patch JSON e sua sintaxe necessária, consulte a [documentação do Patch JSON](http://jsonpatch.com/).

## Esquema JSON {#json-schema}

Esquema JSON é um formato usado para descrever e validar a estrutura dos dados JSON. [O Experience Data Model (XDM)](../xdm/home.md) aproveita os recursos do Esquema JSON para impor restrições na estrutura e no formato dos dados de experiência do cliente assimilados. Para obter mais informações sobre o Esquema JSON, consulte a [documentação oficial](https://json-schema.org/).

## Próximas etapas

Este documento apresentou algumas tecnologias e sintaxes envolvidas no gerenciamento de recursos baseados em JSON para [!DNL Experience Platform]. Consulte o [guia de introdução](api-guide.md) para obter mais informações sobre como trabalhar com APIs de plataforma, incluindo práticas recomendadas. Para obter respostas a perguntas frequentes, consulte o [Guia de solução de problemas da plataforma](troubleshooting.md).
