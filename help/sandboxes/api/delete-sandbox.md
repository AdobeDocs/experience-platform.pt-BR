---
keywords: Experience Platform, home, tópicos populares, excluir sandbox
solution: Experience Platform
title: Excluir uma sandbox na API
topic: guia do desenvolvedor
description: Você pode excluir uma sandbox fazendo uma solicitação de DELETE que inclui o nome da sandbox no caminho da solicitação.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---


# Excluir uma sandbox na API

Você pode excluir uma sandbox fazendo uma solicitação de DELETE que inclui o `name` da sandbox no caminho da solicitação.

>[!NOTE]
>
>Fazer essa chamada de API atualiza a propriedade `status` da sandbox para &quot;deletada&quot; e a desativa. As solicitações do GET ainda podem recuperar os detalhes da sandbox depois que ela for excluída.

**Formato da API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | O `name` da sandbox que você deseja excluir. |

**Solicitação**

A solicitação a seguir exclui uma sandbox chamada &quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes atualizados da sandbox, mostrando que seu `state` é &quot;excluído&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
