---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Estimativas
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Estimativas

introdução

- Recuperar os resultados de uma ordem de produção de estimativa específica

## Introdução

Os pontos finais da API usados neste guia fazem parte da API de segmentação. Antes de continuar, consulte o guia [do desenvolvedor de](./getting-started.md)Segmentação.

Em particular, a seção [de](./getting-started.md#getting-started) introdução do guia do desenvolvedor de Segmentação inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra no documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da plataforma de experiência.

## Recuperar os resultados de uma ordem de produção de estimativa específica

Você pode recuperar detalhes de uma ordem de produção de estimativa específica fazendo uma solicitação GET para o `/estimate` terminal e fornecendo o `id` valor da ordem de produção de estimativa no caminho da solicitação.

**Formato da API**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: O `id` valor da tarefa de estimativa que você deseja recuperar.

**Solicitação**

A solicitação a seguir recupera os resultados de um trabalho de estimativa específico.

//precisa obter uma ID de pré-visualização

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do trabalho de estimativa.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## Próximas etapas

Agora que você sabe como recuperar os resultados da estimativa de trabalho, é melhor