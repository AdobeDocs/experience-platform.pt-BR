---
keywords: Experience Platform, home, tópicos populares, governança de dados, política de uso de dados
solution: Experience Platform
title: Criar uma política de uso de dados na API
topic-legacy: policies
type: Tutorial
description: A API de serviço de política permite criar e gerenciar políticas de uso de dados para determinar quais ações de marketing podem ser realizadas em relação aos dados que contêm determinados rótulos de uso de dados. Este documento fornece um tutorial passo a passo para a criação de uma política usando a API do serviço de política.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 2%

---

# Criar uma política de uso de dados na API

O [API do serviço de política](https://www.adobe.io/experience-platform-apis/references/policy-service/) O permite criar e gerenciar políticas de uso de dados para determinar quais ações de marketing podem ser tomadas em relação aos dados que contêm determinados rótulos de uso de dados.

Este documento fornece um tutorial passo a passo para a criação de uma política usando o [!DNL Policy Service] API. Para obter um guia mais abrangente sobre as diferentes operações disponíveis na API, consulte o [Guia do desenvolvedor do Serviço de políticas](../api/getting-started.md).

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes conceitos-chave envolvidos na criação e avaliação de políticas:

* [Governança de dados do Adobe Experience Platform](../home.md): A estrutura pela qual [!DNL Platform] aplica a conformidade do uso de dados.
   * [Rótulos de uso de dados](../labels/overview.md): Os rótulos de uso de dados são aplicados aos campos de dados XDM, especificando restrições de como esses dados podem ser acessados.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para o [!DNL Policy Service] API, incluindo cabeçalhos obrigatórios e como ler chamadas de API de exemplo.

## Definir uma ação de marketing {#define-action}

Na estrutura de Governança de dados, uma ação de marketing é uma ação que [!DNL Experience Platform] são necessárias para o consumidor de dados, para o que é necessário verificar violações das políticas de uso de dados.

A primeira etapa na criação de uma política de uso de dados é determinar qual ação de marketing a política avaliará. Isso pode ser feito usando uma das seguintes opções:

* [Pesquisar uma ação de marketing existente](#look-up)
* [Criar uma nova ação de marketing](#create-new)

### Pesquisar uma ação de marketing existente {#look-up}

Você pode procurar ações de marketing existentes para serem avaliadas por sua política, fazendo uma solicitação do GET para uma das `/marketingActions` endpoints.

**Formato da API**

Dependendo de você estar procurando uma ação de marketing fornecida pelo [!DNL Experience Platform] ou uma ação de marketing personalizada criada por sua organização, use a variável `marketingActions/core` ou `marketingActions/custom` endpoints, respectivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitação**

A solicitação a seguir usa o `marketingActions/custom` endpoint, que obtém uma lista de todas as ações de marketing definidas pela organização IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o número total de ações de marketing encontradas (`count`) e lista os detalhes das próprias ações de marketing na `children` matriz.

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
| `_links.self.href` | Cada item dentro da variável `children` contém uma ID de URI para a ação de marketing listada. |

Ao encontrar a ação de marketing que deseja usar, registre o valor de suas `href` propriedade. Esse valor é usado durante a próxima etapa de [criação de uma política](#create-policy).

### Criar uma nova ação de marketing {#create-new}

Você pode criar uma nova ação de marketing fazendo uma solicitação de PUT para a variável `/marketingActions/custom/` endpoint e fornecer um nome para a ação de marketing no final do caminho da solicitação.

**Formato da API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da nova ação de marketing que deseja criar. Esse nome atua como o identificador principal da ação de marketing e, portanto, deve ser exclusivo. A prática recomendada é dar à ação de marketing um nome descritivo, mas conciso. |

**Solicitação**

A solicitação a seguir cria uma nova ação de marketing personalizada chamada &quot;exportToThirdParty&quot;. Observe que a variável `name` na carga da solicitação é o mesmo que o nome fornecido no caminho da solicitação.

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
| `name` | O nome da ação de marketing que deseja criar. Esse nome deve corresponder ao nome fornecido no caminho da solicitação ou ocorrerá um erro 400 (Solicitação inválida). |
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
| `_links.self.href` | A ID do URI da ação de marketing. |

Registre a ID do URI da ação de marketing recém-criada, pois ela será usada na próxima etapa da criação de uma política.

## Criar uma política {#create-policy}

A criação de uma nova política exige que você forneça a ID de URI de uma ação de marketing com uma expressão dos rótulos de uso que proíbem essa ação de marketing.

Essa expressão é chamada de expressão de política e é um objeto que contém (A) um rótulo ou (B) um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política. Por exemplo, uma política relacionada à exportação de dados para terceiros pode ser proibida se `C1 OR (C3 AND C7)` estão presentes. Essa expressão seria especificada como:

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
>Somente operadores OR e AND são compatíveis.

Após configurar a expressão de política, é possível criar uma nova política, fazendo uma solicitação de POST para a `/policies/custom` endpoint .

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma política chamada &quot;Exportar dados para terceiros&quot; ao fornecer uma ação de marketing e uma expressão de política na carga da solicitação.

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
| `marketingActionRefs` | Uma matriz contendo o `href` valor de uma ação de marketing, obtido na variável [etapa anterior](#define-action). Embora o exemplo acima liste apenas uma ação de marketing, várias ações também podem ser fornecidas. |
| `deny` | O objeto de expressão de política. Define os rótulos e as condições de uso que fariam com que a política rejeitasse a ação de marketing referenciada em `marketingActionRefs`. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Created) e os detalhes da política recém-criada.

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

Registre a ID do URI da política recém-criada, como ela é usada na próxima etapa para habilitar a política.

## Ativar a política

>[!NOTE]
>
>Embora esta etapa seja opcional se você quiser deixar sua política em `DRAFT` , observe que por padrão, uma política deve ter seu status definido como `ENABLED` para participar na avaliação. Consulte o guia sobre [aplicação da política](../enforcement/api-enforcement.md) para obter informações sobre como fazer exceções para políticas em `DRAFT` status.

Por padrão, as políticas que têm `status` propriedade definida como `DRAFT` não participar na avaliação. Você pode habilitar sua política para avaliação fazendo uma solicitação PATCH para a variável `/policies/custom/` endpoint e fornecendo o identificador exclusivo para a política no final do caminho da solicitação.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` da política que deseja ativar. |

**Solicitação**

A solicitação a seguir executa uma operação PATCH no `status` da política, alterando seu valor de `DRAFT` para `ENABLED`.

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
| `op` | O tipo de operação PATCH a ser executada. Essa solicitação executa uma operação de &quot;substituição&quot;. |
| `path` | O caminho para o campo a ser atualizado. Ao habilitar uma política, o valor deve ser definido como &quot;/status&quot;. |
| `value` | O novo valor a ser atribuído à propriedade especificada em `path`. Esta solicitação define o `status` para &quot;ENABLED&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e os detalhes da política atualizada, com sua `status` agora definido como `ENABLED`.

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

Ao seguir este tutorial, você criou com êxito uma política de uso de dados para uma ação de marketing. Agora você pode continuar para o tutorial em [aplicação de políticas de uso de dados](../enforcement/api-enforcement.md) para saber como verificar violações de política e lidar com elas no aplicativo de experiência.

Para obter mais informações sobre as diferentes operações disponíveis no [!DNL Policy Service] API, consulte o [Guia do desenvolvedor do Serviço de políticas](../api/getting-started.md). Para obter informações sobre como aplicar políticas de [!DNL Real-time Customer Profile] dados, consulte o tutorial em [impor a conformidade do uso de dados para segmentos de público-alvo](../../segmentation/tutorials/governance.md).

Para saber como gerenciar políticas de uso na [!DNL Experience Platform] interface do usuário, consulte a [guia do usuário de política](user-guide.md).
