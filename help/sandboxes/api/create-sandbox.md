---
keywords: Experience Platform, home, tópicos populares, sandbox
solution: Experience Platform
title: Criar uma sandbox na API
topic: guia do desenvolvedor
description: Você pode criar uma nova sandbox fazendo uma solicitação de POST ao endpoint `/sandboxes`.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 2%

---


# Criar uma sandbox na API

Você pode criar uma sandbox de desenvolvimento ou produção, fazendo uma solicitação de POST para o endpoint `/sandboxes`.

## Criar uma sandbox de desenvolvimento

Para criar uma sandbox de desenvolvimento, faça uma solicitação de POST ao endpoint `/sandboxes` e forneça o valor `development` para a propriedade `type`.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O identificador que será usado para acessar a sandbox em solicitações futuras. Esse valor deve ser exclusivo, e a prática recomendada é torná-lo o mais descritivo possível. Esse valor não pode conter espaços ou caracteres especiais. |
| `title` | Um nome legível usado para fins de exibição na interface do usuário da plataforma. |
| `type` | O tipo de sandbox a ser criado. O valor da propriedade `type` pode ser desenvolvimento ou produção. |

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

## Criar uma sandbox de produção

>[!NOTE]
>
>O recurso Várias sandboxes de produção está na versão beta.

Para criar uma sandbox de produção, faça uma solicitação de POST ao endpoint `/sandboxes` e forneça o valor `production` para a propriedade `type`.

**Formato da API**

```http
POST /sandboxes
```

**Solicitação**

A solicitação a seguir cria uma nova sandbox de produção chamada &quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O identificador que será usado para acessar a sandbox em solicitações futuras. Esse valor deve ser exclusivo, e a prática recomendada é torná-lo o mais descritivo possível. Esse valor não pode conter espaços ou caracteres especiais. |
| `title` | Um nome legível usado para fins de exibição na interface do usuário da plataforma. |
| `type` | O tipo de sandbox a ser criado. O valor da propriedade `type` pode ser desenvolvimento ou produção. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox recém-criada, mostrando que seu `state` está &quot;criando&quot;.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
