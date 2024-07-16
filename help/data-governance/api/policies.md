---
keywords: Experience Platform;página inicial;tópicos populares;Imposição de política;Imposição baseada em API;governança de dados
solution: Experience Platform
title: Ponto de extremidade da API de políticas de governança de dados
description: As políticas de governança de dados são regras adotadas pela sua organização que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados no Experience Platform. O ponto de extremidade /policies é usado para todas as chamadas de API relacionadas à exibição, criação, atualização ou exclusão de políticas de governança de dados.
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 3%

---

# Ponto de extremidade de políticas de governança de dados

As políticas de governança de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados no [!DNL Experience Platform]. O ponto de extremidade `/policies` no [!DNL Policy Service API] permite gerenciar programaticamente as políticas de governança de dados da sua organização.

>[!IMPORTANT]
>
>As políticas de governança não devem ser confundidas com as políticas de controle de acesso, que determinam os atributos de dados específicos que podem ser acessados por determinados usuários da Platform em sua organização. Consulte o manual de ponto de extremidade `/policies` da [API de Controle de Acesso](../../access-control/abac/api/policies.md) para obter detalhes sobre como gerenciar programaticamente as políticas de controle de acesso.

## Introdução

O ponto de extremidade de API usado neste guia faz parte da [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Recuperar uma lista de políticas {#list}

Você pode listar todas as políticas de `core` ou `custom` fazendo uma solicitação GET para `/policies/core` ou `/policies/custom`, respectivamente.

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

Uma resposta bem-sucedida inclui uma matriz `children` que lista os detalhes de cada política recuperada, incluindo seus valores `id`. Você pode usar o campo `id` de uma política específica para executar solicitações de [pesquisa](#lookup), [atualização](#update) e [exclusão](#delete) para essa política.

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
| `status` | O status atual de uma política. Há três status possíveis: `DRAFT`, `ENABLED` ou `DISABLED`. Por padrão, apenas `ENABLED` políticas participam da avaliação. Consulte a visão geral na [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis a uma política. |
| `description` | Uma descrição opcional que fornece mais contexto para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada a uma política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Pesquisar uma política {#look-up}

Você pode pesquisar uma política específica incluindo a propriedade `id` dessa política no caminho de uma solicitação GET.

**Formato da API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política que você deseja pesquisar. |

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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED` ou `DISABLED`. Por padrão, apenas `ENABLED` políticas participam da avaliação. Consulte a visão geral na [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. |
| `description` | Uma descrição opcional que fornece mais contexto para o caso de uso da política. |
| `deny` | Um objeto que descreve os rótulos de uso de dados específicos nos quais a ação de marketing associada à política está restrita de ser executada. Consulte a seção sobre [criação de uma política](#create-policy) para obter mais informações sobre essa propriedade. |

## Criar uma política personalizada {#create-policy}

Na API [!DNL Policy Service], uma política é definida pelo seguinte:

* Uma referência a uma ação de marketing específica
* Uma expressão que descreve os rótulos de uso de dados nos quais a ação de marketing está restrita de ser executada

Para atender a esse último requisito, as definições de política devem incluir uma expressão booleana em relação à presença de rótulos de uso de dados. Essa expressão é chamada de expressão de política.

As expressões de política são fornecidas na forma de uma propriedade `deny` em cada definição de política. Um exemplo de um objeto `deny` simples que verifica apenas a presença de um único rótulo seria semelhante ao seguinte:

```json
"deny": {
    "label": "C1"
}
```

No entanto, muitas políticas especificam condições mais complexas em relação à presença de rótulos de uso de dados. Para dar suporte a esses casos de uso, também é possível incluir operações booleanas para descrever suas expressões de política. O objeto de expressão de política deve conter um rótulo ou um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política.

Por exemplo, para definir uma política que proíba uma ação de marketing de ser executada em dados nos quais os rótulos `C1 OR (C3 AND C7)` estão presentes, a propriedade `deny` da política seria especificada como:

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
| `operator` | Indica a relação condicional entre os rótulos fornecidos na matriz irmã `operands`. Os valores aceitos são: <ul><li>`OR`: a expressão é resolvida como verdadeira se qualquer um dos rótulos na matriz `operands` estiver presente.</li><li>`AND`: a expressão somente será resolvida como verdadeira se todos os rótulos na matriz `operands` estiverem presentes.</li></ul> |
| `operands` | Uma matriz de objetos, com cada objeto representando um único rótulo ou um par adicional de propriedades `operator` e `operands`. A presença dos rótulos e/ou operações em uma matriz `operands` é resolvida como verdadeira ou falsa com base no valor de sua propriedade irmã `operator`. |
| `label` | O nome de um único rótulo de uso de dados que se aplica à política. |

Você pode criar uma nova política personalizada fazendo uma solicitação POST para o ponto de extremidade `/policies/custom`.

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma nova política que impede a ação de marketing `exportToThirdParty` de ser executada em dados que contêm rótulos `C1 OR (C3 AND C7)`.

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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED` ou `DISABLED`. Por padrão, apenas `ENABLED` políticas participam da avaliação. Consulte a visão geral na [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. O URI de uma ação de marketing é fornecido em `_links.self.href` na resposta para [procurar uma ação de marketing](./marketing-actions.md#look-up). |
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
>Você só pode atualizar políticas personalizadas. Se quiser habilitar ou desabilitar as políticas principais, consulte a seção sobre [atualização da lista de políticas principais habilitadas](#update-enabled-core).

Você pode atualizar uma política personalizada existente fornecendo a respectiva ID no caminho de uma solicitação PUT com uma carga que inclui a forma atualizada da política em sua totalidade. Em outras palavras, o pedido PUT reescreve essencialmente a política.

>[!NOTE]
>
>Consulte a seção sobre [atualização de uma parte de uma política personalizada](#patch) se desejar atualizar apenas um ou mais campos de uma política, em vez de substituí-la.

**Formato da API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política que você deseja atualizar. |

**Solicitação**

Neste exemplo, as condições para exportar dados para terceiros foram alteradas e agora você precisa da política criada para negar essa ação de marketing se `C1 AND C5` rótulos de dados estiverem presentes.

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
| `status` | O status atual da política. Há três status possíveis: `DRAFT`, `ENABLED` ou `DISABLED`. Por padrão, apenas `ENABLED` políticas participam da avaliação. Consulte a visão geral na [avaliação de política](../enforcement/overview.md) para obter mais informações. |
| `marketingActionRefs` | Uma matriz que lista os URIs de todas as ações de marketing aplicáveis à política. O URI de uma ação de marketing é fornecido em `_links.self.href` na resposta para [procurar uma ação de marketing](./marketing-actions.md#look-up). |
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
>Você só pode atualizar políticas personalizadas. Se quiser habilitar ou desabilitar as políticas principais, consulte a seção sobre [atualização da lista de políticas principais habilitadas](#update-enabled-core).

Uma parte específica de uma política pode ser atualizada usando uma solicitação PATCH. Diferentemente das solicitações PUT que reescrevem a política, as solicitações PATCH atualizam somente as propriedades especificadas no corpo da solicitação. Isso é especialmente útil quando você deseja habilitar ou desabilitar uma política, pois você só precisa fornecer o caminho para a propriedade apropriada (`/status`) e seu valor (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>As cargas das solicitações PATCH seguem a formatação de patch JSON. Consulte o [guia de fundamentos de API](../../landing/api-fundamentals.md) para obter mais informações sobre a sintaxe aceita.

A API [!DNL Policy Service] é compatível com as operações de patch de JSON `add`, `remove` e `replace` e permite combinar várias atualizações em uma única chamada, como mostrado no exemplo abaixo.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política cujas propriedades você deseja atualizar. |

**Solicitação**

A solicitação a seguir usa duas operações `replace` para alterar o status da política de `DRAFT` para `ENABLED` e atualizar o campo `description` com uma nova descrição.

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

Você pode excluir uma política personalizada incluindo seu `id` no caminho de uma solicitação DELETE.

>[!WARNING]
>
>Após a exclusão, as políticas não poderão ser recuperadas. É prática recomendada [executar uma solicitação de pesquisa (GET)](#lookup) primeiro para exibir a política e confirmar se ela é a política correta que você deseja remover.

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

Por padrão, somente as políticas de governança de dados habilitadas participam da avaliação. Você pode recuperar uma lista de políticas principais que estão habilitadas por sua organização fazendo uma solicitação GET para o ponto de extremidade `/enabledCorePolicies`.

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

Uma resposta bem-sucedida retorna a lista de políticas principais habilitadas em uma matriz `policyIds`.

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

Por padrão, somente as políticas de governança de dados habilitadas participam da avaliação. Ao fazer uma solicitação PUT para o ponto de extremidade `/enabledCorePolicies`, você pode atualizar a lista de políticas principais habilitadas para sua organização usando uma única chamada.

>[!NOTE]
>
>Somente as políticas principais podem ser habilitadas ou desabilitadas por este ponto de extremidade. Para habilitar ou desabilitar políticas personalizadas, consulte a seção sobre [atualização de uma parte de uma política](#patch).

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
| `policyIds` | Uma lista de IDs de política principais que devem ser habilitadas. As políticas principais que não forem incluídas serão definidas com o status `DISABLED` e não participarão da avaliação. |

**Resposta**

Uma resposta bem-sucedida retorna a lista atualizada de políticas principais habilitadas em uma matriz `policyIds`.

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

Depois de definir novas políticas ou atualizar as existentes, você pode usar a API [!DNL Policy Service] para testar ações de marketing em rótulos ou conjuntos de dados específicos e ver se as políticas estão gerando violações conforme esperado. Consulte o manual nos [pontos de extremidade de avaliação de política](./evaluation.md) para obter mais informações.
