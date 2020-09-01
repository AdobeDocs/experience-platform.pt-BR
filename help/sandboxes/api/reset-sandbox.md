---
keywords: Experience Platform;home;popular topics;reset sandbox
solution: Experience Platform
title: Redefinir uma caixa de proteção
topic: developer guide
description: As caixas de proteção de desenvolvimento têm um recurso de "redefinição de fábrica" que exclui todos os recursos não padrão de uma caixa de proteção. É possível redefinir uma caixa de proteção fazendo uma solicitação de PUT que inclua o nome da caixa de proteção no caminho da solicitação.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---


# Redefinir uma caixa de proteção

As caixas de proteção de desenvolvimento têm um recurso de &quot;redefinição de fábrica&quot; que exclui todos os recursos não padrão de uma caixa de proteção. É possível redefinir uma caixa de proteção fazendo uma solicitação de PUT que inclua a caixa de proteção `name` no caminho da solicitação.

**Formato da API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A `name` propriedade da caixa de proteção que você deseja redefinir. |

**Solicitação**

A solicitação a seguir redefine uma caixa de proteção chamada &quot;dev-2&quot;.

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
| `action` | Esse parâmetro deve ser fornecido na carga da solicitação com um valor de &quot;reset&quot; para redefinir a caixa de proteção. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da caixa de proteção atualizada, mostrando que ela `state` está &quot;redefinindo&quot;.

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
>Quando uma caixa de proteção é redefinida, o sistema demora aproximadamente 15 minutos para ser provisionado. Depois de provisionada, a caixa de proteção `state` se torna &quot;ativa&quot; ou &quot;falhou&quot;.