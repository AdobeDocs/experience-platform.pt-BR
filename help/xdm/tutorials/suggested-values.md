---
title: Gerenciar valores sugeridos na API
description: Saiba como adicionar valores sugeridos a um campo de string na API do registro de esquema.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Gerenciar valores sugeridos na API

Para qualquer campo de cadeia de caracteres no Experience Data Model (XDM), é possível definir um **enum** que restrinja os valores que o campo pode assimilar em um conjunto predefinido. Se você tentar assimilar dados em um campo enum e o valor não corresponder a nenhum dos definidos em sua configuração, a assimilação será negada.

Ao contrário das enumerações, adicionar **valores sugeridos** a um campo de cadeia de caracteres não restringe os valores que ele pode assimilar. Em vez disso, os valores sugeridos afetam quais valores predefinidos estão disponíveis na [Interface de segmentação](../../segmentation/ui/overview.md) ao incluir o campo de sequência como um atributo.

>[!NOTE]
>
>Há um atraso de aproximadamente cinco minutos para que os valores sugeridos atualizados de um campo sejam refletidos na interface do usuário de segmentação.

Este guia aborda como gerenciar valores sugeridos usando a [API do Registro de Esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Para obter etapas sobre como fazer isso na interface do usuário do Adobe Experience Platform, consulte o [guia da interface sobre enumerações e valores sugeridos](../ui/fields/enum.md).

## Pré-requisitos

Este guia supõe que você esteja familiarizado com os elementos da composição do esquema no XDM e como usar a API do Registro de esquema para criar e editar recursos do XDM. Consulte a documentação a seguir se precisar de uma introdução:

* [Noções básicas da composição do esquema](../schema/composition.md)
* [Guia da API do registro de esquema](../api/overview.md)

Também é altamente recomendável que você revise as [regras de evolução para enumerações e valores sugeridos](../ui/fields/enum.md#evolution) se estiver atualizando campos existentes. Se você estiver gerenciando valores sugeridos para esquemas que participam de uma união, consulte as [regras para mesclar enumerações e valores sugeridos](../ui/fields/enum.md#merging).

## Composição

Na API, os valores restritos de um campo **enum** são representados por uma matriz `enum`, enquanto um objeto `meta:enum` fornece nomes de exibição amigáveis para esses valores:

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Para campos enum, o Registro de Esquema não permite que `meta:enum` seja estendido além dos valores fornecidos em `enum`, pois tentar assimilar valores de cadeia de caracteres fora dessas restrições não passaria na validação.

Como alternativa, você pode definir um campo de cadeia de caracteres que não contenha uma matriz `enum` e use apenas o objeto `meta:enum` para denotar **valores sugeridos**:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Como a cadeia de caracteres não tem uma matriz `enum` para definir restrições, sua propriedade `meta:enum` pode ser estendida para incluir novos valores.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Adicionar valores sugeridos a um campo padrão {#add-suggested-standard}

Para estender o `meta:enum` de um campo de cadeia de caracteres padrão, você pode criar um [descritor de nome amigável](../api/descriptors.md#friendly-name) para o campo em questão em um esquema específico.

>[!NOTE]
>
>Os valores sugeridos para campos de string só podem ser adicionados no nível do esquema. Em outras palavras, estender a `meta:enum` de um campo padrão em um esquema não afeta outros esquemas que empregam o mesmo campo padrão.

A solicitação a seguir adiciona valores sugeridos ao campo padrão `eventType` (fornecido pela [classe XDM ExperienceEvent](../classes/experienceevent.md)) para o esquema identificado em `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

Após aplicar o descritor, o Registro de esquema responde com o seguinte ao recuperar o esquema (resposta truncada por espaço):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Se o campo padrão já contiver valores abaixo de `meta:enum`, os novos valores do descritor não substituirão os campos existentes e serão adicionados em seu lugar:
>
>```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## Gerenciar valores sugeridos para um campo personalizado {#suggested-custom}

Para gerenciar o `meta:enum` de um campo personalizado, você pode atualizar a classe pai, o grupo de campos ou o tipo de dados do campo por meio de uma solicitação PATCH.

>[!WARNING]
>
>Ao contrário dos campos padrão, a atualização da `meta:enum` de um campo personalizado afeta todos os outros esquemas que empregam esse campo. Se você não quiser que as alterações se propaguem nos esquemas, considere criar um novo recurso personalizado:
>
>* [Criar uma classe personalizada](../api/classes.md#create)
>* [Criar um grupo de campos personalizado](../api/field-groups.md#create)
>* [Criar um tipo de dados personalizado](../api/data-types.md#create)

A solicitação a seguir atualiza o `meta:enum` de um campo de &quot;nível de fidelidade&quot; fornecido por um tipo de dados personalizado:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

Depois de aplicar a alteração, o Registro de esquema responde com o seguinte ao recuperar o esquema (resposta truncada por espaço):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Próximas etapas

Este guia abordou como gerenciar valores sugeridos para campos de string na API do registro de esquema. Consulte o manual sobre [definição de campos personalizados na API](./custom-fields-api.md) para obter mais informações sobre como criar tipos de campos diferentes.
