---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Criar um schema
description: O endpoint /schemas na API de Registro de Schemas permite que você gerencie programaticamente schemas XDM no aplicativo de experiência.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 2%

---


# Ponto de extremidade de schemas

Um schema pode ser considerado como o modelo para os dados que você deseja ingerir no Adobe Experience Platform. Cada schema é composto de uma classe e zero ou mais combinações. O `/schemas` endpoint na [!DNL Schema Registry] API permite que você gerencie programaticamente schemas dentro do seu aplicativo de experiência.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de schemas {#list}

Você pode lista todos os schemas sob o `global` container ou `tenant` realizando uma solicitação de GET para `/global/schemas` ou `/tenant/schemas`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o resultado do Limite do Registro do Schema é definido como 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de query adicionais para filtrar resultados e reduzir o número de recursos retornados. Consulte a seção sobre parâmetros [do](./appendix.md#query) query no documento apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container que contém os schemas que você deseja recuperar: `global` para schemas criados por Adobe ou `tenant` para schemas de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de query opcionais para filtrar os resultados. Consulte o documento [de](./appendix.md#query) apêndice para obter uma lista dos parâmetros disponíveis. |

**Solicitação**

A solicitação a seguir recupera uma lista de schemas do `tenant` container, usando um parâmetro de `orderby` query para classificar os resultados pelo `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Os `Accept` cabeçalhos a seguir estão disponíveis para a listagem de schemas:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para a listagem de recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o schema JSON completo para cada recurso, com original `$ref` e `allOf` incluído. (Limite: 300) |

**Resposta**

A solicitação acima usou o `application/vnd.adobe.xed-id+json` cabeçalho, portanto a resposta inclui apenas os atributos `Accept` , `title`, `$id`e `meta:altId``version` para cada schema. Usar o outro `Accept` cabeçalho (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada schema. Selecione o `Accept` cabeçalho apropriado, dependendo das informações necessárias na sua resposta.

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

## Procure um schema {#lookup}

Você pode pesquisar um schema específico fazendo uma solicitação de GET que inclua a ID do schema no caminho.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container que hospeda o schema que você deseja recuperar: `global` para um schema criado por Adobe ou `tenant` para um schema pertencente à sua organização. |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do schema que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera um schema especificado por seu `meta:altId` valor no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Todas as solicitações de pesquisa exigem que `version` sejam incluídas no `Accept` cabeçalho. The following `Accept` headers are available:

| `Accept` header | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Bruto com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido, tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Bruto com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvidos, descritores incluídos. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema. Os campos retornados dependem do `Accept` cabeçalho enviado na solicitação. Experimente com `Accept` cabeçalhos diferentes para comparar as respostas e determinar qual cabeçalho é melhor para seu caso de uso.

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
  "imsOrg": "{IMS_ORG}",
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

## Criar um schema {#create}

O processo de composição do schema começa atribuindo uma classe. A classe define os principais aspectos comportamentais dos dados (registro ou série cronológica), bem como os campos mínimos necessários para descrever os dados que serão assimilados.

>[!NOTE]
>
>A chamada de exemplo abaixo é apenas um exemplo básico de como criar um schema na API, com os requisitos mínimos de composição de uma classe e sem combinações. Para obter as etapas completas sobre como criar um schema na API, incluindo como atribuir campos usando misturas e tipos de dados, consulte o tutorial [de criação de](../tutorials/create-schema-api.md)schemas.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação deve incluir um `allOf` atributo que faça referência ao `$id` de uma classe. Este atributo define a &quot;classe base&quot; que o schema implementará. Neste exemplo, a classe base é uma classe &quot;Informações de propriedade&quot; criada anteriormente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `allOf` | Uma matriz de objetos, com cada objeto referindo-se a uma classe ou combinação cujos campos o schema implementa. Cada objeto contém uma única propriedade (`$ref`) cujo valor representa o valor `$id` da classe ou da combinação no novo schema será implementada. Deve ser fornecida uma classe, com zero ou mais misturas adicionais. No exemplo acima, o único objeto na `allOf` matriz é a classe schema. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga que contém os detalhes do schema recém-criado, incluindo o `$id`, `meta:altId`e `version`. Esses valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

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
    "imsOrg": "{IMS_ORG}",
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

Executar uma solicitação de GET para [lista de todos os schemas](#list) no container do locatário agora inclui o novo schema. Você pode executar uma solicitação [de](#lookup) pesquisa (GET) usando o `$id` URI codificado por URL para visualização direta do novo schema.

Para adicionar campos adicionais a um schema, é possível executar uma operação [de](#patch) PATCH para adicionar combinações ao schema `allOf` e às `meta:extends` matrizes.

## Atualizar um schema {#put}

Você pode substituir um schema inteiro por uma operação de PUT, essencialmente regravando o recurso. Ao atualizar um schema por meio de uma solicitação de PUT, o corpo deve incluir todos os campos que seriam necessários ao [criar um novo schema](#create) em uma solicitação de POST.

>[!NOTE]
>
>Se você quiser apenas atualizar parte de um schema em vez de substituí-lo totalmente, consulte a seção sobre como [atualizar uma parte de um schema](#patch).

**Formato da API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do schema que você deseja regravar. |

**Solicitação**

A solicitação a seguir substitui um schema existente, alterando seus atributos `title`, `description`e `allOf` .

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

## Atualizar uma parte de um schema {#patch}

É possível atualizar uma parte de um schema usando uma solicitação de PATCH. O [!DNL Schema Registry] suporta todas as operações padrão de Patch JSON, incluindo `add`, `remove`e `replace`. Para obter mais informações sobre o Patch JSON, consulte o guia [de fundamentos da](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>Se quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre como [substituir um schema usando uma operação](#put)PUT.

Uma das operações de PATCH mais comuns envolve a adição de misturas previamente definidas a um schema, como demonstrado pelo exemplo abaixo.

**Formato da API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `$id` URI codificado por URL ou `meta:altId` o schema que você deseja atualizar. |

**Solicitação**

A solicitação de exemplo abaixo adiciona uma nova combinação a um schema adicionando o `$id` valor dessa combinação às `meta:extends` matrizes `allOf` e às matrizes.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica para um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`) e quais informações devem ser incluídas nessa operação (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

A resposta mostra que ambas as operações foram executadas com êxito. A mistura `$id` foi adicionada à `meta:extends` matriz e uma referência (`$ref`) à mistura `$id` agora aparece na `allOf` matriz.

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

## Ative um schema para uso no Perfil do cliente em tempo real {#union}

Para que um schema participe do Perfil [Cliente em tempo](../../profile/home.md)real, é necessário adicionar uma `union` tag ao storage do schema `meta:immutableTags` . Para fazer isso, faça uma solicitação PATCH para o schema em questão.

>[!IMPORTANT]
>
>Tags imutáveis são tags que devem ser definidas, mas nunca removidas.

**Formato da API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `$id` URI codificado por URL ou `meta:altId` o schema que você deseja ativar. |

**Solicitação**

A solicitação de exemplo abaixo adiciona uma `meta:immutableTags` matriz a um schema existente, dando ao storage um valor de sequência de caracteres único de `union` para permitir o uso no Perfil.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Uma resposta bem-sucedida retorna os detalhes do schema atualizado, mostrando que o `meta:immutableTags` storage foi adicionado.

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

Agora você pode visualização a união desta classe de schemas para confirmar se os campos de schemas estão representados. Consulte o guia [de endpoint do](./unions.md) união para obter mais informações.

## Excluir um schema {#delete}

Por vezes, pode ser necessário remover um schema do Registro do Schema. Isso é feito executando-se uma solicitação de DELETE com a ID do schema fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `$id` URI codificado por URL ou `meta:altId` o schema que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o schema. Você precisará incluir um `Accept` cabeçalho na solicitação, mas deverá receber um status HTTP 404 (Não encontrado), pois o schema foi removido do Registro do Schema.