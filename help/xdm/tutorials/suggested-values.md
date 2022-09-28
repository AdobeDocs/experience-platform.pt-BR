---
title: Gerenciar valores sugeridos na API
description: Saiba como adicionar valores sugeridos a um campo de cadeia de caracteres na API do Registro de Schema.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 19bd5d9c307ac6e1b852e25438ff42bf52a1231e
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# Gerenciar valores sugeridos na API

Para qualquer campo de string no Experience Data Model (XDM), é possível definir um **enum** que restringe os valores que o campo pode assimilar a um conjunto predefinido. Se você tentar assimilar dados para um campo enum e o valor não corresponder a nenhum daqueles definidos em sua configuração, a assimilação será negada.

Em contraste com enumerações, adicionar **valores sugeridos** para um campo de string não restringe os valores que ele pode assimilar. Em vez disso, os valores sugeridos afetam quais valores predefinidos estão disponíveis na variável [Interface do usuário de segmentação](../../segmentation/ui/overview.md) ao incluir o campo de string como um atributo.

>[!NOTE]
>
>Há um atraso de aproximadamente cinco minutos para que os valores sugeridos atualizados de um campo sejam refletidos na interface do usuário de segmentação.

Este guia aborda como gerenciar os valores sugeridos usando o [API do Registro de Schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Para obter etapas sobre como fazer isso na interface do usuário do Adobe Experience Platform, consulte o [Guia de interface do usuário sobre enumerações e valores sugeridos](../ui/fields/enum.md).

## Pré-requisitos

Este guia pressupõe que você esteja familiarizado com os elementos da composição do esquema no XDM e como usar a API do Registro de Schema para criar e editar recursos do XDM. Consulte a seguinte documentação se você precisar de uma introdução:

* [Noções básicas da composição do schema](../schema/composition.md)
* [Guia da API do Registro de Schema](../api/overview.md)

Também é altamente recomendável revisar a variável [regras de evolução para enumerações e valores sugeridos](../ui/fields/enum.md#evolution) se estiver atualizando campos existentes. Se você estiver gerenciando valores sugeridos para schemas que participam de uma união, consulte o [regras para mesclar enumerações e valores sugeridos](../ui/fields/enum.md#merging).

## Composição

Na API, os valores restritos de um **enum** são representadas por um `enum` array, enquanto um `meta:enum` O objeto fornece nomes de exibição amigáveis para esses valores:

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

Como alternativa, você pode definir um campo de string que não contenha um `enum` e usa somente o `meta:enum` objeto a denotar **valores sugeridos**:

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

Como a cadeia de caracteres não tem um `enum` matriz para definir restrições, sua `meta:enum` pode ser estendida para incluir novos valores.

## Gerenciar valores sugeridos para campos padrão

Para campos padrão existentes, é possível [adicionar valores sugeridos](#add-suggested-standard) ou [remover valores sugeridos](#remove-suggested-standard).

### Adicionar valores sugeridos {#add-suggested-standard}

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

### Remover valores sugeridos {#remove-suggested-standard}

Se um campo de string padrão tiver valores sugeridos predefinidos, você poderá remover quaisquer valores que não deseja ver na segmentação. Isso é feito criando uma [descritor de nome amigável](../api/descriptors.md#friendly-name) para o schema que inclui um `xdm:excludeMetaEnum` propriedade.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir remove os valores sugeridos &quot;[!DNL Web Form Filled Out]&quot; e &quot;[!DNL Media ping]&quot; para `eventType` em um schema baseado na variável [Classe XDM ExperienceEvent](../classes/experienceevent.md).

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

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de nome amigável, esse valor deve ser definido como `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | O `$id` URI do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica cujos valores sugeridos você deseja gerenciar. O caminho deve começar com uma barra (`/`) e não termine com um. Não incluir `properties` no caminho (por exemplo, use `/personalEmail/address` em vez de `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | Um objeto que descreve os valores sugeridos que devem ser excluídos para o campo na segmentação. A chave e o valor de cada entrada devem corresponder aos incluídos no original `meta:enum` do campo para que a entrada seja excluída. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes do descritor recém-criado. Os valores sugeridos incluídos em `xdm:excludeMetaEnum` agora estará oculta da interface do usuário de segmentação.

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
```

## Gerenciar valores sugeridos para um campo personalizado {#suggested-custom}

Para gerenciar a `meta:enum` de um campo personalizado, é possível atualizar a classe pai, o grupo de campos ou o tipo de dados do campo por meio de uma solicitação de PATCH.

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

Este guia cobriu como gerenciar valores sugeridos para campos de sequência na API do Registro de Schema. Consulte o guia sobre [definição de campos personalizados na API](./custom-fields-api.md) para obter mais informações sobre como criar tipos de campos diferentes.
