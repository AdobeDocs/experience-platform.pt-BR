---
keywords: Experience Platform;início;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de tipo de dados;registro de esquema;tipo de dados;tipos de dados;tipos de dados;criar
solution: Experience Platform
title: Endpoint da API de tipos de dados
description: O ponto de extremidade /datatypes na API do registro de esquema permite gerenciar de forma programática os tipos de dados XDM no aplicativo de experiência.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 3%

---

# Ponto de extremidade dos tipos de dados

Os tipos de dados são usados como campos do tipo referência em classes ou grupos de campos de esquema da mesma forma que os campos literais básicos, com a principal diferença sendo que os tipos de dados podem definir vários subcampos. Embora semelhantes a grupos de campos, pois permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do esquema, enquanto os grupos de campos só podem ser adicionados no nível raiz. A variável `/datatypes` endpoint na variável [!DNL Schema Registry] A API permite gerenciar programaticamente os tipos de dados no aplicativo de experiência.

>[!NOTE]
>
>Se um campo for definido como um tipo de dados específico, você não poderá criar o mesmo campo com um tipo de dados diferente em outro esquema. Essa restrição se aplica ao locatário da organização.

## Introdução

O endpoint usado neste guia faz parte da variável [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de tipos de dados {#list}

Você pode listar todos os tipos de dados no `global` ou `tenant` GET contêiner fazendo uma solicitação para `/global/datatypes` ou `/tenant/datatypes`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o Registro de esquema limita os conjuntos de resultados a 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar os resultados e reduzir o número de recursos retornados. Consulte a seção sobre [parâmetros de consulta](./appendix.md#query) no documento do apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container do qual você deseja recuperar tipos de dados: `global` para tipos de dados criados por Adobe ou `tenant` para tipos de dados de propriedade de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados. Consulte a [documento do apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera uma lista de tipos de dados do `tenant` contêiner, usando um `orderby` parâmetro de consulta para classificar os tipos de dados por seus `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. As seguintes `Accept` os cabeçalhos estão disponíveis para listar tipos de dados:

| `Accept` cabeçalho | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o tipo de dados JSON completo para cada recurso, com o original `$ref` e `allOf` incluído. (Limite: 300) |

{style="table-layout:auto"}

**Resposta**

A solicitação acima usou o `application/vnd.adobe.xed-id+json` `Accept` cabeçalho, portanto, a resposta inclui apenas o `title`, `$id`, `meta:altId`, e `version` atributos para cada tipo de dados. Usar o outro `Accept` cabeçalho (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada tipo de dados. Selecione o apropriado `Accept` dependendo das informações que você precisa na sua resposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
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
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## Pesquisar um tipo de dados {#lookup}

Você pode pesquisar um tipo de dados específico incluindo a ID do tipo de dados no caminho de uma solicitação GET.

**Formato da API**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que armazena o tipo de dados que você deseja recuperar: `global` para um tipo de dados criado por Adobe ou `tenant` para um tipo de dados pertencente à sua organização. |
| `{DATA_TYPE_ID}` | A variável `meta:altId` ou codificado em URL `$id` do tipo de dados que você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera um tipo de dados por seus `meta:altId` valor fornecido no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
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

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do tipo de dados. Os campos retornados dependem do tipo `Accept` cabeçalho enviado na solicitação. Experimento com diferentes `Accept` cabeçalhos para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Criar um tipo de dados {#create}

Você pode definir um tipo de dados personalizado na `tenant` fazendo uma solicitação POST.

**Formato da API**

```http
POST /tenant/datatypes
```

**Solicitação**

Ao contrário dos grupos de campos, a definição de um tipo de dados não requer `meta:extends` ou `meta:intendedToExtend` campos, nem os campos precisam ser aninhados para evitar colisões.

Quando se trata de definir a estrutura de campo do próprio tipo de dados, você pode usar tipos primitivos (como `string` ou `object`) ou você pode fazer referência a outros tipos de dados existentes por meio de `$ref` atributos. Consulte o guia sobre [definição de campos XDM personalizados na API](../tutorials/custom-fields-api.md) para obter orientação detalhada sobre o formato esperado para diferentes tipos de campo XDM.

A solicitação a seguir cria um tipo de dados de objeto &quot;Construção de propriedade&quot; com subpropriedades `yearBuilt`, `propertyType`, e `location`:

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga contendo os detalhes do tipo de dados recém-criado, incluindo o `$id`, `meta:altId`, e `version`. Esses três valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Execução de uma solicitação do GET para [listar todos os tipos de dados](#list) no contêiner do locatário agora incluiria o tipo de dados Detalhes da propriedade, ou você pode [executar uma solicitação de pesquisa (GET)](#lookup) usar o URL codificado `$id` URI para visualizar o novo tipo de dados diretamente.

## Atualizar um tipo de dados {#put}

Você pode substituir um tipo de dados inteiro por meio de uma operação PUT, essencialmente reescrevendo o recurso. Ao atualizar um tipo de dados por meio de uma solicitação PUT, o corpo deve incluir todos os campos que seriam necessários ao [criação de um novo tipo de dados](#create) em uma solicitação POST.

>[!NOTE]
>
>Se você quiser atualizar apenas parte de um tipo de dados, em vez de substituí-lo totalmente, consulte a seção sobre [atualização de uma parte de um tipo de dados](#patch).

**Formato da API**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_TYPE_ID}` | A variável `meta:altId` ou codificado em URL `$id` do tipo de dados que você deseja regravar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir reescreve um tipo de dados existente, adicionando um novo `floorSize` campo.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do tipo de dados atualizado.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Atualizar uma parte de um tipo de dados {#patch}

Você pode atualizar uma parte de um tipo de dados usando uma solicitação PATCH. A variável [!DNL Schema Registry] suporta todas as operações de patch JSON padrão, incluindo `add`, `remove`, e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [Guia de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se você quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de um tipo de dados usando uma operação PUT](#put).

**Formato da API**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_TYPE_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do tipo de dados que você deseja atualizar. |

{style="table-layout:auto"}

**Solicitação**

O exemplo de solicitação abaixo atualiza o `description` de um tipo de dados existente e adiciona um novo `floorSize` campo.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica em um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`), e que informações devem ser incluídas nessa operação (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**Resposta**

A resposta mostra que ambas as operações foram executadas com êxito. A variável `description` foi atualizado e `floorSize` foi adicionado em `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type": "object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Excluir um tipo de dados {#delete}

Ocasionalmente, pode ser necessário remover um tipo de dados do Registro de esquemas. Isso é feito executando uma solicitação DELETE com a ID do tipo de dados fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_TYPE_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do tipo de dados que você deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando [solicitação de pesquisa (GET)](#lookup) ao tipo de dados. Será necessário incluir um `Accept` cabeçalho na solicitação, mas deve receber um status HTTP 404 (Não encontrado) porque o tipo de dados foi removido do Registro de esquemas.
