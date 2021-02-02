---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Fundamentos da API Adobe Experience Platform
topic: getting started
description: Este documento fornece uma breve visão geral de algumas tecnologias e sintaxes subjacentes envolvidas com APIs de Experience Platform.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---


# Fundamentos da API Adobe Experience Platform

As APIs da Adobe Experience Platform empregam várias tecnologias e sintaxes subjacentes que são importantes de entender para gerenciar eficientemente os recursos [!DNL Platform] baseados em JSON. Este documento fornece uma breve visão geral dessas tecnologias, além de links para a documentação externa para obter mais informações.

## Ponteiro JSON {#json-pointer}

O ponteiro JSON é uma sintaxe de sequência padronizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos em documentos JSON. Um ponteiro JSON é uma string de tokens separados por `/` caracteres, que especificam chaves de objeto ou índices de matriz, e os tokens podem ser uma string ou um número. As strings de ponteiro JSON são usadas em muitas operações de PATCH para [!DNL Platform] APIs, conforme descrito posteriormente neste documento. Para obter mais informações sobre o ponteiro JSON, consulte a [documentação de visão geral do ponteiro JSON](https://rapidjson.org/md_doc_pointer.html).

### Exemplo de objeto de schema JSON

O seguinte JSON representa um schema XDM simplificado cujos campos podem ser referenciados usando strings de ponteiro JSON. Observe que todos os campos que foram adicionados usando combinações personalizadas (como `loyaltyLevel`) são namespacados sob um objeto `_{TENANT_ID}`, enquanto os campos que foram adicionados usando combinações principais (como `fullName`) não são.

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

### Exemplo de ponteiros JSON com base no objeto schema

| Ponteiro JSON | Resolve para |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Retorna uma referência ao campo `fullName`, fornecida por uma combinação principal.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Retorna uma referência ao campo `loyaltyLevel`, fornecida por uma combinação personalizada.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Ao lidar com os atributos `xdm:sourceProperty` e `xdm:destinationProperty` dos descritores [!DNL Experience Data Model] (XDM), qualquer tecla `properties` deve ser **excluída** da string do ponteiro JSON. Consulte o subguia do desenvolvedor da API [!DNL Schema Registry] em [descritores](../xdm/api/descriptors.md) para obter mais informações.

## Patch JSON {#json-patch}

Há muitas operações de PATCH para [!DNL Platform] APIs que aceitam objetos de Patch JSON para suas cargas de solicitação. O Patch JSON é um formato padronizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para descrever alterações em um documento JSON. Ele permite que você defina atualizações parciais para JSON sem precisar enviar o documento inteiro em um corpo de solicitação.

### Exemplo de objeto de correção JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: O tipo de operação de patch. Embora o Patch JSON suporte vários tipos de operação diferentes, nem todas as operações de PATCH em [!DNL Platform] APIs são compatíveis com cada tipo de operação. Os tipos de operação disponíveis são:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: A parte da estrutura JSON a ser atualizada, identificada usando a  [Pontuação ](#json-pointer) JSON.

Dependendo do tipo de operação indicado em `op`, o objeto Patch JSON pode exigir propriedades adicionais. Para obter mais informações sobre as diferentes operações de Patch JSON e sua sintaxe necessária, consulte a [documentação de Patch JSON](http://jsonpatch.com/).

## Schema JSON

O Schema JSON é um formato usado para descrever e validar a estrutura dos dados JSON. [O Experience Data Model (XDM)](../xdm/home.md) aproveita os recursos do Schema JSON para impor restrições na estrutura e formato dos dados de experiência do cliente assimilados. Para obter mais informações sobre o Schema JSON, consulte a [documentação oficial](https://json-schema.org/).

## Próximas etapas

Este documento apresentou algumas das tecnologias e sintaxes envolvidas com o gerenciamento de recursos baseados em JSON para [!DNL Experience Platform]. Para obter mais informações sobre como trabalhar com [!DNL Platform] APIs, incluindo práticas recomendadas e respostas a perguntas frequentes, consulte o [Guia de solução de problemas da plataforma](troubleshooting.md).