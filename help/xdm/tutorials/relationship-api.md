---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Modelo de dados, Registro de esquema, esquema, esquema, esquemas, esquemas, esquemas, relacionamento, relacionamento, descritor de relacionamento, Descritor de relacionamento, identidade de referência, Identidade de referência;
solution: Experience Platform
title: Definir um relacionamento entre dois esquemas usando a API do Registro de esquema
description: Este documento fornece um tutorial para definir uma relação um para um entre dois schemas definidos pela organização usando a API do Registro de Schema.
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 3%

---

# Definir uma relação entre dois schemas usando o [!DNL Schema Registry] API

A capacidade de entender os relacionamentos entre seus clientes e suas interações com a marca em vários canais é uma parte importante do Adobe Experience Platform. Definir esses relacionamentos dentro da estrutura de [!DNL Experience Data Model] Os esquemas (XDM) permitem que você obtenha insights complexos sobre os dados do cliente.

Embora os relacionamentos de schema possam ser inferidos por meio do uso do schema de união e [!DNL Real-time Customer Profile], isso se aplica somente a esquemas que compartilham a mesma classe. Para estabelecer uma relação entre dois schemas pertencentes a classes diferentes, um campo de relacionamento dedicado deve ser adicionado a um schema de origem, que faz referência à identidade de um schema de destino.

