---
keywords: Experience Platform, home, tópicos populares, schema, esquema, xdm, modelo de dados de experiência, namespace, namespaces, modo de compatibilidade, xed;
solution: Experience Platform
title: Namespacing no Experience Data Model (XDM)
topic-legacy: overviews
description: Saiba como o namespacing no Experience Data Model (XDM) permite estender seus esquemas e evitar colisões de campo, pois diferentes componentes do esquema são reunidos.
source-git-commit: b4c4f8f7e428d27f389bff5591a03925b6afa6d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Namespacing no Experience Data Model (XDM)

Todos os campos nos esquemas do Experience Data Model (XDM) têm um namespace associado. Esses namespaces permitem estender seus esquemas e evitar colisões de campo, pois diferentes componentes do schema são reunidos. Este documento fornece uma visão geral dos namespaces no
XDM e como eles são representados na [API do Registro de Schema](../api/overview.md).

O namespace permite definir um campo em um namespace, significando algo diferente do mesmo campo em um namespace diferente. Na prática, o namespace de um campo indica quem criou o campo (como XDM (Adobe) padrão, um fornecedor ou sua organização).

Por exemplo, considere um esquema XDM que usa o grupo de campos [[!UICONTROL Detalhes do Contato Pessoal]](../field-groups/profile/demographic-details.md), que tem um campo `mobilePhone` padrão que existe no namespace `xdm`. No mesmo schema, você também pode criar um campo `mobilePhone` separado em um namespace diferente (seu [ID do locatário](../api/getting-started.md#know-your-tenant_id)). Ambos os campos podem coexistir enquanto têm significados ou restrições subjacentes diferentes.

## Sintaxe de namespacing

As seções a seguir demonstram como os namespaces são atribuídos na sintaxe XDM.

### XDM padrão {#standard}

A sintaxe XDM padrão fornece informações sobre como os namespaces são representados em schemas (incluindo [como são traduzidos em Adobe Experience Platform](#compatibility)).

O XDM padrão usa a sintaxe [JSON-LD](https://json-ld.org/) para atribuir namespaces a campos. Este namespace vem na forma de um URI (como `https://ns.adobe.com/xdm` para o namespace `xdm`) ou como um prefixo abreviado configurado no atributo `@context` de um schema.

Este é um exemplo de esquema para um produto na sintaxe XDM padrão. Com exceção de `@id` (o identificador exclusivo, conforme definido pela especificação JSON-LD), cada campo em `properties` começa com um namespace e termina com o nome do campo. Se estiver usando um prefixo abreviado definido em `@context`, o namespace e o nome do campo serão separados por dois pontos (`:`). Se não estiver usando um prefixo, o namespace e o nome do campo serão separados por uma barra (`/`).

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
| `@id` | Um identificador exclusivo para o registro, conforme definido pela [especificação JSON-LD](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | Um exemplo de campo que usa um prefixo abreviado para indicar um namespace. Nesse caso, `xdm` é o namespace (`https://ns.adobe.com/xdm`) e `sku` é o nome do campo. |
| `https://ns.adobe.com/xdm/channels/application` | Um exemplo de um campo que usa o URI completo do namespace. Nesse caso, `https://ns.adobe.com/xdm/channels` é o namespace e `application` é o nome do campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Os campos fornecidos pelos recursos do fornecedor usam seus próprios namespaces exclusivos. Neste exemplo, `https://ns.adobe.com/vendorA/product` é o namespace do fornecedor e `stockNumber` é o nome do campo. |
| `tenantId:internalSku` | Os campos definidos pela organização usam a ID de locatário exclusiva como namespace. Neste exemplo, `tenantId` é o namespace do locatário (`https://ns.adobe.com/tenantId`) e `internalSku` é o nome do campo. |

{style=&quot;table-layout:auto&quot;}

### Modo de compatibilidade {#compatibility}

No Adobe Experience Platform, os esquemas XDM são representados na sintaxe [Modo de Compatibilidade](../api/appendix.md#compatibility), que não usa a sintaxe JSON-LD para representar namespaces. Em vez disso, a Platform converte o namespace em um campo pai (começando com um sublinhado) e aninha os campos sob ele.

Por exemplo, o XDM padrão `repo:createdDate` é convertido em `_repo.createdDate` e apareceria sob a seguinte estrutura no Modo de compatibilidade:

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

Os campos que usam o namespace `xdm` aparecem como campos raiz em `properties` e soltam o prefixo `xdm:` que apareceria em [sintaxe XDM padrão](#standard). Por exemplo, `xdm:sku` é simplesmente listado como `sku`.

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

Este guia forneceu uma visão geral dos namespaces XDM e como eles são representados no JSON. Para obter mais informações sobre como configurar esquemas XDM usando a API, consulte o [Guia da API do Registro de Schema](../api/overview.md).
