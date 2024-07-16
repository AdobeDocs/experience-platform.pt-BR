---
title: Ponto de Extremidade de Tags Unificadas
description: Saiba como criar, atualizar, gerenciar e excluir categorias de tags e tags usando as APIs do Adobe Experience Platform.
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 4%

---

# Endpoint de tags unificadas

>[!IMPORTANT]
>
>A URL do ponto de extremidade para este conjunto de pontos de extremidade é `https://experience.adobe.io`.

Tags são um recurso que permite gerenciar taxonomias de metadados para classificar objetos de negócios para facilitar a descoberta e a categorização. Posteriormente, é possível organizar essas tags em outros grupos, adicionando-as a categorias de tags.

Este guia fornece informações para ajudar você a entender melhor as tags e categorias de tags e inclui exemplos de chamadas de API para executar ações básicas usando a API.

## Introdução

Os endpoints usados neste guia fazem parte das APIs do Adobe Experience Platform. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo de API

### Glossário

O glossário a seguir destaca a diferença entre uma **tag** e uma **categoria de tag**.

- **Marca**: uma marca permite gerenciar a taxonomia de metadados de objetos comerciais, permitindo que você classifique esses objetos para facilitar a descoberta e a categorização.
   - **Marca não categorizada**: uma marca não categorizada é uma marca que não pertence a uma categoria de marca. Por padrão, as tags criadas serão descategorizadas.
- **Categoria de marca**: uma categoria de marca permite agrupar suas marcas em conjuntos significativos, permitindo que você forneça mais contexto para a finalidade da marca.

## Recuperar uma lista de categorias de tags {#get-tag-categories}

Você pode recuperar uma lista de categorias de marcas que pertencem à sua organização fazendo uma solicitação GET para o ponto de extremidade `/tagCategory`.

**Formato da API**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Os parâmetros de consulta opcionais a seguir podem ser usados ao recuperar categorias de tags.

| Parâmetro de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `start` | O local de onde a lista de resultados começa. Você pode usar isso para indicar o índice inicial para paginação de resultados. | `start=a` |
| `limit` | O número máximo de categorias de tag que você deseja recuperar por página. | `limit=20` |
| `property` | O atributo pelo qual você deseja filtrar ao recuperar categorias de tag. Os valores suportados incluem: &lt;ul≥<li>`name`: O nome da categoria da marca.</li></ul> | `property=name==category` |
| `sortBy` | A ordem pela qual as categorias de tag são classificadas. Os valores suportados incluem `name`, `createdAt` e `modifiedAt`. | `sortBy=name` |
| `sortOrder` | A direção pela qual as categorias de tag são classificadas. Os valores suportados incluem `asc` e `desc`. | `sortOrder=asc` |

**Solicitação**

+++Uma solicitação de amostra para listar todas as categorias de tags na organização

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de todas as categorias de tags da organização.

