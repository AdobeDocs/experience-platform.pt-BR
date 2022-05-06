---
keywords: Experience Platform; home; tópicos populares; Aplicação de políticas; Aplicação automática; Aplicação baseada em API; governança de dados
solution: Experience Platform
title: Endpoints da API de avaliação de política
topic-legacy: developer guide
description: Depois que as ações de marketing tiverem sido criadas e as políticas tiverem sido definidas, você poderá usar a API do Serviço de política para avaliar se alguma política foi violada por determinadas ações. As restrições retornadas assumem a forma de um conjunto de políticas que seriam violadas ao tentar a ação de marketing nos dados especificados que contêm rótulos de uso de dados.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# Pontos de extremidade de avaliação de política

Depois que as ações de marketing tiverem sido criadas e as políticas tiverem sido definidas, você poderá usar a variável [!DNL Policy Service] API para avaliar se alguma política é violada por determinadas ações. As restrições retornadas assumem a forma de um conjunto de políticas que seriam violadas ao tentar a ação de marketing nos dados especificados que contêm rótulos de uso de dados.

Por padrão, somente as políticas cujo status está definido como `ENABLED` participar na avaliação. No entanto, é possível usar o parâmetro de consulta `?includeDraft=true` para incluir `DRAFT` políticas em avaliação.

Os pedidos de avaliação podem ser apresentados de uma das três formas seguintes:

1. Dada uma ação de marketing e um conjunto de rótulos de uso de dados, a ação viola alguma política?
1. Dada uma ação de marketing e um ou mais conjuntos de dados, a ação viola alguma política?
1. Dada uma ação de marketing, um ou mais conjuntos de dados e um subconjunto de um ou mais campos em cada um desses conjuntos de dados, a ação viola alguma política?

## Introdução

