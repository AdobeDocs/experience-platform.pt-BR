---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---


# Avaliação das políticas

Depois que as ações de marketing tiverem sido criadas e as políticas tiverem sido definidas, você poderá usar a [!DNL Policy Service] API para avaliar se alguma política foi violada por determinadas ações. As restrições retornadas assumem a forma de um conjunto de políticas que seriam violadas ao tentar a ação de marketing nos dados especificados que contêm rótulos de uso de dados.

Por padrão, **somente as políticas cujo status está definido como &quot;ATIVADO&quot; participam da avaliação**, no entanto, você pode usar o parâmetro de query `?includeDraft=true` para incluir as políticas &quot;RASCUNHO&quot; na avaliação.

Os pedidos de avaliação podem ser apresentados de uma das três formas:

1. Considerando um conjunto de rótulos de uso de dados e uma ação de marketing, a ação viola alguma política?
1. Dado um ou mais conjuntos de dados e uma ação de marketing, a ação viola alguma política?
1. Considerando um ou mais conjuntos de dados e um subconjunto de um ou mais campos em cada um desses conjuntos de dados, a ação viola alguma política?

## Avaliar políticas usando rótulos de uso de dados e uma ação de marketing

A avaliação de violações de política com base na presença de rótulos de uso de dados exige que você especifique o conjunto de rótulos que estaria presente nos dados durante a solicitação. Isso é feito por meio do uso de parâmetros de query, nos quais os rótulos de uso de dados são fornecidos como uma lista de valores separada por vírgulas, conforme mostrado no exemplo a seguir.

**Formato da API**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Solicitação**

A solicitação de exemplo abaixo avalia uma ação de marketing contra os rótulos C1 e C3. Ao avaliar políticas usando rótulos de uso de dados, lembre-se do seguinte:
* **Os rótulos de uso de dados fazem distinção entre maiúsculas e minúsculas.** A solicitação mostrada acima retorna uma política violada, enquanto fazer a mesma solicitação usando rótulos minúsculos (por exemplo, `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) não.
* **Esteja ciente dos operadores`AND`e`OR`em suas expressões de política.** Neste exemplo, se um rótulo (`C1` ou `C3`) tivesse aparecido sozinho na solicitação, a ação de marketing não teria violado essa política. São necessárias ambas as etiquetas (`C1 AND C3`) para retornar a política violada. Certifique-se de que você esteja avaliando as políticas com cuidado e definindo expressões políticas com igual cuidado.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto response inclui uma `duleLabels` matriz que deve corresponder aos rótulos enviados na solicitação. Se a execução da ação de marketing especificada em relação aos rótulos de uso de dados violar uma política, a `violatedPolicies` matriz conterá os detalhes da política (ou políticas) afetada. Se nenhuma política for violada, o `violatedPolicies` storage aparecerá vazio (`[]`).

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

## Avaliar políticas usando conjuntos de dados e uma ação de marketing

Você também pode avaliar violações de política especificando a ID de um ou mais conjuntos de dados a partir dos quais os rótulos de uso de dados podem ser coletados. Isso é feito executando uma solicitação de POST para o terminal principal ou personalizado para uma ação de marketing e especificando IDs de conjunto de dados no corpo da solicitação, como mostrado abaixo. `/constraints`

**Formato da API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Solicitação**

O corpo da solicitação contém uma matriz com um objeto para cada ID de conjunto de dados. Como você está enviando um corpo de solicitação, o campo &quot;Tipo de conteúdo: &quot;application/json&quot; é obrigatório, como mostra o exemplo a seguir.

```SHELL
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

**Resposta**

O objeto response inclui uma `duleLabels` matriz que contém uma lista consolidada de todos os rótulos encontrados nos conjuntos de dados especificados. Essa lista inclui rótulos de nível de conjunto de dados e de campo em todos os campos no conjunto de dados.

A resposta também inclui uma `discoveredLabels` matriz que contém objetos para cada conjunto de dados, mostrando `datasetLabels` divididos em rótulos de nível de conjunto de dados e de campo. Cada rótulo de nível de campo mostra o caminho para o campo específico com esse rótulo.

Se a ação de marketing especificada violar uma política que envolve o `duleLabels` dentro dos conjuntos de dados, o `violatedPolicies` storage conterá os detalhes da política (ou políticas) afetada. Se nenhuma política for violada, o `violatedPolicies` storage aparecerá vazio (`[]`).

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

## Avaliar políticas usando conjuntos de dados, campos e uma ação de marketing

Além de fornecer uma ou mais IDs de conjunto de dados, um subconjunto de campos de cada conjunto de dados também pode ser especificado, indicando que apenas os rótulos de uso de dados nesses campos devem ser avaliados. Semelhante à solicitação de POST que envolve apenas conjuntos de dados, essa solicitação adiciona campos específicos para cada conjunto de dados ao corpo da solicitação.

Ao avaliar políticas usando campos de conjunto de dados, lembre-se do seguinte:

* **Os nomes de campo fazem distinção entre maiúsculas e minúsculas.** Ao fornecer campos, eles devem ser gravados exatamente como aparecem no conjunto de dados (por exemplo, `firstName` vs `firstname`).
* **Herança do rótulo do conjunto de dados.** os rótulos de uso de dados podem ser aplicados em vários níveis e são herdados para baixo. Se as avaliações de políticas não retornarem da maneira que você pensou que poderiam, verifique os rótulos herdados dos conjuntos de dados até os campos, além dos aplicados no nível do campo.

**Formato da API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Solicitação**

O corpo da solicitação contém uma matriz com um objeto para cada ID de conjunto de dados e o subconjunto de campos dentro desse conjunto de dados que devem ser usados para avaliação. Como você está enviando um corpo de solicitação, o campo &quot;Tipo de conteúdo: &quot;application/json&quot; é obrigatório, como mostra o exemplo a seguir.

```SHELL
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

**Resposta**

O objeto response inclui uma `duleLabels` matriz que contém a lista consolidada de rótulos encontrados nos campos especificados. Lembre-se de que isso inclui também rótulos de conjunto de dados, já que eles são herdados para campos.

Se uma política for violada ao executar a ação de marketing especificada nos dados nos campos fornecidos, a `violatedPolicies` matriz conterá os detalhes da política (ou políticas) afetada. Se nenhuma política for violada, o `violatedPolicies` storage aparecerá vazio (`[]`).

Na resposta abaixo, você pode ver que a lista de `duleLabels` agora é menor, como é o caso `discoveredLabels` para cada conjunto de dados, pois inclui apenas os campos especificados no corpo da solicitação. Você também notará que a política violada anteriormente, &quot;Anúncios de definição de metas ou Conteúdo&quot;, exigia ambas `C4 AND C6` as etiquetas, portanto, ela não é mais violada e o `violatedPolicies` storage aparece vazio.

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

## Avaliação de políticas para [!DNL Real-time Customer Profile]

A [!DNL Policy Service] API também pode ser usada para verificar violações de política que envolvam o uso de [!DNL Real-time Customer Profile] segmentos. Consulte o tutorial sobre como [impor a conformidade de uso de dados para segmentos](../../segmentation/tutorials/governance.md) de audiência para obter mais informações.