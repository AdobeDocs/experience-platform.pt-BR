---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar uma política de uso de dados
topic: policies
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 2%

---


# Criar uma política de uso de dados na API

O DULE (Data Usage Labeling and Implementation, Rotulação e Aplicação de Uso de Dados) é o mecanismo principal do Adobe Experience Platform [!DNL Data Governance]. A API [do serviço de política](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE permite que você crie e gerencie políticas DULE para determinar quais ações de marketing podem ser tomadas em relação aos dados que contêm determinados rótulos DULE.

Este documento fornece um tutorial passo a passo para a criação de uma política DULE usando a [!DNL Policy Service] API. Para obter um guia mais abrangente das diferentes operações disponíveis na API, consulte o guia [do desenvolvedor do Serviço de](../api/getting-started.md)política.

## Introdução

Este tutorial requer um entendimento prático dos seguintes conceitos chave envolvidos na criação e avaliação de políticas DULE:

* [!DNL Data Governance](../home.md): A estrutura pela qual [!DNL Platform] aplica a conformidade de uso de dados.
* [Rótulos](../labels/overview.md)de uso de dados: Os rótulos de uso de dados são aplicados aos campos de dados XDM, especificando restrições para como esses dados podem ser acessados.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.
* [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

Antes de iniciar este tutorial, reveja o guia [do](../api/getting-started.md) [!DNL Policy Service] desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API DULE, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Definir uma ação de marketing {#define-action}

No [!DNL Data Governance] quadro, uma ação de marketing é uma ação que um consumidor de [!DNL Experience Platform] dados toma, para a qual há necessidade de verificar violações das políticas de uso de dados.

A primeira etapa na criação de uma política DULE é determinar que ação de marketing a política avaliará. Isso pode ser feito usando uma das seguintes opções:

* [Pesquisar uma ação de marketing existente](#look-up)
* [Criar uma nova ação de marketing](#create-new)

### Pesquisar uma ação de marketing existente {#look-up}

Você pode pesquisar ações de marketing existentes a serem avaliadas pela sua política de DULE, fazendo uma solicitação GET para um dos `/marketingActions` pontos finais.

**Formato da API**

Dependendo de se você estiver pesquisando uma ação de marketing fornecida por [!DNL Experience Platform] ou uma ação de marketing personalizada criada por sua organização, use os pontos de extremidade `marketingActions/core` ou `marketingActions/custom` , respectivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitação**

A solicitação a seguir usa o `marketingActions/custom` endpoint, que busca uma lista de todas as ações de marketing definidas pela Organização IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o número total de ações de marketing encontradas (`count`) e lista os detalhes das próprias ações de marketing dentro do `children` storage.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `_links.self.href` | Cada item na `children` matriz contém uma ID de URI para a ação de marketing listada. |

Quando você encontrar a ação de marketing que deseja usar, registre o valor de sua `href` propriedade. Esse valor é usado durante a próxima etapa da [criação de uma política](#create-policy)DULE.

### Criar uma nova ação de marketing {#create-new}

Você pode criar uma nova ação de marketing fazendo uma solicitação PUT ao ponto de `/marketingActions/custom/` extremidade e fornecendo um nome para a ação de marketing no final do caminho da solicitação.

**Formato da API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da nova ação de marketing que você deseja criar. Esse nome atua como o identificador principal da ação de marketing e, portanto, deve ser exclusivo. A prática recomendada é dar à ação de marketing um nome descritivo, mas conciso. |

**Solicitação**

A solicitação a seguir cria uma nova ação de marketing personalizada chamada &quot;exportToThirdParty&quot;. Observe que a carga `name` na solicitação é igual ao nome fornecido no caminho da solicitação.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da ação de marketing que você deseja criar. Esse nome deve corresponder ao nome fornecido no caminho da solicitação ou um erro 400 (solicitação incorreta) ocorrerá. |
| `description` | Uma descrição legível da ação de marketing. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes da ação de marketing recém-criada.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
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

Registre a ID de URI da ação de marketing recém-criada, pois ela será usada na próxima etapa da criação de uma política DULE.

## Criar uma política DULE {#create-policy}

A criação de uma nova política exige que você forneça a ID de URI de uma ação de marketing com uma expressão dos rótulos DULE que proíbem essa ação de marketing.

Essa expressão é chamada de expressão **de** política e é um objeto que contém (A) uma etiqueta DULE ou (B) um operador e operandos, mas não ambos. Por sua vez, cada operando também é um objeto de expressão de política. Por exemplo, uma política relacionada à exportação de dados para terceiros pode ser proibida se `C1 OR (C3 AND C7)` houver etiquetas. Essa expressão seria especificada como:

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
>Somente operadores OR e AND são suportados.

Depois de configurar sua expressão de política, você pode criar uma nova política de DULE, fazendo uma solicitação POST para o `/policies/custom` ponto de extremidade.

**Formato da API**

```http
POST /policies/custom
```

**Solicitação**

A solicitação a seguir cria uma política DULE chamada &quot;Exportar dados para terceiros&quot;, fornecendo uma ação de marketing e uma expressão de política na carga da solicitação.

```shell
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

| Propriedade | Descrição |
| --- | --- |
| `marketingActionRefs` | Uma matriz contendo o `href` valor de uma ação de marketing, obtida na etapa [](#define-action)anterior. Enquanto o exemplo acima lista apenas uma ação de marketing, várias ações também podem ser fornecidas. |
| `deny` | O objeto de expressão de política. Define os rótulos e as condições DULE que fazem com que a política rejeite a ação de marketing mencionada em `marketingActionRefs`. |

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
    "imsOrg": "{IMS_ORG}",
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
| `id` | Um valor somente leitura gerado pelo sistema que identifica exclusivamente a política DULE. |

Registre a ID de URI da política DULE recém-criada, como ela é usada na próxima etapa para habilitar a política.

## Ativar a política DULE

>[!NOTE]
>
>Embora esta etapa seja opcional se você deseja deixar sua política DULE em `DRAFT` status, observe que por padrão uma política deve ter seu status definido como `ENABLED` para participar da avaliação. Consulte o tutorial sobre como [aplicar políticas](../enforcement/api-enforcement.md) DULE para obter informações sobre como fazer exceções para políticas em `DRAFT` status.

Por padrão, as políticas DULE que têm sua `status` propriedade definida para `DRAFT` não participam da avaliação. Você pode habilitar sua política para avaliação fazendo uma solicitação PATCH para o `/policies/custom/` ponto de extremidade e fornecendo o identificador exclusivo da política no final do caminho da solicitação.

**Formato da API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{POLICY_ID}` | O `id` valor da política que você deseja ativar. |

**Solicitação**

A solicitação a seguir executa uma operação PATCH na `status` propriedade da política DULE, alterando seu valor de `DRAFT` para `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | O tipo de operação PATCH a ser executada. Esta solicitação executa uma operação de &quot;substituição&quot;. |
| `path` | O caminho para o campo a ser atualizado. Ao ativar uma política, o valor deve ser definido como &quot;/status&quot;. |
| `value` | O novo valor a ser atribuído à propriedade especificada em `path`. Esta solicitação define a propriedade da política como &quot; `status` ATIVADO&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e os detalhes da política atualizada, com sua definição `status` agora definida como `ENABLED`.

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
    "imsOrg": "{IMS_ORG}",
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

Ao seguir este tutorial, você criou com êxito uma política de uso de dados para uma ação de marketing. Agora você pode continuar com o tutorial sobre como [impor políticas](../enforcement/api-enforcement.md) de uso de dados para saber como verificar violações de política e lidar com elas no aplicativo de experiência.

Para obter mais informações sobre as diferentes operações disponíveis na [!DNL Policy Service] API, consulte o guia [do desenvolvedor do](../api/getting-started.md)Policy Service. Para obter informações sobre como aplicar políticas para [!DNL Real-time Customer Profile] dados, consulte o tutorial sobre como [impor a conformidade de uso de dados para segmentos](../../segmentation/tutorials/governance.md)de audiência.

Para saber como gerenciar políticas de uso na interface do [!DNL Experience Platform] usuário, consulte o guia [do usuário da](user-guide.md)política.