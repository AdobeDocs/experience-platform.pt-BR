---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados da experiência, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema, esquema, Esquema, esquemas, Esquemas, criar
solution: Experience Platform
title: Criar um esquema usando a API do Registro de esquema
type: Tutorial
description: Este tutorial usa a API do Registro de esquema para orientá-lo pelas etapas para compor um esquema usando uma classe padrão.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 6a69dd0bf8945dfef5ac73ee11a0ed6603ee4b9b
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 2%

---

# Crie um schema usando o [!DNL Schema Registry] API

O [!DNL Schema Registry] é usada para acessar o [!DNL Schema Library] no Adobe Experience Platform. O [!DNL Schema Library] contém recursos disponibilizados pelo Adobe, [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa. O registro fornece uma interface de usuário e uma RESTful API a partir da qual todos os recursos de biblioteca disponíveis são acessíveis.

Este tutorial usa o [!DNL Schema Registry] API para orientá-lo pelas etapas para compor um esquema usando uma classe padrão. Se preferir usar a interface do usuário em [!DNL Experience Platform], o [Tutorial do Editor de esquemas](create-schema-ui.md) O fornece instruções passo a passo para executar ações semelhantes no editor de esquema.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para o [!DNL Schema Registry] API. Isso inclui as `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção para a `Accept` e seus possíveis valores).

Este tutorial percorre as etapas da composição de um esquema de Membros de Fidelidade que descreve dados relacionados aos membros de um programa de fidelidade de varejo. Antes de começar, é possível pré-visualizar o [esquema Integrar Membros da Fidelidade](#complete-schema) no apêndice.

## Compor um esquema com uma classe padrão

Um schema pode ser considerado como o blueprint dos dados que você deseja assimilar em [!DNL Experience Platform]. Cada schema é composto de uma classe e zero ou mais grupos de campos de schema. Em outras palavras, não é necessário adicionar um grupo de campos para definir um schema, mas, na maioria dos casos, pelo menos um grupo de campos é usado.

### Atribuir uma classe

O processo de composição do schema começa com a seleção de uma classe. A classe define os principais aspectos comportamentais dos dados (registro vs série de tempo), bem como os campos mínimos necessários para descrever os dados que serão assimilados.

O schema que você está fazendo neste tutorial usa o [!DNL XDM Individual Profile] classe . [!DNL XDM Individual Profile] é uma classe padrão fornecida pelo Adobe para definir o comportamento do registro. Mais informações sobre comportamento podem ser encontradas em [noções básicas da composição do schema](../schema/composition.md).

Para atribuir uma classe, é feita uma chamada de API para criar (POST) um novo schema no contêiner do locatário. Essa chamada inclui a classe que o schema implementará. Cada schema só pode implementar uma classe.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação deve incluir um `allOf` atributo que faz referência ao `$id` de uma classe. Esse atributo define a &quot;classe base&quot; que o schema implementará. Neste exemplo, a classe base é a [!DNL XDM Individual Profile] classe . O `$id` do [!DNL XDM Individual Profile] é usada como o valor da variável `$ref` no campo `allOf` abaixo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "object",
  "title": "Loyalty Members",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile"
    }
  ]
}'
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status de Resposta HTTP 201 (Criado) com um corpo de resposta que contém os detalhes do schema recém-criado, incluindo o `$id`, `meta:altIt`e `version`. Esses valores são somente leitura e são atribuídos pela variável [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310304048,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_tenantId"
}
```

### Pesquisar um esquema

Para exibir o esquema criado recentemente, execute uma solicitação de pesquisa (GET) usando o `meta:altId` ou o URL codificado `$id` URI do esquema.

**Formato da API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que deseja pesquisar. |

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**Resposta**

O formato de resposta depende do `Accept` cabeçalho enviado com a solicitação. Tente experimentar com diferentes `Accept` cabeçalhos para ver qual deles atende melhor às suas necessidades.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310304048,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:allFieldAccess": true
}
```

### Adicionar um grupo de campos {#add-a-field-group}

Agora que o schema Membros de fidelidade foi criado e confirmado, os grupos de campos podem ser adicionados a ele.

Há diferentes grupos de campos padrão disponíveis para uso, dependendo da classe de schema selecionada. Cada grupo de campos contém um `intendedToExtend` que define a(s) classe(s) com a qual esse grupo de campos é compatível.

Os grupos de campos definem conceitos, como &quot;nome&quot; ou &quot;endereço&quot;, que podem ser reutilizados em qualquer schema que precise capturar as mesmas informações.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema ao qual você está adicionando o grupo de campos. |

**Solicitação**

Essa solicitação atualiza o esquema Membros de Fidelidade para incluir os campos na variável [[!UICONTROL Detalhes demográficos] grupo de campos](../field-groups/profile/demographic-details.md) (`profile-person-details`).

Ao adicionar a variável `profile-person-details` grupo de campos, o esquema Membros da Fidelidade agora captura informações demográficas para membros do programa de fidelidade, como nome, sobrenome e aniversário.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**Resposta**

A resposta mostra o grupo de campos recém-adicionado no `meta:extends` e contém um `$ref` para o grupo de campos no `allOf` atributo.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310912096,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Adicionar mais grupos de campos

O esquema Membros de Fidelidade requer mais dois grupos de campos padrão, que podem ser adicionados repetindo as etapas usando outro grupo de campos.

>[!TIP]
>
>Vale a pena revisar todos os grupos de campos disponíveis para se familiarizar com os campos incluídos em cada um. Você pode listar (GET) todos os grupos de campos disponíveis para uso com uma classe específica executando uma solicitação em relação a cada contêiner &quot;global&quot; e &quot;locatário&quot;, retornando somente os grupos de campos em que o campo &quot;meta:pretendidoToExtend&quot; corresponde à classe que você está usando. Nesse caso, é o [!DNL XDM Individual Profile] classe, assim a [!DNL XDM Individual Profile] `$id` é usada:
>
>
```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que você está atualizando. |

