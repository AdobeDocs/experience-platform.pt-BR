---
title: Pesquisar endpoint
description: Saiba como fazer chamadas para o endpoint /search na API do Reactor.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 97%

---

# Pesquisar endpoint

O endpoint `/search` na API do Reactor fornece uma maneira de encontrar recursos que correspondem aos critérios desejados, por meio de uma consulta.

Os seguintes tipos de recursos de API podem ser pesquisados, utilizando a mesma estrutura de dados que os documentos baseados em recursos retornados pela API:

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

Todas as consultas têm como escopo sua empresa atual e as propriedades acessíveis.

>[!IMPORTANT]
>
>A funcionalidade de pesquisa tem as seguintes ressalvas e exceções:
>* meta não é pesquisável nem é retornado nos resultados de pesquisa.
>* Os campos de esquema para delegados de pacote de extensão (ações, condições etc.) são pesquisáveis como texto, não como uma estrutura de dados aninhada.
>* Atualmente, as consultas de intervalo só aceitam números inteiros.


Para obter informações mais detalhadas sobre como usar essa funcionalidade, consulte o [manual de pesquisa](../guides/search.md).

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte o [Guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação na API.

## Executar uma pesquisa {#perform}

Você pode realizar uma pesquisa fazendo uma solicitação de POST.

**Formato da API**

```http
POST /search
```

**Solicitação**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `from` | O número de resultados para compensar a resposta. |
| `size` | A quantidade máxima de resultados a serem retornados. Os resultados não podem exceder 100 itens. |
| `query` | Um objeto que representa uma consulta de pesquisa. Para cada propriedade nesse objeto, a chave deve representar um caminho de campo para consulta e o valor deve ser um objeto cujas subpropriedades determinem o que consultar.<br><br>Para cada caminho de campo, é possível usar as seguintes subpropriedades:<ul><li>`exists`: retornará true se o campo existir no recurso.</li><li>`value`: retornará true se o valor do campo corresponder ao valor dessa propriedade.</li><li>`value_operator`: lógica booliana usada para determinar como uma consulta de `value` deve ser tratada. Os valores permitidos são `AND` e `OR`. Quando excluída, a lógica `AND` é presumida. Consulte a seção sobre [lógica do operador value](#value-operator) para obter mais informações.</li><li>`range` Retornará true se o valor do campo estiver em um intervalo numérico específico. O intervalo em si é determinado pelas seguintes subpropriedades:<ul><li>`gt`: Maior que o valor fornecido, não inclusivo.</li><li>`gte`: Maior que ou igual ao valor fornecido.</li><li>`lt`: Menor que o valor fornecido, não inclusivo.</li><li>`lte`: Menor que ou igual ao valor fornecido.</li></ul></li></ul> |
| `sort` | Uma matriz de objetos, indicando a ordem na qual classificar os resultados. Cada objeto deve conter uma única propriedade: a chave representa o caminho do campo de acordo com o qual classificar, e o valor representa a ordem de classificação (`asc` para crescente, `desc` para decrescente). |
| `resource_types` | Uma matriz de sequências de caracteres, indicando os tipos de recurso específicos a serem pesquisados. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna uma lista de recursos correspondentes para a consulta. Para obter detalhes sobre como a API determina correspondências para valores específicos, consulte a seção do apêndice sobre [convenções correspondentes](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Apêndice

A seção a seguir contém informações adicionais sobre o uso do endpoint `/search`.

### Lógica do operador de valor {#value-operator}

Os valores de consulta de pesquisa são divididos em termos para corresponder a documentos indexados. Entre cada termo, uma relação `AND` é feita.

Quando você usa `AND` como o `value_operator`, um valor de consulta de `My Rule Holiday Sale` é interpretado como documentos com um campo que contém `My AND Rule AND Holiday AND Sale`.

Quando você usa `OR` como o `value_operator`, um valor de consulta de `My Rule Holiday Sale` é interpretado como documentos com um campo que contém `My OR Rule OR Holiday OR Sale`. Quanto mais termos corresponderem, maior será o `match_score`. Devido à natureza da correspondência de termos parciais, quando nada corresponde ao valor desejado, é possível obter um conjunto de resultados no qual o valor é correspondido somente em um nível muito básico, como alguns caracteres de texto.

### Convenções de correspondência {#conventions}

A pesquisa se destina a esclarecer o grau de relevância de um documento para uma consulta fornecida. A forma como os dados do documento são analisados e indexados afeta diretamente isso.

A tabela a seguir detalha as convenções de correspondência para tipos de campos comuns:

| Tipo de campo | Convenções de correspondência |
| --- | --- |
| Strings | Texto com uma análise de termo parcial, não diferencia maiúsculas de minúsculas |
| Valores de enumeração | Correspondência exata, diferencia maiúsculas de minúsculas |
| Inteiros | Correspondência exata |
| Flutuantes | Correspondência exata |
| Carimbos de data e hora | Correspondência exata (formato DateTime) |
| Nomes de exibição | Texto com uma análise de termo parcial, não diferencia maiúsculas de minúsculas |

Há convenções adicionais para campos específicos que aparecem na API:

| Campo | Convenções de correspondência |
| --- | --- |
| `id` | Correspondência exata, diferencia maiúsculas de minúsculas |
| `delegate_descriptor_id` | Correspondência exata. Diferencia maiúsculas de minúsculas, com termos divididos em `::` |
| `name` | Correspondência exata, diferencia maiúsculas de minúsculas |
| `settings` | Texto com uma análise de termo parcial, não diferencia maiúsculas de minúsculas |
| `type` | Correspondência exata, diferencia maiúsculas de minúsculas |
