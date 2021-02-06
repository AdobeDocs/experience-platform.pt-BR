---
keywords: Experience Platform;home;popular topics;delete sandbox
solution: Experience Platform
title: Excluir uma caixa de proteção na API
topic: developer guide
description: É possível excluir uma caixa de proteção fazendo uma solicitação de DELETE que inclua o nome da caixa de proteção no caminho da solicitação.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 3%

---


# Excluir uma caixa de proteção na API

É possível excluir uma caixa de proteção fazendo uma solicitação de DELETE que inclua `name` da caixa de proteção no caminho da solicitação.

>[!NOTE]
>
>Fazer essa chamada de API atualiza a propriedade `status` da caixa de proteção para &quot;deletada&quot; e a desativa. As solicitações do GET ainda podem recuperar os detalhes da caixa de proteção depois que ela for excluída.

**Formato da API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | O `name` da caixa de proteção que deseja excluir. |

**Solicitação**

A solicitação a seguir exclui uma caixa de proteção chamada &quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes atualizados da caixa de proteção, mostrando que seu `state` é &quot;excluído&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
