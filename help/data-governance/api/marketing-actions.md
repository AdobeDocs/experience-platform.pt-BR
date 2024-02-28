---
keywords: Experience Platform;página inicial;tópicos populares;Imposição de política;api de ações de marketing;Imposição baseada em API;governança de dados
solution: Experience Platform
title: Endpoint da API de ações de marketing
description: Uma ação de marketing, no contexto da Governança de dados da Adobe Experience Platform, é uma ação que um consumidor de dados de Experience Platform toma, para a qual é necessário verificar violações das políticas de uso de dados.
role: Developer
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 3%

---

# Endpoint de ações de marketing

Uma ação de marketing, no contexto da Governança de dados do Adobe Experience Platform, é uma ação que [!DNL Experience Platform] o consumidor de dados utiliza, para o qual há a necessidade de verificar violações das políticas de uso de dados.

É possível gerenciar ações de marketing para sua organização usando o `/marketingActions` ponto de extremidade na API do Serviço de política.

## Introdução

Os endpoints de API usados neste guia fazem parte da [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Recuperar uma lista de ações de marketing {#list}

GET Você pode recuperar uma lista de ações de marketing principais ou personalizadas fazendo uma solicitação para `/marketingActions/core` ou `/marketingActions/custom`, respectivamente.

**Formato da API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitação**

A solicitação a seguir recupera uma lista de ações de marketing personalizadas mantidas pela sua organização.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes de cada ação de marketing recuperada, incluindo sua `name` e `href`. A variável `href` é usado para identificar a ação de marketing quando [criação de uma política de uso de dados](policies.md#create-policy).

```json
{
    "_page": {
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `_page.count` | O número total de ações de marketing retornadas. |
| `children` | Uma matriz de objetos que contém os detalhes das ações de marketing recuperadas. |
| `name` | O nome da ação de marketing, que atua como seu identificador exclusivo quando [procurar uma ação de marketing específica](#lookup). |
| `_links.self.href` | Uma referência de URI para a ação de marketing, que pode ser usada para concluir a `marketingActionsRefs` matriz quando [criação de uma política de uso de dados](policies.md#create-policy). |

## Pesquisar uma ação de marketing específica {#lookup}

Você pesquisa os detalhes de uma ação de marketing específica incluindo as ações de marketing `name` propriedade no caminho de uma solicitação GET.

**Formato da API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | A variável `name` propriedade da ação de marketing que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera uma ação de marketing personalizada chamada `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto de resposta contém os detalhes da ação de marketing, incluindo o caminho (`_links.self.href`) necessário para fazer referência à ação de marketing quando [definição de uma política de uso de dados](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Criar ou atualizar uma ação de marketing personalizada {#create-update}

Você pode criar uma nova ação de marketing personalizada ou atualizar uma existente, incluindo o nome existente ou pretendido da ação de marketing no caminho de uma solicitação PUT.

**Formato da API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing a ser criada ou atualizada. Se uma ação de marketing com o nome fornecido já existir no sistema, essa ação de marketing será atualizada. Se não existir, uma nova ação de marketing será criada para o nome fornecido. |

**Solicitação**

A solicitação a seguir cria uma nova ação de marketing chamada `crossSiteTargeting`, desde que uma ação de marketing com o mesmo nome ainda não exista no sistema. Se um `crossSiteTargeting` Caso a ação de marketing exista, essa chamada atualizará a ação de marketing com base nas propriedades fornecidas na carga.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da ação de marketing a ser criada ou atualizada. <br><br>**IMPORTANTE**: esta propriedade deve corresponder ao `{MARKETING_ACTION_NAME}` no caminho, caso contrário, ocorrerá um erro HTTP 400 (Solicitação inválida). Em outras palavras, uma vez criada uma ação de marketing, sua `name` não é possível alterar a propriedade. |
| `description` | Uma descrição opcional para fornecer mais contexto para a ação de marketing. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da ação de marketing. Se uma ação de marketing existente foi atualizada, a resposta retorna o status HTTP 200 (OK). Se uma nova ação de marketing foi criada, a resposta retorna o status HTTP 201 (Criado).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Excluir uma ação de marketing personalizada {#delete}

Você pode excluir uma ação de marketing personalizada incluindo o nome dela no caminho de uma solicitação DELETE.

>[!NOTE]
>
>As ações de marketing referenciadas pelas políticas existentes não podem ser excluídas. Tentar excluir uma dessas ações de marketing resultará em um erro HTTP 400 (Solicitação inválida) junto com uma mensagem que inclui as IDs de todas as políticas que fazem referência à ação de marketing.

**Formato da API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 200 (OK) com um corpo de resposta em branco.

Você pode confirmar a exclusão tentando [pesquisar a ação de marketing](#look-up). Você deverá receber um erro HTTP 404 (Não encontrado) se a ação de marketing tiver sido removida do sistema.
