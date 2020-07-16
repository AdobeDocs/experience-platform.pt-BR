---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Uniões
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 1%

---


# Uniões

Uniões (ou visualizações uniões) são schemas somente leitura gerados pelo sistema que agregação os campos de todos os schemas que compartilham a mesma classe ([!DNL XDM ExperienceEvent] ou [!DNL XDM Individual Profile]) e estão habilitados para [!DNL Real-time Customer Profile](../../profile/home.md).

Este documento aborda conceitos essenciais para trabalhar com o união na API do Registro do Schema, incluindo chamadas de amostra para várias operações. Para obter informações mais gerais sobre uniões no XDM, consulte a seção sobre uniões nas [noções básicas da composição](../schema/composition.md#union)do schema.

## Misturas de União

O [!DNL Schema Registry] inclui automaticamente três combinações dentro do schema da união: `identityMap`, `timeSeriesEvents`e `segmentMembership`.

### Mapa de identidade

Um schema união `identityMap` é uma representação das identidades conhecidas dentro dos schemas de registro associados à união. O mapa de identidade separa identidades em matrizes diferentes colocadas pela namespace. Cada identidade listada é um objeto contendo um `id` valor exclusivo.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### eventos série cronológica

A `timeSeriesEvents` matriz é uma lista de eventos da série de tempo relacionados aos schemas de registro associados à união. Quando [!DNL Profile] os dados são exportados para conjuntos de dados, essa matriz é incluída para cada registro. Isso é útil para vários casos de uso, como aprendizado de máquina em que os modelos precisam de todo o histórico de comportamento do perfil, além de seus atributos de registro.

### Mapa de associação de segmento

O `segmentMembership` mapa armazena os resultados das avaliações de segmentos. Quando os trabalhos de segmento são executados com êxito usando a API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentação, o mapa é atualizado. `segmentMembership` também armazena quaisquer segmentos de audiência pré-avaliados que sejam ingeridos no Platform, permitindo a integração com outras soluções, como o Adobe Audience Manager.

Consulte o tutorial sobre como [criar segmentos usando APIs](../../segmentation/tutorials/create-a-segment.md) para obter mais informações.

## Ativar um schema para associação de união

Para que um schema seja incluído na visualização de união mesclada, a tag &quot;união&quot; deve ser adicionada ao `meta:immutableTags` atributo do schema. Isso é feito por meio de uma solicitação PATCH para atualizar o schema e adicionar a `meta:immutableTags` matriz com um valor de &quot;união&quot;.

>[!NOTE]
>
>Tags imutáveis são tags que devem ser definidas, mas nunca removidas.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `$id` URI codificado por URL ou `meta:altId` o schema no qual você deseja habilitar para uso [!DNL Profile]. |

**Solicitação**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema atualizado, que agora inclui uma `meta:immutableTags` matriz contendo o valor da string, &quot;união&quot;.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## uniões Listas

Quando você define a tag &quot;união&quot; em um schema, o [!DNL Schema Registry] cria e mantém automaticamente uma união para a classe na qual o schema se baseia. A união `$id` é semelhante ao padrão `$id` de uma classe, sendo a única diferença que é anexada por dois sublinhados e a palavra &quot;união&quot; (`"__union"`).

Para visualização de uma lista de uniões disponíveis, é possível executar uma solicitação GET para o `/unions` endpoint.

**Formato da API**

```http
GET /tenant/unions
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma `results` matriz no corpo da resposta. Se as uniões tiverem sido definidas, as  `title`, `$id`, `meta:altId`e `version` para cada união serão fornecidas como objetos dentro da matriz. Se nenhuma união tiver sido definida, o status HTTP 200 (OK) ainda será retornado, mas a `results` matriz ficará vazia.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Pesquisar uma união específica

Você pode visualização uma união específica executando uma solicitação GET que inclui o cabeçalho `$id` e, dependendo do cabeçalho Aceitar, alguns ou todos os detalhes da união.

>[!NOTE]
>
>Pesquisas de União estão disponíveis usando os pontos de extremidade `/unions` e `/schemas` para permitir o uso em [!DNL Profile] exportações para um conjunto de dados.

**Formato da API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{UNION_ID}` | O `$id` URI codificado por URL da união que você deseja pesquisar. Os URIs para schemas de união são anexados com &quot;__união&quot;. |

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

As solicitações de pesquisa de União exigem que `version` sejam incluídas no cabeçalho Aceitar.

Os cabeçalhos Accept (Aceitar) a seguir estão disponíveis para pesquisas com schemas de união:

| Aceitar | Descrição |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Bruto com `$ref` e `allOf`. Inclui títulos e descrições. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` e `allOf` resolvido. Inclui títulos e descrições. |

**Resposta**

Uma resposta bem-sucedida retorna a visualização de união de todos os schemas que implementam a classe que `$id` foi fornecida no caminho da solicitação.

O formato de resposta depende do cabeçalho Aceitar enviado na solicitação. Experimente com cabeçalhos Accept diferentes para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## schemas de Lista em uma união

Para ver quais schemas fazem parte de uma união específica, é possível executar uma solicitação GET usando parâmetros de query para filtrar os schemas dentro do container do locatário.

Usando o parâmetro `property` query, é possível configurar a resposta para apenas schemas que contenham um `meta:immutableTags` campo e um valor `meta:class` igual à classe cuja união você está acessando.

**Formato da API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | A união `$id` da classe à qual você deseja acessar. |

**Solicitação**

A solicitação a seguir procura todos os schemas que fazem parte da união da [!DNL XDM Individual Profile] classe.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista filtrada de schemas, contendo apenas os que atendem a ambos os requisitos. Lembre-se de que ao usar vários parâmetros de query, uma relação E é assumida. O formato da resposta depende do cabeçalho Aceitar enviado na solicitação.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
