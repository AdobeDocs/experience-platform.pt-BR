---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;política de uso de dados
solution: Experience Platform
title: Criar uma política de governança de dados na API
type: Tutorial
description: Saiba como criar uma política de governança de dados usando a API de serviço de política.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 3%

---

# Criar uma política de governança de dados na API

A [API de Serviço de Política](https://www.adobe.io/experience-platform-apis/references/policy-service/) permite criar e gerenciar políticas de governança de dados para determinar quais ações de marketing podem ser executadas em relação aos dados que contêm determinados rótulos de uso de dados.

Este documento fornece um tutorial passo a passo para a criação de uma política de governança usando a API [!DNL Policy Service].

>[!NOTE]
>
>Para obter etapas sobre como criar uma política de controle de acesso, consulte o manual do ponto de extremidade `/policies` para a [API de Controle de Acesso](../../access-control/abac/api/policies.md). Para saber como criar uma política de consentimento, consulte o [guia da interface do usuário de políticas](./user-guide.md#consent-policy).

## Introdução

Este tutorial requer um entendimento prático dos seguintes conceitos-chave envolvidos na criação e avaliação de políticas:

* [Governança de dados do Adobe Experience Platform](../home.md): a estrutura pela qual o [!DNL Experience Platform] impõe conformidade com o uso de dados.
   * [Rótulos de uso de dados](../labels/overview.md): os rótulos de uso de dados são aplicados aos campos de dados XDM, especificando restrições sobre como esses dados podem ser acessados.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API [!DNL Policy Service], incluindo os cabeçalhos necessários e como ler chamadas de exemplo de API.

## Definir uma ação de marketing {#define-action}

Na estrutura de Governança de dados, uma ação de marketing é uma ação que um consumidor de dados [!DNL Experience Platform] toma, para a qual é necessário verificar violações das políticas de uso de dados.

A primeira etapa na criação de uma política de uso de dados é determinar qual ação de marketing a política avaliará. Isso pode ser feito usando uma das seguintes opções:

* [Pesquisar uma ação de marketing existente](#look-up)
* [Criar uma nova ação de marketing](#create-new)

### Pesquisar uma ação de marketing existente {#look-up}

Você pode pesquisar ações de marketing existentes a serem avaliadas pela sua política fazendo uma solicitação GET para um dos endpoints do `/marketingActions`.

**Formato da API**

Dependendo de você estar pesquisando uma ação de marketing fornecida por [!DNL Experience Platform] ou uma ação de marketing personalizada criada por sua organização, use os pontos de extremidade `marketingActions/core` ou `marketingActions/custom`, respectivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitação**

A solicitação a seguir usa o ponto de extremidade `marketingActions/custom`, que busca uma lista de todas as ações de marketing definidas pela sua organização.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o número total de ações de marketing encontradas (`count`) e lista os detalhes das próprias ações de marketing na matriz `children`.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `_links.self.href` | Cada item na matriz `children` contém uma ID de URI para a ação de marketing listada. |

Quando você encontrar a ação de marketing que deseja usar, registre o valor da propriedade `href`. Este valor é usado durante a próxima etapa de [criação de uma política](#create-policy).

### Criar uma nova ação de marketing {#create-new}

Você pode criar uma nova ação de marketing fazendo uma solicitação PUT para o ponto de extremidade `/marketingActions/custom/` e fornecendo um nome para a ação de marketing no final do caminho da solicitação.

**Formato da API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da nova ação de marketing que você deseja criar. Esse nome atua como o identificador principal da ação de marketing e, portanto, deve ser exclusivo. A prática recomendada é dar à ação de marketing um nome descritivo, mas conciso. |

**Solicitação**

A solicitação a seguir cria uma nova ação de marketing personalizada chamada &quot;exportToThirdParty&quot;. Observe que `name` na carga da solicitação é o mesmo nome fornecido no caminho da solicitação.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da ação de marketing que você deseja criar. Esse nome deve corresponder ao nome fornecido no caminho da solicitação ou ocorrerá um erro 400 (Solicitação inválida). |
| `description` | Uma descrição legível da ação de marketing. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes da ação de marketing recém-criada.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `_links.self.href` | A ID de URI da ação de marketing. |

Registre a ID de URI da ação de marketing recém-criada, pois ela será usada na próxima etapa da criação de uma política.

## Criar uma política {#create-policy}

A criação de uma nova política exige que você forneça a ID de URI de uma ação de marketing com uma expressão dos rótulos de uso que proíbem essa ação de marketing.

Essa expressão é chamada de expressão de política e é um objeto que contém (A) um rótulo ou (B) um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política. Por exemplo, uma política relacionada à exportação de dados para terceiros pode ser proibida se `C1 OR (C3 AND C7)` rótulos estiverem presentes. Essa expressão seria especificada como:

```json
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
}
```

>[!NOTE]
>
>Somente os operadores OR e AND são suportados.

Depois de configurar sua expressão de política, você pode criar uma nova política fazendo uma solicitação POST para o ponto de extremidade `/policies/custom`.

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma política chamada &quot;Exportar dados para terceiros&quot; fornecendo uma ação de marketing e uma expressão de política na carga da solicitação.

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

| Propriedade | Descrição |
| --- | --- |
| `marketingActionRefs` | Uma matriz contendo o valor `href` de uma ação de marketing, obtido na [etapa anterior](#define-action). Embora o exemplo acima liste apenas uma ação de marketing, várias ações também podem ser fornecidas. |
| `deny` | O objeto de expressão de política. Define os rótulos e as condições de uso que fariam com que a política rejeitasse a ação de marketing referenciada em `marketingActionRefs`. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes da política recém-criada.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "imsOrg": "{ORG_ID}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | Um valor somente leitura gerado pelo sistema que identifica exclusivamente a política. |

Registre a ID de URI da política recém-criada, como ela é usada na próxima etapa para habilitar a política.

## Ativar a política

>[!NOTE]
>
>Embora esta etapa seja opcional se você quiser deixar sua política com o status `DRAFT`, observe que, por padrão, uma política deve ter seu status definido como `ENABLED` para participar da avaliação. Consulte o manual sobre [imposição de política](../enforcement/api-enforcement.md) para obter informações sobre como fazer exceções para políticas no status `DRAFT`.

Por padrão, as políticas que têm a propriedade `status` definida como `DRAFT` não participam da avaliação. Você pode habilitar sua política para avaliação fazendo uma solicitação PATCH para o ponto de extremidade `/policies/custom/` e fornecendo o identificador exclusivo para a política no final do caminho da solicitação.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O valor `id` da política que você deseja habilitar. |

**Solicitação**

A solicitação a seguir executa uma operação PATCH na propriedade `status` da política, alterando seu valor de `DRAFT` para `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Propriedade | Descrição |
| --- | --- |
| `op` | O tipo de operação do PATCH a ser executada. Esta solicitação executa uma operação de &quot;substituição&quot;. |
| `path` | O caminho para o campo a ser atualizado. Ao ativar uma política, o valor deve ser definido como &quot;/status&quot;. |
| `value` | O novo valor a ser atribuído à propriedade especificada em `path`. Esta solicitação define a propriedade `status` da política como &quot;ENABLED&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e os detalhes da política atualizada, com seu `status` agora definido como `ENABLED`.

```json
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
    "imsOrg": "{ORG_ID}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
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
```

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso uma política de uso de dados para uma ação de marketing. Agora você pode seguir para o tutorial em [aplicação de políticas de uso de dados](../enforcement/api-enforcement.md) para saber como verificar violações de política e lidar com elas no aplicativo de experiência.

Para obter mais informações sobre as diferentes operações disponíveis na API [!DNL Policy Service], consulte o [Guia do desenvolvedor do Serviço de Política](../api/getting-started.md). Para obter informações sobre como impor políticas para dados do [!DNL Real-Time Customer Profile], consulte o tutorial em [impor a conformidade do uso de dados para segmentos de público-alvo](../../segmentation/tutorials/governance.md).

Para saber como gerenciar políticas de uso na interface do usuário do [!DNL Experience Platform], consulte o [guia do usuário de políticas](user-guide.md).
