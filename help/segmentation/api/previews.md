---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Pré-visualizações
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guia do desenvolvedor do Pré-visualização

introdução

- Criar uma nova pré-visualização
- Recuperar resultados de uma pré-visualização específica
- Cancelar ou excluir uma pré-visualização específica

## Introdução

Os pontos finais da API usados neste guia fazem parte da API de segmentação. Antes de continuar, consulte o guia [do desenvolvedor de](./getting-started.md)Segmentação.

Em particular, a seção [de](./getting-started.md#getting-started) introdução do guia do desenvolvedor de Segmentação inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra no documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da plataforma de experiência.

## Criar uma nova pré-visualização

Você pode criar uma nova pré-visualização fazendo uma solicitação POST para o `/preview` ponto de extremidade.

**Formato da API**

```http
POST /preview
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

informações do corpo

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) com detalhes da sua pré-visualização recém-criada.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

informações de resposta, x-location não existe.

## Recuperar resultados de uma pré-visualização específica

Você pode recuperar informações detalhadas sobre uma pré-visualização específica fazendo uma solicitação GET ao ponto final `/preview` `id` e fornecendo o valor da pré-visualização no caminho da solicitação.

**Formato da API**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: O `id` valor da pré-visualização que você deseja recuperar.

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a pré-visualização especificada.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## Cancelar ou excluir uma pré-visualização específica

É possível excluir uma pré-visualização específica fazendo uma solicitação DELETE para o ponto final `/preview` e fornecendo o valor da pré-visualização `id` no caminho da solicitação.

**Formato da API**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` O `id` valor da pré-visualização que você deseja excluir.

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com a seguinte mensagem:

```json
{
  "status": true,
  "message": "KILLED"
}
```

## Próximas etapas
