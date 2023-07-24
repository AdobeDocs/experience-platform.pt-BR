---
description: Esta página aborda o formato da mensagem e a transformação do perfil nos dados exportados do Adobe Experience Platform para destinos.
title: Formato de mensagem
source-git-commit: e500d05858a3242295c6e5aac8284ad301d0cd17
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# Formato de mensagem

## Pré-requisitos - Conceitos do Adobe Experience Platform {#prerequisites}

Para entender o formato da mensagem e o processo de configuração e transformação de perfil no lado do Adobe, familiarize-se com os seguintes conceitos de Experience Platform:

* **Experience Data Model (XDM)**. [Visão geral do XDM](../../../../xdm/home.md) e  [Como criar um esquema XDM no Adobe Experience Platform](../../../../xdm/tutorials/create-schema-ui.md).
* **Classe**. [Criar e editar classes na interface](../../../../xdm/ui/resources/classes.md).
* **IdentityMap**. O mapa de identidade representa um mapa de todas as identidades de usuários finais no Adobe Experience Platform. Consulte `xdm:identityMap` no [Dicionário de campo XDM](../../../../xdm/schema/field-dictionary.md).
* **SegmentMembership**. A variável [segmentMembership](../../../../xdm/schema/field-dictionary.md) O atributo XDM informa a quais públicos-alvo um perfil é membro. Para os três valores diferentes no `status` , leia a documentação em [Grupo de campos de esquema Detalhes da associação do público](../../../../xdm/field-groups/profile/segmentation.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim (apenas as etapas 1 e 2 do diagrama abaixo) |

## Visão geral {#overview}

Esta página aborda o formato da mensagem e a transformação do perfil nos dados exportados do Adobe Experience Platform para destinos.

O Adobe Experience Platform exporta dados para um número significativo de destinos, em vários formatos de dados. Alguns exemplos de tipos de destino são plataformas de publicidade (Google), redes sociais (Facebook) e locais de armazenamento na nuvem (Amazon S3, Hubs de Eventos do Azure).

O Experience Platform pode ajustar o formato da mensagem de perfis exportados para corresponder ao formato esperado no seu lado. Para entender essa personalização, os seguintes conceitos são importantes:

* O esquema XDM de origem (1) e de destino (2) no Adobe Experience Platform
* o formato de mensagem esperado no lado do parceiro (3), e
* A camada de transformação entre o esquema XDM e o formato de mensagem esperado, que pode ser definida ao criar um [template de transformação de mensagem](#using-templating).

![Transformação de esquema em JSON](../../assets/functionality/destination-server/transformations-3-steps.png)

O Experience Platform usa esquemas XDM para descrever a estrutura dos dados de forma consistente e reutilizável.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Esquema do XDM de origem (1)**: este item se refere ao esquema que os clientes usam no Experience Platform. No Experience Platform, no [etapa de mapeamento](../../../ui/activate-segment-streaming-destinations.md#mapping) do workflow ativar destino, os clientes mapeiam campos do esquema XDM para o esquema de destino do seu destino (2).

**Esquema XDM do Target (2)**: com base no esquema padrão JSON (3) do formato esperado do seu destino e nos atributos que seu destino pode interpretar, você pode definir atributos de perfil e identidades no esquema XDM do destino. Você pode fazer isso na configuração de destinos, no campo [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) e [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) objetos.

**Esquema padrão JSON dos atributos do perfil de destino (3)**: este exemplo representa um [Esquema JSON](https://json-schema.org/learn/miscellaneous-examples.html) de todos os atributos de perfil compatíveis com sua plataforma e seus tipos (por exemplo: objeto, string, matriz). Exemplos de campos que seu destino poderia suportar podem ser `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`e assim por diante. Você precisa de um [template de transformação de mensagem](#using-templating) para adaptar os dados exportados do Experience Platform ao formato esperado.

Com base nas transformações de esquema descritas acima, veja como uma configuração de perfil muda entre o esquema XDM de origem e um esquema de amostra no lado do parceiro:

![Exemplo de mensagem de transformações](../../assets/functionality/destination-server/transformations-with-examples.png)

## Introdução - transformação de três atributos básicos {#getting-started}

Para demonstrar o processo de transformação de perfil, o exemplo abaixo usa três atributos de perfil comuns no Adobe Experience Platform: **nome**, **sobrenome**, e **endereço de email**.

>[!NOTE]
>
>O cliente mapeia os atributos do esquema XDM de origem para o esquema XDM do parceiro na interface do usuário do Adobe Experience Platform, na **Mapeamento** etapa do [ativar fluxo de trabalho de destino](../../../ui/activate-segment-streaming-destinations.md#mapping).

Digamos que sua plataforma possa receber um formato de mensagem como:

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

Considerando o formato da mensagem, as transformações correspondentes são as seguintes:

| Atributo no esquema XDM do parceiro no lado do Adobe | Transformação | Atributo em mensagem HTTP do seu lado |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Estrutura de perfil no Experience Platform {#profile-structure}

Para entender os exemplos mais abaixo na página, é importante conhecer a estrutura de um perfil no Experience Platform.

Os perfis têm três seções:

* `segmentMembership` (sempre presente em um perfil)
   * esta seção contém todos os públicos-alvo presentes no perfil. Os públicos-alvo podem ter um destes dois status: `realized` ou `exited`.
* `identityMap` (sempre presente em um perfil)
   * esta seção contém todas as identidades presentes no perfil (email, Google GAID, Apple IDFA e assim por diante) e que o usuário mapeou para exportação no fluxo de trabalho de ativação.
* atributos (dependendo da configuração de destino, eles podem estar presentes no perfil). Também há uma pequena diferença a ser observada entre atributos predefinidos e atributos de forma livre:
   * para *atributos de forma livre*, eles contêm um `.value` caminho se o atributo estiver presente no perfil (consulte a `lastName` atributo do exemplo 1). Se não estiverem presentes no perfil, eles não conterão os `.value` caminho (consulte `firstName` atributo do exemplo 1).
   * para *atributos predefinidos*, eles não contêm um `.value` caminho. Todos os atributos mapeados presentes em um perfil estarão presentes no mapa de atributos. Os que não estiverem não estarão presentes (consulte o Exemplo 2 - a variável `firstName` atributo não existe no perfil).

Veja abaixo dois exemplos de perfis no Experience Platform:

### Exemplo 1 com `segmentMembership`, `identityMap` Atributos e para atributos de forma livre {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Exemplo 2 com `segmentMembership`, `identityMap` atributos e para atributos predefinidos {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de público {#using-templating}

Usos do Adobe [Modelos Pebble](https://pebbletemplates.io/), um idioma de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), para transformar os campos do esquema XDM do Experience Platform em um formato compatível com seu destino.

Esta seção fornece vários exemplos de como essas transformações são feitas, desde o esquema XDM de entrada, passando pelo modelo, até a saída nos formatos de carga útil aceitos pelo seu destino. Os exemplos abaixo são apresentados por complexidade crescente, como se segue:

1. Exemplos simples de transformação. Saiba como a modelagem funciona com transformações simples para [Atributos do perfil](#attributes), [associação de público](#segment-membership), e [Identidade](#identities) campos.
2. Exemplos de maior complexidade de modelos que combinam os campos acima: [Criar um modelo que envia públicos e identidades](./message-format.md#segments-and-identities) e [Criar um modelo que envia segmentos, identidades e atributos de perfil](#segments-identities-attributes).
3. Modelos que incluem a chave de agregação. Quando você usa [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) na configuração de destino, o Experience Platform agrupa os perfis exportados para o seu destino com base em critérios como ID de público-alvo, status do público-alvo ou namespaces de identidade.

### Atributos do perfil {#attributes}

Para transformar os atributos de perfil exportados para o seu destino, consulte o JSON e as amostras de código abaixo.

>[!IMPORTANT]
>
>Para obter uma lista de todos os atributos de perfil disponíveis no Adobe Experience Platform, consulte [Dicionário de campo XDM](../../../../xdm/schema/field-dictionary.md).


**Entrada**

Perfil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Perfil 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### associação de público {#audience-membership}

A variável [segmentMembership](../../../../xdm/schema/field-dictionary.md) O atributo XDM informa a quais públicos-alvo um perfil é membro.
Para os três valores diferentes no `status` , leia a documentação em [Grupo de campos de esquema Detalhes da associação do público](../../../../xdm/field-groups/profile/segmentation.md).

**Entrada**

Perfil 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Perfil 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identidades {#identities}

Para obter informações sobre identidades no Experience Platform, consulte [Visão geral do namespace de identidade](../../../../identity-service/namespaces.md).

**Entrada**

Perfil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Perfil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### Criar um modelo que envia públicos e identidades {#segments-and-identities}

Esta seção fornece um exemplo de uma transformação comumente usada entre o esquema XDM do Adobe e o esquema de destino do parceiro.
O exemplo abaixo mostra como transformar a associação de público-alvo e o formato de identidades e exibi-los no seu destino.

**Entrada**

Perfil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Perfil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering audiences by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

A variável `json` abaixo representa os dados exportados do Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Criar um modelo que envia segmentos, identidades e atributos de perfil {#segments-identities-attributes}

Esta seção fornece um exemplo de uma transformação comumente usada entre o esquema XDM do Adobe e o esquema de destino do parceiro.

Outro caso de uso comum é a exportação de dados que contêm associação de público-alvo, identidades (por exemplo: endereço de email, número de telefone, ID de publicidade) e atributos de perfil. Para exportar dados dessa maneira, consulte o exemplo abaixo:

**Entrada**

Perfil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Perfil 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Resultado**

A variável `json` abaixo representa os dados exportados do Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Inclua a chave de agregação no modelo para acessar perfis exportados agrupados por vários critérios {#template-aggregation-key}

Quando você usa [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) na configuração de destino, você pode agrupar os perfis exportados para o seu destino com base em critérios como ID de público-alvo, alias de público-alvo, associação de público-alvo ou namespaces de identidade.

No template de transformação de mensagem, você pode acessar as chaves de agregação mencionadas acima, conforme mostrado nos exemplos das seções a seguir. Use chaves de agregação para estruturar a mensagem HTTP exportada do Experience Platform para corresponder ao formato e aos limites de taxa esperados pelo seu destino.

#### Usar chave de agregação de ID de público-alvo no modelo {#aggregation-key-segment-id}

Se você usar [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) e defina `includeSegmentId` como verdadeiro, os perfis nas mensagens HTTP exportadas para o seu destino são agrupados pela ID do público-alvo. Veja abaixo como acessar a ID de público-alvo no modelo.

**Entrada**

Considere os quatro perfis abaixo, em que:

* os dois primeiros fazem parte do público-alvo com a ID de público-alvo `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* o terceiro perfil faz parte do público-alvo com a ID de público-alvo `8f812592-3f06-416b-bd50-e7831848a31a`
* o quarto perfil faz parte dos dois públicos-alvo acima.

Perfil 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Perfil 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Perfil 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

Perfil 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observe abaixo como `audienceId` é usado no modelo para acessar IDs de público-alvo. Este exemplo pressupõe que você use `audienceId` para associação de público-alvo na taxonomia de destino. Você pode usar qualquer outro nome de campo, dependendo da sua própria taxonomia.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

Quando exportados para seu destino, os perfis são divididos em dois grupos, com base na ID do público-alvo.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Usar chave de agregação de alias de público-alvo no modelo {#aggregation-key-segment-alias}

Se você usar [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) e defina `includeSegmentId` como true, você também pode acessar o alias de público-alvo no modelo.

Adicione a linha abaixo ao template para acessar os perfis exportados agrupados pelo alias do público-alvo.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Usar chave de agregação de status de público-alvo no modelo {#aggregation-key-segment-status}

Se você usar [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) e defina `includeSegmentId` e `includeSegmentStatus` como true, você pode acessar o status do público-alvo no modelo. Dessa forma, você pode agrupar perfis nas mensagens HTTP exportadas para o seu destino com base no fato de os perfis deverem ser adicionados ou removidos dos segmentos.

Os valores possíveis são:

* realizado
* existente
* encerrado

Adicione a linha abaixo ao modelo para adicionar ou remover perfis de segmentos, com base nos valores acima:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Usar chave de agregação de namespace de identidade no modelo {#aggregation-key-identity}

Abaixo há um exemplo onde a variável [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) na configuração de destino estiver definida para agregar perfis exportados por namespaces de identidade, no formulário `"namespaces": ["email", "phone"]` e `"namespaces": ["GAID", "IDFA"]`. Consulte a `groups` parâmetro no [criar configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) para obter mais detalhes sobre agrupamento.

**Entrada**

Perfil 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

Perfil 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve omitir os caracteres ilegais, como aspas duplas `""` antes de inserir o [modelo](../../functionality/destination-server/templating-specs.md) no [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obter mais informações sobre como evitar aspas duplas, consulte o Capítulo 9 na [JSON padrão](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observe que `input.aggregationKey.identityNamespaces` é usado no modelo abaixo

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Resultado**

Quando exportados para o seu destino, os perfis são divididos em dois grupos, com base nos namespaces de identidade. Email e telefone estão em um grupo, enquanto GAID e IDFA estão em outro.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### Usar a chave de agregação em um modelo de URL {#aggregation-key-url-template}

Dependendo do caso de uso, também é possível usar as chaves de agregação descritas aqui em um URL, conforme mostrado abaixo:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Referência: contexto e funções usados nos templates de transformação {#reference}

O contexto fornecido para o modelo contém `input`  (os perfis/dados exportados nesta chamada) e `destination` (dados sobre o destino para o qual o Adobe está enviando dados, válidos para todos os perfis).

A tabela abaixo fornece descrições para as funções dos exemplos acima.

| Função | Descrição |
|---------|----------|
| `input.profile` | O perfil, representado como um [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Segue o esquema XDM do parceiro mencionado mais acima nesta página. |
| `destination.segmentAliases` | Mapear IDs de público-alvo no namespace do Adobe Experience Platform para aliases de público-alvo no sistema do parceiro. |
| `destination.segmentNames` | Mapear de nomes de público-alvo no namespace do Adobe Experience Platform para nomes de público-alvo no sistema do parceiro. |
| `addedSegments(listOfSegments)` | Retorna somente os públicos-alvo com status `realized`. |
| `removedSegments(listOfSegments)` | Retorna somente os públicos-alvo com status `exited`. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este documento, você sabe como os dados exportados do Experience Platform são transformados. Em seguida, leia as seguintes páginas para concluir seu conhecimento sobre a criação de modelos de transformação de mensagem para seu destino:

* [Criar e testar um modelo de transformação de mensagem](../../testing-api/streaming-destinations/create-template.md)
* [Renderizar operações de API de modelo](../../testing-api/streaming-destinations/render-template-api.md)
* [Funções de transformação compatíveis com o Destination SDK](../destination-server/supported-functions.md)

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](server-specs.md)
* [Especificações de modelo](templating-specs.md)
* [Configuração da formatação de arquivo](file-formatting.md)