Os endpoints de API usados neste guia fazem parte do [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Avaliar violações de política usando rótulos de uso de dados {#labels}

Você pode avaliar violações de política com base na presença de um conjunto específico de rótulos de uso de dados usando o `duleLabels` parâmetro de consulta em uma solicitação GET.

**Formato da API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing para testar em relação a um conjunto de rótulos de uso de dados. É possível recuperar uma lista de ações de marketing disponíveis ao criar uma [Solicitação de GET para o endpoint de ações de marketing](./marketing-actions.md#list). |
| `{LABELS_LIST}` | Uma lista separada por vírgulas de nomes de rótulos de uso de dados para testar a ação de marketing. Por exemplo: `duleLabels=C1,C2,C3`<br><br>Observe que os nomes de rótulos fazem distinção entre maiúsculas e minúsculas. Certifique-se de usar as letras maiúsculas e minúsculas corretas ao listá-las na `duleLabels` parâmetro. |

**Solicitação**

A solicitação de exemplo abaixo avalia uma ação de marketing em relação aos rótulos C1 e C3.

>[!IMPORTANT]
>
>Esteja ciente do `AND` e `OR` nas expressões de política. No exemplo abaixo, se um rótulo (`C1` ou `C3`) se tivesse aparecido sozinho na solicitação, a ação de marketing não teria violado essa política. Ele utiliza ambos os rótulos (`C1` e `C3`) para retornar a política violada. Certifique-se de que você esteja avaliando as políticas com cuidado e definindo expressões de políticas com igual cuidado.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida inclui uma `violatedPolicies` , que contém os detalhes das políticas que foram violadas como resultado da execução da ação de marketing em relação aos rótulos fornecidos. Se nenhuma política for violada, a variável `violatedPolicies` A matriz ficará vazia.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Avaliar violações de política usando conjuntos de dados {#datasets}

Você pode avaliar violações de política com base em um conjunto de um ou mais conjuntos de dados a partir dos quais os rótulos de uso de dados podem ser coletados. Isso é feito executando uma solicitação POST para `/constraints` endpoint para uma ação de marketing específica e o fornecimento de uma lista de IDs de conjunto de dados no corpo da solicitação.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing que será testada em relação a um ou mais conjuntos de dados. É possível recuperar uma lista de ações de marketing disponíveis ao criar uma [Solicitação de GET para o endpoint de ações de marketing](./marketing-actions.md#list). |

**Solicitação**

A solicitação a seguir executa o `crossSiteTargeting` ação de marketing em um conjunto de três conjuntos de dados para avaliar violações de política.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| Propriedade | Descrição |
| --- | --- |
| `entityType` | O tipo de entidade cuja ID é indicada no irmão `entityId` propriedade. Atualmente, o único valor aceito é `dataSet`. |
| `entityId` | A ID de um conjunto de dados para testar a ação de marketing. Uma lista de conjuntos de dados e suas IDs correspondentes pode ser obtida fazendo uma solicitação do GET para o `/dataSets` endpoint no [!DNL Catalog Service] API. Consulte o guia sobre [listagem [!DNL Catalog] objetos](../../catalog/api/list-objects.md) para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida inclui uma `violatedPolicies` , que contém os detalhes das políticas que foram violadas como resultado da execução da ação de marketing em relação aos conjuntos de dados fornecidos. Se nenhuma política for violada, a variável `violatedPolicies` A matriz ficará vazia.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `duleLabels` | O objeto de resposta inclui um `duleLabels` que contém uma lista consolidada de todos os rótulos encontrados nos conjuntos de dados especificados. Essa lista inclui rótulos de conjunto de dados e de campo em todos os campos no conjunto de dados. |
| `discoveredLabels` | A resposta também inclui um `discoveredLabels` matriz que contém objetos para cada conjunto de dados, mostrando `datasetLabels` detalhado em rótulos de conjunto de dados e de campo. Cada rótulo de nível de campo mostra o caminho para o campo específico com esse rótulo. |

## Avaliar violações de política usando campos específicos do conjunto de dados {#fields}

Você pode avaliar violações de política com base em um subconjunto de campos de um ou mais conjuntos de dados, de modo que apenas os rótulos de uso de dados aplicados a esses campos sejam avaliados.

Ao avaliar políticas usando campos de conjunto de dados, lembre-se do seguinte:

* **Os nomes de campos fazem distinção entre maiúsculas e minúsculas**: Ao fornecer campos, eles devem ser escritos exatamente como aparecem no conjunto de dados (por exemplo, `firstName` vs `firstname`).
* **Herança do rótulo do conjunto de dados**: Os campos individuais em um conjunto de dados herdam quaisquer rótulos que foram aplicados no nível do conjunto de dados. Se as avaliações de política não retornarem como esperado, verifique se há rótulos que possam ter sido herdados do nível do conjunto de dados para os campos, além daqueles aplicados no nível do campo.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing para testar em relação a um subconjunto de campos do conjunto de dados. É possível recuperar uma lista de ações de marketing disponíveis ao criar uma [Solicitação de GET para o endpoint de ações de marketing](./marketing-actions.md#list). |

**Solicitação**

A solicitação a seguir testa a ação de marketing `crossSiteTargeting` em um conjunto específico de campos pertencentes a três conjuntos de dados. A carga é semelhante a um [solicitação de avaliação envolvendo somente conjuntos de dados](#datasets), adicionar campos específicos para cada conjunto de dados do para coletar rótulos.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Propriedade | Descrição |
| --- | --- |
| `entityType` | O tipo de entidade cuja ID é indicada no irmão `entityId` propriedade. Atualmente, o único valor aceito é `dataSet`. |
| `entityId` | A ID de um conjunto de dados cujos campos devem ser avaliados em relação à ação de marketing. Uma lista de conjuntos de dados e suas IDs correspondentes pode ser obtida fazendo uma solicitação do GET para o `/dataSets` endpoint no [!DNL Catalog Service] API. Consulte o guia sobre [listagem [!DNL Catalog] objetos](../../catalog/api/list-objects.md) para obter mais informações. |
| `entityMeta.fields` | Uma matriz de caminhos para campos específicos dentro do esquema do conjunto de dados, fornecido no formato de sequências de ponteiro JSON. Consulte a seção sobre [Ponteiro JSON](../../landing/api-fundamentals.md#json-pointer) no guia de fundamentos da API para obter detalhes sobre a sintaxe aceita para essas cadeias de caracteres. |

**Resposta**

Uma resposta bem-sucedida inclui uma `violatedPolicies` , que contém os detalhes das políticas que foram violadas como resultado da execução da ação de marketing em relação aos campos do conjunto de dados fornecidos. Se nenhuma política for violada, a variável `violatedPolicies` A matriz ficará vazia.

Comparação da resposta de exemplo abaixo com a [resposta envolvendo somente conjuntos de dados](#datasets), observe que a lista de rótulos coletados é menor. O `discoveredLabels` para cada conjunto de dados também foram reduzidos, pois incluem apenas os campos especificados no corpo da solicitação. Além disso, a política violada anteriormente `Targeting Ads or Content` exige que `C4 AND C6` rótulos para apresentar e, portanto, não é mais violado conforme indicado pelo campo vazio `violatedPolicies` matriz.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Avaliar políticas em massa {#bulk}

O `/bulk-eval` O endpoint permite executar vários trabalhos de avaliação em uma única chamada de API.

**Formato da API**

```http
POST /bulk-eval
```

**Solicitação**

A carga de um pedido de avaliação em massa deve ser uma matriz de objetos; um para cada trabalho de avaliação a ser executado. Para trabalhos que avaliam com base em conjuntos de dados e campos, um `entityList` deve ser fornecida. Para tarefas que são avaliadas com base em rótulos de uso de dados, uma `labels` deve ser fornecida.

>[!WARNING]
>
>Se algum trabalho de avaliação listado contiver um `entityList` e `labels` , resultará em um erro. Se desejar avaliar a mesma ação de marketing com base em conjuntos de dados e rótulos, você deve incluir tarefas de avaliação separadas para essa ação de marketing.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Propriedade | Descrição |
| --- | --- |
| `evalRef` | O URI da ação de marketing para testar rótulos ou conjuntos de dados em caso de violações de política. |
| `includeDraft` | Por padrão, somente as políticas ativadas participam da avaliação. If `includeDraft` está definida como `true`, políticas que estejam em `DRAFT` também participará. |
| `labels` | Uma matriz de rótulos de uso de dados para testar a ação de marketing.<br><br>**IMPORTANTE**: Ao usar essa propriedade, um `entityList` NÃO deve ser incluída no mesmo objeto. Para avaliar a mesma ação de marketing usando conjuntos de dados e/ou campos, você deve incluir um objeto separado na carga da solicitação que contenha um `entityList` matriz. |
| `entityList` | Uma matriz de conjuntos de dados e campos específicos (opcionalmente) nesses conjuntos de dados para testar a ação de marketing.<br><br>**IMPORTANTE**: Ao usar essa propriedade, um `labels` NÃO deve ser incluída no mesmo objeto. Para avaliar a mesma ação de marketing usando rótulos específicos de uso de dados, você deve incluir um objeto separado na carga da solicitação que contenha um `labels` matriz. |
| `entityType` | O tipo de entidade para a qual testar a ação de marketing. Atualmente, somente `dataSet` é compatível. |
| `entityId` | A ID de um conjunto de dados para testar a ação de marketing. |
| `entityMeta.fields` | (Opcional) Uma lista de campos específicos no conjunto de dados para testar a ação de marketing. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de resultados de avaliação; um para cada tarefa de avaliação de política enviada na solicitação.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{ORG_ID}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Avaliação de políticas para [!DNL Real-time Customer Profile]

O [!DNL Policy Service] A API também pode ser usada para verificar violações de política envolvendo o uso de [!DNL Real-time Customer Profile] segmentos. Veja o tutorial em [impor a conformidade do uso de dados para segmentos de público-alvo](../../segmentation/tutorials/governance.md) para obter mais informações.
