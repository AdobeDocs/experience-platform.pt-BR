---
title: Ponto de extremidade de elementos de dados
description: Saiba como fazer chamadas para o endpoint /data_elements na API do Reator.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 6%

---

# Ponto de extremidade de elementos de dados

Um elemento de dados funciona como uma variável que aponta para um dado importante em seu aplicativo. Os elementos de dados são usados nas configurações [rules](./rules.md) e [extension](./extensions.md). Quando uma regra é acionada no tempo de execução em um navegador ou aplicativo, o valor do elemento de dados é resolvido e usado na regra. Os elementos de dados funcionam da mesma forma para configurações de extensão.

O uso de vários elementos de dados juntos resulta em um dicionário de dados ou mapa de dados. Este dicionário representa os dados que a Adobe Experience Platform conhece e que podem usar.

Um elemento de dados pertence a exatamente um [propriedade](./properties.md). Uma propriedade pode ter muitos elementos de dados.

Para obter informações mais gerais sobre elementos de dados e seu uso em tags, consulte o [guia de elementos de dados](../../ui/managing-resources/data-elements.md) na documentação da interface do usuário.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Recuperar uma lista de elementos de dados {#list}

Você pode recuperar uma lista de elementos de dados para uma propriedade, incluindo a ID da propriedade no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /properties/{PROPERTY_ID}/data_elements
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da propriedade que possui os elementos de dados. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, elementos de dados listados podem ser filtrados com base nos seguintes atributos:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Consulte o guia sobre [respostas de filtragem](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de elementos de dados para a propriedade especificada.

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
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
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
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Pesquisar um elemento de dados {#lookup}

Você pode pesquisar um elemento de dados fornecendo sua ID no caminho de uma solicitação do GET.

>[!NOTE]
>
>Quando os elementos de dados são excluídos, eles são marcados como excluídos, mas não são realmente removidos do sistema. Portanto, é possível procurar um elemento de dados excluído. Os elementos de dados excluídos podem ser identificados pela presença de um atributo `data.meta.deleted_at`.

**Formato da API**

```http
GET /data_elements/{DATA_ELEMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `DATA_ELEMENT_ID` | O `id` do elemento de dados que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do elemento de dados.

```json
{
  "data": {
    "id": "DE8097636264104451ac3a18c95d5ff833",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:35:54.956Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:35:54 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:35:54.956Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/property"
        },
        "data": {
          "id": "PRa5621686159f44c880557e12af412a95",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/origin"
        },
        "data": {
          "id": "DE8097636264104451ac3a18c95d5ff833",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/extension"
        },
        "data": {
          "id": "EX085a465793b54be39b5408d13b50b46e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension"
        },
        "data": {
          "id": "EXf9a32699efde42e9b9410b43bd660848",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa5621686159f44c880557e12af412a95",
      "origin": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "self": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "extension": "https://reactor.adobe.io/extensions/EX085a465793b54be39b5408d13b50b46e"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Criar um elemento de dados {#create}

Você pode criar um novo elemento de dados fazendo uma solicitação de POST.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/data_elements
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da [propriedade](./properties.md) em que você está definindo o elemento de dados. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria um novo elemento de dados para a propriedade especificada. A chamada também associa o elemento de dados a uma extensão existente por meio da propriedade `relationships` . Consulte o guia sobre [relações](../guides/relationships.md) para obter mais informações.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Data Element 2020-12-14 17:33:21 +0000",
            "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
            "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}",
            "default_value": "general_label",
            "enabled": true,
            "force_lower_case": true,
            "clean_text": true,
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
                "type": "extensions"
              }
            }
          },
          "type": "data_elements"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.name` | **(Obrigatório)** Um nome legível para o elemento de dados. |
| `attributes.delegate_descriptor_id` | **(Obrigatório)** Uma string formatada que associa o elemento de dados a um pacote de extensão. Todos os elementos de dados devem ser associados a um pacote de extensão quando são criados pela primeira vez, pois cada pacote de extensão define os tipos compatíveis para seus elementos de dados delegados, bem como seu comportamento pretendido. Consulte o guia em [IDs do descritor delegado](../guides/delegate-descriptor-ids.md) para obter mais informações. |
| `attributes.settings` | Um objeto JSON de configurações representado como uma string. |
| `attributes.default_value` | Um valor padrão a ser retornado se o elemento de dados for avaliado como `undefined`. |
| `attributes.enabled` | Um valor booleano indicando se o elemento de dados está ativado. |
| `attributes.force_lower_case` | Um valor booleano que indica se o valor do elemento de dados deve ser convertido em minúsculas antes de ser armazenado. |
| `attributes.clean_text` | Um valor booleano que indica se os espaços em branco à esquerda e à direita devem ser removidos do valor do elemento de dados antes de serem armazenados. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `data_elements`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do elemento de dados recém-criado.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Atualizar um elemento de dados {#update}

Você pode atualizar um elemento de dados incluindo sua ID no caminho de uma solicitação de PATCH.

**Formato da API**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `DATA_ELEMENT_ID` | O `id` do elemento de dados que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir atualiza o `name` de um elemento de dados existente.

```shell
curl -X PUT \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Um objeto cujas propriedades representam os atributos a serem atualizados para o elemento de dados. Todos os atributos do elemento de dados podem ser atualizados. Consulte o exemplo de chamada para [criar um elemento de dados](#create) para obter uma lista de atributos e seu caso de uso. |
| `id` | O `id` do elemento de dados que você deseja atualizar. Isso deve corresponder ao valor `{DATA_ELEMENT_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `data_elements`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do elemento de dados atualizado.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Revisar um elemento de dados {#revise}

Ao revisar um elemento de dados, uma nova revisão do elemento de dados é criada com a revisão atual (head). Cada revisão de um elemento de dados terá sua própria ID. O elemento de dados original pode ser descoberto por meio de um link de origem.

Você pode revisar um elemento de dados fornecendo uma propriedade `meta.action` com um valor `revise` no corpo de uma solicitação de PATCH.

**Formato da API**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `DATA_ELEMENT_ID` | O `id` do elemento de dados que você deseja revisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X PUT \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "meta": {
            "action": "revise"
          },
          "id": "DE7d7284657ee540ee8f402277860e9f8a",
          "type": "data_elements"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Um objeto cujas propriedades representam os atributos a serem atualizados para o elemento de dados. Todos os atributos do elemento de dados podem ser atualizados. Consulte o exemplo de chamada para [criar um elemento de dados](#create) para obter uma lista de atributos e seu caso de uso. |
| `meta.action` | Quando incluída com um valor `revise`, essa propriedade indica que uma nova revisão deve ser criada para o elemento de dados. |
| `id` | O `id` do elemento de dados que você deseja revisar. Isso deve corresponder ao valor `{DATA_ELEMENT_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo revisado. Para esse ponto de extremidade, o valor deve ser `data_elements`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nova revisão do elemento de dados, conforme indicado pelo atributo incrementado `meta.latest_revision_number`.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Excluir um elemento de dados

Você pode excluir um elemento de dados incluindo sua ID no caminho de uma solicitação de DELETE.

**Formato da API**

```http
DELETE /data_elements/{DATA_ELEMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `DATA_ELEMENT_ID` | O `id` do elemento de dados que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta, indicando que o elemento de dados foi excluído.

## Gerenciar notas de um elemento de dados {#notes}

Os elementos de dados são recursos &quot;notáveis&quot;, o que significa que você pode criar e recuperar notas baseadas em texto em cada recurso individual. Consulte o [guia de ponto de extremidade de notas](./notes.md) para obter mais informações sobre como gerenciar notas para elementos de dados e outros recursos compatíveis.

## Recuperar recursos relacionados para um elemento de dados {#related}

As chamadas a seguir demonstram como recuperar os recursos relacionados para um elemento de dados. Quando [procurar um elemento de dados](#lookup), esses relacionamentos são listados na propriedade `relationships`.

Consulte o [guia de relacionamentos](../guides/relationships.md) para obter mais informações sobre relacionamentos na API de Reator.

### Listar as bibliotecas relacionadas para um elemento de dados {#libraries}

Você pode listar as bibliotecas que utilizam um elemento de dados ao anexar `/libraries` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/libraries
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_ELEMENT_ID}` | O `id` do elemento de dados cujas bibliotecas você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de bibliotecas que usam o elemento de dados especificado.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Listar as revisões relacionadas de um elemento de dados {#revisions}

Você pode listar as revisões anteriores de um elemento de dados ao anexar `/revisions` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/revisions
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_ELEMENT_ID}` | O `id` do elemento de dados cujas revisões você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de revisões para o elemento de dados especificado.

```json
{
  "data": [
    {
      "id": "DEaeceb5164d494c768c18e37ec6f3b091",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:06.488Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:37:06.488Z",
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
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "DE5172417ff56e43d2a99ca149021bf65a",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:05.920Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:37:05.920Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

### Pesquisar a extensão relacionada para um elemento de dados {#extension}

Você pode buscar a extensão que usa um elemento de dados ao anexar `/extension` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/extension
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_ELEMENT_ID}` | O `id` do elemento de dados cuja extensão você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da extensão que usa o elemento de dados especificado.

```json
{
  "data": {
    "id": "EX9c7f9f1e826149978f2dadaf4c639679",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:37:31.952Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:31.952Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/property"
        },
        "data": {
          "id": "PR5c15543ef7bb403abc79d65fee0bf1f9",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/origin"
        },
        "data": {
          "id": "EX9c7f9f1e826149978f2dadaf4c639679",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5c15543ef7bb403abc79d65fee0bf1f9",
      "origin": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "self": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Pesquisar a origem relacionada de um elemento de dados {#origin}

Você pode buscar a origem de um elemento de dados ao anexar `/origin` ao caminho de uma solicitação do GET. A origem de um elemento de dados é a revisão anterior que foi atualizada para criar a revisão atual.

**Formato da API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/origin
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_ELEMENT_ID}` | O `id` do elemento de dados cuja origem você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da origem do elemento de dados especificado.

```json
{
  "data": {
    "id": "DE790cb76f91594c2082a727b9f97024f6",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:37:19.891Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:37:19 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:19.891Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/property"
        },
        "data": {
          "id": "PRf1ac400fb1e04c689e28d5efcd675c94",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/origin"
        },
        "data": {
          "id": "DE790cb76f91594c2082a727b9f97024f6",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/extension"
        },
        "data": {
          "id": "EX2345dba2c8b34d1cbe2795e29c62bf27",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension"
        },
        "data": {
          "id": "EXad7ebb72d721478483b741eebfffda6a",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRf1ac400fb1e04c689e28d5efcd675c94",
      "origin": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "self": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "extension": "https://reactor.adobe.io/extensions/EX2345dba2c8b34d1cbe2795e29c62bf27"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Pesquise a propriedade relacionada de um elemento de dados {#property}

Você pode pesquisar a propriedade que possui um elemento de dados ao anexar `/property` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/property
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATA_ELEMENT_ID}` | O `id` do elemento de dados cuja propriedade você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da propriedade proprietária do elemento de dados especificado.

```json
{
  "data": {
    "id": "PRae9440b0f3234c4286569485f2b7a6a2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:40.829Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:40.829Z",
      "platform": "web",
      "development": false,
      "token": "42daac072e1e",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments",
      "extensions": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions",
      "rules": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules",
      "self": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
