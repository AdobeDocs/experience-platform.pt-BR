---
keywords: Experience Platform;página inicial;tópicos populares;Imposição de política;Imposição baseada em API;governança de dados
solution: Experience Platform
title: Ponto de extremidade da API de políticas de governança de dados
description: As políticas de governança de dados são regras adotadas pela sua organização que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados no Experience Platform. O ponto de extremidade /policies é usado para todas as chamadas de API relacionadas à exibição, criação, atualização ou exclusão de políticas de governança de dados.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 3%

---

# Ponto de extremidade de políticas de governança de dados

As políticas de governança de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para realizar em dados dentro do [!DNL Experience Platform]. A variável `/policies` endpoint na variável [!DNL Policy Service API] O permite gerenciar programaticamente as políticas de governança de dados da sua organização.

>[!IMPORTANT]
>
>As políticas de governança não devem ser confundidas com as políticas de controle de acesso, que determinam os atributos de dados específicos que podem ser acessados por determinados usuários da Platform em sua organização. Consulte a `/policies` manual de endpoint para o [API de controle de acesso](../../access-control/abac/api/policies.md) para obter detalhes sobre como gerenciar programaticamente as políticas de controle de acesso.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, reveja o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Recuperar uma lista de políticas {#list}

Você pode listar todos `core` ou `custom` fazendo uma solicitação para GET `/policies/core` ou `/policies/custom`, respectivamente.

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

Uma resposta bem-sucedida inclui uma `children` que lista os detalhes de cada política recuperada, incluindo suas `id` valores. Você pode usar o `id` de uma política específica a ser executada [pesquisa](#lookup), [atualizar](#update), e [excluir](#delete) para essa política.

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
| `status` | O status atual de uma política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` políticas participam da avaliação. Consulte a visão geral em [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis a uma política. |
| `description` | Uma descrição opcional que fornece mais contexto para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada a uma política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Pesquisar uma política {#look-up}

É possível pesquisar uma política específica incluindo as `id` propriedade no caminho de uma solicitação GET.

**Formato da API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A variável `id` da política que você deseja pesquisar. |

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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` políticas participam da avaliação. Consulte a visão geral em [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. |
| `description` | Uma descrição opcional que fornece mais contexto para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Criar uma política personalizada {#create-policy}

No [!DNL Policy Service] , uma política é definida pelo seguinte:

* Uma referência a uma ação de marketing específica
* Uma expressão que descreve os rótulos de uso de dados nos quais a ação de marketing está restrita de ser executada

Para atender a esse último requisito, as definições de política devem incluir uma expressão booleana em relação à presença de rótulos de uso de dados. Essa expressão é chamada de expressão de política.

As expressões de política são fornecidas no formato de um `deny` em cada definição de política. Um exemplo de uma `deny` O objeto que verifica apenas a presença de um único rótulo seria semelhante ao seguinte:

```json
"deny": {
    "label": "C1"
}
```

No entanto, muitas políticas especificam condições mais complexas em relação à presença de rótulos de uso de dados. Para dar suporte a esses casos de uso, também é possível incluir operações booleanas para descrever suas expressões de política. O objeto de expressão de política deve conter um rótulo ou um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política.

Por exemplo, para definir uma política que proíba uma ação de marketing de ser executada em dados em que `C1 OR (C3 AND C7)` rótulos estiverem presentes, a política de `deny` A propriedade seria especificada como:

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
| `operator` | Indica a relação condicional entre os rótulos fornecidos no irmão `operands` matriz. Os valores aceitos são: <ul><li>`OR`: a expressão declara verdadeiro se qualquer um dos rótulos na `operands` estão presentes.</li><li>`AND`: a expressão somente resolverá como true se todos os rótulos na `operands` estão presentes.</li></ul> |
| `operands` | Uma matriz de objetos, com cada objeto representando um único rótulo ou um par adicional de `operator` e `operands` propriedades. A presença dos rótulos e/ou operações num `operands` A matriz resolve para verdadeiro ou falso com base no valor de seu irmão `operator` propriedade. |
| `label` | O nome de um único rótulo de uso de dados que se aplica à política. |

Você pode criar uma nova política personalizada fazendo uma solicitação POST para a `/policies/custom` terminal.

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma nova política que restringe a ação de marketing `exportToThirdParty` de ser executado em dados que contêm rótulos `C1 OR (C3 AND C7)`.

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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` políticas participam da avaliação. Consulte a visão geral em [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. O URI para uma ação de marketing é fornecido em `_links.self.href` na resposta a [pesquisar uma ação de marketing](./marketing-actions.md#look-up). |
| `description` | Uma descrição opcional que fornece mais contexto para o caso de uso da política. |
| `deny` | A expressão de política que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada à política está restrita de ser executada. |

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
>Você só pode atualizar políticas personalizadas. Se quiser ativar ou desativar as políticas principais, consulte a seção sobre [atualização da lista de políticas principais ativadas](#update-enabled-core).

Você pode atualizar uma política personalizada existente fornecendo a respectiva ID no caminho de uma solicitação PUT com uma carga que inclui a forma atualizada da política em sua totalidade. Em outras palavras, o pedido PUT reescreve essencialmente a política.

>[!NOTE]
>
>Consulte a seção sobre [atualização de uma parte de uma política personalizada](#patch) se você quiser atualizar apenas um ou mais campos de uma política, em vez de substituí-la.

**Formato da API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A variável `id` da política que você deseja atualizar. |

**Solicitação**

Neste exemplo, as condições para exportar dados para terceiros foram alteradas e agora é necessário ter a política criada para negar essa ação de marketing se `C1 AND C5` os rótulos de dados estão presentes.

A solicitação a seguir atualiza a política existente para incluir a nova expressão de política. Como essa solicitação reescreve essencialmente a política, todos os campos devem ser incluídos na carga, mesmo se alguns de seus valores não estiverem sendo atualizados.

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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`. Por padrão, somente `ENABLED` políticas participam da avaliação. Consulte a visão geral em [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. O URI para uma ação de marketing é fornecido em `_links.self.href` na resposta a [pesquisar uma ação de marketing](./marketing-actions.md#look-up). |
| `description` | Uma descrição opcional que fornece mais contexto para o caso de uso da política. |
| `deny` | A expressão de política que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

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
>Você só pode atualizar políticas personalizadas. Se quiser ativar ou desativar as políticas principais, consulte a seção sobre [atualização da lista de políticas principais ativadas](#update-enabled-core).

Uma parte específica de uma política pode ser atualizada usando uma solicitação PATCH. Diferentemente das solicitações PUT que reescrevem a política, as solicitações PATCH atualizam somente as propriedades especificadas no corpo da solicitação. Isso é especialmente útil quando você deseja ativar ou desativar uma política, pois só é necessário fornecer o caminho para a propriedade apropriada (`/status`) e seu valor (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>As cargas das solicitações PATCH seguem a formatação de patch JSON. Consulte a [Guia de fundamentos de API](../../landing/api-fundamentals.md) para obter mais informações sobre a sintaxe aceita.

A variável [!DNL Policy Service] A API oferece suporte às operações de patch de JSON `add`, `remove`, e `replace`, e permite combinar várias atualizações em uma única chamada, como mostrado no exemplo abaixo.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A variável `id` da política cujas propriedades você deseja atualizar. |

**Solicitação**

A solicitação a seguir usa dois `replace` operações para alterar o status da política de `DRAFT` para `ENABLED`e para atualizar a `description` com uma nova descrição.

>[!IMPORTANT]
>
>Ao enviar várias operações de PATCH em uma única solicitação, elas serão processadas na ordem em que aparecem na matriz. Verifique se você está enviando as solicitações na ordem correta, quando necessário.

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

É possível excluir uma política personalizada incluindo suas `id` no caminho de uma solicitação DELETE.

>[!WARNING]
>
>Após a exclusão, as políticas não poderão ser recuperadas. A prática recomendada é [executar uma solicitação de pesquisa (GET)](#lookup) primeiro, visualize a política e confirme se ela é a política correta que deseja remover.

**Formato da API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | A ID da política que você deseja excluir. |

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

Você pode confirmar a exclusão tentando pesquisar (GET) a política novamente. Você deverá receber um erro HTTP 404 (Não encontrado) se a política tiver sido excluída com sucesso.

## Recuperar uma lista de políticas principais habilitadas {#list-enabled-core}

Por padrão, somente as políticas de governança de dados habilitadas participam da avaliação. Você pode recuperar uma lista de políticas principais que estão atualmente habilitadas por sua organização fazendo uma solicitação GET para a `/enabledCorePolicies` terminal.

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

Uma resposta bem-sucedida retorna a lista de políticas principais habilitadas em um `policyIds` matriz.

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

## Atualizar a lista de políticas principais habilitadas {#update-enabled-core}

Por padrão, somente as políticas de governança de dados habilitadas participam da avaliação. Ao fazer uma solicitação PUT para o `/enabledCorePolicies` você pode atualizar a lista de políticas principais habilitadas para sua organização usando uma única chamada.

>[!NOTE]
>
>Somente as políticas principais podem ser habilitadas ou desabilitadas por este ponto de extremidade. Para ativar ou desativar políticas personalizadas, consulte a seção sobre [atualização de uma parte de uma política](#patch).

**Formato da API**

```http
PUT /enabledCorePolicies
```

**Solicitação**

A solicitação a seguir atualiza a lista de políticas principais habilitadas com base nas IDs fornecidas na carga.

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
| `policyIds` | Uma lista de IDs de política principais que devem ser habilitadas. Todas as políticas principais que não forem incluídas serão definidas como `DISABLED` status e não participarão da avaliação. |

**Resposta**

Uma resposta bem-sucedida retorna a lista atualizada de políticas principais habilitadas em um `policyIds` matriz.

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

Depois de definir novas políticas ou atualizar as existentes, você poderá usar o [!DNL Policy Service] API para testar ações de marketing em relação a rótulos ou conjuntos de dados específicos e ver se suas políticas estão gerando violações conforme esperado. Consulte o guia no [endpoints de avaliação de política](./evaluation.md) para obter mais informações.
