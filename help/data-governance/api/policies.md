---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas
topic: developer guide
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---


# Políticas

As políticas de uso de dados são regras adotadas por sua organização que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro de [!DNL Experience Platform]você.

O `/policies` terminal é usado para todas as chamadas de API relacionadas à exibição, criação, atualização ou exclusão de políticas de uso de dados.

## Lista de todas as políticas

Para visualização de uma lista de políticas, uma solicitação de GET pode ser feita para `/policies/core` ou `/policies/custom` que retorna todas as políticas para o container especificado.

**Formato da API**

```http
GET /policies/core
GET /policies/custom
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui uma &quot;contagem&quot; que mostra o número total de políticas dentro do container especificado, bem como os detalhes de cada política, incluindo sua política `id`. O `id` campo é usado para executar solicitações de pesquisa para visualização de políticas específicas, bem como para executar operações de atualização e exclusão.

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## Procurar uma política

Cada política contém um `id` campo que pode ser usado para solicitar os detalhes de uma política específica. Se o conteúdo `id` de uma política for desconhecido, poderá ser encontrado usando a solicitação de listagem (GET) para lista de todas as políticas dentro de um container específico (`core` ou `custom`), conforme mostrado na etapa anterior.

**Formato da API**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta contém os detalhes da política, incluindo campos chave como `id` (esse campo deve corresponder ao `id` enviado na solicitação), `name`, `status`e `description`, bem como um link de referência para a ação de marketing em que a política se baseia (`marketingActionRefs`).

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Criar uma política {#create-policy}

A criação de uma política requer a inclusão de uma ação de marketing com uma expressão dos rótulos DULE que proíbem essa ação de marketing. As definições de política devem incluir uma `deny` propriedade, que é uma expressão booleana em relação à presença de rótulos DULE.

Essa expressão é chamada de e é um objeto que contém `PolicyExpression` uma etiqueta _ou_ __ um operador e operandos, mas não ambos. Por sua vez, cada operando também é um `PolicyExpression` objeto. Por exemplo, uma política relacionada à exportação de dados para terceiros pode ser proibida se `C1 OR (C3 AND C7)` houver etiquetas. Essa expressão seria especificada como:

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

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

```SHELL
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
          "../marketingActions/custom/exportToThirdParty"
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

**Resposta**

Se criado com êxito, você receberá um Status HTTP 201 (Criado) e o corpo da resposta conterá os detalhes da política recém-criada, incluindo sua `id`. Esse valor é somente leitura e é atribuído automaticamente quando a política é criada.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Atualizar uma política

Talvez seja necessário atualizar uma política de uso de dados após sua criação. Isso é feito por meio de uma solicitação PUT à política `id` com uma carga que inclui a forma atualizada da política, em sua totalidade. Por outras palavras, o pedido de PUT está essencialmente a _reescrever_ a política, pelo que o organismo deve incluir todas as informações necessárias, como mostra o exemplo abaixo.

**Formato da API**

```http
PUT /policies/custom/{id}
```

**Solicitação**

Neste exemplo, as condições para exportar dados para terceiros foram alteradas e agora você precisa da política criada para negar essa ação de marketing se houver rótulos de `C1 AND (C3 OR C7)` dados. Você usaria a chamada a seguir para atualizar a política existente.

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Resposta**

Uma solicitação de atualização bem-sucedida retorna um Status HTTP 200 (OK) e o corpo da resposta mostrará a política atualizada. A solicitação `id` deve corresponder à `id` enviada.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Atualizar uma parte de uma política

Uma parte específica de uma política pode ser atualizada usando uma solicitação de PATCH. Diferentemente das solicitações de PUT que _reescrevem_ a política, as solicitações de PATCH atualizam somente o caminho especificado no corpo da solicitação. Isso é especialmente útil quando você deseja ativar ou desativar uma política, pois é necessário enviar apenas o caminho específico que deseja atualizar (`/status`) e seu valor (`ENABLE` ou `DISABLE`).

A [!DNL Policy Service] API suporta atualmente operações de PATCH &quot;add&quot;, &quot;replace&quot; e &quot;remove&quot; e permite combinar várias atualizações em uma única chamada adicionando cada uma como um objeto dentro da matriz, como mostrado nos exemplos a seguir.

**Formato da API**

```http
PATCH /policies/custom/{id}
```

**Solicitação**

Neste exemplo, estamos usando a operação &quot;substituir&quot; para alterar o status da política de &quot;RASCUNHO&quot; para &quot;ATIVADO&quot; e atualizar o campo de descrição com uma nova descrição. Também poderíamos ter atualizado o campo de descrição usando a operação &quot;excluir&quot; para remover a descrição da política e, em seguida, usando a operação &quot;adicionar&quot; para adicionar uma nova vez, assim:

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

Ao enviar várias operações de PATCH em uma única solicitação, lembre-se de que elas serão processadas na ordem em que aparecem no storage, portanto, verifique se você está enviando as solicitações na ordem correta, onde necessário.

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

Uma solicitação de atualização bem-sucedida retornará um Status HTTP 200 (OK) e o corpo da resposta mostrará a política atualizada (&quot;status&quot; agora é &quot;ENABLED&quot; e &quot;descrição&quot; foi alterada). A política `id` deve corresponder à `id` enviada na solicitação.


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Excluir uma política

Se for necessário remover uma política que você criou, é possível fazer isso emitindo uma solicitação de DELETE para a política que deseja excluir. `id` É prática recomendada executar uma solicitação de pesquisa (GET) primeiro para visualização da política e confirmar se ela é a política correta que você deseja remover. **Depois de excluídas, as políticas não podem ser recuperadas.**

**Formato da API**

```http
DELETE /policies/custom/{id}
```

**Solicitação**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Se a política tiver sido excluída com êxito, o corpo da resposta ficará em branco com um Status HTTP 200 (OK).

Você pode confirmar a exclusão tentando pesquisar (GET) a política novamente. Você deve receber um Status HTTP 404 (Não encontrado) juntamente com uma mensagem de erro &quot;Não encontrado&quot; porque a política foi removida.
