---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados da experiência, Modelo de dados, Modelo de dados, registro mixin, Registro de esquemas, mixin, mixins, mixins, criar
solution: Experience Platform
title: Ponto de extremidade da API Mixins
description: O endpoint /mixins na API do Registro de Schema permite gerenciar programaticamente mixins XDM no aplicativo de experiência.
topic-legacy: developer guide
exl-id: 93ba2fe3-0277-4c06-acf6-f236cd33252e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 5%

---


# Ponto de extremidade Mixins (obsoleto)

>[!IMPORTANT]
>
>As misturas foram renomeadas para grupos de campos de esquema e, portanto, o ponto de extremidade `/mixins` foi substituído no ponto de extremidade `/fieldgroups`.
>
>Embora `/mixins` continue sendo mantido como um endpoint herdado, é altamente recomendável usar `/fieldgroups` para novas implementações da API do Registro de Schema em seus aplicativos de experiência. Consulte o [guia de ponto de extremidade de grupos de campos](./field-groups.md) para obter mais informações.

As misturas são componentes reutilizáveis que definem um ou mais campos que representam um conceito específico, como uma pessoa individual, um endereço de correspondência ou um ambiente de navegador da Web. As misturas devem ser incluídas como parte de um schema que implementa uma classe compatível, dependendo do comportamento dos dados que representam (registro ou série de tempo). O endpoint `/mixins` na API [!DNL Schema Registry] permite gerenciar programaticamente as combinações no aplicativo de experiência.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de mixins {#list}

Você pode listar todas as combinações no contêiner `global` ou `tenant` fazendo uma solicitação GET para `/global/mixins` ou `/tenant/mixins`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o resultado dos limites do Registro de Esquema é definido como 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar resultados e reduzir o número de recursos retornados. Consulte a seção [parâmetros de consulta](./appendix.md#query) no documento de apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner do qual você deseja recuperar mixins de: `global` para mixins criados por Adobe ou `tenant` para mixins de propriedade de sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte o [documento de apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera uma lista de mixins do contêiner `tenant`, usando um parâmetro de consulta `orderby` para classificar os mixins pelo atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Os seguintes cabeçalhos `Accept` estão disponíveis para listar mixins:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna a combinação JSON completa para cada recurso, com `$ref` original e `allOf` incluídas. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Resposta**

A solicitação acima usou o cabeçalho `application/vnd.adobe.xed-id+json` `Accept`, portanto, a resposta inclui apenas os atributos `title`, `$id`, `meta:altId` e `version` para cada mixin. Usar o outro cabeçalho `Accept` (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada mixin. Selecione o cabeçalho `Accept` apropriado, dependendo das informações necessárias na resposta.

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
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/mixins"
    }
  }
}
```

## Procure uma mistura {#lookup}

Você pode pesquisar um mixin específico incluindo a ID do mixin no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que contém o mixin que você deseja recuperar: `global` para um mixin criado por Adobe ou `tenant` para um mixin de propriedade de sua organização. |
| `{MIXIN_ID}` | O `meta:altId` ou o `$id` codificado por URL do mixin que você deseja procurar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera um mixin pelo seu valor `meta:altId` fornecido no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Todas as solicitações de pesquisa exigem que `version` seja incluído no cabeçalho `Accept`. Os seguintes cabeçalhos `Accept` estão disponíveis:

| `Accept` header | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Simples com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e  `allOf` resolvidas, tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | Simples com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e  `allOf` resolvidas, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e  `allOf` resolvidos, incluíam descritores. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da mistura. Os campos retornados dependem do cabeçalho `Accept` enviado na solicitação. Experimente com cabeçalhos `Accept` diferentes para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

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
  "imsOrg": "{IMS_ORG}",
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

## Criar um mixin {#create}

Você pode definir um mixin personalizado no contêiner `tenant` fazendo uma solicitação de POST.

**Formato da API**

```http
POST /tenant/mixins
```

**Solicitação**

Ao definir um novo mixin, ele deve incluir um atributo `meta:intendedToExtend`, listando o `$id` das classes com as quais o mixin é compatível. Neste exemplo, o mixin é compatível com uma classe `Property` que foi definida anteriormente. Campos personalizados devem ser aninhados em `_{TENANT_ID}` (como mostrado no exemplo) para evitar colisões com campos semelhantes fornecidos por classes e outras combinações.

>[!NOTE]
>
>Para obter detalhes sobre como definir diferentes tipos de campo para incluir no seu mixin, consulte o [guia de restrições de campo](../schema/field-constraints.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga contendo os detalhes da mixin recém-criada, incluindo `$id`, `meta:altId` e `version`. Esses valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

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
  "imsOrg": "{IMS_ORG}",
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

Executar uma solicitação de GET para [listar todas as mixins](#list) no contêiner do locatário agora inclui o mixin Detalhes da propriedade ou você pode [executar uma solicitação de pesquisa (GET)](#lookup) usando o URI codificado por URL `$id` para exibir o novo mixin diretamente.

## Atualizar um mixin {#put}

Você pode substituir um mixin inteiro por uma operação de PUT, essencialmente regravando o recurso. Ao atualizar um mixin por meio de uma solicitação de PUT, o corpo deve incluir todos os campos que seriam necessários ao [criar um novo mixin](#create) em uma solicitação de POST.

>[!NOTE]
>
>Se quiser atualizar apenas parte de um mixin em vez de substituí-lo totalmente, consulte a seção sobre [atualizar uma parte de um mixin](#patch).

**Formato da API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MIXIN_ID}` | O `meta:altId` ou `$id` codificado por URL do mixin que você deseja regravar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir reescreve um mixin existente, adicionando um novo campo `propertyCountry`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Uma resposta bem-sucedida retorna os detalhes da mixin atualizada.

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
  "imsOrg": "{IMS_ORG}",
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

## Atualizar uma parte de uma mistura {#patch}

Você pode atualizar uma parte de um mixin usando uma solicitação de PATCH. O [!DNL Schema Registry] suporta todas as operações padrão de Patch JSON, incluindo `add`, `remove` e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [guia de fundamentos da API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de um mixin usando uma operação PUT](#put).

**Formato da API**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{MIXIN_ID}` | O URL codificado `$id` ou `meta:altId` do mixin que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação de exemplo abaixo atualiza o `description` de um mixin existente e adiciona um novo campo `propertyCity`.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica para um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`), e quais informações devem ser incluídas nessa operação (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

A resposta mostra que ambas as operações foram executadas com êxito. O `description` foi atualizado e `propertyCountry` foi adicionado em `definitions`.

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
  "imsOrg": "{IMS_ORG}",
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

## Excluir um mixin {#delete}

Por vezes, pode ser necessário remover uma mistura do Registro de Schema. Isso é feito executando uma solicitação DELETE com a ID de mixin fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MIXIN_ID}` | O URL codificado `$id` URI ou `meta:altId` do mixin que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de [pesquisa (GET)](#lookup) para o mixin. Você precisará incluir um cabeçalho `Accept` na solicitação, mas deverá receber um status HTTP 404 (Não encontrado), pois o mixin foi removido do Registro de Schema.
