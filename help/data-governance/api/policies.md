---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas
topic: developer guide
translation-type: tm+mt
source-git-commit: 7bc7050d64727f09d3a13d803d532a9a3ba5d1a7
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 2%

---


# Ponto de extremidade de políticas

As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro de [!DNL Experience Platform]. O `/policies` endpoint no [!DNL Policy Service API] permite gerenciar programaticamente as políticas de uso de dados para sua organização.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, reveja o guia [de](getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Recuperar uma lista de políticas {#list}

Você pode lista todas `core` as políticas ou `custom` as políticas, fazendo uma solicitação de GET para `/policies/core` ou `/policies/custom`, respectivamente.

**Formato da API**

```http
GET /policies/core
GET /policies/custom
```

**Solicitação**

A solicitação a seguir recupera uma lista de políticas personalizadas definidas por sua organização.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida inclui uma `children` matriz que lista os detalhes de cada política recuperada, incluindo seus `id` valores. Você pode usar o `id` campo de uma política específica para executar [pesquisa](#lookup), [atualização](#update)e [excluir](#delete) solicitações para essa política.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| Propriedade | Descrição |
| --- | --- |
| `_page.count` | O número total de políticas recuperadas. |
| `name` | O nome de exibição de uma política. |
| `status` | O status atual de uma política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` as políticas participam da avaliação. Para obter mais informações, consulte a visão geral da avaliação [](../enforcement/overview.md) política. |
| `marketingActionRefs` | Um array que lista os URIs de todas as ações de marketing aplicáveis a uma política. |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos de uso de dados específicos nos quais uma ação de marketing associada a uma política está restrita a ser executada. Consulte a seção sobre como [criar uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Procurar uma política {#look-up}

Você pode procurar uma política específica incluindo a propriedade dessa política no caminho de uma solicitação de GET. `id`

**Formato da API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política que você quer procurar. |

**Solicitação**

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome de exibição da política. |
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` as políticas participam da avaliação. Para obter mais informações, consulte a visão geral da avaliação [](../enforcement/overview.md) política. |
| `marketingActionRefs` | Um array que lista os URIs de todas as ações de marketing aplicáveis à política. |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre como [criar uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Create a custom policy {#create-policy}

Na [!DNL Policy Service] API, uma política é definida pelo seguinte:

* Uma referência a uma ação de marketing específica
* Uma expressão que descreve os rótulos de uso de dados com os quais a ação de marketing está restrita a não ser executada em relação

Para atender ao último requisito, as definições de política devem incluir uma expressão booleana em relação à presença de rótulos de uso de dados. Esta expressão é chamada de expressão **** política.

Expressões de políticas são fornecidas na forma de uma `deny` propriedade dentro de cada definição de política. Um exemplo de um `deny` objeto simples que verifica apenas a presença de um único rótulo seria semelhante ao seguinte:

```json
"deny": {
    "label": "C1"
}
```

Entretanto, muitas políticas especificam condições mais complexas relacionadas à presença de rótulos de uso de dados. Para suportar esses casos de uso, você também pode incluir operações booleanas para descrever suas expressões de política. O objeto de expressão de política deve conter _uma etiqueta_ ou __ um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política.

Por exemplo, para definir uma política que proíbe que uma ação de marketing seja executada em dados onde `C1 OR (C3 AND C7)` os rótulos estão presentes, a propriedade da política `deny` será especificada como:

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `operator` | Indica a relação condicional entre os rótulos fornecidos na `operands` matriz irmão. Os valores aceitos são: <ul><li>`OR`: A expressão é resolvida como true se algum dos rótulos no `operands` storage estiver presente.</li><li>`AND`: A expressão só será resolvida como true se todos os rótulos na `operands` matriz estiverem presentes.</li></ul> |
| `operands` | Uma matriz de objetos, com cada objeto representando um único rótulo ou um par adicional de `operator` propriedades e `operands` propriedades. A presença dos rótulos e/ou das operações em um `operands` storage resolve para true ou false com base no valor de sua `operator` propriedade irmão. |
| `label` | O nome de um único rótulo de uso de dados que se aplica à política. |

Você pode criar uma nova política personalizada fazendo uma solicitação POST para o `/policies/custom` terminal.

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma nova política que impede que a ação de marketing seja executada `exportToThirdParty` em dados que contenham rótulos `C1 OR (C3 AND C7)`.

```sh
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome de exibição da política. |
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` as políticas participam da avaliação. Para obter mais informações, consulte a visão geral da avaliação [](../enforcement/overview.md) política. |
| `marketingActionRefs` | Um array que lista os URIs de todas as ações de marketing aplicáveis à política. O URI para uma ação de marketing é fornecido `_links.self.href` na resposta para [pesquisar uma ação](./marketing-actions.md#look-up)de marketing. |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | A expressão de política que descreve os rótulos de uso de dados específicos em que a ação de marketing associada à política está restrita de ser executada. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política recém-criada, incluindo sua `id`. Esse valor é somente leitura e é atribuído automaticamente quando a política é criada.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Atualizar uma política personalizada {#update}

>[!IMPORTANT]
>
>Você só pode atualizar políticas personalizadas. Se desejar ativar ou desativar as principais políticas, consulte a seção sobre como [atualizar a lista das principais políticas](#update-enabled-core)habilitadas.

É possível atualizar uma política personalizada existente fornecendo sua ID no caminho de uma solicitação de PUT com uma carga que inclui o formulário atualizado da política na sua totalidade. Por outras palavras, o pedido de PUT _reescreve_ essencialmente a política.

>[!NOTE]
>
>Consulte a seção sobre como [atualizar uma parte de uma política](#patch) personalizada se quiser apenas atualizar um ou mais campos para uma política, em vez de substituí-la.

**Formato da API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A `id` política que você deseja atualizar. |

**Solicitação**

Neste exemplo, as condições para exportar dados para terceiros foram alteradas e agora você precisa da política criada para negar essa ação de marketing se houver rótulos de `C1 AND C5` dados.

A solicitação a seguir atualiza a política existente para incluir a nova expressão de política. Observe que, como essa solicitação essencialmente regrava a política, todos os campos devem ser incluídos na carga, mesmo se alguns de seus valores não estiverem sendo atualizados.

```sh
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome de exibição da política. |
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` as políticas participam da avaliação. Para obter mais informações, consulte a visão geral da avaliação [](../enforcement/overview.md) política. |
| `marketingActionRefs` | Um array que lista os URIs de todas as ações de marketing aplicáveis à política. O URI para uma ação de marketing é fornecido `_links.self.href` na resposta para [pesquisar uma ação](./marketing-actions.md#look-up)de marketing. |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | A expressão de política que descreve os rótulos de uso de dados específicos em que a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre como [criar uma política](#create-policy) para obter mais informações sobre essa propriedade. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política atualizada.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Atualizar uma parte de uma política personalizada {#patch}

>[!IMPORTANT]
>
>Você só pode atualizar políticas personalizadas. Se desejar ativar ou desativar as principais políticas, consulte a seção sobre como [atualizar a lista das principais políticas](#update-enabled-core)habilitadas.

Uma parte específica de uma política pode ser atualizada usando uma solicitação de PATCH. Diferentemente das solicitações de PUT que regravam a política, as solicitações de PATCH atualizam somente as propriedades especificadas no corpo da solicitação. Isso é especialmente útil quando você deseja ativar ou desativar uma política, pois você só precisa fornecer o caminho para a propriedade (`/status`) apropriada e seu valor (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>As cargas para solicitações de PATCH seguem a formatação do patch JSON. Consulte o guia [de fundamentos da](../../landing/api-fundamentals.md) API para obter mais informações sobre a sintaxe aceita.

A [!DNL Policy Service] API suporta as operações de Patch JSON `add`, `remove`e `replace`, e permite combinar várias atualizações em uma única chamada, como mostrado no exemplo abaixo.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A `id` da política cujas propriedades você deseja atualizar. |

**Solicitação**

A solicitação a seguir usa duas `replace` operações para alterar o status da política de `DRAFT` para `ENABLED`e para atualizar o `description` campo com uma nova descrição.

>[!IMPORTANT]
>
>Ao enviar várias operações de PATCH em uma única solicitação, elas serão processadas na ordem em que aparecem no storage. Certifique-se de enviar as solicitações na ordem correta, onde necessário.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política atualizada.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Excluir uma política personalizada {#delete}

É possível excluir uma política personalizada incluindo-a `id` no caminho de uma solicitação de DELETE.

>[!WARNING]
>
>Depois de excluídas, as políticas não podem ser recuperadas. É prática recomendada [executar uma solicitação](#lookup) de pesquisa (GET) primeiro para visualização da política e confirmar se ela é a política correta que você deseja remover.

**Formato da API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A ID da política que você deseja excluir. |

**Solicitação**

```sh
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) com um corpo em branco.

Você pode confirmar a exclusão tentando pesquisar (GET) a política novamente. Você deve receber um erro HTTP 404 (Não encontrado) se a política tiver sido excluída com êxito.

## Recuperar uma lista de políticas principais ativadas {#list-enabled-core}

Por padrão, somente as políticas de uso de dados ativadas participam da avaliação. Você pode recuperar uma lista de políticas principais que estão ativadas atualmente pela sua organização, fazendo uma solicitação de GET para o `/enabledCorePolicies` endpoint.

**Formato da API**

```http
GET /enabledCorePolicies
```

**Solicitação**

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a lista de políticas principais ativadas em um `policyIds` storage.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Atualizar a lista das políticas principais ativadas {#update-enabled-core}

Por padrão, somente as políticas de uso de dados ativadas participam da avaliação. Ao fazer uma solicitação de PUT para o `/enabledCorePolicies` endpoint, você pode atualizar a lista de políticas principais habilitadas para sua organização usando uma única chamada.

>[!NOTE]
>
>Somente as políticas principais podem ser ativadas ou desativadas por esse terminal. Para ativar ou desativar políticas personalizadas, consulte a seção sobre como [atualizar uma parte de uma política](#patch).

**Formato da API**

```http
PUT /enabledCorePolicies
```

**Solicitação**

A solicitação a seguir atualiza a lista das políticas principais ativadas com base nas IDs fornecidas na carga.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `policyIds` | Uma lista de IDs de política principais que devem ser ativadas. Quaisquer políticas principais que não estejam incluídas estão definidas como `DISABLED` status e não participarão na avaliação. |

**Resposta**

Uma resposta bem-sucedida retorna a lista atualizada das políticas principais ativadas em um `policyIds` storage.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Próximas etapas

Depois de definir novas políticas ou atualizar as existentes, você pode usar a [!DNL Policy Service] API para testar ações de marketing em relação a rótulos ou conjuntos de dados específicos e verificar se suas políticas estão gerando violações conforme esperado. Consulte o guia sobre os pontos finais [de avaliação de](./evaluation.md) políticas para obter mais informações.