+++Um exemplo de resposta que contém uma lista de todas as categorias de tags na organização.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Criar uma nova categoria de tag {#create-tag-category}

>[!IMPORTANT]
>
>Somente o administrador do sistema e o administrador do produto podem usar essa chamada de API.

Você pode criar uma nova categoria de tag fazendo uma solicitação POST para o ponto de extremidade `/tagCategory`.

**Formato da API**

```http
POST /tagCategory
```

**Solicitação**

+++Uma solicitação de amostra para criar uma nova categoria de tag.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da categoria de tag que você deseja criar. |
| `description` | Uma descrição da categoria de tag que você deseja criar. |

+++

**Resposta**

Uma resposta de amostra retorna o status HTTP 200 com detalhes da categoria de tag recém-criada.

+++Uma resposta de amostra que contém detalhes da categoria de tag recém-criada.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Recuperar uma categoria de tag específica {#get-tag-category}

Você pode recuperar uma categoria de marca específica que pertença à sua organização fazendo uma solicitação GET para o ponto de extremidade `/tagCategory` e especificando a ID da categoria da marca.

**Formato da API**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | A ID da categoria de tag que você está recuperando. |

**Solicitação**

+++Uma solicitação de amostra para recuperar uma categoria de tag específica

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da categoria de tag especificada.

+++Uma resposta de amostra que contém detalhes da categoria de tag especificada.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID da categoria de tag solicitada. |
| `name` | O nome da categoria de tag solicitada. |
| `description` | A descrição da categoria de tag solicitada. |
| `createdBy` | A ID do usuário que criou a categoria de tag. |
| `createdAt` | O carimbo de data e hora de quando a categoria de tag foi criada. |
| `modifiedBy` | A ID do usuário que atualizou a categoria da tag pela última vez. |
| `modifiedAt` | O carimbo de data e hora de quando a categoria de tag foi atualizada pela última vez. |
| `tagCount` | O número de tags que pertencem à categoria de tag. |

+++

## Atualizar uma categoria de tag específica {#update-tag-category}

>[!IMPORTANT]
>
>Somente o administrador do sistema e o administrador do produto podem usar essa chamada de API.

Você pode atualizar os detalhes de uma categoria de tag específica que pertence à sua organização fazendo uma solicitação PATCH para o ponto de extremidade `/tagCategory` e especificando a ID da categoria de tag.

**Formato da API**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | A ID da categoria de tag que você está recuperando. |

**Solicitação**

+++Uma solicitação de amostra para atualizar uma categoria de tag específica

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `op` | A operação que foi concluída. Para atualizar uma categoria de marca específica, defina esse valor como `replace`. |
| `path` | O caminho do campo que será atualizado. Os valores suportados incluem `name` e `description`. |
| `value` | O valor atualizado do campo que você deseja atualizar. |
| `from` | O valor original do campo que você deseja atualizar. |

+++

**Resposta**

Uma resposta HTTP status 200 bem-sucedida com informações sobre a categoria de tag recém-atualizada.

+++Uma resposta de amostra que contém detalhes da categoria de tag recém-atualizada.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Excluir uma categoria de tag específica {#delete-tag-category}

>[!IMPORTANT]
>
>Somente o administrador do sistema e o administrador do produto podem usar essa chamada de API.

Você pode excluir uma categoria de tag específica que pertence à sua organização fazendo uma solicitação DELETE para o ponto de extremidade `/tagCategory` e especificando a ID da categoria de tag.

**Formato da API**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | A ID da categoria de tag que você está recuperando. |

**Solicitação**

+++Uma solicitação de amostra para excluir uma categoria de tag específica

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta vazia.

## Recuperar uma lista de tags {#get-tags}

Você pode recuperar uma lista de marcas que pertencem à sua organização fazendo uma solicitação GET para o ponto de extremidade `/tags` e a ID da categoria da marca.

**Formato da API**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Os parâmetros de consulta opcionais a seguir podem ser usados ao recuperar tags.

| Parâmetro de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `start` | O local de onde a lista de resultados começa. Você pode usar isso para indicar o índice inicial para paginação de resultados. | `start=a` |
| `limit` | O número máximo de tags que você deseja recuperar por página. | `limit=20` |
| `property` | O atributo pelo qual você deseja filtrar ao recuperar tags. Os valores compatíveis incluem:<ul><li>`name`: O nome da marca.</li><li>`archived`: Se as marcas estão ou não arquivadas. Você pode definir este valor como `true` ou `false`.</li><li>`tagCategoryId`: A identificação da categoria de marcas à qual a marca pertence.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | A ordem pela qual as tags são classificadas. Os valores suportados incluem `name`, `createdAt` e `modifiedAt`. | `sortBy=name` |
| `sortOrder` | A direção pela qual as categorias de tag são classificadas. Os valores suportados incluem `asc` e `desc`. | `sortOrder=asc` |


**Solicitação**

+++Uma solicitação de amostra para recuperar todas as tags que pertencem a uma categoria de tag específica

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das tags pertencentes a essa categoria de tag.

+++ Uma resposta de amostra que contém detalhes das tags solicitadas.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Criar uma nova tag {#create-tag}

>[!IMPORTANT]
>
>Somente o administrador do sistema e o administrador do produto podem usar essa chamada de API para criar uma nova tag em uma categoria de tag especificada.
>
>Se você estiver criando uma marca sem categoria, **não** precisará de permissões de administrador.

Você pode criar uma nova tag fazendo uma solicitação POST para o ponto de extremidade `/tags`.

**Formato da API**

```http
POST /tags
```

**Solicitação**

+++Uma solicitação de amostra para criar uma nova tag.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | **Obrigatório**. O nome da tag que você deseja criar. |
| `tagCategoryId` | *Opcional*. A ID da categoria da tag à qual você deseja que a tag pertença. Se não especificada, a tag será criada como parte da categoria Sem categoria. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da tag recém-criada.

+++Uma resposta de amostra que contém detalhes da tag recém-criada.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `name` | O nome da tag recém-criada. |
| `id` | A ID da tag recém-criada. |
| `org` | A ID da organização à qual a tag pertence. |
| `createdAt` | O carimbo de data e hora de quando a tag foi criada. |
| `createdBy` | A ID do usuário que criou a tag. |
| `modifiedAt` | O carimbo de data e hora de quando a tag foi atualizada pela última vez. |
| `modifiedBy` | A ID do último usuário que atualizou a tag. |
| `tagCategoryId` | A ID da categoria da tag à qual a tag pertence. |
| `tagCategoryName` | O nome da categoria da tag à qual a tag pertence. |

+++

## Recuperar uma tag específica {#get-tag}

Você pode recuperar uma marca específica que pertença à sua organização fazendo uma solicitação GET para o ponto de extremidade `/tags` e especificando a ID da marca que deseja recuperar.

**Formato da API**

```http
GET /tags/{TAG_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TAG_ID}` | A ID da tag que você está recuperando. |

**Solicitação**

+++Uma solicitação de amostra para recuperar uma tag específica

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da tag especificada.

+++Uma resposta de amostra que contém detalhes da tag especificada.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `name` | O nome da tag recuperada. |
| `id` | A ID da tag recuperada. |
| `org` | A ID da organização à qual a tag pertence. |
| `createdAt` | O carimbo de data e hora de quando a tag foi criada. |
| `createdBy` | A ID do usuário que criou a tag. |
| `modifiedAt` | O carimbo de data e hora de quando a tag foi atualizada pela última vez. |
| `modifiedBy` | A ID do último usuário que atualizou a tag. |
| `tagCategoryId` | A ID da categoria da tag à qual a tag pertence. |
| `tagCategoryName` | O nome da categoria da tag à qual a tag pertence. |
| `archived` | O status de arquivamento da tag. Se definido como `true`, significa que a tag está arquivada. |

+++

## Validar tags {#validate-tags}

Você pode validar se as marcas existem fazendo uma solicitação POST para o ponto de extremidade `/tags/validate`.

**Formato da API**

```http
POST /tags/validate
```

**Solicitação**

+++Uma solicitação de amostra para validar as IDs de tag fornecidas.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `ids` | Uma matriz que contém uma lista de IDs de tag que você deseja validar. |
| `entity` | A entidade que solicita a validação. Você pode usar o valor `{API_KEY}` para este parâmetro. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre quais tags são válidas e inválidas.

+++Uma resposta de amostra que exibe quais tags são válidas e inválidas.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `invalidTags` | Uma matriz que contém uma lista de IDs de tag inválidas. |
| `validTags` | Uma matriz que contém uma lista de IDs de tag válidas. |

+++

## Atualizar uma tag específica {#update-tag}

Você pode atualizar uma tag especificada fazendo uma solicitação PATCH para o ponto de extremidade `/tags` e fornecendo a ID da tag que deseja atualizar.

**Formato da API**

```http
PATCH /tags/{TAG_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TAG_ID}` | A ID da tag que você está atualizando. |

**Solicitação**

+++Uma solicitação de amostra para atualizar uma tag específica

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `op` | A operação que precisa ser feita. Neste caso de uso, sempre será definido como `replace`. |
| `path` | O caminho do campo que será atualizado. Os valores suportados incluem `name`, `archived` e `tagCategoryId`. |
| `value` | O valor atualizado do campo que você deseja atualizar. |
| `from` | O valor original do campo que você deseja atualizar. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da tag recém-atualizada.

+++Uma resposta de amostra que contém detalhes da tag atualizada.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Excluir uma tag específica {#delete-tag}

>[!IMPORTANT]
>
>Somente o administrador do sistema e o administrador do produto podem usar essa chamada de API.
>
>Além disso, a marca **não pode** ser associada a qualquer objeto comercial e **deve** ser arquivada antes que você possa excluir a marca. Você pode arquivar a marca usando o [ponto de extremidade da marca de atualização](#update-tag).

Você pode excluir uma tag específica criando uma tag DELETE para o ponto de extremidade `/tags` e especificando a ID da tag que você deseja excluir.

**Formato da API**

```http
DELETE /tags/{TAG_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TAG_ID}` | A ID da tag que você está excluindo. |

**Solicitação**

+++Uma solicitação de amostra para excluir uma tag específica

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta vazia.

## Próximas etapas

Depois de ler este guia, você compreenderá melhor como criar, gerenciar e excluir tags e categorias de tags usando as APIs do Adobe Experience Platform. Para obter mais informações sobre como gerenciar tags usando a interface do usuário, leia o [guia de gerenciamento de tags](../ui/managing-tags.md). Para obter mais informações sobre como gerenciar categorias de marcas usando a interface do usuário, leia o [guia de categorias de marcas](../ui/tags-categories.md).