**Solicitação**

Essa solicitação atualiza o esquema Membros de Fidelidade para incluir os campos nos seguintes grupos de campos padrão:

* [[!UICONTROL Detalhes de contato pessoal]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`): Adiciona informações de contato, como endereço residencial, endereço de email e telefone residencial.
* [[!UICONTROL Detalhes da Fidelidade]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`): Adiciona informações de contato, como endereço residencial, endereço de email e telefone residencial.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**Resposta**

A resposta mostra os grupos de campos recém-adicionados na variável `meta:extends` e contém um `$ref` para o grupo de campos no `allOf` atributo.

O esquema Membros de Fidelidade agora deve conter quatro `$ref` na `allOf` array: `profile`, `profile-person-details`, `profile-personal-details`e `profile-loyalty-details` conforme mostrado abaixo.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.2",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673311559934,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Definir um novo grupo de campos

Enquanto o padrão [!UICONTROL Detalhes da Fidelidade] O grupo de campos fornece campos úteis relacionados à fidelidade ao esquema, há campos de fidelidade adicionais que não estão incluídos em nenhum grupo de campos padrão.

Para adicionar esses campos, você pode definir seus próprios grupos de campos personalizados na variável `tenant` contêiner. Esses grupos de campos são exclusivos de sua organização e não são visíveis ou editáveis por ninguém fora de sua organização.

Para criar (POST) um novo grupo de campos, sua solicitação deve incluir um `meta:intendedToExtend` campo contendo o `$id` para as classes base com as quais o grupo de campos é compatível, juntamente com as propriedades que o grupo de campos incluirá.

Todas as propriedades personalizadas devem ser aninhadas em `TENANT_ID` para evitar colisões com outros grupos de campos ou campos.

**Formato da API**

```http
POST /tenant/fieldgroups
```

**Solicitação**

