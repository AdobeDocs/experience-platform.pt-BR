---
title: Ponto de extremidade da API de exportação de eventos de auditoria
description: Saiba como exportar eventos de auditoria no Experience Platform usando a API de consulta de auditoria.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 4%

---

# Exportar uma lista de eventos de auditoria

Você pode recuperar dados de eventos fazendo uma solicitação GET para o ponto de extremidade `/audit/export`, especificando os eventos que deseja recuperar na carga.

**Formato da API**

```http
GET /audit/export
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `timestamp` | Ao filtrar por carimbo de data e hora, é prática recomendada usar um intervalo usando os operadores > e &lt;, em vez de um valor exato. <br/>Exemplo: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | O status da ação. Um status pode ser qualquer um dos seguintes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>Exemplo: `?property=status==Deny`. |
| `action` | O tipo de ação que foi gravado para o evento. Uma ação pode ser qualquer um dos seguintes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Exemplo: `?property=action==Create`. |
| `user` | O usuário que executou o evento. |
| `assetType` | O tipo de recurso do Experience Platform no qual a ação foi executada. <br/>Exemplo: `?property=assetType==<an asset type>`. |

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

Os resultados são gerados em um arquivo CSV para exportação, cada entrada representando um evento de auditoria principal ou aprimorado. Uma resposta bem-sucedida retorna HTTP 307 sem corpo de resposta. Um link para o arquivo de exportação é fornecido no cabeçalho de resposta `Location`.
