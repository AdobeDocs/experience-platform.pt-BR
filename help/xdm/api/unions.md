---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;modelo de dados da experiência;Modelo de dados da experiência;Modelo de dados;Modelo de dados;Modelo de dados;Registro do schema;Registro do Schema;união;uniões;Uniões;segmentMembship;timeSeriesEvents;
solution: Experience Platform
title: Uniões
description: O endpoint /união na API do Registro do Schema permite que você gerencie programaticamente schemas de união XDM em seu aplicativo de experiência.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---


# Ponto de extremidade União

O União (ou o união visualização) são schemas somente leitura gerados pelo sistema que agregação os campos de todos os schemas que compartilham a mesma classe ([!DNL XDM ExperienceEvent] ou [!DNL XDM Individual Profile]) e estão habilitados para [[!DNL Real-time Customer Profile]](../../profile/home.md).

Este documento aborda conceitos essenciais para trabalhar com o união na API do Registro do Schema, incluindo chamadas de amostra para várias operações. Para obter informações mais gerais sobre uniões no XDM, consulte a seção sobre uniões nas [noções básicas de composição de schemas](../schema/composition.md#union).

## Campos de schema de união

O [!DNL Schema Registry] inclui automaticamente três campos chave em um schema de união: `identityMap`, `timeSeriesEvents` e `segmentMembership`.

### Mapa de identidade

Um schema união `identityMap` é uma representação das identidades conhecidas dentro dos schemas de registro associados à união. O mapa de identidade separa identidades em matrizes diferentes colocadas pela namespace. Cada identidade listada é um objeto contendo um valor `id` exclusivo. Consulte a [documentação do Serviço de Identidade](../../identity-service/home.md) para obter mais informações.

### Eventos série cronológica

A matriz `timeSeriesEvents` é uma lista de eventos de série de tempo relacionados aos schemas de registro associados à união. Quando os dados do perfil são exportados para conjuntos de dados, essa matriz é incluída para cada registro. Isso é útil para vários casos de uso, como aprendizado de máquina em que os modelos precisam de todo o histórico de comportamento do perfil, além de seus atributos de registro.

### Mapa de associação de segmento

O mapa `segmentMembership` armazena os resultados das avaliações de segmentos. Quando os trabalhos de segmento são executados com êxito usando a [API de segmentação](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), o mapa é atualizado. `segmentMembership` também armazena quaisquer segmentos de audiência pré-avaliados que sejam ingeridos na Plataforma, permitindo a integração com outras soluções como a Adobe Audience Manager. Consulte o tutorial em [criar segmentos usando APIs](../../segmentation/tutorials/create-a-segment.md) para obter mais informações.

## Recuperar uma lista do união {#list}

Quando você define a tag `union` em um schema, o [!DNL Schema Registry] adiciona automaticamente o schema à união da classe na qual o schema se baseia. Se não houver união para a classe em questão, uma nova união será criada automaticamente. O `$id` para a união é semelhante ao padrão `$id` de outros recursos [!DNL Schema Registry], com a única diferença sendo que é anexada por dois sublinhados e a palavra &quot;união&quot; (`__union`).

Você pode visualização uma lista de uniões disponíveis, fazendo solicitação de GET para o terminal `/tenant/unions`.

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

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Os seguintes cabeçalhos `Accept` estão disponíveis para uniões de listagem:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para a listagem de recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna a classe JSON completa para cada recurso, com `$ref` e `allOf` originais incluídos. (Limite: 300) |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma matriz `results` no corpo da resposta. Se as uniões tiverem sido definidas, os detalhes de cada união serão fornecidos como objetos dentro do storage. Se nenhuma união tiver sido definida, o status HTTP 200 (OK) ainda será retornado, mas a matriz `results` estará vazia.

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

## Procure uma união {#lookup}

Você pode visualização uma união específica executando uma solicitação de GET que inclui `$id` e, dependendo do cabeçalho Accept (Aceitar), alguns ou todos os detalhes da união.

>[!NOTE]
>
>Pesquisas de união estão disponíveis usando o endpoint `/unions` e `/schemas` para permitir o uso em [!DNL Profile] exportações para um conjunto de dados.

**Formato da API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{UNION_ID}` | O URI `$id` codificado por URL da união que você deseja pesquisar. Os URIs para schemas de união são anexados com &quot;__união&quot;. |

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

As solicitações de pesquisa de união exigem que `version` sejam incluídas no cabeçalho Aceitar.

Os cabeçalhos Accept (Aceitar) a seguir estão disponíveis para pesquisas com schemas de união:

| Accept | Descrição |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Bruto com `$ref` e `allOf`. Inclui títulos e descrições. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` e  `allOf` resolvido. Inclui títulos e descrições. |

**Resposta**

Uma resposta bem-sucedida retorna a visualização de união de todos os schemas que implementam a classe cujo `$id` foi fornecido no caminho da solicitação.

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

## Habilitar um schema para associação de união {#enable}

Para que um schema seja incluído na união de sua classe, uma tag `union` deve ser adicionada ao atributo schema `meta:immutableTags`. Para fazer isso, faça uma solicitação de PATCH para adicionar uma matriz `meta:immutableTags` com um valor de cadeia de caracteres único `union` ao schema em questão. Consulte o guia de ponto de extremidade [schemas](./schemas.md#union) para obter um exemplo detalhado.

## Schemas de lista em uma união {#list-schemas}

Para ver quais schemas fazem parte de uma união específica, é possível executar uma solicitação de GET para o terminal `/tenant/schemas`. Usando o parâmetro de query `property`, é possível configurar a resposta para apenas schemas que contenham um campo `meta:immutableTags` e um `meta:class` igual à classe cuja união você está acessando.

**Formato da API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O `$id` da classe cujos schemas habilitados para união você deseja lista. |

**Solicitação**

A solicitação a seguir recupera uma lista de todos os schemas que fazem parte da união da classe [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Os seguintes cabeçalhos `Accept` estão disponíveis para schemas de listagem:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para a listagem de recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o schema JSON completo para cada recurso, com `$ref` e `allOf` originais incluídos. (Limite: 300) |

**Resposta**

Uma resposta bem-sucedida retorna uma lista filtrada de schemas, contendo apenas os que pertencem à classe especificada que foram habilitados para associação de união. Lembre-se de que ao usar vários parâmetros de query, uma relação E é assumida.

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
