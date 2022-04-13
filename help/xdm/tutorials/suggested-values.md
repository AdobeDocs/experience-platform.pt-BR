---
title: Adicionar valores sugeridos a um campo
description: Saiba como adicionar valores sugeridos a um campo de cadeia de caracteres na API do Registro de Schema.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Adicionar valores sugeridos a um campo

No Experience Data Model (XDM), um campo enum representa um campo de string que está restrito a um subconjunto predefinido de valores. Os campos Enum podem fornecer validação para garantir que os dados assimilados estejam em conformidade com um conjunto de valores aceitos. No entanto, também é possível definir um conjunto de valores sugeridos para um campo de sequência sem aplicá-los como restrições.

No [API do Registro de Schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/), os valores restritos de um campo enum são representados por um `enum` array, enquanto um `meta:enum` O objeto fornece nomes de exibição amigáveis para esses valores:

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

Para campos enum, o Registro de Esquema não permite `meta:enum` , para além dos valores previstos no `enum`, pois tentar assimilar valores de string fora dessas restrições não passaria pela validação.

Como alternativa, você pode definir um campo de string que não contenha um `enum` e usa somente o `meta:enum` objeto para indicar valores sugeridos:

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

Como a cadeia de caracteres não tem um `enum` matriz para definir restrições, sua `meta:enum` pode ser estendida para incluir novos valores. Este tutorial aborda como adicionar valores sugeridos a campos de sequência padrão e personalizados na API do Registro de Schema.

## Pré-requisitos

Este guia pressupõe que você esteja familiarizado com os elementos da composição do esquema no XDM e como usar a API do Registro de Schema para criar e editar recursos do XDM. Consulte a seguinte documentação se você precisar de uma introdução:

* [Noções básicas da composição do schema](../schema/composition.md)
* [Guia da API do Registro de Schema](../api/overview.md)

## Adicionar valores sugeridos a um campo padrão

Para estender o `meta:enum` de um campo de string padrão, é possível criar um [descritor de nome amigável](../api/descriptors.md#friendly-name) para o campo em questão em um schema específico.

>[!NOTE]
>
>Os valores sugeridos para campos de cadeia de caracteres só podem ser adicionados no nível do esquema. Por outras palavras, estender a `meta:enum` de um campo padrão em um schema não afeta outros schemas que usam o mesmo campo padrão.

A solicitação a seguir adiciona valores sugeridos ao padrão `eventType` (fornecido pelo [Classe XDM ExperienceEvent](../classes/experienceevent.md)) para o schema identificado em `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Depois de aplicar o descritor, o Registro de Esquema responde com o seguinte ao recuperar o esquema (resposta truncada para espaço):

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
>Se o campo padrão já contiver valores em `meta:enum`, os novos valores do descritor não substituem os campos existentes e são adicionados em:
>
>
```json
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

## Adicionar valores sugeridos a um campo personalizado

Para estender o `meta:enum` de um campo personalizado, é possível atualizar a classe pai, o grupo de campos ou o tipo de dados do campo por meio de uma solicitação de PATCH.

>[!WARNING]
>
>Em contraste com os campos padrão, atualize o `meta:enum` de um campo personalizado afeta todos os outros schemas que empregam esse campo. Se você não quiser que as alterações se propaguem entre esquemas, considere criar um novo recurso personalizado:
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Depois de aplicar a alteração, o Registro de Esquema responde com o seguinte ao recuperar o esquema (resposta truncada para espaço):

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

Este guia cobriu como adicionar valores sugeridos a campos de sequência na API do Registro de Schema. Consulte o guia sobre [definição de campos personalizados na API](./custom-fields-api.md) para obter mais informações sobre como criar tipos de campos diferentes.
