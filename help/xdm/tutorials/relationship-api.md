---
keywords: Experience Platform;home;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;registro de esquemas;esquema;Esquemas;relacionamento;Relacionamento;descritor de relacionamento;descritor de relacionamento;identidade de referência;identidade de referência;
title: Definir uma relação entre dois esquemas usando a API do registro de esquema
description: Este documento fornece um tutorial para definir uma relação individualizada entre dois esquemas definidos pela organização usando a API do Registro de esquemas.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 2%

---

# Definir uma relação entre dois esquemas usando a API [!DNL Schema Registry]

A capacidade de entender os relacionamentos entre seus clientes e as interações deles com sua marca em vários canais é uma parte importante do Adobe Experience Platform. A definição dessas relações na estrutura dos esquemas do [!DNL Experience Data Model] (XDM) permite que você obtenha insights complexos sobre os dados do cliente.

Embora as relações de esquema possam ser inferidas por meio do uso do esquema de união e [!DNL Real-Time Customer Profile], isso se aplica somente a esquemas que compartilham a mesma classe. Para estabelecer uma relação entre dois esquemas pertencentes a classes diferentes, um campo de relação dedicado deve ser adicionado a um **esquema de origem**, que indica a identidade de um **esquema de referência** separado.

>[!NOTE]
>
>A API do Registro de esquemas refere-se aos esquemas de referência como &quot;esquemas de destino&quot;. Estes não devem ser confundidos com esquemas de destino em [Conjuntos de mapeamento de Preparo de Dados](../../data-prep/mapping-set.md) ou esquemas para [conexões de destino](../../destinations/home.md).

