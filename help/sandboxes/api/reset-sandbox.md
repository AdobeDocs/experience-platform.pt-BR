---
keywords: Experience Platform, home, tópicos populares, redefinir sandbox
solution: Experience Platform
title: Redefinir uma sandbox na API
topic-legacy: developer guide
description: As sandboxes de desenvolvimento têm um recurso de "redefinição de fábrica" que exclui todos os recursos não padrão de uma sandbox. Você pode redefinir uma sandbox fazendo uma solicitação de PUT que inclui o nome da sandbox no caminho da solicitação.
exl-id: 3a82735d-a043-4fe4-9042-1eb373748d35
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 3%

---

# Redefinir uma sandbox na API

As sandboxes de desenvolvimento têm um recurso de &quot;redefinição de fábrica&quot; que exclui todos os recursos não padrão de uma sandbox. Você pode redefinir uma sandbox fazendo uma solicitação de PUT que inclui o `name` da sandbox no caminho da solicitação.

**Formato da API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja redefinir. |

**Solicitação**

A solicitação a seguir redefine uma sandbox chamada &quot;dev-2&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `action` | Esse parâmetro deve ser fornecido na carga da solicitação com um valor de &quot;redefinir&quot; para redefinir a sandbox. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox atualizada, mostrando que seu `state` é uma &quot;redefinição&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Depois que uma sandbox é redefinida, leva aproximadamente 15 minutos para ser provisionada pelo sistema. Depois de provisionado, o `state` da sandbox torna-se &quot;ativo&quot; ou &quot;falhou&quot;.
