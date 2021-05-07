---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro de esquema, Registro de esquema, união, união, uniões, Uniões, segmentMembership, timeSeriesEvents;
solution: Experience Platform
title: Ponto de Extremidade da API Unions
description: O endpoint /unips na API do Registro de Schema permite gerenciar programaticamente esquemas de união XDM em seu aplicativo de experiência.
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---

# Ponto de extremidade de Unions

Uniões (ou visualizações de união) são esquemas somente leitura gerados pelo sistema que agregam os campos de todos os esquemas que compartilham a mesma classe ([!DNL XDM ExperienceEvent] ou [!DNL XDM Individual Profile]) e são ativados para [[!DNL Real-time Customer Profile]](../../profile/home.md).

Este documento aborda conceitos essenciais para trabalhar com uniões na API do Registro de Schema, incluindo chamadas de amostra para várias operações. Para obter informações mais gerais sobre uniões no XDM, consulte a seção sobre uniões no [básico da composição do schema](../schema/composition.md#union).

## Campos de esquema União

O [!DNL Schema Registry] inclui automaticamente três campos principais dentro de um schema de união: `identityMap`, `timeSeriesEvents` e `segmentMembership`.

### Mapa de identidade

Um `identityMap` do schema de união é uma representação das identidades conhecidas nos esquemas de registro associados da união. O mapa de identidade separa identidades em matrizes diferentes criadas pelo namespace. Cada identidade listada é, ela mesma, um objeto contendo um valor `id` exclusivo. Consulte a [documentação do Serviço de identidade](../../identity-service/home.md) para obter mais informações.

### Eventos da série cronológica

A matriz `timeSeriesEvents` é uma lista de eventos de séries de tempo relacionados aos esquemas de registro associados à união. Quando os dados do perfil são exportados para conjuntos de dados, essa matriz é incluída para cada registro. Isso é útil para vários casos de uso, como aprendizado de máquina, em que os modelos precisam de todo o histórico de comportamento de um perfil, além de seus atributos de registro.

### Mapa de associação de segmento

O mapa `segmentMembership` armazena os resultados das avaliações de segmento. Quando as tarefas de segmento são executadas com êxito usando a [API de segmentação](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), o mapa é atualizado. `segmentMembership` O também armazena todos os segmentos de público-alvo pré-avaliados que são assimilados no Platform, permitindo a integração com outras soluções como o Adobe Audience Manager. Consulte o tutorial em [criar segmentos usando APIs](../../segmentation/tutorials/create-a-segment.md) para obter mais informações.

## Recuperar uma lista de uniões {#list}

Quando você define a tag `union` em um schema, o [!DNL Schema Registry] adiciona automaticamente o schema à união para a classe na qual o schema se baseia. Se não houver união para a classe em questão, uma nova união será criada automaticamente. O `$id` para a união é semelhante ao `$id` padrão de outros recursos [!DNL Schema Registry], sendo a única diferença que é anexada por dois sublinhados e a palavra &quot;união&quot; (`__union`).

É possível exibir uma lista de uniões disponíveis fazendo uma solicitação de GET para o endpoint `/tenant/unions`.

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

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Os seguintes cabeçalhos `Accept` estão disponíveis para listar uniões:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna a classe JSON completa para cada recurso, com `$ref` original e `allOf` incluídas. (Limite: 300) |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma matriz `results` no corpo da resposta. Se sindicatos tiverem sido definidos, os detalhes de cada união serão fornecidos como objetos dentro do storage. Se nenhuma união tiver sido definida, o status HTTP 200 (OK) ainda será retornado, mas a matriz `results` estará vazia.

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

## Procurar uma união {#lookup}

Você pode visualizar uma união específica executando uma solicitação do GET que inclui o `$id` e, dependendo do cabeçalho Accept, alguns ou todos os detalhes da união.

>[!NOTE]
>
>As pesquisas de União estão disponíveis usando o endpoint `/unions` e `/schemas` para permitir seu uso em [!DNL Profile] exportações para um conjunto de dados.

**Formato da API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{UNION_ID}` | O URI `$id` codificado no URL da união que você deseja pesquisar. Os URIs para esquemas de união são anexados com &quot;__union&quot;. |

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

As solicitações de pesquisa de União exigem que `version` seja incluído no cabeçalho Aceitar.

Os seguintes cabeçalhos Accept estão disponíveis para pesquisas de schema de união:

| Accept | Descrição |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Bruto com `$ref` e `allOf`. Inclui títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e  `allOf` resolvidos. Inclui títulos e descrições. |

**Resposta**

Uma resposta bem-sucedida retorna a exibição de união de todos os schemas que implementam a classe cujo `$id` foi fornecido no caminho da solicitação.

O formato de resposta depende do cabeçalho Accept enviado na solicitação. Experimente com cabeçalhos Accept diferentes para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/477bb01d7125b015b4feba7bccc2e599"
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
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/477bb01d7125b015b4feba7bccc2e599",
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

## Habilitar um esquema para associação de união {#enable}

Para que um schema seja incluído na união de sua classe, uma tag `union` deve ser adicionada ao atributo `meta:immutableTags` do schema. Você pode fazer isso fazendo uma solicitação de PATCH para adicionar uma matriz `meta:immutableTags` com um único valor de string `union` ao schema em questão. Consulte o [guia do ponto de extremidade de schemas](./schemas.md#union) para obter um exemplo detalhado.

## Listar esquemas em uma união {#list-schemas}

Para ver quais schemas fazem parte de uma união específica, você pode executar uma solicitação de GET para o endpoint `/tenant/schemas`. Usando o parâmetro de consulta `property`, você pode configurar a resposta para retornar apenas schemas contendo um campo `meta:immutableTags` e um `meta:class` igual à classe cuja união você está acessando.

**Formato da API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O `$id` da classe cujos esquemas ativados por união você deseja listar. |

**Solicitação**

A solicitação a seguir recupera uma lista de todos os schemas que fazem parte da união para a classe [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Os seguintes cabeçalhos `Accept` estão disponíveis para listar schemas:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o esquema JSON completo para cada recurso, com `$ref` e `allOf` originais incluídos. (Limite: 300) |

**Resposta**

Uma resposta bem-sucedida retorna uma lista filtrada de schemas, que contém apenas aqueles que pertencem à classe especificada que foram habilitados para associação de união. Lembre-se de que, ao usar vários parâmetros de consulta, uma relação AND é assumida.

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
