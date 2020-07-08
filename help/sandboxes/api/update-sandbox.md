---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Atualizar uma caixa de proteção
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 4%

---


# Atualizar uma caixa de proteção

Você pode atualizar um ou mais campos em uma caixa de proteção, fazendo uma solicitação PATCH que inclui os da caixa de proteção `name` no caminho da solicitação e a propriedade a ser atualizada na carga da solicitação.

>[!NOTE]
>
>Atualmente, apenas a propriedade de uma caixa de proteção pode ser atualizada. `title`

**Formato da API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A `name` propriedade da caixa de proteção que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza a `title` propriedade da caixa de proteção chamada &quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) com os detalhes da caixa de proteção recém-atualizada.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
