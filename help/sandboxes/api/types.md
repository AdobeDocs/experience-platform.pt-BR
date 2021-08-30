---
keywords: Experience Platform, home, tópicos populares, sandboxes de lista
solution: Experience Platform
title: Ponto de extremidade da API de tipos de sandbox
topic-legacy: developer guide
description: Você pode recuperar uma lista dos tipos de sandbox suportados para sua organização fazendo uma solicitação do GET para o endpoint /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Ponto de extremidade Tipos de sandbox

Você pode recuperar uma lista dos tipos de sandbox suportados para sua organização fazendo uma solicitação de GET para o endpoint `/sandboxTypes`.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista dos tipos de sandbox suportados

Você pode recuperar uma lista dos tipos de sandbox suportados para sua organização fazendo uma solicitação de GET para o endpoint `/sandboxTypes`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
