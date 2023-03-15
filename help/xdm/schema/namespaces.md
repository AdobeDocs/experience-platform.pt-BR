---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;xdm;modelo de dados de experiência;namespace;namespaces;modo de compatibilidade;xed;
solution: Experience Platform
title: Namespace no Experience Data Model (XDM)
description: Saiba como o namespace no Experience Data Model (XDM) permite estender seus esquemas e evitar colisões de campo enquanto diferentes componentes do esquema são trazidos juntos.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Namespace no Experience Data Model (XDM)

Todos os campos nos esquemas do Experience Data Model (XDM) têm um namespace associado. Esses namespaces permitem estender seus esquemas e evitar colisões de campo à medida que diferentes componentes de esquema são reunidos. Este documento fornece uma visão geral dos namespaces no XDM e como eles são representados na variável [API do registro de esquema](../api/overview.md).

O namespace permite definir um campo em um namespace como significando algo diferente do mesmo campo em um namespace diferente. Na prática, o namespace de um campo indica quem criou o campo (como o XDM padrão (Adobe), um fornecedor ou sua organização).

Por exemplo, considere um esquema XDM que usa o [[!UICONTROL Detalhes de contato pessoal] grupo de campos](../field-groups/profile/demographic-details.md), que tem um padrão `mobilePhone` campo que existe na variável `xdm` namespace. No mesmo esquema, você também pode criar uma `mobilePhone` em um namespace diferente (seu [ID do inquilino](../api/getting-started.md#know-your-tenant_id)). Ambos os campos podem coexistir enquanto têm diferentes significados ou restrições subjacentes.

## Sintaxe de namespace

As seções a seguir demonstram como os namespaces são atribuídos na sintaxe XDM.

### XDM padrão {#standard}

A sintaxe XDM padrão fornece informações sobre como os namespaces são representados em esquemas (incluindo [como são traduzidos no Adobe Experience Platform](#compatibility)).

Usos padrão do XDM [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) sintaxe para atribuir namespaces a campos. Esse namespace vem na forma de um URI (como `https://ns.adobe.com/xdm` para o `xdm` ou como um prefixo abreviado que é configurado na variável `@context` atributo de um esquema.

Veja a seguir um exemplo de esquema para um produto na sintaxe XDM padrão. Com exceção da `@id` (o identificador exclusivo conforme definido pela especificação JSON-LD), cada campo em `properties` começa com um namespace e termina com o nome do campo. Se estiver usando um prefixo abreviado definido em `@context`, o namespace e o nome do campo são separados por dois pontos (`:`). Se não estiver usando um prefixo, o namespace e o nome do campo serão separados por uma barra (`/`).

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `@context` | Um objeto que define os prefixos abreviados que podem ser usados em vez de um URI de namespace completo em `properties`. |
| `@id` | Um identificador exclusivo do registro, conforme definido pelo [Especificação JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Um exemplo de um campo que usa um prefixo abreviado para denotar um namespace. Nesse caso, `xdm` é o namespace (`https://ns.adobe.com/xdm`) e `sku` é o nome do campo. |
| `https://ns.adobe.com/xdm/channels/application` | Um exemplo de um campo que usa o URI de namespace completo. Nesse caso, `https://ns.adobe.com/xdm/channels` é o namespace e `application` é o nome do campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Os campos fornecidos pelos recursos do fornecedor usam seus próprios namespaces exclusivos. Neste exemplo, `https://ns.adobe.com/vendorA/product` é o namespace do fornecedor e `stockNumber` é o nome do campo. |
| `tenantId:internalSku` | Os campos definidos pela organização usam a ID de locatário exclusiva como namespace. Neste exemplo, `tenantId` é o namespace do locatário (`https://ns.adobe.com/tenantId`) e `internalSku` é o nome do campo. |

{style="table-layout:auto"}

### Modo de compatibilidade {#compatibility}

No Adobe Experience Platform, os esquemas XDM são representados em [Modo de compatibilidade](../api/appendix.md#compatibility) sintaxe, que não usa a sintaxe JSON-LD para representar namespaces. Em vez disso, o Platform converte o namespace em um campo principal (começando com um sublinhado) e aninha os campos sob ele.

Por exemplo, o padrão XDM `repo:createdDate` é convertido em `_repo.createdDate` e apareceriam sob a seguinte estrutura no Modo de compatibilidade:

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Campos que usam a variável `xdm` O namespace aparece como campos raiz em `properties` e solte a `xdm:` prefixo que apareceria em [sintaxe XDM padrão](#standard). Por exemplo, `xdm:sku` é simplesmente listado como `sku` em vez disso.

O JSON a seguir representa como o exemplo de sintaxe XDM padrão mostrado acima é traduzido para o Modo de compatibilidade.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Próximas etapas

Este guia forneceu uma visão geral dos namespaces XDM e como eles são representados no JSON. Para obter mais informações sobre como configurar esquemas XDM usando a API, consulte a [Guia da API do registro de esquema](../api/overview.md).
