---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas
topic: developer guide
translation-type: tm+mt
source-git-commit: 12c53122d84e145a699a2a86631dc37ee0073578
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 1%

---


# Pontos finais de avaliação de políticas

Depois que as ações de marketing tiverem sido criadas e as políticas tiverem sido definidas, você poderá usar a [!DNL Policy Service] API para avaliar se alguma política foi violada por determinadas ações. As restrições retornadas assumem a forma de um conjunto de políticas que seriam violadas ao tentar a ação de marketing nos dados especificados que contêm rótulos de uso de dados.

Por padrão, somente políticas cujo status está definido para `ENABLED` participar da avaliação. No entanto, você pode usar o parâmetro query `?includeDraft=true` para incluir `DRAFT` políticas na avaliação.

Os pedidos de avaliação podem ser apresentados de uma das três formas:

1. Considerando uma ação de marketing e um conjunto de rótulos de uso de dados, a ação viola alguma política?
1. Dada uma ação de marketing e um ou mais conjuntos de dados, a ação viola alguma política?
1. Dada uma ação de marketing, um ou mais conjuntos de dados e um subconjunto de um ou mais campos em cada um desses conjuntos de dados, a ação viola alguma política?

## Introdução

Os pontos finais da API usados neste guia fazem parte da [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, reveja o guia [de](./getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Avaliar violações de política usando rótulos de uso de dados {#labels}

Você pode avaliar violações de política com base na presença de um conjunto específico de rótulos de uso de dados usando o parâmetro `duleLabels` query em uma solicitação de GET.

**Formato da API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing para testar em relação a um conjunto de rótulos de uso de dados. Você pode recuperar uma lista de ações de marketing disponíveis, fazendo uma solicitação de [GET para o endpoint](./marketing-actions.md#list)de ações de marketing. |
| `{LABELS_LIST}` | Uma lista separada por vírgulas de nomes de rótulos de uso de dados para testar a ação de marketing. Por exemplo: `duleLabels=C1,C2,C3`<br><br>Observe que os nomes dos rótulos fazem distinção entre maiúsculas e minúsculas. Certifique-se de usar a letra correta ao listá-las no `duleLabels` parâmetro. |

**Solicitação**

A solicitação de exemplo abaixo avalia uma ação de marketing contra os rótulos C1 e C3.

>[!IMPORTANT]
>
>Esteja ciente dos operadores `AND` e `OR` em suas expressões de política. No exemplo abaixo, se um rótulo (`C1` ou `C3`) tivesse aparecido sozinho na solicitação, a ação de marketing não teria violado essa política. São necessárias ambas as etiquetas (`C1` e `C3`) para retornar a política violada. Certifique-se de que você esteja avaliando as políticas com cuidado e definindo expressões políticas com igual cuidado.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida inclui um `violatedPolicies` storage, que contém os detalhes das políticas que foram violadas como resultado da execução da ação de marketing contra os rótulos fornecidos. Se nenhuma política for violada, o `violatedPolicies` storage ficará vazio.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Você pode avaliar violações de política com base em um conjunto de um ou mais conjuntos de dados a partir dos quais os rótulos de uso de dados podem ser coletados. Isso é feito executando uma solicitação de POST para o `/constraints` endpoint de uma ação de marketing específica e fornecendo uma lista de IDs de conjunto de dados no corpo da solicitação.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing a ser testada em relação a um ou mais conjuntos de dados. Você pode recuperar uma lista de ações de marketing disponíveis, fazendo uma solicitação de [GET para o endpoint](./marketing-actions.md#list)de ações de marketing. |

**Solicitação**

A solicitação a seguir executa a ação de `crossSiteTargeting` marketing em um conjunto de três conjuntos de dados para avaliar se há violações de política.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | O tipo de entidade cuja ID é indicada na `entityId` propriedade irmão. Atualmente, o único valor aceito é `dataSet`. |
| `entityId` | A ID de um conjunto de dados para testar a ação de marketing. Uma lista de conjuntos de dados e suas IDs correspondentes pode ser obtida por meio de uma solicitação de GET para o `/dataSets` endpoint na [!DNL Catalog Service] API. Consulte o guia na [ [!DNL Catalog] listagem de objetos](../../catalog/api/list-objects.md) para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida inclui um `violatedPolicies` storage, que contém os detalhes das políticas que foram violadas como resultado da execução da ação de marketing em relação aos conjuntos de dados fornecidos. Se nenhuma política for violada, o `violatedPolicies` storage ficará vazio.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `duleLabels` | O objeto response inclui uma `duleLabels` matriz que contém uma lista consolidada de todos os rótulos encontrados nos conjuntos de dados especificados. Essa lista inclui rótulos de nível de conjunto de dados e de campo em todos os campos no conjunto de dados. |
| `discoveredLabels` | A resposta também inclui uma `discoveredLabels` matriz que contém objetos para cada conjunto de dados, mostrando `datasetLabels` divididos em rótulos de nível de conjunto de dados e de campo. Cada rótulo de nível de campo mostra o caminho para o campo específico com esse rótulo. |

## Avaliar violações de política usando campos de conjunto de dados específicos {#fields}

É possível avaliar violações de política com base em um subconjunto de campos de um ou mais conjuntos de dados, de modo que somente os rótulos de uso de dados aplicados a esses campos sejam avaliados.

Ao avaliar políticas usando campos de conjunto de dados, lembre-se do seguinte:

* **Os nomes de campo fazem distinção entre maiúsculas e minúsculas**: Ao fornecer campos, eles devem ser gravados exatamente como aparecem no conjunto de dados (por exemplo, `firstName` vs `firstname`).
* **Herança** do rótulo do conjunto de dados: Campos individuais em um conjunto de dados herdam quaisquer rótulos que foram aplicados no nível do conjunto de dados. Se suas avaliações de política não retornarem conforme esperado, verifique se há etiquetas que possam ter sido herdadas do nível do conjunto de dados para baixo para os campos, além das aplicadas no nível do campo.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing a ser testada em relação a um subconjunto de campos de conjunto de dados. Você pode recuperar uma lista de ações de marketing disponíveis, fazendo uma solicitação de [GET para o endpoint](./marketing-actions.md#list)de ações de marketing. |

**Solicitação**

A solicitação a seguir testa a ação de marketing `crossSiteTargeting` em um conjunto específico de campos pertencentes a três conjuntos de dados. A carga é semelhante a uma solicitação de [avaliação que envolve apenas conjuntos](#datasets)de dados, adicionando campos específicos para cada conjunto de dados dos quais coletar rótulos.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | O tipo de entidade cuja ID é indicada na `entityId` propriedade irmão. Atualmente, o único valor aceito é `dataSet`. |
| `entityId` | A ID de um conjunto de dados cujos campos devem ser avaliados em relação à ação de marketing. Uma lista de conjuntos de dados e suas IDs correspondentes pode ser obtida por meio de uma solicitação de GET para o `/dataSets` endpoint na [!DNL Catalog Service] API. Consulte o guia na [ [!DNL Catalog] listagem de objetos](../../catalog/api/list-objects.md) para obter mais informações. |
| `entityMeta.fields` | Uma matriz de caminhos para campos específicos no schema do conjunto de dados, fornecida na forma de strings de ponteiro JSON. Consulte a seção sobre Ponteiro [](../../landing/api-fundamentals.md#json-pointer) JSON no guia Fundamentos da API para obter detalhes sobre a sintaxe aceita para essas strings. |

**Resposta**

Uma resposta bem-sucedida inclui um `violatedPolicies` storage, que contém os detalhes das políticas que foram violadas como resultado da execução da ação de marketing em relação aos campos do conjunto de dados fornecido. Se nenhuma política for violada, o `violatedPolicies` storage ficará vazio.

Comparando a resposta de exemplo abaixo com a [resposta que envolve apenas conjuntos de dados](#datasets), observe que a lista de rótulos coletados é menor. Os valores `discoveredLabels` para cada conjunto de dados também foram reduzidos, pois incluem apenas os campos especificados no corpo da solicitação. Além disso, a política violada anteriormente `Targeting Ads or Content` exige que ambas as `C4 AND C6` etiquetas sejam apresentadas e, portanto, não é mais violada conforme indicado pelo `violatedPolicies` storage vazio.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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

O `/bulk-eval` endpoint permite executar vários trabalhos de avaliação em uma única chamada de API.

**Formato da API**

```http
POST /bulk-eval
```

**Solicitação**

A carga útil de um pedido de avaliação em massa deve ser uma gama de objetos; uma para cada tarefa de avaliação a executar. Para trabalhos que avaliam com base em conjuntos de dados e campos, um `entityList` storage deve ser fornecido. Para trabalhos que avaliam com base em rótulos de uso de dados, um `labels` storage deve ser fornecido.

>[!WARNING]
>
>Se algum trabalho de avaliação listado contiver um `entityList` e um `labels` storage, ocorrerá um erro. Se você deseja avaliar a mesma ação de marketing com base em conjuntos de dados e rótulos, é necessário incluir trabalhos de avaliação separados para essa ação de marketing.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `evalRef` | O URI da ação de marketing para testar rótulos ou conjuntos de dados para violações de políticas. |
| `includeDraft` | Por padrão, somente as políticas ativadas participam da avaliação. Se `includeDraft` estiver definido como `true`, as políticas que estão em `DRAFT` status também participarão. |
| `labels` | Uma matriz de rótulos de uso de dados para testar a ação de marketing.<br><br>**IMPORTANTE**: Ao usar essa propriedade, uma `entityList` propriedade NÃO deve ser incluída no mesmo objeto. Para avaliar a mesma ação de marketing usando conjuntos de dados e/ou campos, você deve incluir um objeto separado na carga da solicitação que contenha uma `entityList` matriz. |
| `entityList` | Uma matriz de conjuntos de dados e campos específicos (opcionalmente) nesses conjuntos de dados para testar a ação de marketing.<br><br>**IMPORTANTE**: Ao usar essa propriedade, uma `labels` propriedade NÃO deve ser incluída no mesmo objeto. Para avaliar a mesma ação de marketing usando rótulos de uso de dados específicos, é necessário incluir um objeto separado na carga da solicitação que contenha uma `labels` matriz. |
| `entityType` | O tipo de entidade para o qual testar a ação de marketing. Atualmente, somente `dataSet` é suportado. |
| `entityId` | A ID de um conjunto de dados para testar a ação de marketing. |
| `entityMeta.fields` | (Opcional) Uma lista de campos específicos no conjunto de dados para testar a ação de marketing. |

**Resposta**

Uma resposta bem sucedida retorna uma série de resultados de avaliação; uma para cada tarefa de avaliação de política enviada no pedido.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
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
      "imsOrg": "{IMS_ORG}",
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
          "imsOrg": "{IMS_ORG}",
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

A [!DNL Policy Service] API também pode ser usada para verificar violações de política que envolvam o uso de [!DNL Real-time Customer Profile] segmentos. Consulte o tutorial sobre como [impor a conformidade de uso de dados para segmentos](../../segmentation/tutorials/governance.md) de audiência para obter mais informações.