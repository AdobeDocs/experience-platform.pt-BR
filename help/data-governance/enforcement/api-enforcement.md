---
keywords: Experience Platform; home; tópicos populares; Aplicação de políticas; Aplicação automática; Aplicação baseada em API; governança de dados; teste
solution: Experience Platform
title: Impor políticas de uso de dados usando a API do serviço de política
topic-legacy: guide
type: Tutorial
description: Depois de criar rótulos de uso de dados para seus dados e criar políticas de uso para ações de marketing em relação a esses rótulos, você pode usar a API do Serviço de política para avaliar se uma ação de marketing executada em um conjunto de dados ou em um grupo arbitrário de rótulos constitui uma violação de política. Em seguida, você pode configurar seus próprios protocolos internos para lidar com violações de política com base na resposta da API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Impor políticas de uso de dados usando a API [!DNL Policy Service]

Depois de criar rótulos de uso de dados para seus dados e ter criado políticas de uso para ações de marketing em relação a esses rótulos, você pode usar o [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) para avaliar se uma ação de marketing executada em um conjunto de dados ou em um grupo arbitrário de rótulos constitui uma violação de política. Em seguida, você pode configurar seus próprios protocolos internos para lidar com violações de política com base na resposta da API.

>[!NOTE]
>
>Por padrão, somente as políticas cujo status está definido como `ENABLED` podem participar da avaliação. Para permitir que as políticas `DRAFT` participem na avaliação, você deve incluir o parâmetro de consulta `includeDraft=true` no caminho da solicitação.

Este documento fornece etapas sobre como usar a API [!DNL Policy Service] para verificar violações de política em diferentes cenários.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes conceitos-chave envolvidos na aplicação das políticas de uso de dados:

* [Governança](../home.md) de dados: A estrutura pela qual  [!DNL Platform] aplica a conformidade do uso de dados.
   * [Rótulos](../labels/overview.md) de uso de dados: Os rótulos de uso de dados são aplicados aos conjuntos de dados (e/ou campos individuais nesses conjuntos de dados), especificando restrições para como esses dados podem ser usados.
   * [Políticas](../policies/overview.md) de uso de dados: As políticas de uso de dados são regras que descrevem os tipos de ações de marketing permitidas ou restritas para determinados conjuntos de rótulos de uso de dados.
* [Sandboxes](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API [!DNL Policy Service], incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Avaliar usando rótulos e uma ação de marketing

É possível avaliar uma política testando uma ação de marketing em relação a um conjunto de rótulos de uso de dados que estaria hipotético presente em um conjunto de dados. Isso é feito com o uso do parâmetro de consulta `duleLabels`, onde os rótulos são fornecidos como uma lista de valores separados por vírgulas, como mostrado no exemplo abaixo.

**Formato da API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing associada à política de uso de dados que você está avaliando. |
| `{LABEL_1}` | Um rótulo de uso de dados para testar a ação de marketing. Pelo menos um rótulo deve ser fornecido. Ao fornecer vários rótulos, eles devem ser separados por vírgulas. |

**Solicitação**

A solicitação a seguir testa a ação de marketing `exportToThirdParty` em relação aos rótulos `C1` e `C3`. Como a política de uso de dados criada anteriormente neste tutorial define o rótulo `C1` como uma das condições `deny` em sua expressão de política, a ação de marketing deve acionar uma violação de política.

>[!NOTE]
>
>Os rótulos de uso de dados fazem distinção entre maiúsculas e minúsculas. Violações de política só ocorrem quando os rótulos definidos em suas expressões de política são correspondidos exatamente. Neste exemplo, um rótulo `C1` acionaria uma violação, enquanto um rótulo `c1` não.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o URL da ação de marketing, os rótulos de uso com os quais foi testado e uma lista de todas as políticas que foram violadas como resultado do teste da ação contra esses rótulos. Neste exemplo, a política &quot;Exportar dados para terceiros&quot; é mostrada na matriz `violatedPolicies`, indicando que a ação de marketing acionou a violação de política esperada.

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
| `violatedPolicies` | Uma matriz que lista todas as políticas que foram violadas pelo teste da ação de marketing (especificada em `marketingActionRef`) em relação ao `duleLabels` fornecido. |

## Avaliar usando conjuntos de dados

É possível avaliar uma política de uso de dados testando uma ação de marketing em relação a um ou mais conjuntos de dados a partir dos quais os rótulos podem ser coletados. Isso é feito fazendo uma solicitação POST para `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` e fornecendo IDs de conjuntos de dados no corpo da solicitação, conforme mostrado no exemplo abaixo.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing associada à política que você está avaliando. |

**Solicitação**

A solicitação a seguir testa a ação de marketing `exportToThirdParty` em relação a três conjuntos de dados diferentes. Os conjuntos de dados são referenciados por tipo e ID em uma matriz fornecida na carga.

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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Propriedade | Descrição |
| --- | --- |
| `entityType` | Cada item na matriz de carga deve indicar o tipo de entidade que está sendo definida. Para esse caso de uso, o valor sempre será &quot;dataSet&quot;. |
| `entityId` | Cada item na matriz de carga deve fornecer a ID exclusiva para um conjunto de dados. |
| `entityMeta.fields` | (Opcional) Uma matriz de cadeias de caracteres [JSON Pointer](../../landing/api-fundamentals.md#json-pointer), que fazem referência a campos específicos no esquema do conjunto de dados. Se essa matriz estiver incluída, somente os campos contidos na matriz participarão da avaliação. Nenhum campo de esquema incluído na matriz participará da avaliação.<br><br>Se esse campo não for incluído, todos os campos no esquema do conjunto de dados serão incluídos na avaliação. |

**Resposta**

Uma resposta bem-sucedida retorna o URL da ação de marketing, os rótulos de uso que foram coletados dos conjuntos de dados fornecidos e uma lista de todas as políticas que foram violadas como resultado do teste da ação contra esses rótulos. Neste exemplo, a política &quot;Exportar dados para terceiros&quot; é mostrada na matriz `violatedPolicies`, indicando que a ação de marketing acionou a violação de política esperada.

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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
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
| `duleLabels` | Uma lista de rótulos de uso de dados que foram extraídos dos conjuntos de dados fornecidos na carga da solicitação. |
| `discoveredLabels` | Uma lista dos conjuntos de dados que foram fornecidos na carga da solicitação, exibindo os rótulos a nível do conjunto de dados e a nível de campo que foram encontrados em cada um. |
| `violatedPolicies` | Uma matriz que lista todas as políticas que foram violadas pelo teste da ação de marketing (especificada em `marketingActionRef`) em relação ao `duleLabels` fornecido. |

## Próximas etapas

Ao ler este documento, você verificou com êxito violações de política ao executar uma ação de marketing em um conjunto de dados ou em um conjunto de rótulos de uso de dados. Usando os dados retornados nas respostas da API, você pode configurar protocolos no aplicativo de experiência para aplicar adequadamente as violações de política quando elas ocorrerem.

Para obter informações sobre como a Platform fornece automaticamente a imposição de políticas para segmentos ativados, consulte o guia em [imposição automática](./auto-enforcement.md).