Este documento fornece um tutorial para definir uma relação um para um entre dois esquemas definidos pela sua organização usando o [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Introdução

Este tutorial requer uma compreensão funcional do [!DNL Experience Data Model] (XDM) e do [!DNL XDM System]. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): uma visão geral do XDM e sua implementação em [!DNL Experience Platform].
   * [Noções básicas sobre a composição de esquema](../schema/composition.md): uma introdução aos blocos de construção de esquemas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, consulte o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API [!DNL Schema Registry] com êxito. Isso inclui o `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho [!DNL Accept] e seus valores possíveis).

## Definir um esquema de origem e de referência {#define-schemas}

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Este tutorial cria uma relação entre os membros do programa de fidelidade atual de uma organização (definido em um esquema &quot;[!DNL Loyalty Members]&quot;) e seus hotéis favoritos (definido em um esquema &quot;[!DNL Hotels]&quot;).

As relações de esquema são representadas por um **esquema de origem** com um campo que faz referência a outro campo dentro de um **esquema de referência**. Nas etapas a seguir, &quot;[!DNL Loyalty Members]&quot; será o esquema de origem, enquanto &quot;[!DNL Hotels]&quot; atuará como o esquema de referência.

>[!IMPORTANT]
>
>Para estabelecer uma relação, ambos os esquemas devem ter identidades primárias definidas e estar habilitados para [!DNL Real-Time Customer Profile]. Consulte a seção sobre [habilitação de um esquema para uso no Perfil](./create-schema-api.md#profile) no tutorial de criação de esquema se precisar de orientação sobre como configurar seus esquemas adequadamente.

Para definir uma relação entre dois esquemas, primeiro você deve adquirir os valores `$id` para ambos os esquemas. Se você souber os nomes para exibição (`title`) dos esquemas, poderá encontrar seus valores `$id` fazendo uma solicitação GET para o ponto de extremidade `/tenant/schemas` na API [!DNL Schema Registry].

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
>O cabeçalho [!DNL Accept] `application/vnd.adobe.xed-id+json` retorna somente os títulos, as IDs e as versões dos esquemas resultantes.

**Resposta**

Uma resposta bem-sucedida retorna uma lista de esquemas definidos pela sua organização, incluindo os `name`, `$id`, `meta:altId` e `version`.

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

Registre os `$id` valores dos dois esquemas entre os quais você deseja definir uma relação. Esses valores serão usados em etapas posteriores.

## Definir um campo de referência para o esquema de origem

Dentro de [!DNL Schema Registry], os descritores de relacionamento funcionam de forma semelhante às chaves estrangeiras nas tabelas do banco de dados relacional: um campo no esquema de origem atua como uma referência ao campo de identidade principal de um esquema de referência. Se o esquema de origem não tiver um campo para essa finalidade, talvez seja necessário criar um grupo de campos de esquema com o novo campo e adicioná-lo ao esquema. Este novo campo deve ter um valor `type` de `string`.

>[!IMPORTANT]
>
>O esquema de origem não pode usar sua identidade primária como um campo de referência.

Neste tutorial, o esquema de referência &quot;[!DNL Hotels]&quot; contém um campo `hotelId` que serve como a identidade principal do esquema. No entanto, o esquema de origem &quot;[!DNL Loyalty Members]&quot; não tem um campo dedicado a ser usado como referência para `hotelId` e, portanto, um grupo de campos personalizado precisa ser criado para adicionar um novo campo ao esquema: `favoriteHotel`.

>[!NOTE]
>
>Se o esquema de origem já tiver um campo dedicado que você planeja usar como campo de referência, pule para a etapa em [criando um descritor de referência](#reference-identity).

### Criar um novo grupo de campos

Para adicionar um novo campo a um esquema, ele deve primeiro ser definido em um grupo de campos. Você pode criar um novo grupo de campos fazendo uma solicitação POST para o ponto de extremidade `/tenant/fieldgroups`.

**Formato da API**

```http
POST /tenant/fieldgroups
```

**Solicitação**

A solicitação a seguir cria um novo grupo de campos que adiciona um campo `favoriteHotel` no namespace `_{TENANT_ID}` de qualquer esquema ao qual ele tenha sido adicionado.

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

{style="table-layout:auto"}

Registre o URI `$id` do grupo de campos, a ser usado na próxima etapa da adição do grupo de campos ao esquema de origem.

### Adicionar o grupo de campos ao esquema de origem

Depois de criar um grupo de campos, você pode adicioná-lo ao esquema de origem fazendo uma solicitação PATCH para o ponto de extremidade `/tenant/schemas/{SCHEMA_ID}`.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URI `$id` codificado na URL ou `meta:altId` do esquema de origem. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir adiciona o grupo de campos &quot;[!DNL Favorite Hotel]&quot; ao esquema &quot;[!DNL Loyalty Members]&quot;.

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
| `op` | A operação do PATCH a ser executada. Esta solicitação usa a operação `add`. |
| `path` | O caminho para o campo de esquema onde o novo recurso será adicionado. Ao adicionar grupos de campos a esquemas, o valor deve ser &quot;/allOf/-&quot;. |
| `value.$ref` | O `$id` do grupo de campos a ser adicionado. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do esquema atualizado, que agora inclui o valor `$ref` do grupo de campos adicionado em sua matriz `allOf`.

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

Os campos de esquema devem ter um descritor de identidade de referência aplicado a eles se estiverem sendo usados como referência para outro esquema em uma relação. Como o campo `favoriteHotel` em &quot;[!DNL Loyalty Members]&quot; se referirá ao campo `hotelId` em &quot;[!DNL Hotels]&quot;, `favoriteHotel` deve receber um descritor de identidade de referência.

Crie um descritor de referência para o esquema de origem fazendo uma solicitação POST para o ponto de extremidade `/tenant/descriptors`.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um descritor de referência para o campo `favoriteHotel` no esquema de origem &quot;[!DNL Loyalty Members]&quot;.

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
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para descritores de referência, o valor deve ser `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | A URL `$id` do esquema de origem. |
| `xdm:sourceVersion` | O número da versão do esquema de origem. |
| `sourceProperty` | O caminho para o campo no esquema de origem que será usado para fazer referência à identidade principal do esquema de referência. |
| `xdm:identityNamespace` | O namespace de identidade do campo de referência. Deve ser o mesmo namespace que a identidade primária do esquema de referência. Consulte a [visão geral do namespace de identidade](../../identity-service/home.md) para obter mais informações. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor de referência recém-criado para o campo de origem.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Criar um descritor de relacionamento {#create-descriptor}

Os descritores de relacionamento estabelecem uma relação um para um entre um esquema de origem e um esquema de referência. Depois de definir um descritor de identidade de referência para o campo apropriado no esquema de origem, você pode criar um novo descritor de relacionamento fazendo uma solicitação POST para o ponto de extremidade `/tenant/descriptors`.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um novo descritor de relação, com &quot;[!DNL Loyalty Members]&quot; como esquema de origem e &quot;[!DNL Hotels]&quot; como esquema de referência.

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
| `@type` | O tipo de descritor a ser criado. O valor `@type` dos descritores de relacionamento é `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | A URL `$id` do esquema de origem. |
| `xdm:sourceVersion` | O número da versão do esquema de origem. |
| `xdm:sourceProperty` | O caminho para o campo de referência no esquema de origem. |
| `xdm:destinationSchema` | A URL `$id` do esquema de referência. |
| `xdm:destinationVersion` | O número da versão do esquema de referência. |
| `xdm:destinationProperty` | O caminho para o campo de identidade principal no esquema de referência. |

{style="table-layout:auto"}

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

Ao seguir este tutorial, você criou uma relação um para um entre dois esquemas com sucesso. Para obter mais informações sobre como trabalhar com descritores usando a API [!DNL Schema Registry], consulte o [guia do desenvolvedor do Registro de Esquemas](../api/descriptors.md). Para obter etapas sobre como definir relações de esquema na interface, consulte o tutorial em [definição de relações de esquema usando o Editor de esquemas](relationship-ui.md).
