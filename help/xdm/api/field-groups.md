---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;Registro de esquemas;grupo de campos;grupos de campos;criar
solution: Experience Platform
title: Endpoint da API de grupos de campos
description: O ponto de extremidade /fieldgroups na API do registro de esquemas permite gerenciar programaticamente os grupos de campos de esquema XDM no aplicativo de experiência.
exl-id: d26257e4-c7d5-4bff-b555-7a2997c88c74
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 4%

---

# Ponto de extremidade dos grupos de campos de esquema

Grupos de campos de esquema são componentes reutilizáveis que definem um ou mais campos que representam um conceito específico, como uma pessoa individual, um endereço de correspondência ou um ambiente de navegador da Web. Os grupos de campos devem ser incluídos como parte de um esquema que implementa uma classe compatível, dependendo do comportamento dos dados que representam (registro ou série de tempo). A variável `/fieldgroups` endpoint na variável [!DNL Schema Registry] A API permite gerenciar programaticamente grupos de campos no aplicativo de experiência.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de grupos de campos {#list}

Você pode listar todos os grupos de campos sob a `global` ou `tenant` GET contêiner fazendo uma solicitação para `/global/fieldgroups` ou `/tenant/fieldgroups`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o Registro de esquema limita os conjuntos de resultados a 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar os resultados e reduzir o número de recursos retornados. Consulte a seção sobre [parâmetros de consulta](./appendix.md#query) no documento do apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container do qual você deseja recuperar grupos de campos: `global` para grupos de campos criados por Adobe ou `tenant` para grupos de campos de propriedade de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados. Consulte a [documento do apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera uma lista de grupos de campos do `tenant` contêiner, usando um `orderby` parâmetro de consulta para classificar os grupos de campos por seus `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. As seguintes `Accept` os cabeçalhos estão disponíveis para listar grupos de campos:

| `Accept` cabeçalho | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna o grupo de campos JSON completo para cada recurso, com o original `$ref` e `allOf` incluído. (Limite: 300) |

{style="table-layout:auto"}

**Resposta**

A solicitação acima usou o `application/vnd.adobe.xed-id+json` `Accept` cabeçalho, portanto, a resposta inclui apenas o `title`, `$id`, `meta:altId`, e `version` atributos para cada grupo de campos. Usar o outro `Accept` cabeçalho (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada grupo de campos. Selecione o apropriado `Accept` dependendo das informações que você precisa na sua resposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.mixins.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.mixins.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.mixins.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.mixins.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## Pesquisar um grupo de campos {#lookup}

Você pode pesquisar um grupo de campos específico incluindo a ID do grupo de campos no caminho de uma solicitação GET.

**Formato da API**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que abriga o grupo de campos que você deseja recuperar: `global` para um grupo de campos criado por Adobe ou `tenant` para um grupo de campos de propriedade de sua organização. |
| `{FIELD_GROUP_ID}` | A variável `meta:altId` ou codificado em URL `$id` do grupo de campos que você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera um grupo de campos por sua `meta:altId` valor fornecido no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Todas as solicitações de pesquisa exigem uma `version` ser incluído na lista `Accept` cabeçalho. As seguintes `Accept` os cabeçalhos estão disponíveis:

| `Accept` cabeçalho | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Simples com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvida, tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Simples com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvida, nenhum título ou descrição. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido, descritores incluídos. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do grupo de campos. Os campos retornados dependem do tipo `Accept` cabeçalho enviado na solicitação. Experimento com diferentes `Accept` cabeçalhos para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
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

## Crie um grupo de campos {#create}

Você pode definir um grupo de campos personalizado em `tenant` fazendo uma solicitação POST.

**Formato da API**

```http
POST /tenant/fieldgroups
```

**Solicitação**

Ao definir um novo grupo de campos, ele deve incluir uma `meta:intendedToExtend` atributo, listando o `$id` das classes com as quais o grupo de campos é compatível. Neste exemplo, o grupo de campos é compatível com um `Property` que foi definida anteriormente. Os campos personalizados devem ser aninhados em `_{TENANT_ID}` (como mostrado no exemplo ) para evitar colisões com campos semelhantes fornecidos por classes e outros grupos de campos.

>[!NOTE]
>
>Para obter detalhes sobre como definir diferentes tipos de campo para incluir no grupo de campos, consulte o guia em [definição de campos personalizados na API](../tutorials/custom-fields-api.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
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
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga contendo os detalhes do grupo de campos recém-criado, incluindo o `$id`, `meta:altId`, e `version`. Esses valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
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

Execução de uma solicitação do GET para [listar todos os grupos de campos](#list) no contêiner do locatário agora incluiria o grupo de campos Detalhes da propriedade, ou você pode [executar uma solicitação de pesquisa (GET)](#lookup) usar o URL codificado `$id` URI para visualizar o novo grupo de campos diretamente.

## Atualizar um grupo de campos {#put}

Você pode substituir um grupo de campos inteiro por meio de uma operação PUT, essencialmente reescrevendo o recurso. Ao atualizar um grupo de campos por meio de uma solicitação PUT, o corpo deve incluir todos os campos que seriam necessários ao [criação de um novo grupo de campos](#create) em uma solicitação POST.

>[!NOTE]
>
>Se você quiser atualizar apenas parte de um grupo de campos, em vez de substituí-lo totalmente, consulte a seção sobre [atualizar uma parte de um grupo de campos](#patch).

**Formato da API**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{FIELD_GROUP_ID}` | A variável `meta:altId` ou codificado em URL `$id` do grupo de campos que você deseja regravar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir reescreve um grupo de campos existente, adicionando um novo `propertyCountry` campo.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
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
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do grupo de campos atualizado.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
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

## Atualizar uma parte de um grupo de campos {#patch}

Você pode atualizar uma parte de um grupo de campos usando uma solicitação PATCH. A variável [!DNL Schema Registry] suporta todas as operações de patch JSON padrão, incluindo `add`, `remove`, e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [Guia de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se você quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de um grupo de campos usando uma operação PUT](#put).

**Formato da API**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{FIELD_GROUP_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do grupo de campos que você deseja atualizar. |

{style="table-layout:auto"}

**Solicitação**

O exemplo de solicitação abaixo atualiza o `description` de um grupo de campos existente e adiciona um novo `propertyCity` campo.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica em um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`), e que informações devem ser incluídas nessa operação (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**Resposta**

A resposta mostra que ambas as operações foram executadas com êxito. A variável `description` foi atualizado e `propertyCountry` foi adicionado em `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
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

## Excluir um grupo de campos {#delete}

Ocasionalmente, pode ser necessário remover um grupo de campos do Registro de esquemas. Isso é feito executando uma solicitação DELETE com a ID do grupo de campos fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{FIELD_GROUP_ID}` | O formato codificado por URL `$id` URI ou `meta:altId` do grupo de campos que você deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando [solicitação de pesquisa (GET)](#lookup) ao grupo de campos. Será necessário incluir um `Accept` cabeçalho na solicitação, mas deve receber um status HTTP 404 (Não encontrado) porque o grupo de campos foi removido do Registro de esquemas.
