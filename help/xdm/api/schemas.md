---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados da experiência, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema, esquema, Esquema, esquemas, Esquemas, criar
solution: Experience Platform
title: Ponto de Extremidade da API de Esquemas
description: O endpoint /schemas na API do Registro de Schema permite gerenciar programaticamente os esquemas XDM no aplicativo de experiência.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 666f424355fd1104971bb1566b72e207d00f4a56
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 5%

---

# Ponto de extremidade de esquemas

Um schema pode ser considerado como o blueprint para os dados que você deseja assimilar no Adobe Experience Platform. Cada schema é composto de uma classe e zero ou mais grupos de campos de schema. O `/schemas` endpoint no [!DNL Schema Registry] A API permite gerenciar esquemas de forma programática no aplicativo de experiência.

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de schemas {#list}

Você pode listar todos os esquemas no `global` ou `tenant` ao fazer uma solicitação do GET para `/global/schemas` ou `/tenant/schemas`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o resultado dos limites do Registro de Esquema é definido como 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar resultados e reduzir o número de recursos retornados. Consulte a seção sobre [parâmetros de consulta](./appendix.md#query) no documento em anexo para mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que contém os esquemas que você deseja recuperar: `global` para esquemas criados por Adobe ou `tenant` para esquemas de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte a [documento de apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera uma lista de schemas do `tenant` contêiner, usando um `orderby` parâmetro de consulta para classificar os resultados por `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. O seguinte `Accept` os cabeçalhos estão disponíveis para listar schemas:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o esquema JSON completo para cada recurso, com o original `$ref` e `allOf` incluído. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Resposta**

A solicitação acima usou o `application/vnd.adobe.xed-id+json` `Accept` , portanto, a resposta inclui somente o cabeçalho `title`, `$id`, `meta:altId`e `version` atributos para cada esquema. Usar a outra `Accept` header (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada schema. Selecione o `Accept` dependendo das informações necessárias na resposta.

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

Você pode pesquisar um schema específico fazendo uma solicitação do GET que inclui a ID do schema no caminho.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container que hospeda o schema que você deseja recuperar: `global` para um esquema criado por Adobe ou `tenant` para um esquema pertencente à sua organização. |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera um esquema especificado por seu `meta:altId` no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Todas as solicitações de pesquisa exigem uma `version` ser incluídos no `Accept` cabeçalho. O seguinte `Accept` os cabeçalhos estão disponíveis:

| `Accept` header | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Simples com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` resolvido, tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | Simples com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` resolvido, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` resolvido, descritores incluídos. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` resolvido, tem títulos e descrições. Os campos obsoletos são indicados com um `meta:status` atributo de `deprecated`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema . Os campos retornados dependem do `Accept` cabeçalho enviado na solicitação. Experimentar com diferentes `Accept` cabeçalhos para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

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

O processo de composição de schema começa pela atribuição de uma classe. A classe define os principais aspectos comportamentais dos dados (registro ou série de tempo), bem como os campos mínimos necessários para descrever os dados que serão assimilados.

>[!NOTE]
>
>A chamada de exemplo abaixo é apenas um exemplo básico de como criar um schema na API, com os requisitos mínimos de composição de uma classe e nenhum grupo de campo. Para obter as etapas completas sobre como criar um esquema na API, incluindo como atribuir campos usando grupos de campos e tipos de dados, consulte o [tutorial de criação de schema](../tutorials/create-schema-api.md).

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação deve incluir um `allOf` atributo que faz referência ao `$id` de uma classe. Esse atributo define a &quot;classe base&quot; que o schema implementará. Neste exemplo, a classe base é uma classe &quot;Informações de propriedade&quot; criada anteriormente.

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
| `allOf` | Uma matriz de objetos, com cada objeto referindo-se a uma classe ou grupo de campos cujos campos o esquema implementa. Cada objeto contém uma única propriedade (`$ref`) cujo valor representa a variável `$id` da classe ou do grupo de campos que o novo schema implementará. Uma classe deve ser fornecida, com zero ou mais grupos de campo adicionais. No exemplo acima, o objeto único na variável `allOf` array é a classe do schema. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Created) e uma carga útil contendo os detalhes do schema recém-criado, incluindo o `$id`, `meta:altId`e `version`. Esses valores são somente leitura e são atribuídos pela variável [!DNL Schema Registry].

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

Executar uma solicitação GET para [listar todos os schemas](#list) no contêiner do locatário agora inclui o novo schema . Você pode executar um [solicitação de pesquisa (GET)](#lookup) usando o URL codificado `$id` URI para exibir o novo schema diretamente.

Para adicionar campos adicionais a um schema, é possível executar um [operação PATCH](#patch) para adicionar grupos de campos ao esquema `allOf` e `meta:extends` matrizes.

## Atualizar um esquema {#put}

Você pode substituir um schema inteiro por meio de uma operação PUT, essencialmente regravando o recurso. Ao atualizar um schema por meio de uma solicitação de PUT, o corpo deve incluir todos os campos que seriam necessários quando [criação de um novo schema](#create) em uma solicitação de POST.

>[!NOTE]
>
>Se quiser atualizar apenas parte de um schema em vez de substituí-lo por completo, consulte a seção em [atualização de uma parte de um schema](#patch).

**Formato da API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que deseja regravar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir substitui um schema existente, alterando seu `title`, `description`e `allOf` atributos.

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

Uma resposta bem-sucedida retorna os detalhes do schema atualizado.

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

Você pode atualizar uma parte de um schema usando uma solicitação de PATCH. O [!DNL Schema Registry] suporta todas as operações padrão de patch JSON, incluindo `add`, `remove`e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [Guia de fundamentos da API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de um schema por uma operação PUT](#put).

Uma das operações de PATCH mais comuns envolve adicionar grupos de campos definidos anteriormente a um schema, conforme demonstrado pelo exemplo abaixo.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URL codificado `$id` URI ou `meta:altId` do esquema que deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação de exemplo abaixo adiciona um novo grupo de campos a um schema adicionando esse grupo de campos `$id` para ambos `meta:extends` e `allOf` matrizes.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica para um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`) e que informações devem ser incluídas nessa operação (`value`).

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

## Ativar um esquema para usar no Perfil do cliente em tempo real {#union}

Para que um schema participe de [Perfil do cliente em tempo real](../../profile/home.md), você deve adicionar um `union` para o `meta:immutableTags` matriz. Você pode fazer isso fazendo uma solicitação PATCH para o schema em questão.

>[!IMPORTANT]
>
>Tags imutáveis são tags destinadas a serem definidas, mas nunca removidas.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URL codificado `$id` URI ou `meta:altId` do schema que deseja ativar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação de exemplo abaixo adiciona um `meta:immutableTags` para um schema existente, dando à matriz um único valor de string de `union` para habilitá-lo para uso no Perfil.

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

Uma resposta bem-sucedida retorna os detalhes do schema atualizado, mostrando que a variável `meta:immutableTags` foi adicionada.

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

Agora é possível visualizar a união da classe desse schema para confirmar se os campos do schema são representados. Consulte a [guia de endpoint de sindicatos](./unions.md) para obter mais informações.

## Excluir um esquema {#delete}

Ocasionalmente, pode ser necessário remover um esquema do Registro de Schema. Isso é feito executando-se uma solicitação DELETE com a ID de esquema fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URL codificado `$id` URI ou `meta:altId` do esquema que deseja excluir. |

{style=&quot;table-layout:auto&quot;}

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

É possível confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o esquema. Você precisará incluir um `Accept` na solicitação, mas deve receber um status HTTP 404 (Not Found) porque o schema foi removido do Registro de Schema.
