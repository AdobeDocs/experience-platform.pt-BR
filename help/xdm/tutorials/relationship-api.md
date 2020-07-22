---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definir uma relação entre dois schemas usando a API do Registro de Schemas
topic: tutorials
translation-type: tm+mt
source-git-commit: 849142e44c56f2958e794ca6aefaccd5670c28ba
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 1%

---


# Definir uma relação entre dois schemas usando a [!DNL Schema Registry] API


A capacidade de entender os relacionamentos entre seus clientes e suas interações com a sua marca em vários canais é uma parte importante do Adobe Experience Platform. A definição desses relacionamentos dentro da estrutura dos schemas [!DNL Experience Data Model] (XDM) permite obter insights complexos sobre os dados do cliente.

Embora as relações com os schemas possam ser inferidas com o uso do schema da união e [!DNL Real-time Customer Profile], isso se aplica somente aos schemas que compartilham a mesma classe. Para estabelecer uma relação entre dois schemas pertencentes a classes diferentes, um campo **de** relacionamento dedicado deve ser adicionado a um schema de origem, que faz referência à identidade de um schema de destino.

Este documento fornece um tutorial para definir uma relação um para um entre dois schemas definidos pela sua organização usando o [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Introdução

Este tutorial requer uma compreensão de trabalho do [!DNL Experience Data Model] (XDM) e do [!DNL XDM System]. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação em [!DNL Experience Platform].
   * [Noções básicas da composição](../schema/composition.md)do schema: Uma introdução dos blocos de construção dos schemas XDM.
* [!DNL Real-time Customer Profile](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o guia [do](../api/getting-started.md) desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas à [!DNL Schema Registry] API com êxito. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho [!DNL Accept] e seus possíveis valores).

## Definir um schema de origem e de destino {#define-schemas}

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Este tutorial cria uma relação entre os membros do programa de fidelidade atual de uma organização (definido em um &quot;[!DNL Loyalty Members]&quot; schema) e seus hotéis favoritos (definido em um schema &quot;[!DNL Hotels]&quot;).

As relações de Schema são representadas por um schema **de** origem com um campo que se refere a outro campo dentro de um schema **de** destino. Nas etapas a seguir, &quot;[!DNL Loyalty Members]&quot; será o schema de origem, enquanto &quot;[!DNL Hotels]&quot; atuará como o schema de destino.

>[!IMPORTANT] Para estabelecer uma relação, ambos os schemas devem ter identidades primárias definidas e estar habilitados para [!DNL Real-time Customer Profile]. Consulte a seção sobre como [ativar um schema para uso no Perfil](./create-schema-api.md#profile) no tutorial de criação do schema se precisar de orientação sobre como configurar seus schemas de acordo.

Para definir uma relação entre dois schemas, primeiro você deve adquirir os `$id` valores para ambos os schemas. Se você souber os nomes para exibição (`title`) dos schemas, poderá encontrar seus `$id` valores fazendo uma solicitação GET para o `/tenant/schemas` endpoint na [!DNL Schema Registry] API.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>O [!DNL Accept] cabeçalho `application/vnd.adobe.xed-id+json` retorna somente os títulos, IDs e versões dos schemas resultantes.

**Resposta**

Uma resposta bem-sucedida retorna uma lista de schemas definidos pela sua organização, incluindo seus `name`, `$id`, `meta:altId`e `version`.

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

Registre os `$id` valores dos dois schemas entre os quais deseja definir uma relação. Esses valores serão usados em etapas posteriores.

## Definir um campo de referência para o schema de origem

Dentro do [!DNL Schema Registry], os descritores de relacionamento funcionam de forma semelhante às chaves estrangeiras nas tabelas de banco de dados relacionais: um campo no schema de origem atua como uma referência ao campo de identidade **** principal de um schema de destino. Se o schema de origem não tiver um campo para essa finalidade, talvez seja necessário criar uma combinação com o novo campo e adicioná-la ao schema. Esse novo campo deve ter um `type` valor de &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>Ao contrário do schema de destino, o schema de origem não pode usar sua identidade primária como campo de referência.

Neste tutorial, o schema de destino &quot;[!DNL Hotels]&quot; contém um `email` campo que serve como a identidade principal do schema e, portanto, também atuará como seu campo de referência. No entanto, o schema de origem &quot;[!DNL Loyalty Members]&quot; não tem um campo dedicado para ser usado como referência e deve receber uma nova combinação que adicione um novo campo ao schema: `favoriteHotel`.

>[!NOTE] Se o seu schema de origem já tiver um campo dedicado que você planeja usar como campo de referência, você pode pular para a etapa de [criação de um descritor](#reference-identity)de referência.

### Criar uma nova mistura

Para adicionar um novo campo a um schema, ele deve primeiro ser definido em uma mistura. Você pode criar um novo mixin, fazendo uma solicitação POST para o `/tenant/mixins` terminal.

**Formato da API**

```http
POST /tenant/mixins
```

**Solicitação**

A solicitação a seguir cria um novo mixin que adiciona um `favoriteHotel` campo sob a `_{TENANT_ID}` namespace de qualquer schema ao qual ele seja adicionado.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
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

Uma resposta bem-sucedida retorna os detalhes da combinação recém-criada.

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
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
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
| `$id` | O sistema gerou um identificador exclusivo somente leitura para a nova combinação. Assume a forma de um URI. |

Registre o `$id` URI da mistura, a ser usado na próxima etapa da adição do mixin ao schema de origem.

### Adicionar a mistura ao schema de origem

Depois de criar um mixin, você pode adicioná-lo ao schema de origem, fazendo uma solicitação PATCH ao `/tenant/schemas/{SCHEMA_ID}` endpoint.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `$id` URI codificado por URL ou `meta:altId` do schema de origem. |

**Solicitação**

A solicitação a seguir adiciona a combinação &quot;[!DNL Favorite Hotel]&quot; ao schema &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | A operação PATCH a ser executada. Esta solicitação usa a `add` operação. |
| `path` | O caminho para o campo schema no qual o novo recurso será adicionado. Ao adicionar misturas a schemas, o valor deve ser &quot;/allOf/-&quot;. |
| `value.$ref` | A `$id` mistura a ser adicionada. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema atualizado, que agora inclui o `$ref` valor da mistura adicionada sob sua `allOf` matriz.

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
    "imsOrg": "{IMS_ORG}",
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

Os campos de Schema devem ter um descritor de identidade de referência aplicado a eles se estiverem sendo usados como referência de outros schemas em um relacionamento. Como o `favoriteHotel` campo em &quot;[!DNL Loyalty Members]&quot; fará referência ao `email` campo em &quot;[!DNL Hotels]&quot;, `email` deve ser fornecido um descritor de identidade de referência.

Crie um descritor de referência para o schema de destino, fazendo uma solicitação POST para o `/tenant/descriptors` ponto final.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um descritor de referência para o `email` campo no schema de destino &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para descritores de referência, o valor deve ser &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | O `$id` URL do schema de destino. |
| `xdm:sourceVersion` | O número da versão do schema de destino. |
| `sourceProperty` | O caminho para o campo de identidade principal do schema de destino. |
| `xdm:identityNamespace` | A namespace de identidade do campo de referência. Essa deve ser a mesma namespace usada ao definir o campo que a identidade principal do schema. Consulte a visão geral [da namespace de](../../identity-service/home.md) identidade para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor de referência recém-criado para o schema de destino.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Criar um descritor de relação {#create-descriptor}

Os descritores de relacionamento estabelecem uma relação um para um entre um schema de origem e um schema de destino. Depois de definir um descritor de referência para o schema de destino, você pode criar um novo descritor de relação, enviando uma solicitação POST para o `/tenant/descriptors` ponto de extremidade.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/email"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor a ser criado. O `@type` valor dos descritores de relação é &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | O `$id` URL do schema de origem. |
| `xdm:sourceVersion` | O número da versão do schema de origem. |
| `xdm:sourceProperty` | O caminho para o campo de referência no schema de origem. |
| `xdm:destinationSchema` | O `$id` URL do schema de destino. |
| `xdm:destinationVersion` | O número da versão do schema de destino. |
| `xdm:destinationProperty` | O caminho para o campo de referência no schema de destino. |

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

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas. Para obter mais informações sobre como trabalhar com descritores usando a [!DNL Schema Registry] API, consulte o guia [do desenvolvedor do Registro de](../api/descriptors.md)Schemas. Para obter etapas sobre como definir relações de schema na interface do usuário, consulte o tutorial sobre como [definir relações de schema usando o Editor](relationship-ui.md)de Schemas.
