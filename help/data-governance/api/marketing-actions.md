---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ações de marketing
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# Ações de marketing

Uma ação de marketing, no contexto do Adobe Experience Platform Data Governance, é uma ação que um consumidor de [!DNL Experience Platform] dados toma, para a qual há necessidade de verificar violações das políticas de uso de dados.

Trabalhar com ações de marketing na API exige que você use o `/marketingActions` terminal.

## Lista de todas as ações de marketing

Para visualização de uma lista de todas as ações de marketing, é possível fazer uma solicitação GET para `/marketingActions/core` ou `/marketingActions/custom` que retorne todas as políticas para o container especificado.

**Formato da API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitação**

A solicitação a seguir retornará uma lista de todas as ações de marketing personalizadas definidas pela Organização IMS.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto response fornece o número total de ações de marketing no container (`count`) e a `children` matriz contém os detalhes de cada ação de marketing, incluindo o `name` e um `href` para a ação de marketing. Esse caminho (`_links.self.href`) é usado para concluir a `marketingActionsRefs` matriz ao [criar uma política](policies.md#create-policy)de uso de dados.

```JSON
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

## Pesquisar uma ação de marketing específica

Você também pode executar uma solicitação de pesquisa (GET) para visualização dos detalhes de uma ação de marketing específica. Isso é feito usando a ação `name` de marketing. Se o nome for desconhecido, ele poderá ser encontrado usando a solicitação de listagem (GET) mostrada anteriormente.

**Formato da API**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto response contém os detalhes da ação de marketing, incluindo o caminho (`_links.self.href`) necessário para fazer referência à ação de marketing ao definir uma política de uso de dados (`marketingActionsRefs`).

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

## Criar ou atualizar uma ação de marketing

A [!DNL Policy Service] API permite que você defina suas próprias ações de marketing, bem como atualize as existentes. A criação e atualização são feitas usando uma operação PUT para o nome da ação de marketing.

**Formato da API**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Solicitação**

Na solicitação a seguir, observe que a carga `name` na solicitação é a mesma da chamada `{marketingActionName}` da API. Ao contrário `id` de uma política que é somente leitura e gerada pelo sistema, a criação de uma ação de marketing exige que você forneça o nome _pretendido_ da ação de marketing à medida que ela é criada.

>[!NOTE]
>
>A falha ao fornecer o `{marketingActionName}` na chamada resultará em um erro 405 (método não permitido), pois você não tem permissão para executar uma PUT diretamente no `/marketingActions/custom` terminal. Além disso, se a carga `name` não corresponder à `{marketingActionName}` no caminho, você receberá um erro 400 (solicitação incorreta).

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Resposta**

Se criado com êxito, você receberá um Status HTTP 201 (Criado) e o corpo da resposta conterá os detalhes da ação de marketing recém-criada. A resposta `name` deve corresponder ao que foi enviado na solicitação.

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

## Excluir uma ação de marketing

É possível excluir ações de marketing enviando uma solicitação de DELETE para o site `{marketingActionName}` da ação de marketing que você deseja remover.

>[!NOTE]
>
>Não é possível excluir ações de marketing referenciadas por políticas existentes. Tentar fazer isso resultará em um erro 400 (solicitação incorreta) junto com uma mensagem de erro que inclui a `id` (ou várias IDs) de qualquer política (ou políticas) que contenha uma referência à ação de marketing que você está tentando excluir.

**Formato da API**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Solicitação**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Se a ação de marketing tiver sido excluída com êxito, o corpo da resposta ficará em branco com um Status HTTP 200 (OK).

Você pode confirmar a exclusão tentando pesquisar (GET) a ação de marketing. Você deve receber um status HTTP 404 (Não encontrado) juntamente com uma mensagem de erro &quot;Não encontrado&quot; porque a ação de marketing foi removida.
