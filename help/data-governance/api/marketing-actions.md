---
keywords: Experience Platform, home, tópicos populares, aplicação de políticas, api de ações de marketing, aplicação baseada em API, controle de dados
solution: Experience Platform
title: Endpoint da API de ações de marketing
topic-legacy: developer guide
description: Uma ação de marketing, no contexto da Governança de dados do Adobe Experience Platform, é uma ação que um consumidor de dados do Experience Platform toma, para a qual é necessário verificar violações das políticas de uso de dados.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---

# Ponto de extremidade de ações de marketing

Uma ação de marketing, no contexto do Adobe Experience Platform [!DNL Data Governance], é uma ação que um [!DNL Experience Platform] consumidor de dados toma, para a qual há necessidade de verificar violações das políticas de uso de dados.

Você pode gerenciar ações de marketing de sua organização usando o terminal `/marketingActions` na API do Serviço de política .

## Introdução

Os endpoints de API usados neste guia fazem parte da [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API [!DNL Experience Platform].

## Recupere uma lista de ações de marketing {#list}

Você pode recuperar uma lista de ações de marketing principais ou personalizadas fazendo uma solicitação do GET para `/marketingActions/core` ou `/marketingActions/custom`, respectivamente.

**Formato da API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitação**

A solicitação a seguir recupera uma lista de ações de marketing personalizadas mantidas por sua organização.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes de cada ação de marketing recuperada, incluindo seus `name` e `href`. O valor `href` é usado para identificar a ação de marketing ao [criar uma política de uso de dados](policies.md#create-policy).

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `name` | O nome da ação de marketing, que atua como seu identificador exclusivo ao [pesquisar uma ação de marketing específica](#lookup). |
| `_links.self.href` | Uma referência de URI para a ação de marketing, que pode ser usada para concluir a matriz `marketingActionsRefs` ao [criar uma política de uso de dados](policies.md#create-policy). |

## Procure uma ação de marketing específica {#lookup}

Você pesquisa os detalhes de uma ação de marketing específica ao incluir a propriedade `name` da ação de marketing no caminho de uma solicitação de GET.

**Formato da API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | A propriedade `name` da ação de marketing que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera uma ação de marketing personalizada chamada `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto de resposta contém os detalhes da ação de marketing, incluindo o caminho (`_links.self.href`) necessário para fazer referência à ação de marketing ao [definir uma política de uso de dados](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
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

Você pode criar uma nova ação de marketing personalizada ou atualizar uma existente, incluindo o nome existente ou pretendido da ação de marketing no caminho de uma solicitação de PUT.

**Formato da API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing a ser criada ou atualizada. Se uma ação de marketing com o nome fornecido já existir no sistema, essa ação de marketing será atualizada. Se não existir, uma nova ação de marketing será criada para o nome fornecido. |

**Solicitação**

A solicitação a seguir cria uma nova ação de marketing chamada `crossSiteTargeting`, desde que uma ação de marketing com o mesmo nome ainda não exista no sistema. Se uma ação de marketing `crossSiteTargeting` não existir, essa chamada atualizará essa ação de marketing com base nas propriedades fornecidas na carga.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da ação de marketing a ser criada ou atualizada. <br><br>**IMPORTANTE**: Essa propriedade deve corresponder ao  `{MARKETING_ACTION_NAME}` no caminho, caso contrário, ocorrerá um erro HTTP 400 (Solicitação incorreta). Em outras palavras, depois que uma ação de marketing é criada, sua propriedade `name` não pode ser alterada. |
| `description` | Uma descrição opcional para fornecer um contexto adicional para a ação de marketing. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da ação de marketing. Se uma ação de marketing existente foi atualizada, a resposta retorna o status HTTP 200 (OK). Se uma nova ação de marketing foi criada, a resposta retorna o status HTTP 201 (Created).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
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

Você pode excluir uma ação de marketing personalizada incluindo seu nome no caminho de uma solicitação de DELETE.

>[!NOTE]
>
>As ações de marketing referenciadas por políticas existentes não podem ser excluídas. Tentar excluir uma dessas ações de marketing resultará em um erro HTTP 400 (Solicitação inválida) junto com uma mensagem que inclui as IDs de todas as políticas que fazem referência à ação de marketing.

**Formato da API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 200 (OK) com um corpo de resposta em branco.

Você pode confirmar a exclusão tentando [pesquisar a ação de marketing](#look-up). Você deve receber um erro HTTP 404 (Not Found) se a ação de marketing tiver sido removida do sistema.
