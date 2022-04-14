---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro de classe, Registro de esquema, classe, classe, classes, classes, criar
solution: Experience Platform
title: Endpoint da API de classes
description: O endpoint /classes na API do Registro de Schema permite gerenciar programaticamente as classes XDM no aplicativo de experiência.
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 74ef1b3abb90ab3ca24690c88c073083f02a2f1b
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 4%

---

# Ponto de extremidade de classes

Todos os esquemas do Experience Data Model (XDM) devem ser baseados em uma classe. Uma classe determina a estrutura base das propriedades comuns que todos os schemas baseados nessa classe devem conter, bem como quais grupos de campos de schema estão qualificados para uso nesses schemas. Além disso, a classe de um schema determina os aspectos comportamentais dos dados que um schema conterá, dos quais há dois tipos:

* **[!UICONTROL Registro]**: Fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.
* **[!UICONTROL Série cronológica]**: Fornece um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de registro.

>[!NOTE]
>
>Para obter mais informações sobre classes de comportamentos de dados em termos de como eles afetam a composição do schema, consulte [noções básicas da composição do schema](../schema/composition.md).

O `/classes` endpoint no [!DNL Schema Registry] A API permite gerenciar classes programaticamente no aplicativo de experiência.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de classes {#list}

Você pode listar todas as classes na variável `global` ou `tenant` ao fazer uma solicitação do GET para `/global/classes` ou `/tenant/classes`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o resultado dos limites do Registro de Esquema é definido como 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de consulta adicionais para filtrar resultados e reduzir o número de recursos retornados. Consulte a seção sobre [parâmetros de consulta](./appendix.md#query) no documento em anexo para mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner do qual você deseja recuperar classes: `global` para classes criadas por Adobe ou `tenant` para classes pertencentes à sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte a [documento de apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera uma lista de classes do `tenant` contêiner, usando um `orderby` parâmetro de consulta para classificar as classes por seus `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. O seguinte `Accept` os cabeçalhos estão disponíveis para listar classes:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para listar recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna a classe JSON completa para cada recurso, com o original `$ref` e `allOf` incluído. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Resposta**

A solicitação acima usou o `application/vnd.adobe.xed-id+json` `Accept` , portanto, a resposta inclui somente o cabeçalho `title`, `$id`, `meta:altId`e `version` atributos para cada classe. Usar a outra `Accept` header (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada classe. Selecione o `Accept` dependendo das informações necessárias na resposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Pesquisar uma classe {#lookup}

Você pode pesquisar uma classe específica incluindo a ID da classe no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O contêiner que contém a classe que você deseja recuperar: `global` para uma classe criada por Adobe ou `tenant` para uma classe pertencente à sua organização. |
| `{CLASS_ID}` | O `meta:altId` ou codificado por URL `$id` da classe que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera uma classe por seu `meta:altId` valor fornecido no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da classe . Os campos retornados dependem do `Accept` cabeçalho enviado na solicitação. Experimentar com diferentes `Accept` cabeçalhos para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Criar uma classe {#create}

Você pode definir uma classe personalizada sob a variável `tenant` fazendo uma solicitação de POST.

>[!IMPORTANT]
>
>Ao compor um schema baseado em uma classe personalizada que você define, você não poderá usar grupos de campos padrão. Cada grupo de campos define as classes com as quais são compatíveis em suas `meta:intendedToExtend` atributo. Depois de começar a definir grupos de campos compatíveis com sua nova classe (usando o `$id` da nova classe na `meta:intendedToExtend` do grupo de campos), você poderá reutilizar esses grupos de campos toda vez que definir um esquema que implemente a classe que você definiu. Veja as seções em [criação de grupos de campos](./field-groups.md#create) e [criação de schemas](./schemas.md#create) nos respectivos guias de endpoint para obter mais informações.
>
>Se você estiver planejando usar esquemas com base em classes personalizadas no Perfil do cliente em tempo real, também é importante ter em mente que os esquemas de união só são construídos com base em esquemas que compartilham a mesma classe. Se desejar incluir um schema de classe personalizada na união para outra classe como [!UICONTROL Perfil individual XDM] ou [!UICONTROL ExperiênciaEvento XDM], você deve estabelecer uma relação com outro schema que emprega essa classe. Veja o tutorial em [estabelecer uma relação entre dois schemas na API](../tutorials/relationship-api.md) para obter mais informações.

**Formato da API**

```http
POST /tenant/classes
```

**Solicitação**

A solicitação para criar (POST) uma classe deve incluir um `allOf` atributo contendo um `$ref` para um de dois valores: `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Esses valores representam o comportamento no qual a classe se baseia (registro ou série de tempo, respectivamente). Para obter mais informações sobre as diferenças entre dados de registro e dados de série de tempo, consulte a seção sobre tipos de comportamento na [noções básicas da composição do schema](../schema/composition.md).

Ao definir uma classe, você também pode incluir grupos de campos ou campos personalizados dentro da definição de classe. Isso faria com que os grupos e campos de campo adicionados fossem incluídos em todos os esquemas que implementassem a classe. A solicitação de exemplo a seguir define uma classe chamada &quot;Propriedade&quot;, que captura informações sobre diferentes propriedades pertencentes e operadas por uma empresa. Ele inclui um `propertyId` campo a ser incluído sempre que a classe for usada.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `_{TENANT_ID}` | O `TENANT_ID` namespace para sua organização. Todos os recursos criados pela organização devem incluir essa propriedade para evitar colisões com outros recursos na [!DNL Schema Registry]. |
| `allOf` | Uma lista de recursos cujas propriedades devem ser herdadas pela nova classe. Um dos `$ref` objetos na matriz define o comportamento da classe. Neste exemplo, a classe herda o comportamento &quot;record&quot;. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga contendo os detalhes da classe recém-criada, incluindo o `$id`, `meta:altId`e `version`. Esses três valores são somente leitura e são atribuídos pela variável [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

Executar uma solicitação GET para [listar todas as classes](#list) no `tenant` agora, o contêiner incluiria a classe Propriedade. Você também pode [executar uma solicitação de pesquisa (GET)](#lookup) usando o URL codificado `$id` para exibir a nova classe diretamente.

## Atualizar uma classe {#put}

Você pode substituir uma classe inteira por meio de uma operação PUT, essencialmente regravando o recurso. Ao atualizar uma classe por meio de uma solicitação de PUT, o corpo deve incluir todos os campos que seriam necessários quando [criação de uma nova classe](#create) em uma solicitação de POST.

>[!NOTE]
>
>Se quiser atualizar apenas parte de uma classe em vez de substituí-la totalmente, consulte a seção em [atualização de uma parte de uma classe](#patch).

**Formato da API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O `meta:altId` ou codificado por URL `$id` da classe que você deseja reescrever. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir reescreve uma classe existente, alterando sua `description` e `title` de um de seus campos.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da classe atualizada.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Atualizar uma parte de uma classe {#patch}

Você pode atualizar uma parte de uma classe usando uma solicitação de PATCH. O [!DNL Schema Registry] suporta todas as operações padrão de patch JSON, incluindo `add`, `remove`e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [Guia de fundamentos da API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de uma classe usando uma operação PUT](#put).

**Formato da API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O URL codificado `$id` URI ou `meta:altId` da classe que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação de exemplo abaixo atualiza o `description` de uma classe existente, e `title` de um de seus campos.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica para um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`) e que informações devem ser incluídas nessa operação (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Resposta**

A resposta mostra que ambas as operações foram executadas com êxito. O `description` O foi atualizado, juntamente com a variável `title` do `propertyId` campo.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Excluir uma classe {#delete}

Ocasionalmente, pode ser necessário remover uma classe do Registro de Schema. Isso é feito executando-se uma solicitação de DELETE com a ID de classe fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O URL codificado `$id` URI ou `meta:altId` da classe que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

É possível confirmar a exclusão tentando uma [solicitação de pesquisa (GET)](#lookup) para a classe . Você precisará incluir um `Accept` na solicitação, mas deve receber um status HTTP 404 (Not Found) porque a classe foi removida do Registro de Schema.
