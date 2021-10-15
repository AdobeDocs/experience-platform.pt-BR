---
description: Esta página aborda o formato da mensagem e a transformação do perfil em dados exportados do Adobe Experience Platform para destinos .
title: Formato de mensagem
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 2%

---

# Formato de mensagem

## Pré-requisitos - Conceitos do Adobe Experience Platform {#prerequisites}

Para entender o formato da mensagem, a configuração do perfil e o processo de transformação no Adobe, familiarize-se com os seguintes conceitos do Experience Platform:

* **Experience Data Model (XDM)**. [Visão ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR) geral do XDM e   [Como criar um esquema XDM no Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Classe**. [Crie e edite classes na interface do usuário](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **Mapa de identidade**. O mapa de identidade representa um mapa de todas as identidades de usuário final no Adobe Experience Platform. Consulte `xdm:identityMap` no [Dicionário de campo XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. O atributo XDM [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) informa quais segmentos um perfil é membro. Para os três valores diferentes no campo `status`, leia a documentação no [grupo de campos Detalhes da associação ao segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Visão geral {#overview}

Use o conteúdo desta página junto com o restante das opções de configuração [para destinos de parceiros](./configuration-options.md). Esta página aborda o formato da mensagem e a transformação do perfil em dados exportados do Adobe Experience Platform para destinos . A outra página aborda especificamente a conexão e autenticação com seu destino.

O Adobe Experience Platform exporta dados para um número significativo de destinos, em vários formatos de dados. Alguns exemplos de tipos de destino são plataformas de publicidade (Google), redes sociais (Facebook) e locais de armazenamento em nuvem (Amazon S3, Hubs de Eventos do Azure).

O Experience Platform pode ajustar o formato de mensagem dos perfis exportados para corresponder ao formato esperado no seu lado. Para entender essa personalização, os seguintes conceitos são importantes:
* O esquema XDM de origem (1) e de destino (2) no Adobe Experience Platform
* O formato de mensagem esperado no lado do parceiro (3) e
* A camada de transformação entre o esquema XDM e o formato de mensagem esperado, que você pode definir criando um [template de transformação de mensagem](./message-format.md#using-templating).

![Schema para transformação JSON](./assets/transformations-3-steps.png)

O Experience Platform usa esquemas XDM para descrever a estrutura dos dados de uma maneira consistente e reutilizável.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Esquema XDM de origem (1)**: Este item se refere ao schema usado pelos clientes no Experience Platform. Na Experience Platform, no [etapa de mapeamento](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) do workflow para ativar destino, os clientes mapeariam campos de seu schema de origem para o schema de destino do seu destino (2).

**Esquema XDM do Target (2)**: Com base no esquema padrão JSON (3) do formato esperado do seu destino, você pode definir atributos e identidades de perfil no esquema XDM de destino. Você pode fazer isso na configuração de destinos, nos objetos [schemaConfig](./destination-configuration.md#schema-configuration) e [identityNamespaces](./destination-configuration.md#identities-and-attributes).

**Esquema padrão JSON dos atributos de perfil de destino (3)**: Este item representa um esquema  [JSON ](https://json-schema.org/learn/miscellaneous-examples.html) de todos os atributos de perfil compatíveis com sua plataforma e seus tipos (por exemplo: objeto, string, matriz). Os campos de exemplo que seu destino poderia suportar podem ser `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` e assim por diante. Você precisa de um [template de transformação de mensagem](./message-format.md#using-templating) para adaptar os dados exportados do Experience Platform para o formato esperado.

Com base nas transformações de schema descritas acima, veja como uma configuração de perfil muda entre o schema XDM de origem e um schema de amostra no lado do parceiro:

![Exemplo de mensagem de transformações](./assets/transformations-with-examples.png)

<br> 


## Introdução - transformação de três atributos básicos {#getting-started}

Para demonstrar o processo de transformação do perfil, o exemplo abaixo usa três atributos comuns do perfil no Adobe Experience Platform: **nome**, **sobrenome** e **endereço de e-mail**.

>[!NOTE]
>
>O cliente mapeia os atributos do esquema XDM de origem para o esquema XDM do parceiro na interface do usuário do Adobe Experience Platform, na etapa **Mapping** do [workflow de destino de ativação](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

Considere que sua plataforma pode receber um formato de mensagem como:

```curl
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

| Atributo no esquema XDM do parceiro no lado do Adobe | Transformação | Atributo na mensagem HTTP ao seu lado |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

## Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento {#using-templating}

O Adobe usa uma linguagem de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar os campos do esquema XDM em um formato compatível com seu destino.

Esta seção fornece vários exemplos de como essas transformações são feitas - do schema XDM de entrada, por meio do template e da saída em formatos de carga aceitos pelo seu destino. Os exemplos abaixo são apresentados pela complexidade crescente, como a seguir:

1. Exemplos simples de transformação. Saiba como a modelagem funciona com transformações simples para campos [Atributos de perfil](./message-format.md#attributes), [Associação de segmento](./message-format.md#segment-membership) e [Identidade](./message-format.md#identities).
2. Exemplos de complexidade maior de modelos que combinam os campos acima: [Crie um modelo que envie segmentos e identidades](./message-format.md#segments-and-identities) e [Crie um modelo que envie segmentos, identidades e atributos de perfil](./message-format.md#segments-identities-attributes).
3. Modelos que incluem a chave de agregação. Ao usar [agregação configurável](./destination-configuration.md#configurable-aggregation) na configuração de destino, o Experience Platform agrupa os perfis exportados para seu destino com base em critérios como ID do segmento, status do segmento ou namespaces de identidade.

### Atributos do perfil {#attributes}

Para transformar os atributos de perfil exportados para seu destino, consulte o JSON e as amostras de código abaixo.

>[!IMPORTANT]
>
>Para obter uma lista de todos os atributos de perfil disponíveis no Adobe Experience Platform, consulte o [dicionário de campos XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


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
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Associação de segmento {#segment-membership}

O atributo XDM [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) informa quais segmentos um perfil é membro.
Para os três valores diferentes no campo `status`, leia a documentação no [grupo de campos Detalhes da associação ao segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
        "status": "existing"
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
        "status": "existing"
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
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

Para obter informações sobre identidades no Experience Platform, consulte a [Visão geral do namespace de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR).

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
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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


### Criar um modelo que envie segmentos e identidades {#segments-and-identities}

Esta seção fornece um exemplo de uma transformação comumente usada entre o esquema Adobe XDM e o schema de destino do parceiro.
O exemplo abaixo mostra como transformar a associação de segmentos e o formato de identidades e enviá-las para o destino.

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
              "status": "existing"
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
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                    {# Alternative syntax for filtering segments by status: #}
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

O `json` abaixo representa os dados exportados do Adobe Experience Platform.

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

### Criar um modelo que envie segmentos, identidades e atributos de perfil {#segments-identities-attributes}

Esta seção fornece um exemplo de uma transformação comumente usada entre o esquema Adobe XDM e o schema de destino do parceiro.

Outro caso de uso comum é a exportação de dados que contém associação de segmento, identidades (por exemplo: endereço de email, número de telefone, ID de publicidade) e atributos de perfil. Para exportar dados dessa maneira, consulte o exemplo abaixo:

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
              "status": "existing"
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
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

O `json` abaixo representa os dados exportados do Adobe Experience Platform.

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

Ao usar [agregação configurável](./destination-configuration.md#configurable-aggregation) na configuração de destino, você pode agrupar os perfis exportados para seu destino com base em critérios como ID do segmento, alias do segmento, associação de segmento ou namespaces de identidade.

No template de transformação de mensagem, você pode acessar as chaves de agregação mencionadas acima, conforme mostrado nos exemplos nas seções a seguir. Use chaves de agregação para estruturar a mensagem HTTP exportada do Experience Platform para corresponder aos limites de formato e taxa esperados pelo seu destino.

#### Usar chave de agregação de ID de segmento no modelo {#aggregation-key-segment-id}

Se você usar [agregação configurável](./destination-configuration.md#configurable-aggregation) e definir `includeSegmentId` como true, os perfis nas mensagens HTTP exportadas para o seu destino serão agrupados por ID de segmento. Veja abaixo como você pode acessar a ID de segmento no modelo.

**Entrada**

Considere os quatro perfis abaixo, onde:
* as duas primeiras são parte do segmento com a ID de segmento `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* o terceiro perfil faz parte do segmento com a ID de segmento `8f812592-3f06-416b-bd50-e7831848a31a`
* o quarto perfil faz parte dos dois segmentos acima.

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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

**Modelo**

>[!IMPORTANT]
>
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observe abaixo como `audienceId` é usado no modelo para acessar IDs de segmento. Este exemplo assume que você usa `audienceId` para associação de segmento em sua taxonomia de destino. Você pode usar qualquer outro nome de campo, dependendo da sua própria taxonomia.

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

Quando exportados para seu destino, os perfis são divididos em dois grupos, com base na ID do segmento.

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

#### Usar chave de agregação de alias de segmento no modelo {#aggregation-key-segment-alias}

Se você usar [agregação configurável](./destination-configuration.md#configurable-aggregation) e definir `includeSegmentId` como true, também poderá acessar o alias de segmento no template.

Adicione a linha abaixo ao template para acessar os perfis exportados agrupados por alias de segmento.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Usar chave de agregação de status de segmento no modelo {#aggregation-key-segment-status}

Se você usar [agregação configurável](./destination-configuration.md#configurable-aggregation) e definir `includeSegmentId` e `includeSegmentStatus` como true, poderá acessar o status do segmento no template. Dessa forma, você pode agrupar perfis nas mensagens HTTP exportadas para o seu destino com base no fato de os perfis deverem ser adicionados ou removidos dos segmentos.

Os valores possíveis são:

* realizado
* existente
* encerrado

Adicione a linha abaixo ao modelo para adicionar ou remover perfis dos segmentos, com base nos valores acima:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Usar chave de agregação de namespace de identidade no modelo {#aggregation-key-identity}

Abaixo está um exemplo em que a [agregação configurável](./destination-configuration.md#configurable-aggregation) na configuração de destino é definida para agregar perfis exportados por namespaces de identidade, no formato `"namespaces": ["email", "phone"]` e `"namespaces": ["GAID", "IDFA"]`. Consulte o parâmetro `groups` no [referência da API de configuração de destino](./destination-configuration-api.md) para obter mais informações sobre esse agrupamento.

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
>Para todos os modelos que você usa, você deve evitar os caracteres ilegais, como aspas duplas `""` antes de inserir o modelo no [configuração do servidor de destino](./server-and-template-configuration.md#template-specs). Para obter mais informações sobre o escape de aspas duplas, consulte o Capítulo 9 no [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Quando exportados para seu destino, os perfis são divididos em dois grupos, com base em seus namespaces de identidade. E-mail e telefone estão em um grupo, enquanto GAID e IDFA estão em outro.

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

Dependendo do caso de uso, você também pode usar as chaves de agregação descritas aqui em um URL, conforme mostrado abaixo:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Referência: Contexto e funções usadas nos templates de transformação {#reference}

O contexto fornecido para o modelo contém `input` (os perfis/dados exportados nesta chamada) e `destination` (dados sobre o destino para o qual o Adobe está enviando dados, válidos para todos os perfis).

A tabela abaixo fornece descrições para as funções nos exemplos acima.

| Função | Descrição |
|---------|----------|
| `input.profile` | O perfil, representado como um [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Segue o esquema XDM do parceiro mencionado mais acima nesta página. |
| `destination.segmentAliases` | Mapeie de IDs de segmento no namespace do Adobe Experience Platform para aliases de segmento no sistema do parceiro. |
| `destination.segmentNames` | Mapeie de nomes de segmentos no namespace do Adobe Experience Platform para nomes de segmentos no sistema do parceiro. |
| `addedSegments(listOfSegments)` | Retorna somente os segmentos com status `realized` ou `existing`. |
| `removedSegments(listOfSegments)` | Retorna somente os segmentos com status `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
