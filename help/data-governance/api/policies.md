---
keywords: Experience Platform, home, tópicos populares, imposição de políticas, aplicação baseada em API, controle de dados
solution: Experience Platform
title: Endpoint da API de políticas
topic-legacy: developer guide
description: As políticas de uso de dados são regras adotadas por sua organização que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito, executando em dados no Experience Platform. O endpoint /Policies é usado para todas as chamadas de API relacionadas à exibição, criação, atualização ou exclusão das políticas de uso de dados.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 3%

---

# Ponto de extremidade de políticas

As políticas de uso de dados são regras que descrevem os tipos de ações de marketing das quais você tem permissão para ou tem restrição para executar em dados dentro de [!DNL Experience Platform]. O `/policies` endpoint no [!DNL Policy Service API] O permite gerenciar programaticamente as políticas de uso de dados da sua organização.

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, reveja o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Recuperar uma lista de políticas {#list}

Você pode listar tudo `core` ou `custom` , fazendo uma solicitação GET para `/policies/core` ou `/policies/custom`, respectivamente.

**Formato da API**

```http
GET /policies/core
GET /policies/custom
```

**Solicitação**

A solicitação a seguir recupera uma lista de políticas personalizadas definidas por sua organização.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida inclui uma `children` matriz que lista os detalhes de cada política recuperada, incluindo seus `id` valores. Você pode usar o `id` de uma determinada política [pesquisa](#lookup), [atualizar](#update)e [excluir](#delete) solicitações para essa política.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `status` | O status atual de uma política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` As políticas participam na avaliação. Consulte a visão geral em [avaliação política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis de uma política. |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos específicos de uso de dados em que a ação de marketing associada a uma política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Procurar uma política {#look-up}

Você pode procurar uma política específica incluindo o `id` no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política que você quer procurar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` As políticas participam na avaliação. Consulte a visão geral em [avaliação política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos específicos de uso de dados em que a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Criar uma política personalizada {#create-policy}

No [!DNL Policy Service] Uma política é definida pela seguinte API:

* Uma referência a uma ação de marketing específica
* Uma expressão que descreve os rótulos de uso de dados com os quais a ação de marketing está restrita de ser executada.

Para atender ao último requisito, as definições de política devem incluir uma expressão booleana em relação à presença de rótulos de uso de dados. Essa expressão é chamada de expressão de política.

As expressões de política são fornecidas na forma de um `deny` dentro de cada definição de política. Um exemplo de um `deny` que verifica apenas a presença de um único rótulo seria semelhante ao seguinte:

```json
"deny": {
    "label": "C1"
}
```

No entanto, muitas políticas especificam condições mais complexas relacionadas à presença de rótulos de uso de dados. Para suportar esses casos de uso, também é possível incluir operações booleanas para descrever suas expressões de política. O objeto de expressão de política deve conter um rótulo ou um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política.

Por exemplo, para definir uma política que proíbe que uma ação de marketing seja executada em dados em que `C1 OR (C3 AND C7)` os rótulos estão presentes, a política `deny` seria especificada como:

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
| `operator` | Indica a relação condicional entre os rótulos fornecidos no irmão `operands` matriz. Os valores aceitos são: <ul><li>`OR`: A expressão resolverá como true se qualquer um dos rótulos no `operands` estão presentes.</li><li>`AND`: A expressão só resolverá para verdadeiro se todos os rótulos na variável `operands` estão presentes.</li></ul> |
| `operands` | Uma matriz de objetos, com cada objeto representando um único rótulo ou um par adicional de `operator` e `operands` propriedades. A presença de rótulos e/ou operações em um `operands` O array resolve para true ou false com base no valor de seu irmão `operator` propriedade. |
| `label` | O nome de um único rótulo de uso de dados que se aplica à política. |

Você pode criar uma nova política personalizada fazendo uma solicitação de POST para a `/policies/custom` endpoint .

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma nova política que restringe a ação de marketing `exportToThirdParty` de ser executado em dados contendo rótulos `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` As políticas participam na avaliação. Consulte a visão geral em [avaliação política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. O URI de uma ação de marketing é fornecido em `_links.self.href` na resposta a [pesquisa de uma ação de marketing](./marketing-actions.md#look-up). |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | A expressão de política que descreve os rótulos específicos de uso de dados em que a ação de marketing associada à política está restrita de ser executada. |

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
    "imsOrg": "{ORG_ID}",
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
>Você só pode atualizar políticas personalizadas. Se desejar ativar ou desativar as políticas principais, consulte a seção em [atualização da lista de políticas principais ativadas](#update-enabled-core).

Você pode atualizar uma política personalizada existente fornecendo sua ID no caminho de uma solicitação de PUT com uma carga que inclui o formulário atualizado da política em sua totalidade. Por outras palavras, o pedido de PUT reescreve essencialmente a política.

>[!NOTE]
>
>Consulte a seção sobre [atualização de uma parte de uma política personalizada](#patch) se quiser atualizar apenas um ou mais campos de uma política, em vez de substituí-los.

**Formato da API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política que deseja atualizar. |

**Solicitação**

Neste exemplo, as condições para exportar dados para terceiros foram alteradas e agora você precisa da política criada para negar essa ação de marketing se `C1 AND C5` os rótulos de dados estão presentes.

A solicitação a seguir atualiza a política existente para incluir a nova expressão de política. Observe que, como essa solicitação essencialmente reescreve a política, todos os campos devem ser incluídos na carga, mesmo que alguns de seus valores não estejam sendo atualizados.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` As políticas participam na avaliação. Consulte a visão geral em [avaliação política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. O URI de uma ação de marketing é fornecido em `_links.self.href` na resposta a [pesquisa de uma ação de marketing](./marketing-actions.md#look-up). |
| `description` | Uma descrição opcional que fornece contexto adicional para o caso de uso da política. |
| `deny` | A expressão de política que descreve os rótulos específicos de uso de dados em que a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

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
    "imsOrg": "{ORG_ID}",
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
>Você só pode atualizar políticas personalizadas. Se desejar ativar ou desativar as políticas principais, consulte a seção em [atualização da lista de políticas principais ativadas](#update-enabled-core).

Uma parte específica de uma política pode ser atualizada usando uma solicitação de PATCH. Ao contrário das solicitações de PUT que reescrevem a política, as solicitações de PATCH atualizam somente as propriedades especificadas no corpo da solicitação. Isso é especialmente útil quando você deseja habilitar ou desabilitar uma política, pois você só precisa fornecer o caminho para a propriedade apropriada (`/status`) e seu valor (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>As cargas para solicitações de PATCH seguem a formatação do patch JSON. Consulte a [Guia de fundamentos da API](../../landing/api-fundamentals.md) para obter mais informações sobre a sintaxe aceita.

O [!DNL Policy Service] A API suporta as operações de patch JSON `add`, `remove`e `replace`e permite combinar várias atualizações em uma única chamada, como mostrado no exemplo abaixo.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política cujas propriedades você deseja atualizar. |

**Solicitação**

A solicitação a seguir usa dois `replace` operações para alterar o status da política de `DRAFT` para `ENABLED`e para atualizar o `description` com uma nova descrição.

>[!IMPORTANT]
>
>Ao enviar várias operações do PATCH em uma única solicitação, elas serão processadas na ordem em que aparecem no storage. Certifique-se de enviar as solicitações na ordem correta, onde necessário.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Você pode excluir uma política personalizada incluindo sua `id` no caminho de uma solicitação de DELETE.

>[!WARNING]
>
>Depois de excluídas, as políticas não podem ser recuperadas. A prática recomendada é [executar uma solicitação de pesquisa (GET)](#lookup) primeiro, para visualizar a política e confirmar que é a política correta que você deseja remover.

**Formato da API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A ID da política que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) com um corpo em branco.

Você pode confirmar a exclusão tentando pesquisar (GET) a política novamente. Você deve receber um erro HTTP 404 (Not Found) se a política tiver sido excluída com êxito.

## Recuperar uma lista de políticas principais ativadas {#list-enabled-core}

Por padrão, somente as políticas de uso de dados ativadas participam da avaliação. Você pode recuperar uma lista de políticas principais que estão habilitadas atualmente pela organização, fazendo uma solicitação do GET para a `/enabledCorePolicies` endpoint .

**Formato da API**

```http
GET /enabledCorePolicies
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a lista de políticas principais ativadas em uma `policyIds` matriz.

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
  "imsOrg": "{ORG_ID}",
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

## Atualizar a lista de políticas principais ativadas {#update-enabled-core}

Por padrão, somente as políticas de uso de dados ativadas participam da avaliação. Ao fazer uma solicitação de PUT para a `/enabledCorePolicies` endpoint , é possível atualizar a lista de políticas principais habilitadas para sua organização usando uma única chamada .

>[!NOTE]
>
>Somente as políticas principais podem ser ativadas ou desativadas por este ponto de extremidade. Para ativar ou desativar políticas personalizadas, consulte a seção em [atualização de uma parte de uma política](#patch).

**Formato da API**

```http
PUT /enabledCorePolicies
```

**Solicitação**

A solicitação a seguir atualiza a lista de políticas principais ativadas com base nas IDs fornecidas no payload.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `policyIds` | Uma lista de IDs de política principais que devem ser ativadas. Quaisquer políticas principais não incluídas são definidas como `DISABLED` e não participará na avaliação. |

**Resposta**

Uma resposta bem-sucedida retorna a lista atualizada de políticas principais ativadas em uma `policyIds` matriz.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
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

Depois de definir novas políticas ou atualizar as existentes, você pode usar a variável [!DNL Policy Service] API para testar ações de marketing em rótulos ou conjuntos de dados específicos e ver se suas políticas estão gerando violações conforme esperado. Consulte o guia sobre [endpoints de avaliação de política](./evaluation.md) para obter mais informações.
