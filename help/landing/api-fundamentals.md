---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fundamentos da API Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 2%

---


# Fundamentos da API Adobe Experience Platform

As APIs da Adobe Experience Platform empregam várias tecnologias e sintaxes subjacentes que são importantes de entender para gerenciar com eficácia [!DNL Platform] os recursos baseados em JSON. Este documento fornece uma breve visão geral dessas tecnologias, além de links para a documentação externa para obter mais informações.

## Ponteiro JSON {#json-pointer}

JSON Pointer é uma sintaxe de sequência padronizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos em documentos JSON. Um ponteiro JSON é uma string de tokens separados por `/` caracteres, que especifica chaves de objeto ou índices de matriz, e os tokens podem ser uma string ou um número. As strings de ponteiro JSON são usadas em muitas operações de PATCH para [!DNL Platform] APIs, conforme descrito posteriormente neste documento. Para obter mais informações sobre o ponteiro JSON, consulte a documentação [de visão geral do ponteiro](https://rapidjson.org/md_doc_pointer.html)JSON.

### Exemplo de objeto de schema JSON

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Exemplo de ponteiros JSON com base no objeto schema

| Ponteiro JSON | Resolve para |
|--- | ---|
| `"/title"` | &quot;Detalhes do Membro de Fidelidade&quot; |
| `"/definitions/loyalty"` | (Retorna o conteúdo do `loyalty` objeto) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Ao lidar com os atributos `xdm:sourceProperty` e `xdm:destinationProperty` dos descritores [!DNL Experience Data Model] (XDM), qualquer `properties` chave deve ser **excluída** da string Ponteiro JSON. Consulte o subguia do desenvolvedor da [!DNL Schema Registry] API em [descritores](../xdm/api/descriptors.md) para obter mais informações.

## Patch JSON

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
* `path`: A parte da estrutura JSON a ser atualizada, identificada usando a notação [JSON Pointer](#json-pointer) .

Dependendo do tipo de operação indicado em `op`, o objeto JSON Patch pode exigir propriedades adicionais. Para obter mais informações sobre as diferentes operações de Patch JSON e sua sintaxe necessária, consulte a documentação [do Patch](http://jsonpatch.com/)JSON.

## Schema JSON

O Schema JSON é um formato usado para descrever e validar a estrutura dos dados JSON. [O Experience Data Model (XDM)](../xdm/home.md) aproveita os recursos do Schema JSON para impor restrições na estrutura e formato dos dados de experiência do cliente assimilados. Para obter mais informações sobre o Schema JSON, consulte a documentação [](https://json-schema.org/)oficial.

## Próximas etapas

Este documento apresentou algumas das tecnologias e sintaxes envolvidas com o gerenciamento de recursos baseados em JSON para [!DNL Experience Platform]. Para obter mais informações sobre como trabalhar com [!DNL Platform] APIs, incluindo práticas recomendadas e respostas a perguntas frequentes, consulte o guia [de solução de problemas da](troubleshooting.md)plataforma.