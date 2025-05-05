---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;xdm;modelo de dados de experiência;namespace;namespaces;modo de compatibilidade;xed;
solution: Experience Platform
title: Namespace no Experience Data Model (XDM)
description: Saiba como o namespace no Experience Data Model (XDM) permite estender seus esquemas e evitar colisões de campo enquanto diferentes componentes do esquema são trazidos juntos.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Namespace no Experience Data Model (XDM)

>[!IMPORTANT]
>
>No XDM, o namespace (o tópico desta página) é usado para distinguir campos em um esquema. Isso é diferente do conceito de namespace de identidade no Serviço de identidade, em que o namespace é usado para distinguir valores de identidade. Leia a documentação sobre [namespace no Serviço de Identidade](../../identity-service/features/namespaces.md) para obter mais informações.

Todos os campos nos esquemas do Experience Data Model (XDM) têm um namespace associado. Esses namespaces permitem estender seus esquemas e evitar colisões de campo à medida que diferentes componentes de esquema são reunidos. Este documento fornece uma visão geral dos namespaces no XDM e como eles são representados na [API do Registro de Esquema](../api/overview.md).

O namespace permite definir um campo em um namespace como significando algo diferente do mesmo campo em um namespace diferente. Na prática, o namespace de um campo indica quem criou o campo (como o XDM padrão (Adobe), um fornecedor ou sua organização).

Por exemplo, considere um esquema XDM que usa o [[[!UICONTROL grupo de campos &#x200B;]](../field-groups/profile/demographic-details.md) de Detalhes de Contato Pessoal], que tem um campo `mobilePhone` padrão que existe no namespace `xdm`. No mesmo esquema, você também pode criar um campo `mobilePhone` separado em um namespace diferente (sua [ID de locatário](../api/getting-started.md#know-your-tenant_id)). Ambos os campos podem coexistir enquanto têm diferentes significados ou restrições subjacentes.

## Sintaxe de namespace

As seções a seguir demonstram como os namespaces são atribuídos na sintaxe XDM.

### XDM padrão {#standard}

A sintaxe XDM padrão fornece à insight como os namespaces são representados nos esquemas (incluindo [como são traduzidos no Adobe Experience Platform](#compatibility)).

O XDM padrão usa a sintaxe [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) para atribuir namespaces a campos. Este namespace vem na forma de um URI (como `https://ns.adobe.com/xdm` para o namespace `xdm`) ou como um prefixo abreviado que é configurado no atributo `@context` de um esquema.

Veja a seguir um exemplo de esquema para um produto na sintaxe XDM padrão. Com exceção de `@id` (o identificador exclusivo conforme definido pela especificação JSON-LD), cada campo em `properties` começa com um namespace e termina com o nome do campo. Se estiver usando um prefixo abreviado definido em `@context`, o namespace e o nome do campo serão separados por dois-pontos (`:`). Se não estiver usando um prefixo, o namespace e o nome do campo serão separados por uma barra (`/`).

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
| `@id` | Um identificador exclusivo para o registro conforme definido pela [especificação JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Um exemplo de um campo que usa um prefixo abreviado para denotar um namespace. Nesse caso, `xdm` é o namespace (`https://ns.adobe.com/xdm`) e `sku` é o nome do campo. |
| `https://ns.adobe.com/xdm/channels/application` | Um exemplo de um campo que usa o URI de namespace completo. Nesse caso, `https://ns.adobe.com/xdm/channels` é o namespace e `application` é o nome do campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Os campos fornecidos pelos recursos do fornecedor usam seus próprios namespaces exclusivos. Neste exemplo, `https://ns.adobe.com/vendorA/product` é o namespace do fornecedor e `stockNumber` é o nome do campo. |
| `tenantId:internalSku` | Os campos definidos pela organização usam a ID de locatário exclusiva como namespace. Neste exemplo, `tenantId` é o namespace do locatário (`https://ns.adobe.com/tenantId`) e `internalSku` é o nome do campo. |

{style="table-layout:auto"}

### Modo de compatibilidade {#compatibility}

No Adobe Experience Platform, os esquemas XDM são representados na sintaxe [Modo de Compatibilidade](../api/appendix.md#compatibility), que não usa a sintaxe JSON-LD para representar namespaces. Em vez disso, o Experience Platform converte o namespace em um campo pai (começando com um sublinhado) e aninha os campos sob ele.

Por exemplo, o XDM padrão `repo:createdDate` é convertido em `_repo.createdDate` e aparece na seguinte estrutura no Modo de Compatibilidade:

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

Os campos que usam o namespace `xdm` aparecem como campos raiz em `properties` e removem o prefixo `xdm:` que apareceria na [sintaxe XDM padrão](#standard). Por exemplo, `xdm:sku` está simplesmente listado como `sku`.

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

Este guia forneceu uma visão geral dos namespaces XDM e como eles são representados no JSON. Para obter mais informações sobre como configurar esquemas XDM usando a API, consulte o [Guia da API do Registro de Esquemas](../api/overview.md).