Este documento fornece um tutorial para definir uma relação um para um entre dois schemas definidos pela organização usando o [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Introdução

Este tutorial requer uma compreensão funcional do [!DNL Experience Data Model] (XDM) e [!DNL XDM System]. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no [!DNL Experience Platform].
   * [Noções básicas da composição do schema](../schema/composition.md): Uma introdução dos blocos de construção dos esquemas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para o [!DNL Schema Registry] API. Isso inclui as `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção para a [!DNL Accept] e seus possíveis valores).

## Definir um esquema de origem e de destino {#define-schemas}

Espera-se que você já tenha criado os dois schemas que serão definidos na relação. Este tutorial cria uma relação entre membros do programa de fidelidade atual de uma organização (definido em um &quot;[!DNL Loyalty Members]&quot; schema) e seus hotéis favoritos (definidos em um &quot;[!DNL Hotels]&quot; schema).

Os relacionamentos de esquema são representados por um **esquema de origem** ter um campo que se refere a outro campo dentro de um **esquema de destino**. Nas etapas a seguir, &quot;[!DNL Loyalty Members]&quot; será o schema de origem, enquanto &quot;[!DNL Hotels]&quot; atuará como o schema de destino.

>[!IMPORTANT]
>
>Para estabelecer uma relação, ambos os esquemas devem ter identidades primárias definidas e devem ser habilitados para [!DNL Real-time Customer Profile]. Consulte a seção sobre [ativar um esquema para usar no Perfil](./create-schema-api.md#profile) no tutorial de criação de esquema se você precisar de orientação sobre como configurar seus esquemas adequadamente.

Para definir uma relação entre dois schemas, primeiro você deve adquirir o `$id` para ambos os esquemas. Se você souber os nomes de exibição (`title`) dos esquemas, você pode encontrar seus `$id` ao fazer uma solicitação GET para a variável `/tenant/schemas` endpoint no [!DNL Schema Registry] API.

**Formato da API**

```http
GET /tenant/schemas
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>O [!DNL Accept] header `application/vnd.adobe.xed-id+json` retorna somente os títulos, IDs e versões dos schemas resultantes.

**Resposta**

Uma resposta bem-sucedida retorna uma lista de esquemas definidos pela organização, incluindo seus `name`, `$id`, `meta:altId`e `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Registre o `$id` dos dois schemas que você deseja definir uma relação entre. Esses valores serão usados em etapas posteriores.

## Definir um campo de referência para o schema de origem

No [!DNL Schema Registry], descritores de relacionamento funcionam de forma semelhante a chaves estrangeiras em tabelas de banco de dados relacionais: um campo no schema de origem atua como uma referência para o campo de identidade primário de um schema de destino. Se o schema de origem não tiver um campo para essa finalidade, talvez seja necessário criar um grupo de campos de esquema com o novo campo e adicioná-lo ao schema. Este novo campo deve ter um `type` valor de &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>Diferente do schema de destino, o schema de origem não pode usar sua identidade primária como um campo de referência.

Neste tutorial, o schema de destino &quot;[!DNL Hotels]&quot; contém um `hotelId` que serve como a identidade primária do schema e, portanto, também atuará como seu campo de referência. No entanto, o schema de origem &quot;[!DNL Loyalty Members]&quot; não tem um campo dedicado para ser usado como referência e deve receber um novo grupo de campos que adicione um novo campo ao schema: `favoriteHotel`.

>[!NOTE]
>
>Se o schema de origem já tiver um campo dedicado que você planeja usar como um campo de referência, ignore a etapa em [criação de um descritor de referência](#reference-identity).

### Criar um novo grupo de campos

Para adicionar um novo campo a um schema, ele deve primeiro ser definido em um grupo de campos. Você pode criar um novo grupo de campos fazendo uma solicitação de POST para a variável `/tenant/fieldgroups` endpoint .

**Formato da API**

```http
POST /tenant/fieldgroups
```

**Solicitação**

A solicitação a seguir cria um novo grupo de campos que adiciona um `favoriteHotel` no campo `_{TENANT_ID}` namespace de qualquer schema ao qual ele for adicionado.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do grupo de campos recém-criado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel field group for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
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
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `$id` | O identificador exclusivo gerado pelo sistema, somente leitura, do novo grupo de campos. Assume a forma de um URI. |

{style=&quot;table-layout:auto&quot;}

Registre o `$id` URI do grupo de campos, a ser usado na próxima etapa de adicionar o grupo de campos ao schema de origem.

### Adicionar o grupo de campos ao schema de origem

Depois de criar um grupo de campos, você pode adicioná-lo ao schema de origem fazendo uma solicitação de PATCH para a variável `/tenant/schemas/{SCHEMA_ID}` endpoint .

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URL codificado `$id` URI ou `meta:altId` do schema de origem. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir adiciona o &quot;[!DNL Favorite Hotel]&quot; grupo de campos para o &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Propriedade | Descrição |
| --- | --- |
| `op` | A operação PATCH a ser executada. Essa solicitação usa o `add` operação. |
| `path` | O caminho para o campo de esquema onde o novo recurso será adicionado. Ao adicionar grupos de campos a schemas, o valor deve ser &quot;/allOf/-&quot;. |
| `value.$ref` | O `$id` do grupo de campos a ser adicionado. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema atualizado, que agora inclui o `$ref` valor do grupo de campos adicionados em seu `allOf` matriz.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{ORG_ID}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Criar um descritor de identidade de referência {#reference-identity}

Os campos de esquema devem ter um descritor de identidade de referência aplicado a eles se estiverem sendo usados como referência de outros esquemas em um relacionamento. Como a variável `favoriteHotel` no campo &quot;[!DNL Loyalty Members]&quot; fará referência ao `hotelId` no campo &quot;[!DNL Hotels]&quot;, `hotelId` deve ser fornecido um descritor de identidade de referência.

Crie um descritor de referência para o schema de destino fazendo uma solicitação de POST para a variável `/tenant/descriptors` endpoint .

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um descritor de referência para a variável `hotelId` no schema de destino &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para descritores de referência, o valor deve ser &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | O `$id` URL do esquema de destino. |
| `xdm:sourceVersion` | O número da versão do schema de destino. |
| `sourceProperty` | O caminho para o campo de identidade principal do esquema de destino. |
| `xdm:identityNamespace` | O namespace de identidade do campo de referência. Deve ser o mesmo namespace usado ao definir o campo como a identidade primária do schema. Consulte a [visão geral do namespace de identidade](../../identity-service/home.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor de referência recém-criado para o esquema de destino.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Criar um descritor de relacionamento {#create-descriptor}

Os descritores de relacionamento estabelecem uma relação um para um entre um schema de origem e um schema de destino. Depois de definir um descritor de referência para o schema de destino, você pode criar um novo descritor de relacionamento fazendo uma solicitação de POST para a `/tenant/descriptors` endpoint .

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um novo descritor de relacionamento, com &quot;[!DNL Loyalty Members]&quot; como o schema de origem e &quot;[!DNL Legacy Loyalty Members]&quot; como o schema de destino.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor a ser criado. O `@type` o valor para descritores de relacionamento é &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | O `$id` URL do schema de origem. |
| `xdm:sourceVersion` | O número da versão do schema de origem. |
| `xdm:sourceProperty` | O caminho para o campo de referência no schema de origem. |
| `xdm:destinationSchema` | O `$id` URL do esquema de destino. |
| `xdm:destinationVersion` | O número da versão do schema de destino. |
| `xdm:destinationProperty` | O caminho para o campo de referência no schema de destino. |

{style=&quot;table-layout:auto&quot;}

### Resposta

Uma resposta bem-sucedida retorna os detalhes do descritor de relacionamento recém-criado.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas. Para obter mais informações sobre como trabalhar com descritores usando o [!DNL Schema Registry] API, consulte o [Guia do desenvolvedor do Registro de Schema](../api/descriptors.md). Para obter etapas sobre como definir relações de esquema na interface do usuário, consulte o tutorial em [definição de relações de esquema usando o Editor de esquema](relationship-ui.md).
