---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;esquema;Esquema;esquemas;esquemas;criar
solution: Experience Platform
title: Endpoint da API de esquemas
description: O ponto de extremidade /schemas na API do registro de esquema permite gerenciar de forma programática esquemas XDM no aplicativo de experiência.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 3%

---

# Endpoint de esquemas

Um esquema pode ser visto como o blueprint dos dados que você deseja assimilar na Adobe Experience Platform. Cada esquema é composto por uma classe e zero ou mais grupos de campos de esquema. A variável `/schemas` endpoint na variável [!DNL Schema Registry] A API permite gerenciar esquemas de forma programática no aplicativo de experiência.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de esquemas {#list}

Você pode listar todos os esquemas na variável `global` ou `tenant` GET contêiner fazendo uma solicitação para `/global/schemas` ou `/tenant/schemas`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o Registro de esquema limita os conjuntos de resultados a 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar os resultados e reduzir o número de recursos retornados. Consulte a seção sobre [parâmetros de consulta](./appendix.md#query) no documento do apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container que abriga os esquemas que você deseja recuperar: `global` para esquemas criados por Adobe ou `tenant` para esquemas de propriedade de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados. Consulte a [documento do apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera uma lista de esquemas do `tenant` contêiner, usando um `orderby` parâmetro de consulta para classificar os resultados por seus `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
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

A solicitação acima usou o `application/vnd.adobe.xed-id+json` `Accept` cabeçalho, portanto, a resposta inclui apenas o `title`, `$id`, `meta:altId`, e `version` atributos para cada esquema. Usar o outro `Accept` cabeçalho (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada esquema. Selecione o apropriado `Accept` dependendo das informações que você precisa na sua resposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Pesquisar um esquema {#lookup}

Você pode pesquisar um esquema específico fazendo uma solicitação GET que inclui a ID do esquema no caminho.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que abriga o esquema que você deseja recuperar: `global` para um esquema criado por Adobe ou `tenant` para um esquema de propriedade de sua organização. |
| `{SCHEMA_ID}` | A variável `meta:altId` ou codificado em URL `$id` do esquema que você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera um esquema especificado por seus `meta:altId` no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Todas as solicitações de pesquisa exigem uma `version` ser incluído na lista `Accept` cabeçalho. As seguintes `Accept` os cabeçalhos estão disponíveis:

| `Accept` cabeçalho | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Simples com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` resolvida, tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | Simples com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` resolvida, nenhum título ou descrição. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` resolvido, descritores incluídos. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` resolvida, tem títulos e descrições. Os campos obsoletos são indicados com uma `meta:status` atributo de `deprecated`. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do esquema. Os campos retornados dependem do tipo `Accept` cabeçalho enviado na solicitação. Experimento com diferentes `Accept` cabeçalhos para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Criar um esquema {#create}

O processo de composição do esquema começa atribuindo uma classe. A classe define os principais aspectos comportamentais dos dados (registro ou série temporal), bem como os campos mínimos necessários para descrever os dados que serão assimilados.

>[!NOTE]
>
>O exemplo de chamada abaixo é apenas um exemplo de linha de base de como criar um esquema na API, com os requisitos mínimos de composição de uma classe e nenhum grupo de campos. Para obter etapas completas sobre como criar um esquema na API, incluindo como atribuir campos usando grupos de campos e tipos de dados, consulte a [tutorial de criação de esquema](../tutorials/create-schema-api.md).

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

O pedido deve incluir uma `allOf` atributo que faz referência ao `$id` de uma classe. Esse atributo define a &quot;classe base&quot; que o esquema implementará. Neste exemplo, a classe base é uma classe &quot;Informações de propriedade&quot; criada anteriormente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `allOf` | Uma matriz de objetos, com cada objeto referindo-se a uma classe ou grupo de campos cujos campos o esquema implementa. Cada objeto contém uma única propriedade (`$ref`) cujo valor representa o `$id` da classe ou grupo de campos que o novo esquema implementará. Uma classe deve ser fornecida, com zero ou mais grupos de campos adicionais. No exemplo acima, o único objeto na variável `allOf` matriz é a classe do esquema. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga contendo os detalhes do esquema recém-criado, incluindo o `$id`, `meta:altId`, e `version`. Esses valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Execução de uma solicitação do GET para [listar todos os esquemas](#list) no contêiner de locatário agora incluiria o novo esquema. Você pode executar um [solicitação de pesquisa (GET)](#lookup) usar o URL codificado `$id` URI para visualizar o novo esquema diretamente.

Para adicionar campos extras a um esquema, é possível executar uma [operação PATCH](#patch) para adicionar grupos de campos ao esquema `allOf` e `meta:extends` matrizes.

## Atualizar um esquema {#put}

Você pode substituir um esquema inteiro por meio de uma operação PUT, essencialmente reescrevendo o recurso. Ao atualizar um esquema por meio de uma solicitação PUT, o corpo deve incluir todos os campos que seriam necessários ao [criação de um novo schema](#create) em uma solicitação POST.

>[!NOTE]
>
>Se quiser atualizar apenas parte de um esquema, em vez de substituí-lo totalmente, consulte a seção sobre [atualização de uma parte de um esquema](#patch).

**Formato da API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | A variável `meta:altId` ou codificado em URL `$id` do esquema que você deseja regravar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir substitui um esquema existente, alterando seu `title`, `description`, e `allOf` atributos.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do esquema atualizado.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Atualizar uma parte de um esquema {#patch}

Você pode atualizar uma parte de um esquema usando uma solicitação PATCH. A variável [!DNL Schema Registry] suporta todas as operações de patch JSON padrão, incluindo `add`, `remove`, e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [Guia de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se você quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de um esquema usando uma operação PUT](#put).

Uma das operações de PATCH mais comuns envolve a adição de grupos de campos definidos anteriormente a um esquema, conforme demonstrado pelo exemplo abaixo.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do esquema que deseja atualizar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação de exemplo abaixo adiciona um novo grupo de campos a um esquema adicionando o do grupo de campos `$id` para a variável `meta:extends` e `allOf` matrizes.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica em um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`), e que informações devem ser incluídas nessa operação (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Resposta**

A resposta mostra que ambas as operações foram executadas com êxito. O grupo de campos `$id` foi adicionado ao `meta:extends` matriz e uma referência (`$ref`) ao grupo de campos `$id` agora aparece no `allOf` matriz.

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
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Ativar um esquema para uso no Perfil do cliente em tempo real {#union}

Para que um esquema participe de [Perfil do cliente em tempo real](../../profile/home.md), é necessário adicionar um `union` para o do esquema `meta:immutableTags` matriz. Você pode fazer isso fazendo uma solicitação PATCH para o esquema em questão.

>[!IMPORTANT]
>
>Tags imutáveis são tags que devem ser definidas, mas nunca removidas.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do esquema que deseja ativar. |

{style="table-layout:auto"}

**Solicitação**

O exemplo de solicitação abaixo adiciona um `meta:immutableTags` para um esquema existente, dando à matriz um único valor de string de `union` para habilitá-lo para uso no Perfil.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do esquema atualizado, mostrando que `meta:immutableTags` matriz foi adicionada.

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
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

Agora você pode visualizar a união da classe deste esquema para confirmar que os campos do esquema são representados. Consulte a [manual de endpoint de uniões](./unions.md) para obter mais informações.

## Excluir um esquema {#delete}

Ocasionalmente, pode ser necessário remover um esquema do Registro de esquemas. Isso é feito executando uma solicitação DELETE com a ID do esquema fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do esquema que deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o esquema. Será necessário incluir um `Accept` cabeçalho na solicitação, mas deve receber um status HTTP 404 (Não encontrado) porque o esquema foi removido do Registro de esquemas.
