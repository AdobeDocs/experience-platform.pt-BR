---
keywords: Experience Platform;página inicial;tópicos populares;listar sandboxes
solution: Experience Platform
title: Ponto de acesso da API de tipos de sandbox
description: Você pode recuperar uma lista de tipos de sandbox compatíveis para sua organização fazendo uma solicitação GET para o endpoint /sandboxTypes.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# Ponto de extremidade de Tipos de sandbox

Você pode recuperar uma lista de tipos de sandbox compatíveis para sua organização fazendo uma solicitação GET para a `/sandboxTypes` terminal.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de tipos de sandbox compatíveis

Você pode recuperar uma lista de tipos de sandbox compatíveis para sua organização fazendo uma solicitação GET para a `/sandboxTypes` terminal.

**Formato da API**

```http
GET /sandboxTypes
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de tipos de sandbox compatíveis com sua organização.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
