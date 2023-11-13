---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;Registro de esquemas;união;uniões;uniões;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Endpoint da API de uniões
description: O ponto de extremidade /unions na API do registro de esquema permite gerenciar programaticamente os esquemas de união XDM no aplicativo de experiência.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 3da2e8f66f08a7bb9533795f7854ad583734911c
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 2%

---

# Endpoint de uniões

As uniões (ou exibições de união) são esquemas somente leitura gerados pelo sistema que agregam os campos de todos os esquemas que compartilham a mesma classe ([!DNL XDM ExperienceEvent] ou [!DNL XDM Individual Profile]) e estão ativados para [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Este documento aborda conceitos essenciais para trabalhar com sindicatos na API do registro de esquema, incluindo chamadas de amostra para várias operações. Para obter informações mais gerais sobre uniões no XDM, consulte a seção sobre uniões no [noções básicas da composição do esquema](../schema/composition.md#union).

## Campos de esquema de união

A variável [!DNL Schema Registry] O inclui automaticamente três campos principais em um esquema de união: `identityMap`, `timeSeriesEvents`, e `segmentMembership`.

### Mapa de identidade

De um esquema de união `identityMap` é uma representação das identidades conhecidas nos schemas de registro associados da união. O mapa de identidade separa as identidades em matrizes diferentes digitadas pelo namespace. Cada identidade listada é um objeto que contém uma `id` valor. Consulte a [Documentação do Serviço de identidade](../../identity-service/home.md) para obter mais informações.

### Eventos de série temporal

A variável `timeSeriesEvents` matriz é uma lista de eventos de série temporal relacionados aos esquemas de registro associados à união. Quando os dados do perfil são exportados para conjuntos de dados, essa matriz é incluída para cada registro. Isso é útil para vários casos de uso, como aprendizado de máquina, em que os modelos precisam de todo o histórico de comportamento de um perfil, além dos atributos de registro.

### Mapa da associação de segmento

A variável `segmentMembership` o mapa armazena os resultados da avaliação de uma definição de segmento. Quando os trabalhos de segmento são executados com sucesso usando o [API de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/), o mapa é atualizado. `segmentMembership` O também armazena quaisquer públicos-alvo pré-avaliados que são assimilados na Platform, permitindo a integração com outras soluções, como o Adobe Audience Manager. Veja o tutorial sobre [criação de públicos usando APIs](../../segmentation/tutorials/create-a-segment.md) para obter mais informações.

## Recuperar uma lista de uniões {#list}

Ao definir a variável `union` em um esquema, a variável [!DNL Schema Registry] adiciona automaticamente o esquema à união para a classe em que o esquema se baseia. Se nenhuma união existir para a classe em questão, uma nova união será criada automaticamente. A variável `$id` para a união é semelhante ao padrão `$id` de outros [!DNL Schema Registry] recursos, com a única diferença sendo que é anexada por dois sublinhados e a palavra &quot;união&quot; (`__union`).

Você pode exibir uma lista de uniões disponíveis fazendo uma solicitação GET para o `/tenant/unions` terminal.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. As seguintes `Accept` os cabeçalhos estão disponíveis para listar uniões:

| `Accept` cabeçalho | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna a classe JSON completa para cada recurso, com o original `$ref` e `allOf` incluído. (Limite: 300) |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e uma `results` no corpo da resposta. Se as uniões tiverem sido definidas, os detalhes de cada união serão fornecidos como objetos dentro da matriz. Se nenhuma união tiver sido definida, o status HTTP 200 (OK) ainda será retornado, mas a variável `results` A matriz estará vazia.

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

## Pesquisar uma união {#lookup}

Você pode visualizar uma união específica executando uma solicitação GET que inclui `$id` e, dependendo do cabeçalho Aceitar, alguns ou todos os detalhes da união.

>[!NOTE]
>
>As pesquisas de união estão disponíveis usando o `/unions` e `/schemas` ponto de extremidade para habilitá-los para uso no [!DNL Profile] O exporta para um conjunto de dados.

**Formato da API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{UNION_ID}` | O formato codificado por URL `$id` URI da união que você deseja pesquisar. Os URIs para esquemas de união são anexados com &quot;__union&quot;. |

{style="table-layout:auto"}

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

As solicitações de pesquisa de União exigem uma `version` ser incluído no cabeçalho Aceitar.

Os seguintes cabeçalhos Aceitar estão disponíveis para pesquisas de esquema de união:

| Accept | Descrição |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Simples com `$ref` e `allOf`. Inclui títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos e `allOf` resolvido. Inclui títulos e descrições. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna a visualização de união de todos os esquemas que implementam a classe cuja `$id` foi fornecido no caminho da solicitação.

O formato da resposta depende do cabeçalho Aceitar enviado na solicitação. Experimente com diferentes cabeçalhos Aceitar para comparar as respostas e determinar qual cabeçalho é melhor para o seu caso de uso.

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

## Ativar um esquema para associação de união {#enable}

Para que um esquema seja incluído na união para sua classe, uma variável `union` deve ser adicionada à tag do esquema `meta:immutableTags` atributo. Você pode fazer isso fazendo uma solicitação PATCH para adicionar um `meta:immutableTags` matriz com um único valor de string de `union` ao esquema em questão. Consulte a [manual de endpoint de esquemas](./schemas.md#union) para obter um exemplo detalhado.

## Listar esquemas em uma união {#list-schemas}

Para ver quais esquemas fazem parte de uma união específica, você pode executar uma solicitação GET para o `/tenant/schemas` terminal. Usar o `property` parâmetro de consulta, você pode configurar a resposta para retornar apenas schemas que contenham uma `meta:immutableTags` e um `meta:class` igual à classe cuja união você está acessando.

**Formato da API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | A variável `$id` da classe cujos esquemas ativados para união você deseja listar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera uma lista de todos os esquemas que fazem parte da união para a [!DNL XDM Individual Profile] classe.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. As seguintes `Accept` os cabeçalhos estão disponíveis para listar schemas:

| `Accept` cabeçalho | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o esquema JSON completo para cada recurso, com o original `$ref` e `allOf` incluído. (Limite: 300) |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna uma lista filtrada de esquemas, contendo apenas aqueles que pertencem à classe especificada e que foram ativados para associação de união. Lembre-se de que, ao usar vários parâmetros de consulta, uma relação AND é presumida.

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
