---
keywords: Experience Platform;home;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;esquema;Esquema;esquemas;esquemas;criar
solution: Experience Platform
title: Endpoint da API de esquemas
description: O ponto de extremidade /schemas na API do registro de esquema permite gerenciar de forma programática esquemas XDM no aplicativo de experiência.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 4586a820556919aeb6cebd94d961c3f726637f16
workflow-type: tm+mt
source-wordcount: '2095'
ht-degree: 4%

---

# Endpoint de esquemas

Um esquema pode ser visto como o blueprint dos dados que você deseja assimilar na Adobe Experience Platform. Cada esquema é composto por uma classe e zero ou mais grupos de campos de esquema. O ponto de extremidade `/schemas` na API [!DNL Schema Registry] permite gerenciar esquemas de forma programática no aplicativo de experiência.

## Introdução

O ponto de extremidade de API usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de esquemas {#list}

Você pode listar todos os esquemas no contêiner `global` ou `tenant` fazendo uma solicitação GET para `/global/schemas` ou `/tenant/schemas`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o Registro de esquema limita os conjuntos de resultados a 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar os resultados e reduzir o número de recursos retornados. Consulte a seção sobre [parâmetros de consulta](./appendix.md#query) no documento do apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que abriga os esquemas que você deseja recuperar: `global` para esquemas criados pela Adobe ou `tenant` para esquemas de propriedade de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados. Consulte o [documento do apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera uma lista de esquemas do contêiner `tenant`, usando um parâmetro de consulta `orderby` para classificar os resultados por seu atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato da resposta depende do cabeçalho `Accept` enviado na solicitação. Os `Accept` cabeçalhos a seguir estão disponíveis para listar esquemas:

| Cabeçalho `Accept` | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o esquema JSON completo para cada recurso, com os `$ref` e `allOf` originais incluídos. (Limite: 300) |

{style="table-layout:auto"}

**Resposta**

A solicitação acima usou o cabeçalho `application/vnd.adobe.xed-id+json` `Accept`, portanto, a resposta inclui apenas os atributos `title`, `$id`, `meta:altId` e `version` para cada esquema. O uso do outro cabeçalho `Accept` (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada esquema. Selecione o cabeçalho `Accept` apropriado, dependendo das informações que você precisa na sua resposta.

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
| `{CONTAINER_ID}` | O contêiner que abriga o esquema que você deseja recuperar: `global` para um esquema criado pela Adobe ou `tenant` para um esquema pertencente à sua organização. |
| `{SCHEMA_ID}` | O `meta:altId` ou o `$id` codificado na URL do esquema que você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera um esquema especificado por seu valor `meta:altId` no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato da resposta depende do cabeçalho `Accept` enviado na solicitação. Todas as solicitações de pesquisa exigem que um `version` seja incluído no cabeçalho `Accept`. Os seguintes `Accept` cabeçalhos estão disponíveis:

| Cabeçalho `Accept` | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Simples com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` resolvidos, têm títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | Simples com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` resolvidos, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` resolvidos, descritores incluídos. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` resolvidos, têm títulos e descrições. Campos obsoletos são indicados com um atributo `meta:status` de `deprecated`. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do esquema. Os campos retornados dependem do cabeçalho `Accept` enviado na solicitação. Experimente com diferentes cabeçalhos `Accept` para comparar as respostas e determinar qual cabeçalho é melhor para o seu caso de uso.

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

Para obter instruções sobre como criar um esquema sem classes ou grupos de campos, conhecido como esquema baseado em modelo, consulte a seção [Criar um esquema baseado em modelo](#create-model-based-schema).

>[!NOTE]
>
>O exemplo de chamada abaixo é apenas um exemplo de linha de base de como criar um esquema na API, com os requisitos mínimos de composição de uma classe e nenhum grupo de campos. Para obter as etapas completas sobre como criar um esquema na API, incluindo como atribuir campos usando grupos de campos e tipos de dados, consulte o [tutorial de criação de esquema](../tutorials/create-schema-api.md).

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação deve incluir um atributo `allOf` que faça referência a `$id` de uma classe. Esse atributo define a &quot;classe base&quot; que o esquema implementará. Neste exemplo, a classe base é uma classe &quot;Informações de propriedade&quot; criada anteriormente.

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
| `allOf` | Uma matriz de objetos, com cada objeto referindo-se a uma classe ou grupo de campos cujos campos o esquema implementa. Cada objeto contém uma única propriedade (`$ref`) cujo valor representa o `$id` da classe ou do grupo de campos que o novo esquema implementará. Uma classe deve ser fornecida, com zero ou mais grupos de campos adicionais. No exemplo acima, o único objeto na matriz `allOf` é a classe do esquema. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga contendo os detalhes do esquema recém-criado, incluindo `$id`, `meta:altId` e `version`. Esses valores são somente leitura e são atribuídos por [!DNL Schema Registry].

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

A execução de uma solicitação GET para [listar todos os esquemas](#list) no contêiner de locatário agora incluiria o novo esquema. Você pode executar uma [solicitação de pesquisa (GET)](#lookup) usando o URI `$id` codificado em URL para exibir o novo esquema diretamente.

Para adicionar campos extras a um esquema, você pode executar uma [operação do PATCH](#patch) para adicionar grupos de campos às matrizes `allOf` e `meta:extends` do esquema.

## Crie um esquema baseado em modelo {#create-model-based-schema}

>[!AVAILABILITY]
>
>O Data Mirror e os esquemas baseados em modelo estão disponíveis para os **titulares de licença de campanhas orquestradas** da Adobe Journey Optimizer. Eles também estão disponíveis como uma **versão limitada** para usuários do Customer Journey Analytics, dependendo da sua licença e da ativação de recursos. Entre em contato com o representante da Adobe para obter acesso.

Crie um esquema baseado em modelo fazendo uma solicitação POST para o ponto de extremidade `/schemas`. Esquemas baseados em modelo armazenam dados estruturados de estilo relacional **sem** classes ou grupos de campos. Defina campos diretamente no esquema e identifique o esquema como baseado em modelo usando uma tag de comportamento lógico.

>[!IMPORTANT]
>
>Para criar um esquema baseado em modelo, defina `meta:extends` como `"https://ns.adobe.com/xdm/data/adhoc-v2"`. Este é um **identificador de comportamento lógico** (não é uma classe ou comportamento físico). **não** faz referência a classes ou grupos de campos em `allOf`, e **não** inclui classes ou grupos de campos em `meta:extends`.

Crie o esquema primeiro com `POST /tenant/schemas`. Em seguida, adicione os descritores necessários com a [API de descritores (`POST /tenant/descriptors`)](../api/descriptors.md):

- [Descritor de chave primária](../api/descriptors.md#primary-key-descriptor): um campo de chave primária deve estar no **nível raiz** e **marcado como obrigatório**.
- [Descritor de versão](../api/descriptors.md#version-descriptor): **Obrigatório** quando existe uma chave primária.
- [Descritor de relacionamento](../api/descriptors.md#relationship-descriptor): opcional, define junções; cardinalidade não imposta na assimilação.
- [Descritor de carimbo de data/hora](../api/descriptors.md#timestamp-descriptor): para esquemas de série temporal, a chave primária deve ser uma chave **composta** que inclua o campo de carimbo de data/hora.

>[!NOTE]
>
>No Editor de Esquema de Interface do Usuário, o descritor de versão e os descritores de carimbo de data/hora aparecem como &quot;[!UICONTROL Identificador de versão]&quot; e &quot;[!UICONTROL Identificador de carimbo de data/hora]&quot;, respectivamente.

<!-- >[!AVAILABILITY]
>
>Although `meta:behaviorType` technically accepts `time-series`, support is not currently available for model-based schemas. Set `meta:behaviorType` to `"record"`. -->

>[!CAUTION]
>
>Os esquemas baseados em modelo **não são compatíveis com os esquemas de união**. Não aplique a marca `union` a `meta:immutableTags` ao trabalhar com esquemas baseados em modelo. Essa configuração está bloqueada na interface do usuário, mas não está bloqueada no momento pela API. Consulte o [manual de endpoint de uniões](./unions.md) para obter mais informações sobre o comportamento do esquema de união.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### Propriedades do corpo da solicitação

| Propriedade | Tipo | Descrição |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | String | Nome de exibição do esquema. |
| `description` | String | Breve explicação da finalidade do esquema. |
| `type` | String | Deve ser `"object"` para esquemas baseados em modelo. |
| `definitions` | Objeto | Contém os objetos de nível raiz que definem os campos do esquema. |
| `definitions.<name>.properties` | Objeto | Nomes de campos e tipos de dados. |
| `allOf` | Matriz | Faz referência à definição de objeto de nível raiz (por exemplo, `#/definitions/marketing_customers`). |
| `meta:extends` | Matriz | É necessário incluir `"https://ns.adobe.com/xdm/data/adhoc-v2"` para identificar o esquema como baseado em modelo. |
| `meta:behaviorType` | String | Defina como `"record"`. Use `"time-series"` somente quando habilitado e apropriado. |

>[!IMPORTANT]
>
>A evolução do esquema para esquemas baseados em modelo segue as mesmas regras aditivas que os esquemas padrão. Você pode adicionar novos campos com uma solicitação PATCH. Alterações como renomear ou remover campos só são permitidas se nenhum dado tiver sido assimilado no conjunto de dados.

**Resposta**

Uma solicitação bem-sucedida retorna **HTTP 201 (Criado)** e o esquema criado.

>[!NOTE]
>
>Os esquemas baseados em modelo não herdam campos pré-implantados (por exemplo, id, carimbo de data e hora ou eventType). Defina todos os campos obrigatórios explicitamente no esquema.

**Exemplo de resposta**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### Propriedades do corpo de resposta

| Propriedade | Tipo | Descrição |
| ------------------- | ------ | -------------------------- |
| `$id` | String | O URL exclusivo do esquema criado. Use em chamadas de API subsequentes. |
| `meta:altId` | String | Um identificador alternativo do esquema. |
| `meta:resourceType` | String | O tipo de recurso (sempre `"schemas"`). |
| `version` | String | Uma versão de esquema atribuída na criação. |
| `title` | String | O nome de exibição do esquema. |
| `description` | String | Uma breve explicação da finalidade do esquema. |
| `type` | String | O tipo de esquema. |
| `definitions` | Objeto | Define objetos reutilizáveis ou grupos de campos usados no esquema. Normalmente, isso inclui a estrutura de dados principal e é referenciado na matriz `allOf` para definir a raiz do esquema. |
| `allOf` | Matriz | Especifica o objeto raiz do esquema referenciando uma ou mais definições (por exemplo, `#/definitions/marketing_customers`). |
| `meta:extends` | Matriz | Identifica o esquema como baseado em modelo (`adhoc-v2`). |
| `meta:behaviorType` | String | Tipo de comportamento (`record` ou `time-series`, quando habilitado). |
| `meta:containerId` | String | Contêiner no qual o esquema é armazenado (por exemplo, `tenant`). |

Para adicionar campos a um esquema baseado em modelo após sua criação, faça uma [solicitação PATCH](#patch). Os esquemas baseados em modelo não herdam ou evoluem automaticamente. Alterações estruturais como renomear ou excluir campos só são permitidas se nenhum dado tiver sido assimilado no conjunto de dados. Quando os dados existirem, somente **alterações aditivas** (como a adição de novos campos) serão suportadas.

Você pode adicionar novos campos de nível raiz (dentro da definição raiz ou raiz `properties`), mas não pode remover, renomear ou alterar o tipo de campos existentes.

>[!CAUTION]
>
>A evolução do esquema fica restrita depois que um conjunto de dados é inicializado usando o esquema. Planeje os nomes e tipos de campo com antecedência, pois após a assimilação dos dados, os campos não poderão ser excluídos ou modificados.

## Atualizar um esquema {#put}

É possível substituir um esquema inteiro por meio de uma operação do PUT, essencialmente reescrevendo o recurso. Ao atualizar um esquema por meio de uma solicitação PUT, o corpo deve incluir todos os campos que seriam necessários ao [criar um novo esquema](#create) em uma solicitação POST.

>[!NOTE]
>
>Se você quiser atualizar apenas parte de um esquema, em vez de substituí-lo totalmente, consulte a seção sobre [atualização de uma parte de um esquema](#patch).

**Formato da API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou o `$id` codificado na URL do esquema que você deseja regravar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir substitui um esquema existente, alterando seus atributos `title`, `description` e `allOf`.

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

Você pode atualizar uma parte de um esquema usando uma solicitação PATCH. O [!DNL Schema Registry] dá suporte a todas as operações de patch de JSON padrão, incluindo `add`, `remove` e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [guia de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se você quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de um esquema usando uma operação PUT](#put).

Uma das operações mais comuns do PATCH envolve adicionar grupos de campos definidos anteriormente a um esquema, conforme demonstrado pelo exemplo abaixo.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URI `$id` codificado na URL ou `meta:altId` do esquema que você deseja atualizar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação de exemplo abaixo adiciona um novo grupo de campos a um esquema adicionando o valor `$id` desse grupo de campos às matrizes `meta:extends` e `allOf`.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica em um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`) e quais informações devem ser incluídas nessa operação (`value`).

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

A resposta mostra que ambas as operações foram executadas com êxito. O grupo de campos `$id` foi adicionado à matriz `meta:extends` e uma referência (`$ref`) ao grupo de campos `$id` agora aparece na matriz `allOf`.

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

Para que um esquema participe do [Perfil de Cliente em Tempo Real](../../profile/home.md), é necessário adicionar uma marca `union` à matriz `meta:immutableTags` do esquema. Você pode fazer isso fazendo uma solicitação PATCH para o esquema em questão.

>[!IMPORTANT]
>
>Tags imutáveis são tags que devem ser definidas, mas nunca removidas.

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URI `$id` codificado na URL ou `meta:altId` do esquema que você deseja habilitar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação de exemplo abaixo adiciona uma matriz `meta:immutableTags` a um esquema existente, dando à matriz um único valor de cadeia de caracteres de `union` para habilitá-la para uso no Perfil.

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

Uma resposta bem-sucedida retorna os detalhes do esquema atualizado, mostrando que a matriz `meta:immutableTags` foi adicionada.

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

Agora você pode visualizar a união da classe deste esquema para confirmar que os campos do esquema são representados. Consulte o [manual de ponto de extremidade de uniões](./unions.md) para obter mais informações.

## Excluir um esquema {#delete}

Ocasionalmente, pode ser necessário remover um esquema do Registro de esquemas. Isso é feito executando uma solicitação DELETE com a ID do esquema fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URI `$id` codificado na URL ou `meta:altId` do esquema que você deseja excluir. |

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

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o esquema. Você precisará incluir um cabeçalho `Accept` na solicitação, mas deverá receber um status HTTP 404 (Não encontrado) porque o esquema foi removido do Registro de esquemas.
