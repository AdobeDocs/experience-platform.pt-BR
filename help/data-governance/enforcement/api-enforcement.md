---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Impor políticas de uso de dados usando a API do Serviço de Política
topic: enforcement
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 2%

---


# Impor políticas de uso de dados usando a [!DNL Policy Service] API

Depois de criar rótulos de uso de dados para seus dados e criar políticas de uso para ações de marketing contra esses rótulos, você pode usar a [[!DNL DULE Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) para avaliar se uma ação de marketing executada em um conjunto de dados ou em um grupo arbitrário de rótulos constitui uma violação de política. Em seguida, você pode configurar seus próprios protocolos internos para lidar com violações de política com base na resposta da API.

>[!NOTE]
>
>Por padrão, somente as políticas cujo status está definido para `ENABLED` poder participar da avaliação. Para permitir que `DRAFT` as políticas participem da avaliação, é necessário incluir o parâmetro query `includeDraft=true` no caminho da solicitação.

Este documento fornece etapas sobre como usar a [!DNL Policy Service] API para verificar violações de políticas em diferentes cenários.

## Introdução

Este tutorial requer um entendimento prático dos seguintes conceitos chave envolvidos na aplicação das políticas DULE:

* [Controle](../home.md)de dados: A estrutura pela qual [!DNL Platform] aplica a conformidade de uso de dados.
   * [Rótulos](../labels/overview.md)de uso de dados: Os rótulos de uso de dados são aplicados a conjuntos de dados (e/ou campos individuais nesses conjuntos de dados), especificando restrições para como esses dados podem ser usados.
   * [Políticas](../policies/overview.md)de uso de dados: As políticas de uso de dados são regras que descrevem os tipos de ações de marketing que são permitidas ou restritas para determinados conjuntos de rótulos DULE.
* [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o guia [do](../api/getting-started.md) [!DNL Policy Service] desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API DULE, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Avaliar usando rótulos DULE e uma ação de marketing

É possível avaliar uma política testando uma ação de marketing em relação a um conjunto de rótulos DULE que estariam presentes em um conjunto de dados. Isso é feito por meio do uso do parâmetro do `duleLabels` query, onde os rótulos DULE são fornecidos como uma lista de valores separada por vírgulas, como mostrado no exemplo abaixo.

**Formato da API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing associada à política DULE que você está avaliando. |
| `{LABEL_1}` | Um rótulo de uso de dados para testar a ação de marketing. Pelo menos um rótulo deve ser fornecido. Ao fornecer vários rótulos, eles devem ser separados por vírgulas. |

**Solicitação**

A solicitação a seguir testa a ação `exportToThirdParty` de marketing contra rótulos `C1` e `C3`. Como a política de uso de dados criada anteriormente neste tutorial define o `C1` rótulo como uma das `deny` condições em sua expressão de política, a ação de marketing deve acionar uma violação de política.

>[!NOTE]
>
>Os rótulos de uso de dados fazem distinção entre maiúsculas e minúsculas. As violações de política ocorrem somente quando os rótulos definidos em suas expressões de política são correspondidos exatamente. Neste exemplo, um `C1` rótulo acionaria uma violação, ao passo que um `c1` rótulo não.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o URL da ação de marketing, os rótulos DULE com os quais foi testada e uma lista de quaisquer políticas DULE que foram violadas como resultado do teste da ação contra esses rótulos. Neste exemplo, a política &quot;Exportar dados para terceiros&quot; é mostrada no `violatedPolicies` storage, indicando que a ação de marketing acionou a violação de política esperada.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `violatedPolicies` | Um storage que lista quaisquer políticas DULE que foram violadas ao testar a ação de marketing (especificada em `marketingActionRef`) em relação ao fornecido `duleLabels`. |

## Avaliar usando conjuntos de dados

É possível avaliar uma política DULE testando uma ação de marketing em relação a um ou mais conjuntos de dados dos quais os rótulos DULE podem ser coletados. Isso é feito fazendo uma solicitação POST para `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` e fornecendo IDs de conjunto de dados no corpo da solicitação, como mostrado no exemplo abaixo.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing associada à política DULE que você está avaliando. |

**Solicitação**

A solicitação a seguir testa a ação de `exportToThirdParty` marketing em relação a três conjuntos de dados diferentes. Os conjuntos de dados são referenciados por tipo e ID em uma matriz fornecida na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
| `entityType` | Cada item na matriz de carga deve indicar o tipo de entidade que está sendo definida. Nesse caso de uso, o valor sempre será &quot;dataSet&quot;. |
| `entityId` | Cada item na matriz de carga deve fornecer a ID exclusiva para um conjunto de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o URL da ação de marketing, os rótulos DULE que foram coletados dos conjuntos de dados fornecidos e uma lista de quaisquer políticas DULE que foram violadas como resultado do teste da ação contra esses rótulos. Neste exemplo, a política &quot;Exportar dados para terceiros&quot; é mostrada no `violatedPolicies` storage, indicando que a ação de marketing acionou a violação de política esperada.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `duleLabels` | Uma lista de rótulos DULE que foram extraídos dos conjuntos de dados fornecidos na carga da solicitação. |
| `discoveredLabels` | Uma lista dos conjuntos de dados fornecidos na carga da solicitação, exibindo os rótulos DULE de nível de conjunto de dados e de campo que foram encontrados em cada um deles. |
| `violatedPolicies` | Um storage que lista quaisquer políticas DULE que foram violadas ao testar a ação de marketing (especificada em `marketingActionRef`) em relação ao fornecido `duleLabels`. |

## Próximas etapas

Ao ler esse documento, você verificou com êxito violações de política ao executar uma ação de marketing em um conjunto de dados ou em um conjunto de rótulos DULE. Usando os dados retornados nas respostas da API, você pode configurar protocolos em seu aplicativo de experiência para aplicar adequadamente as violações de política quando elas ocorrem.

Para obter etapas sobre como aplicar políticas de uso de dados para segmentos de audiência em [!DNL Real-time Customer Profile], consulte o seguinte [tutorial](../../segmentation/tutorials/governance.md).