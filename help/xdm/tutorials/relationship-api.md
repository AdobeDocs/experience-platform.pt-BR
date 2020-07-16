---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definir uma relação entre dois schemas usando a API do Registro de Schemas
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 1%

---


# Definir uma relação entre dois schemas usando a [!DNL Schema Registry] API


A capacidade de entender os relacionamentos entre seus clientes e suas interações com a sua marca em vários canais é uma parte importante do Adobe Experience Platform. A definição desses relacionamentos dentro da estrutura dos schemas [!DNL Experience Data Model] (XDM) permite obter insights complexos sobre os dados do cliente.

Este documento fornece um tutorial para definir uma relação um para um entre dois schemas definidos pela sua organização usando o [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Introdução

Este tutorial requer uma compreensão de trabalho do [!DNL Experience Data Model] (XDM) e do [!DNL XDM System]. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no Experience Platform.
   * [Noções básicas da composição](../schema/composition.md)do schema: Uma introdução dos blocos de construção dos schemas XDM.
* [!DNL Real-time Customer Profile](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o guia [do](../api/getting-started.md) desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas à [!DNL Schema Registry] API com êxito. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).

## Definir um schema de origem e de destino {#define-schemas}

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Este tutorial cria uma relação entre os membros do programa de fidelidade atual de uma organização (definido em um schema &quot;Membros da Fidelidade&quot;) e seus hotéis favoritos (definido em um schema &quot;Hotéis&quot;).

As relações de Schema são representadas por um schema **[!UICONTROL de]** origem com um campo que se refere a outro campo dentro de um schema **[!UICONTROL de]** destino. Nas etapas a seguir, &quot;Membros[!UICONTROL de]fidelidade&quot; será o schema de origem, enquanto &quot;[!UICONTROL Hotéis]&quot; atuará como o schema de destino.

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
>O cabeçalho Accept (Aceitar) `application/vnd.adobe.xed-id+json` retorna somente os títulos, IDs e versões dos schemas resultantes.

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

## Definir campos de referência para ambos os schemas

Dentro do [!DNL Schema Registry], os descritores de relacionamento funcionam de forma semelhante às chaves estrangeiras nas tabelas SQL: um campo no schema de origem atua como uma referência para um campo de um schema de destino. Ao definir um relacionamento, cada schema deve ter um campo dedicado para ser usado como referência para o outro schema.

>[!IMPORTANT]
>
>Se os schemas forem ativados para uso em, [!DNL Real-time Customer Profile](../../profile/home.md)o campo de referência para o schema de destino deve ser sua identidade **** principal. Isso é explicado mais detalhadamente neste tutorial.

Se um dos schemas não tiver um campo para essa finalidade, talvez seja necessário criar uma combinação com o novo campo e adicioná-lo ao schema. Esse novo campo deve ter um `type` valor de &quot;string&quot;.

Para os fins deste tutorial, o schema de destino &quot;Hotéis&quot; já contém um campo para essa finalidade: `hotelId`. No entanto, o schema de origem &quot;Membros da Fidelidade&quot; não tem esse campo e deve receber um novo mixin que adicione um novo campo, `favoriteHotel`, sob sua `TENANT_ID` namespace.

### Criar uma nova mistura

Para adicionar um novo campo a um schema, ele deve primeiro ser definido em uma mistura. Você pode criar um novo mixin, fazendo uma solicitação POST para o `/tenant/mixins` terminal.

**Formato da API**

```http
POST /tenant/mixins
```

**Solicitação**

A solicitação a seguir cria um novo mixin que adiciona um `favoriteHotel` campo sob a `TENANT_ID` namespace de qualquer schema ao qual ele seja adicionado.

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

A solicitação a seguir adiciona a combinação &quot;Hotel Favorito&quot; ao schema &quot;Membros da Fidelidade&quot;.

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
| `path` | O caminho para o campo schema no qual o novo recurso será adicionado. Ao adicionar misturas a schemas, o valor deve ser `/allOf/-`. |
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

## Definir campos de identidade primários para ambos os schemas

>[!NOTE]
>
>Esta etapa só é necessária para schemas que serão ativados para uso em [!DNL Real-time Customer Profile](../../profile/home.md). Se você não quiser que nenhum dos schemas participe de uma união, ou se os schemas já tiverem identidades primárias definidas, vá para a próxima etapa da [criação de um descritor](#create-descriptor) de identidade de referência para o schema de destino.

Para que os schemas possam ser habilitados para uso em [!DNL Real-time Customer Profile], eles devem ter uma identidade primária definida. Além disso, o schema de destino de uma relação deve usar sua identidade primária como campo de referência.

Para os fins deste tutorial, o schema de origem já tem uma identidade primária definida, mas o schema de destino não tem. É possível marcar um campo de schema como um campo de identidade principal criando um descritor de identidade. Isso é feito fazendo uma solicitação POST ao `/tenant/descriptors` terminal.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um novo descritor de identidade que define o `hotelId` campo do schema de destino &quot;Hotéis&quot; como um campo de identidade principal.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor a ser criado. O `@type` valor dos descritores de identidade é `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | O `$id` valor do schema de destino, obtido na etapa [](#define-schemas)anterior. |
| `xdm:sourceVersion` | O número da versão do schema. |
| `sourceProperty` | O caminho para o campo específico que servirá como a identidade principal do schema. Esse caminho deve começar com &quot;/&quot; e não terminar com um, além de excluir qualquer namespace de &quot;propriedades&quot;. Por exemplo, a solicitação acima usa `/_{TENANT_ID}/hotelId` em vez de `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | A namespace de identidade para o campo de identidade. `hotelId` é um valor ECID neste exemplo, portanto, a namespace &quot;ECID&quot; é usada. Consulte a visão geral [da namespace de](../../identity-service/home.md) identidade para obter uma lista das namespaces disponíveis. |
| `xdm:isPrimary` | Uma propriedade booleana que determina se o campo de identidade será a identidade primária do schema. Como essa solicitação define uma identidade primária, o valor é definido como true. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor de identidade recém-criado.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Criar um descritor de identidade de referência

Os campos de Schema devem ter um descritor de identidade de referência aplicado a eles se estiverem sendo usados como referência de outros schemas em um relacionamento. Uma vez que o `favoriteHotel` campo &quot;Membros da fidelidade&quot; se referirá ao `hotelId` campo em &quot;Hotéis&quot;, `hotelId` deve ser atribuído um descritor de identidade de referência.

Crie um descritor de referência para o schema de destino, fazendo uma solicitação POST para o `/tenant/descriptors` ponto final.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um descritor de referência para o `hotelId` campo no schema de destino &quot;Hotéis&quot;.

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
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `xdm:sourceSchema` | O `$id` URL do schema de destino. |
| `xdm:sourceVersion` | O número da versão do schema de destino. |
| `sourceProperty` | O caminho para o campo de identidade principal do schema de destino. |
| `xdm:identityNamespace` | A namespace de identidade do campo de referência. `hotelId` é um valor ECID neste exemplo, portanto, a namespace &quot;ECID&quot; é usada. Consulte a visão geral [da namespace de](../../identity-service/home.md) identidade para obter uma lista das namespaces disponíveis. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor de referência recém-criado para o schema de destino.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Criar um descritor de relação {#create-descriptor}

Os descritores de relacionamento estabelecem uma relação um para um entre um schema de origem e um schema de destino. Você pode criar um novo descritor de relação, fazendo uma solicitação POST para o `/tenant/descriptors` ponto de extremidade.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir cria um novo descritor de relacionamento, com &quot;Membros de Fidelidade&quot; como o schema de origem e &quot;Membros de Fidelidade Herdados&quot; como o schema de destino.

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
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `@type` | O tipo de descritor a ser criado. O `@type` valor dos descritores de relacionamento é `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | O `$id` URL do schema de origem. |
| `xdm:sourceVersion` | O número da versão do schema de origem. |
| `sourceProperty`: | O caminho para o campo de referência no schema de origem. |
| `xdm:destinationSchema` | O `$id` URL do schema de destino. |
| `xdm:destinationVersion` | O número da versão do schema de destino. |
| `destinationProperty`: | O caminho para o campo de referência no schema de destino. |

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

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas. Para obter mais informações sobre como trabalhar com descritores usando a [!DNL Schema Registry] API, consulte o guia [do desenvolvedor do Registro de](../api/getting-started.md)Schemas. Para obter etapas sobre como definir relações de schema na interface do usuário, consulte o tutorial sobre como [definir relações de schema usando o Editor](relationship-ui.md)de Schemas.