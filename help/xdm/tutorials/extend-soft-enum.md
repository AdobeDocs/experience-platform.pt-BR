---
title: Estender um campo Enum suave
description: Saiba como estender um campo soft enum na API do Registro de Schema.
source-git-commit: 2d85db789e6e6a28402bb68122a3b5cfe9d0c5dc
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Estender um campo de enumeração suave

No Experience Data Model (XDM), um campo enum representa um campo de string que está restrito a um subconjunto predefinido de valores. Os campos Enum podem fornecer validação para garantir que os dados assimilados estejam em conformidade com um conjunto de valores aceitos (referido como &quot;enum duro&quot;) ou simplesmente representam um conjunto de valores sugeridos sem impor restrições (referido como &quot;enum suave&quot;).

Na API do Registro de Schema, os valores restritos de um enum rígido são representados por um `enum` array, enquanto um `meta:enum` O objeto fornece nomes de exibição amigáveis para esses valores:

```json
"sampleHardEnumField": {
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

Para campos de enum rígido, o Registro de Schema não permite `meta:enum` , para além dos valores previstos no `enum`, pois tentar assimilar valores de string fora dessas restrições não passaria pela validação.

Por outro lado, um campo de enum suave não contém um `enum` e usa somente o `meta:enum` objeto para indicar valores sugeridos:

```json
"sampleSoftEnumField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Como os enumerações suaves não têm as mesmas restrições de validação que os enumerações rígidos, seus `meta:enum` As propriedades podem ser estendidas para incluir novos valores. Este tutorial aborda como estender campos de soft enum padrão e personalizados na API do Registro de Schema.

## Pré-requisitos

Este guia pressupõe que você esteja familiarizado com os elementos da composição do esquema no XDM e como usar a API do Registro de Schema para criar e editar recursos do XDM. Consulte a seguinte documentação se você precisar de uma introdução:

* [Noções básicas da composição do schema](../schema/composition.md)
* [Guia da API do Registro de Schema](../api/overview.md)

## Estender um campo de soft enum padrão

Para estender o `meta:enum` de um campo de string padrão, é possível criar um [descritor de nome amigável](../api/descriptors.md#friendly-name) para o campo em questão em um schema específico.

>[!NOTE]
>
>As enumerações suaves padrão só podem ser estendidas no nível do schema. Por outras palavras, estender a `meta:enum` de um campo padrão em um schema não afeta outros schemas que usam o mesmo campo padrão.

A solicitação a seguir adiciona valores soft enum ao padrão `eventType` (fornecido pelo [Classe XDM ExperienceEvent](../classes/experienceevent.md)) para o schema identificado em `sourceSchema`:

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

## Estender um campo personalizado de soft enum

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

Este guia aborda como estender enumerações temporárias na API do Registro de Schema. Para obter mais informações sobre como definir tipos de campos diferentes na API, consulte o guia sobre [Restrições do tipo de campo XDM](../schema/field-constraints.md#define-fields).
