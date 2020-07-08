---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Excluir uma caixa de proteção
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 4%

---


# Excluir uma caixa de proteção

Você pode excluir uma caixa de proteção fazendo uma solicitação DELETE que inclui a caixa de proteção `name` no caminho da solicitação.

>[!NOTE]
>
>Fazer esta chamada de API atualiza a propriedade da caixa de proteção para &quot; `status` excluída&quot; e a desativa. As solicitações GET ainda podem recuperar os detalhes da caixa de proteção após sua exclusão.

**Formato da API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A `name` da caixa de proteção que deseja excluir. |

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

Uma resposta bem-sucedida retorna os detalhes atualizados da caixa de proteção, mostrando que ela `state` é &quot;excluída&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
