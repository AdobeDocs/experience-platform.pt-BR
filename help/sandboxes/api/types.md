---
keywords: Experience Platform, home, tópicos populares, sandboxes de lista
solution: Experience Platform
title: Ponto de extremidade da API de tipos de sandbox
topic-legacy: developer guide
description: Você pode recuperar uma lista dos tipos de sandbox suportados para sua organização fazendo uma solicitação do GET para o endpoint /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Ponto de extremidade Tipos de sandbox

É possível recuperar uma lista dos tipos de sandbox suportados pela organização fazendo uma solicitação do GET para a `/sandboxTypes` endpoint .

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista dos tipos de sandbox suportados

É possível recuperar uma lista dos tipos de sandbox suportados pela organização fazendo uma solicitação do GET para a `/sandboxTypes` endpoint .

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
