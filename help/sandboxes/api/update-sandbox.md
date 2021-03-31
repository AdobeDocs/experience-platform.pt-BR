---
keywords: Experience Platform, home, tópicos populares, atualizar sandbox
solution: Experience Platform
title: Atualizar uma sandbox na API
topic: guia do desenvolvedor
description: Você pode atualizar um ou mais campos em uma sandbox fazendo uma solicitação de PATCH que inclui o nome da sandbox no caminho da solicitação e a propriedade a ser atualizada no payload da solicitação.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# Atualizar uma sandbox na API

Você pode atualizar um ou mais campos em uma sandbox fazendo uma solicitação de PATCH que inclui o sandbox `name` no caminho da solicitação e a propriedade a ser atualizada no payload da solicitação.

>[!NOTE]
>
>Atualmente, somente a propriedade `title` de uma sandbox pode ser atualizada.

**Formato da API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza a propriedade `title` da sandbox chamada &quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) com os detalhes da sandbox recém-atualizada.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
