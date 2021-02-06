---
keywords: Experience Platform;home;popular topics;Sandbox;sandbox
solution: Experience Platform
title: Criar uma caixa de proteção na API
topic: developer guide
description: Você pode criar uma nova caixa de proteção fazendo uma solicitação de POST para o ponto de extremidade '/sandboxes'.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---


# Criar uma caixa de proteção na API

Você pode criar uma nova caixa de proteção, fazendo uma solicitação POST para o ponto de extremidade `/sandboxes`.

**Formato da API**

```http
POST /sandboxes
```

**Solicitação**

A solicitação a seguir cria uma nova caixa de proteção de desenvolvimento chamada &quot;dev-3&quot;.

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
| `name` | O identificador que será usado para acessar a caixa de proteção em solicitações futuras. Esse valor deve ser exclusivo e a prática recomendada é torná-lo o mais descritivo possível. Não pode conter espaços nem letras maiúsculas. |
| `title` | Um nome legível para humanos usado para fins de exibição na interface do usuário da plataforma. |
| `type` | O tipo de caixa de proteção a ser criada. Atualmente, somente as caixas de proteção do tipo &quot;desenvolvimento&quot; podem ser criadas por uma organização. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da caixa de proteção recém-criada, mostrando que seu `state` está &quot;criando&quot;.

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
>As caixas de proteção levam aproximadamente 15 minutos para serem provisionadas pelo sistema, após o que seus `state` se tornarão &quot;ativos&quot; ou &quot;falharam&quot;.
