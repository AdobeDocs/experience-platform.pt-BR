---
keywords: Experience Platform, home, tópicos populares, sandbox
solution: Experience Platform
title: Criar uma sandbox na API
topic: developer guide
description: Você pode criar uma nova sandbox fazendo uma solicitação de POST ao endpoint `/sandboxes`.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---


# Criar uma sandbox na API

Você pode criar uma nova sandbox fazendo uma solicitação de POST para o endpoint `/sandboxes`.

**Formato da API**

```http
POST /sandboxes
```

**Solicitação**

A solicitação a seguir cria uma nova sandbox de desenvolvimento chamada &quot;dev-3&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O identificador que será usado para acessar a sandbox em solicitações futuras. Esse valor deve ser exclusivo, e a prática recomendada é torná-lo o mais descritivo possível. Não pode conter espaços ou letras maiúsculas. |
| `title` | Um nome legível usado para fins de exibição na interface do usuário da plataforma. |
| `type` | O tipo de sandbox a ser criado. Atualmente, apenas as sandboxes do tipo &quot;desenvolvimento&quot; podem ser criadas por uma organização. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox recém-criada, mostrando que seu `state` está &quot;criando&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>As sandboxes levam aproximadamente 15 minutos para serem provisionadas pelo sistema, depois elas `state` se tornarão &quot;ativas&quot; ou &quot;com falha&quot;.
