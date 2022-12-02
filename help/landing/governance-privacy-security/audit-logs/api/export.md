---
title: Ponto de extremidade da API de exportação de eventos de auditoria
description: Saiba como exportar eventos de auditoria no Experience Platform usando a API de consulta de auditoria.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Exportar uma lista de eventos de auditoria

Você pode recuperar dados de eventos fazendo uma solicitação do GET para o `/audit/export` endpoint, especificando os eventos que deseja recuperar no payload.

**Formato da API**

```http
GET /audit/export
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `timestamp` | Ao filtrar por carimbo de data e hora, é prática recomendada usar um intervalo usando operadores > e &lt; em vez de um valor exato. <br/>Exemplo: ?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48.610862Z. |
| `status` | O status da ação. Um status pode ser qualquer um dos seguintes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | O tipo de ação que foi gravada para o evento. Uma ação pode ser qualquer um dos seguintes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | O usuário que executou o evento. |
| `assetType` | O tipo de recurso da Plataforma no qual a ação foi executada. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Resposta**

Os resultados são gerados em um arquivo CSV para exportação. Uma resposta bem-sucedida retorna HTTP 307 sem corpo de resposta. Um link para o arquivo de exportação é fornecido no `Location` cabeçalho de resposta.
