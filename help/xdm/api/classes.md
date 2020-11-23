---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: Criar uma classe
description: O endpoint /classes na API do Registro de Schemas permite que você gerencie programaticamente as classes XDM no aplicativo da experiência.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---


# Ponto de extremidade de classes

Todos os schemas do Modelo de Dados de Experiência (XDM) devem se basear em uma classe. Uma classe determina a estrutura básica das propriedades comuns que todos os schemas baseados nessa classe devem conter, bem como quais combinações são elegíveis para uso nesses schemas. Além disso, uma classe de schemas determina os aspectos comportamentais dos dados que um schema conterá, dos quais existem dois tipos:

* **[!UICONTROL Registro]**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **[!UICONTROL Séries]** cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

>[!NOTE]
>
>Para obter mais informações sobre os comportamentos de dados em termos de como eles afetam a composição do schema, consulte os [fundamentos da composição](../schema/composition.md)do schema.

O `/classes` endpoint na [!DNL Schema Registry] API permite gerenciar programaticamente as classes no aplicativo de experiência.

## Introdução

O endpoint usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de classes {#list}

Você pode lista todas as classes sob o `global` container ou `tenant` realizando uma solicitação de GET para `/global/classes` ou `/tenant/classes`, respectivamente.

>[!NOTE]
>
>Ao listar recursos, o resultado do Limite do Registro do Schema é definido como 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros de paginação. Também é recomendável usar parâmetros de query adicionais para filtrar resultados e reduzir o número de recursos retornados. Consulte a seção sobre parâmetros [do](./appendix.md#query) query no documento apêndice para obter mais informações.

**Formato da API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container do qual você deseja recuperar as classes: `global` para classes criadas por Adobe ou `tenant` para classes pertencentes à sua organização. |
| `{QUERY_PARAMS}` | Parâmetros de query opcionais para filtrar os resultados. Consulte o documento [de](./appendix.md#query) apêndice para obter uma lista dos parâmetros disponíveis. |

**Solicitação**

A solicitação a seguir recupera uma lista de classes do `tenant` container, usando um parâmetro de `orderby` query para classificar as classes pelo `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Os seguintes `Accept` cabeçalhos estão disponíveis para listar classes:

| `Accept` header | Descrição |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para a listagem de recursos. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Retorna a classe JSON completa para cada recurso, com original `$ref` e `allOf` incluído. (Limite: 300) |

**Resposta**

A solicitação acima usou o `application/vnd.adobe.xed-id+json` cabeçalho, portanto a resposta inclui apenas os atributos `Accept` , `title`, `$id`e `meta:altId``version` de cada classe. Usar o outro `Accept` cabeçalho (`application/vnd.adobe.xed+json`) retorna todos os atributos de cada classe. Selecione o `Accept` cabeçalho apropriado, dependendo das informações necessárias na sua resposta.

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

## Procure uma classe {#lookup}

Você pode pesquisar uma classe específica incluindo a ID da classe no caminho de uma solicitação de GET.

**Formato da API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container que hospeda a classe que você deseja recuperar: `global` para uma classe criada por Adobe ou `tenant` para uma classe pertencente à sua organização. |
| `{CLASS_ID}` | A `meta:altId` classe ou `$id` a classe codificada por URL que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera uma classe de acordo com seu `meta:altId` valor fornecido no caminho.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

Uma resposta bem-sucedida retorna os detalhes da classe. Os campos retornados dependem do `Accept` cabeçalho enviado na solicitação. Experimente com `Accept` cabeçalhos diferentes para comparar as respostas e determinar qual cabeçalho é melhor para seu caso de uso.

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

Você pode definir uma classe personalizada sob o `tenant` container, fazendo uma solicitação de POST.

>[!IMPORTANT]
>
>Ao compor um schema com base em uma classe personalizada que você define, você não poderá usar misturas padrão. Cada mixin define as classes com as quais são compatíveis em seus `meta:intendedToExtend` atributos. Depois de começar a definir misturas compatíveis com sua nova classe (usando o `$id` da nova classe no `meta:intendedToExtend` campo da mistura), você poderá reutilizar essas misturas toda vez que definir um schema que implemente a classe definida. Consulte as seções sobre a [criação de mixins](./mixins.md#create) e a [criação de schemas](./schemas.md#create) nos respectivos guias de endpoint para obter mais informações.
>
>Se você estiver planejando usar schemas com base em classes personalizadas no Perfil do cliente em tempo real, também é importante ter em mente que os schemas de união só são construídos com base em schemas que compartilham a mesma classe. Se você quiser incluir um schema de classe personalizada na união para outra classe, como o Perfil [!UICONTROL individual] XDM ou o [!UICONTROL XDM ExperienceEvent], é necessário estabelecer uma relação com outro schema que emprega essa classe. Consulte o tutorial sobre como [estabelecer uma relação entre dois schemas na API](../tutorials/relationship-api.md) para obter mais informações.

**Formato da API**

```http
POST /tenant/classes
```

**Solicitação**

A solicitação para criar (POST) uma classe deve incluir um `allOf` atributo que contenha um `$ref` para um de dois valores: `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Esses valores representam o comportamento no qual a classe se baseia (registro ou série de tempo, respectivamente). Para obter mais informações sobre as diferenças entre os dados de registro e os dados de série de tempo, consulte a seção sobre tipos de comportamento dentro dos [fundamentos da composição](../schema/composition.md)do schema.

Ao definir uma classe, você também pode incluir combinações ou campos personalizados na definição da classe. Isso faria com que as combinações e os campos adicionados fossem incluídos em todos os schemas que implementam a classe. A solicitação de exemplo a seguir define uma classe chamada &quot;Propriedade&quot;, que captura informações relacionadas a diferentes propriedades pertencentes e operadas por uma empresa. Inclui um `propertyId` campo a ser incluído toda vez que a classe é usada.

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
| `_{TENANT_ID}` | A `TENANT_ID` namespace de sua organização. Todos os recursos criados pela sua organização devem incluir essa propriedade para evitar colisões com outros recursos no [!DNL Schema Registry]. |
| `allOf` | Uma lista de recursos cujas propriedades devem ser herdadas pela nova classe. Um dos `$ref` objetos dentro da matriz define o comportamento da classe. Neste exemplo, a classe herda o comportamento &quot;record&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga que contém os detalhes da classe recém-criada, incluindo `$id`, `meta:altId`e `version`. Esses três valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

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

Executar uma solicitação de GET para [lista de todas as classes](#list) no `tenant` container agora inclui a classe Property. Você também pode [executar uma solicitação](#lookup) de pesquisa (GET) usando o URL codificado `$id` para visualização da nova classe diretamente.

## Atualizar uma classe {#put}

Você pode substituir uma classe inteira por uma operação PUT, essencialmente regravando o recurso. Ao atualizar uma classe por meio de uma solicitação de PUT, o corpo deve incluir todos os campos que seriam necessários ao [criar uma nova classe](#create) em uma solicitação de POST.

>[!NOTE]
>
>Se você quiser apenas atualizar parte de uma classe em vez de substituí-la totalmente, consulte a seção sobre como [atualizar uma parte de uma classe](#patch).

**Formato da API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | A `meta:altId` ou a codificação de URL `$id` da classe que você deseja reescrever. |

**Solicitação**

A solicitação a seguir regrava uma classe existente novamente, alterando sua `description` e a `title` de um de seus campos.

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

Você pode atualizar uma parte de uma classe usando uma solicitação de PATCH. O [!DNL Schema Registry] suporta todas as operações padrão de Patch JSON, incluindo `add`, `remove`e `replace`. Para obter mais informações sobre o Patch JSON, consulte o guia [de fundamentos da](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>Se quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte a seção sobre [substituição de uma classe usando uma operação](#put)de PUT.

**Formato da API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O `$id` URI codificado por URL ou `meta:altId` da classe que você deseja atualizar. |

**Solicitação**

A solicitação de exemplo abaixo atualiza o número `description` de uma classe existente e o número `title` de um de seus campos.

O corpo da solicitação assume a forma de uma matriz, com cada objeto listado representando uma alteração específica para um campo individual. Cada objeto inclui a operação a ser executada (`op`), em qual campo a operação deve ser executada (`path`) e quais informações devem ser incluídas nessa operação (`value`).

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

A resposta mostra que ambas as operações foram executadas com êxito. O `description` foi atualizado, junto com o `title` do `propertyId` campo.

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

Ocasionalmente, pode ser necessário remover uma classe do Registro do Schema. Isso é feito executando-se uma solicitação de DELETE com a ID de classe fornecida no caminho.

**Formato da API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CLASS_ID}` | O `$id` URI codificado por URL ou `meta:altId` da classe que você deseja excluir. |

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

Você pode confirmar a exclusão tentando uma solicitação [de](#lookup) pesquisa (GET) para a classe. Você precisará incluir um `Accept` cabeçalho na solicitação, mas deverá receber um status HTTP 404 (Não encontrado), pois a classe foi removida do Registro do Schema.