Essa solicitação cria um novo grupo de campos que tem um objeto de &quot;fidelidade&quot; contendo quatro campos específicos do programa de fidelidade: &quot;loyaltyId&quot;, &quot;loyaltyLevel&quot;, &quot;loyaltyPoints&quot; e &quot;memberSince&quot;.

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Tier",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
            "loyaltyTier": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "loyaltyTier": {
                      "type": "object",
                      "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier."
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier."
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                        }
                      }
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyaltyTier"
            }
        ]
    }'
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status de Resposta HTTP 201 (Criado) com um corpo de resposta contendo os detalhes do grupo de campos recém-criado, incluindo o `$id`, `meta:altIt`e `version`. Esses valores são somente leitura e são atribuídos pela variável [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Captures info about the current loyalty tier of a customer.",
    "definitions": {
        "loyaltyTier": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyTier": {
                            "type": "object",
                            "properties": {
                                "id": {
                                    "title": "Loyalty Tier Identifier",
                                    "type": "string",
                                    "description": "Loyalty Tier Identifier.",
                                    "meta:xdmType": "string"
                                },
                                "effectiveDate": {
                                    "title": "Effective Date",
                                    "type": "string",
                                    "format": "date-time",
                                    "description": "Date the member joined their current loyalty tier.",
                                    "meta:xdmType": "date-time"
                                },
                                "currentThreshold": {
                                    "title": "Current Point Threshold",
                                    "type": "integer",
                                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                                    "meta:xdmType": "int"
                                },
                                "nextThreshold": {
                                    "title": "Next Point Threshold",
                                    "type": "integer",
                                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                                    "meta:xdmType": "int"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673313004645,
        "repo:lastModifiedDate": 1673313004645,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Adicionar o grupo de campos personalizado ao esquema

Agora você pode seguir as mesmas etapas para [adição de um grupo de campos padrão](#add-a-field-group) para adicionar este grupo de campos recém-criado ao esquema.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema. |

**Solicitação**

Essa solicitação atualiza (PATCH) o schema Membros de Fidelidade para incluir os campos no novo grupo de campos &quot;Camada de Fidelidade&quot;.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**Resposta**

Você pode ver que o grupo de campos foi adicionado com êxito, pois a resposta agora mostra o grupo de campos recém-adicionado no `meta:extends` e conter uma `$ref` para o grupo de campos no `allOf` atributo.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Exibir o esquema atual

Agora é possível executar uma solicitação do GET para visualizar o schema atual e ver como os grupos de campos adicionados contribuíram para a estrutura geral do schema.

**Formato da API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema. |

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Resposta**

Ao usar a variável `application/vnd.adobe.xed-full+json; version=1` `Accept` é possível ver o schema completo mostrando todas as propriedades. Essas propriedades são os campos contribuídos pela classe e pelos grupos de campos que foram usados para compor o schema. No exemplo de resposta abaixo, somente os campos adicionados recentemente são mostrados para espaço. É possível exibir o esquema completo, incluindo todas as propriedades e seus atributos, na [apêndice](#appendix) no final deste documento.

Em `"properties"`, você pode ver a variável `_{TENANT_ID}` namespace criado ao adicionar o grupo de campos personalizado. Dentro desse namespace, há o objeto &quot;fidelidade&quot; e os campos que foram definidos quando o grupo de campos foi criado.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "properties": {
        "_{TENANT_ID}": {
            "type": "object",
            "properties": {
                "loyaltyTier": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier.",
                            "meta:xdmType": "string"
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier.",
                            "meta:xdmType": "date-time"
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                            "meta:xdmType": "int"
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                            "meta:xdmType": "int"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "meta:xdmType": "object"
        }
    },
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:allFieldAccess": true
}
```

### Criar um tipo de dados

O grupo de campos Camada de fidelidade criado contém propriedades específicas que podem ser úteis em outros esquemas. Por exemplo, os dados podem ser assimilados como parte de um evento de experiência ou usados por um schema que implementa uma classe diferente. Nesse caso, faz sentido salvar a hierarquia de objetos como um tipo de dados para facilitar a reutilização da definição em outro lugar.

Os tipos de dados permitem definir uma hierarquia de objeto uma vez e fazer referência a ela em um campo da mesma forma que faria com qualquer outro tipo escalar.

Em outras palavras, os tipos de dados permitem o uso consistente de estruturas de vários campos, com mais flexibilidade do que grupos de campos, pois podem ser incluídos em qualquer lugar de um schema, adicionando-os como o &quot;tipo&quot; de um campo.

**Formato da API**

```http
POST /tenant/datatypes
```

**Solicitação**

A definição de um tipo de dados não requer `meta:extends` ou `meta:intendedToExtend` campos e não precisam ser aninhados sob a ID do locatário para evitar colisões.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
            "loyaltyTier": {
                "type": "object",
                "properties": {
                    "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                    },
                    "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                    },
                    "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                    },
                    "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                    }
                }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyaltyTier"
            }
        ]
      }'
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status de Resposta HTTP 201 (Criado) com um corpo de resposta contendo os detalhes do tipo de dados recém-criado, incluindo o `$id`, `meta:altIt`e `version`. Esses valores são somente leitura e são atribuídos pela variável [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
    "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
    "meta:resourceType": "datatypes",
    "version": "1.0",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Loyalty Tier data type",
    "definitions": {
        "loyaltyTier": {
            "type": "object",
            "properties": {
                "id": {
                    "title": "Loyalty Tier Identifier",
                    "type": "string",
                    "description": "Loyalty Tier Identifier.",
                    "meta:xdmType": "string"
                },
                "effectiveDate": {
                    "title": "Effective Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined their current loyalty tier.",
                    "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                    "title": "Current Point Threshold",
                    "type": "integer",
                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                    "meta:xdmType": "int"
                },
                "nextThreshold": {
                    "title": "Next Point Threshold",
                    "type": "integer",
                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                    "meta:xdmType": "int"
                }
            },
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673378256699,
        "repo:lastModifiedDate": 1673378256699,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Você pode executar uma solicitação de pesquisa (GET) usando o URL codificado `$id` URI para exibir o novo tipo de dados diretamente. Certifique-se de incluir a variável `version` em seu `Accept` para uma solicitação de pesquisa.

### Usar tipo de dados no schema

Agora que o tipo de dados Camada de fidelidade foi criado, você pode atualizar (PATCH) a variável `loyaltyTier` no grupo de campos criado para fazer referência ao tipo de dados no lugar dos campos que estavam lá anteriormente.

**Formato da API**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{FIELD_GROUP_ID}` | O `meta:altId` ou codificado por URL `$id` do grupo de campos a ser atualizado. |

**Solicitação**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "op": "replace",
            "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
            "value": {
                "loyaltyTier": {
                    "title": "Loyalty Tier",
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
                    "description": "Loyalty tier info"
                }
            }
        }
    ]
```

**Resposta**

A resposta agora inclui uma referência (`$ref`) ao tipo de dados no objeto &quot;fidelidade&quot; em vez dos campos que foram definidos anteriormente.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:resourceType": "mixins",
    "version": "1.1",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Captures info about the current loyalty tier of a customer.",
    "definitions": {
        "loyaltyTier": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyTier": {
                            "title": "Loyalty Tier",
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
                            "description": "Loyalty tier info",
                            "type": "object",
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673313004645,
        "repo:lastModifiedDate": 1673378970276,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

Se você executar uma solicitação do GET para pesquisar o esquema agora, a variável `loyaltyTier` mostra a referência ao tipo de dados em `meta:referencedFrom`:

```JSON
"_{TENANT_ID}": {
    "type": "object",
    "meta:xdmType": "object",
    "properties": {
        "loyaltyTier": {
            "title": "Loyalty Tier",
            "description": "Loyalty tier info",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "id": {
                    "title": "Loyalty Tier Identifier",
                    "type": "string",
                    "description": "Loyalty Tier Identifier.",
                    "meta:xdmType": "string"
                },
                "effectiveDate": {
                    "title": "Effective Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined their current loyalty tier.",
                    "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                    "title": "Current Point Threshold",
                    "type": "integer",
                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                    "meta:xdmType": "int"
                },
                "nextThreshold": {
                    "title": "Next Point Threshold",
                    "type": "integer",
                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                    "meta:xdmType": "int"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
    }
}
```

### Definir um descritor de identidade

Os esquemas são usados para assimilar dados em [!DNL Experience Platform]. Esses dados são usados em vários serviços para criar uma única visualização unificada de um indivíduo. Para ajudar nesse processo, os campos principais podem ser marcados como &quot;Identidade&quot; e, após a assimilação de dados, os dados nesses campos são inseridos no &quot;Gráfico de identidade&quot; desse indivíduo. Os dados do gráfico podem ser acessados em [[!DNL Real-Time Customer Profile]](../../profile/home.md) e outros [!DNL Experience Platform] serviços para fornecer uma visão unificada de cada cliente individual.

Os campos comumente marcados como &quot;Identidade&quot; incluem: endereço de e-mail, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR), ID do CRM ou outros campos de ID exclusivos. Considere todos os identificadores exclusivos específicos da organização, pois também podem ser bons campos de identidade.

Os descritores de identidade sinalizam que a variável `sourceProperty` do `sourceSchema` é um identificador exclusivo que deve ser considerado uma identidade.

Para obter mais informações sobre como trabalhar com descritores, consulte o [Guia do desenvolvedor do Registro de Schema](../api/getting-started.md).

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade no `personalEmail.address` para o esquema Membros da Fidelidade. Isso diz [!DNL Experience Platform] para usar o endereço de email do membro do programa de fidelidade como um identificador para ajudar a unir informações sobre o indivíduo. Essa chamada também define este campo como a identidade primária do schema ao definir `xdm:isPrimary` para `true`, que é um requisito [ativação do schema para uso no Perfil do cliente em tempo real](#profile).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE]
>
>Você pode listar os valores &quot;xdm:namespace&quot; disponíveis ou criar novos, usando o [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). O valor para &quot;xdm:property&quot; pode ser &quot;xdm:code&quot; ou &quot;xdm:id&quot;, dependendo do &quot;xdm:namespace&quot; usado.

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) com um corpo de resposta contendo os detalhes do descritor recém-criado, incluindo seu `@id`. O `@id` é um campo somente leitura atribuído pelo [!DNL Schema Registry] e é usado para referenciar o descritor na API.

```JSON
{
    "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/personalEmail/address",
    "imsOrg": "{ORG_ID}",
    "version": "1",
    "xdm:namespace": "Email",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

## Habilitar esquema para uso em [!DNL Real-Time Customer Profile] {#profile}

Depois que o esquema tiver um descritor de identidade primário aplicado, você poderá ativar o esquema Membros de Fidelidade para usar [!DNL Real-Time Customer Profile] adicionando uma `union` à `meta:immutableTags` atributo.

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com visualizações de união, consulte a seção sobre [sindicatos](../api/unions.md) no [!DNL Schema Registry] guia do desenvolvedor.

### Adicione um `union` tag

Para que um schema seja incluído na exibição de união mesclada, a variável `union` deve ser adicionada à tag `meta:immutableTags` do schema. Isso é feito por meio de uma solicitação PATCH para atualizar o esquema e adicionar um `meta:immutableTags` matriz com um valor de `union`.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que você está ativando para o Perfil. |

**Solicitação**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Resposta**

A resposta mostra que a operação foi executada com êxito e o schema agora contém um atributo de nível superior, `meta:immutableTags`, que é uma matriz que contém o valor, &quot;union&quot;.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673380280074,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Listar esquemas em uma união

Agora, você adicionou seu esquema com êxito à variável [!DNL XDM Individual Profile] união. Para ver uma lista de todos os schemas que fazem parte da mesma união, é possível executar uma solicitação do GET usando parâmetros de consulta para filtrar a resposta.

Usar o `property` parâmetro de consulta , você pode especificar que apenas schemas contenham um `meta:immutableTags` com um `meta:class` igual a `$id` do [!DNL XDM Individual Profile] classe são retornadas.

**Formato da API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**Solicitação**

A solicitação de exemplo abaixo retorna todos os esquemas que fazem parte do [!DNL XDM Individual Profile] união.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta é uma lista filtrada de schemas, que contém apenas aqueles que atendem a ambos os requisitos. Lembre-se de que, ao usar vários parâmetros de consulta, uma relação AND é assumida. O formato da resposta da lista depende do `Accept` cabeçalho enviado na solicitação.

```JSON
{
    "results": [
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
            "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
            "version": "1.2",
            "title": "Profile Schema"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
            "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
            "version": "1.3",
            "title": "CRM Onboarding"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
            "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
            "version": "1.1",
            "title": "Profile consents"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
            "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
            "version": "1.4",
            "title": "Loyalty Members"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 4
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```

## Próximas etapas

Ao seguir este tutorial, você terá composto um schema com êxito usando grupos de campos padrão e um grupo de campos definido. Agora é possível usar esse esquema para criar um conjunto de dados e assimilar dados de registro no Adobe Experience Platform.

O schema de membros de fidelidade completo, conforme criado em todo este tutorial, está disponível no apêndice a seguir. Ao observar o esquema, é possível ver como os grupos de campos contribuem para a estrutura geral e quais campos estão disponíveis para assimilação de dados.

Depois de criar mais de um schema, você pode definir relacionamentos entre eles usando descritores de relacionamento. Consulte o tutorial para [definição de uma relação entre dois schemas](relationship-api.md) para obter mais informações. Para obter exemplos detalhados de como executar todas as operações (GET, POST, PUT, PATCH e DELETE) no registro, consulte o [Guia do desenvolvedor do Registro de Schema](../api/getting-started.md) ao trabalhar com a API.

## Apêndice {#appendix}

As informações a seguir complementam o tutorial da API.

## Schema Concluir Membros da Fidelidade {#complete-schema}

Ao longo deste tutorial, um schema é composto para descrever os membros de um programa de fidelidade de varejo.

O esquema implementa o [!DNL XDM Individual Profile] e combina vários grupos de campos. Ele captura informações sobre os membros de fidelidade usando o padrão [!DNL Demographic Details], [!UICONTROL Detalhes de contato pessoal]e [!UICONTROL Detalhes da Fidelidade] grupos de campos, bem como por meio de um grupo de campo Camada de fidelidade personalizado definido durante o tutorial.

A seguir, é exibido o esquema Membros da Fidelidade concluído no formato JSON:

+++Exibir esquema completo

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "properties": {
        "_{TENANT_ID}": {
            "type": "object",
            "properties": {
                "loyaltyTier": {
                    "title": "Loyalty Tier",
                    "description": "Loyalty tier info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier.",
                            "meta:xdmType": "string"
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier.",
                            "meta:xdmType": "date-time"
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                            "meta:xdmType": "int"
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                            "meta:xdmType": "int"
                        }
                    },
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
                }
            },
            "meta:xdmType": "object"
        },
        "_id": {
            "title": "Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "A unique identifier for the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "@id"
        },
        "_repo": {
            "properties": {
                "createDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:immutable": true,
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "repo:createDate"
                },
                "modifyDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "repo:modifyDate"
                }
            },
            "type": "object",
            "meta:xdmType": "object",
            "meta:xedConverted": true
        },
        "billingAddress": {
            "title": "Billing Address",
            "description": "Billing postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:billingAddress"
        },
        "createdByBatchID": {
            "title": "Created by batch identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The dataset files in Catalog which has been originating the creation of the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:createdByBatchID"
        },
        "faxPhone": {
            "title": "Fax Phone",
            "description": "Fax phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:faxPhone"
        },
        "homeAddress": {
            "title": "Home Address",
            "description": "A home postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:homeAddress"
        },
        "homePhone": {
            "title": "Home Phone",
            "description": "Home phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:homePhone"
        },
        "loyalty": {
            "type": "object",
            "description": "Captures details related to the customer's loyalty rewards.",
            "properties": {
                "joinDate": {
                    "title": "Program Join Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date which the visitor registered for the loyalty program.",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "xdm:joinDate"
                },
                "loyaltyID": {
                    "title": "Program ID",
                    "type": "array",
                    "items": {
                        "type": "string",
                        "meta:xdmType": "string"
                    },
                    "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
                    "meta:xdmType": "array",
                    "meta:xdmField": "xdm:loyaltyID"
                },
                "points": {
                    "title": "Program Points Balance",
                    "type": "number",
                    "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
                    "meta:xdmType": "number",
                    "meta:xdmField": "xdm:points"
                },
                "pointsExpiration": {
                    "title": "Points Expiration",
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "pointsExpirationDate": {
                                "type": "string",
                                "format": "date-time",
                                "description": "Date on which the given portion of the loyalty points expire.",
                                "meta:xdmType": "date-time",
                                "meta:xdmField": "xdm:pointsExpirationDate"
                            },
                            "pointsExpiring": {
                                "title": "Points Expiring",
                                "type": "number",
                                "description": "Point balance expiring as of the associated expiration date.",
                                "meta:xdmType": "number",
                                "meta:xdmField": "xdm:pointsExpiring"
                            }
                        },
                        "meta:xdmType": "object"
                    },
                    "meta:xdmType": "array",
                    "meta:xdmField": "xdm:pointsExpiration"
                },
                "pointsRedeemed": {
                    "title": "Points Redeemed",
                    "type": "number",
                    "description": "Amount of points applied toward a purchase or otherwise redeemed.",
                    "meta:xdmType": "number",
                    "meta:xdmField": "xdm:pointsRedeemed"
                },
                "program": {
                    "title": "Program Name",
                    "type": "string",
                    "description": "This should define the loyalty progam in which a visitor is enrolled.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:program"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "tier": {
                    "title": "Tier",
                    "type": "string",
                    "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:tier"
                },
                "upgradeDate": {
                    "title": "Program Name",
                    "type": "string",
                    "description": "Date which the customer was upgraded to the next tier level.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:upgradeDate"
                }
            },
            "meta:xdmType": "object",
            "meta:xdmField": "xdm:loyalty"
        },
        "mailingAddress": {
            "title": "Mailing Address",
            "description": "Mailing postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:mailingAddress"
        },
        "mobilePhone": {
            "title": "Mobile Phone",
            "description": "Mobile phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:mobilePhone"
        },
        "modifiedByBatchID": {
            "title": "Modified by batch identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "title": "Birth date(YYYY-MM-DD)",
                    "type": "string",
                    "format": "date",
                    "description": "The full date a person was born.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:birthDate"
                },
                "birthDayAndMonth": {
                    "title": "Birth date (MM-DD)",
                    "type": "string",
                    "pattern": "[0-1][0-9]-[0-9][0-9]",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:birthDayAndMonth"
                },
                "birthYear": {
                    "title": "Birth year",
                    "type": "integer",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
                    "minimum": 1,
                    "maximum": 32767,
                    "meta:xdmType": "short",
                    "meta:xdmField": "xdm:birthYear"
                },
                "gender": {
                    "title": "Gender",
                    "type": "string",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Non-specific"
                    },
                    "description": "Gender identity of the person.\n",
                    "default": "not_specified",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:gender"
                },
                "maritalStatus": {
                    "title": "Marital Status",
                    "type": "string",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "married": "Married",
                        "single": "Single",
                        "divorced": "Divorced",
                        "widowed": "Widowed",
                        "not_specified": "Not Specified"
                    },
                    "description": "Describes a person's relationship with a significant other.",
                    "default": "not_specified",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:maritalStatus"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "title": "Courtesy title",
                            "type": "string",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:courtesyTitle"
                        },
                        "firstName": {
                            "title": "First name",
                            "type": "string",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:firstName"
                        },
                        "fullName": {
                            "title": "Full name",
                            "type": "string",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:fullName"
                        },
                        "lastName": {
                            "title": "Last name",
                            "type": "string",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:lastName"
                        },
                        "middleName": {
                            "title": "Middle name",
                            "type": "string",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:middleName"
                        },
                        "suffix": {
                            "title": "Suffix",
                            "type": "string",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:suffix"
                        }
                    },
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
                    "meta:xdmField": "xdm:name"
                },
                "nationality": {
                    "title": "Nationality",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:nationality"
                },
                "taxId": {
                    "title": "Tax ID",
                    "type": "string",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:taxId"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The type of individual in different business contexts like B2C.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:type"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
            "meta:xdmField": "xdm:person"
        },
        "personID": {
            "title": "Person ID",
            "description": "Unique identifier of Person/Profile fragment.",
            "type": "string",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:personID"
        },
        "personalEmail": {
            "title": "Personal Email",
            "description": "A personal email address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "address": {
                    "title": "Address",
                    "type": "string",
                    "format": "email",
                    "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:address",
                    "minLength": 1
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the email address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The way the account relates to the person for example 'work' or 'personal'.",
                    "meta:enum": {
                        "unknown": "Unknown",
                        "personal": "Personal",
                        "work": "Work",
                        "education": "Education"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:type"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
            "meta:xdmField": "xdm:personalEmail",
            "required": [
                "address"
            ]
        },
        "repositoryCreatedBy": {
            "title": "Created by user identifier",
            "type": "string",
            "description": "User ID of who created the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
            "title": "Modified by user identifier",
            "type": "string",
            "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "shippingAddress": {
            "title": "Shipping Address",
            "description": "Shipping postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:shippingAddress"
        }
    },
    "required": [
        "personalEmail"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673380280074,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:allFieldAccess": true
}
```

+++
