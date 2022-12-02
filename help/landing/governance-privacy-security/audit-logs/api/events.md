---
title: Ponto de extremidade da API de eventos de auditoria
description: Saiba como recuperar eventos de auditoria no Experience Platform usando a API de consulta de auditoria.
source-git-commit: 2abd3ea6f1affa7d83a3ae6ee368fa4b5b890d94
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 10%

---

# Endpoint de eventos de auditoria

Os logs de auditoria são usados para fornecer detalhes da atividade do usuário para vários serviços e recursos. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação. O `/audit/events` endpoint no [!DNL Audit Query] A API permite recuperar programaticamente os dados do evento para a atividade de sua organização em [!DNL Platform].

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Listar eventos de auditoria

Você pode recuperar dados de eventos fazendo uma solicitação do GET para o `/audit/events` endpoint, especificando os eventos que deseja recuperar no payload.

**Formato da API**

```http
GET /audit/events
```

O [!DNL Audit Query] A API suporta o uso de parâmetros de consulta para página e filtrar resultados ao listar eventos.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. O padrão `limit` 50. |
| `start` | Um ponteiro para o primeiro item para os resultados de pesquisa retornados. Para acessar a próxima página de resultados, esse parâmetro deve incrementar pelo mesmo valor indicado por limite. Exemplo: Para acessar a próxima página de resultados de uma solicitação com limite=50, use o parâmetro start=50 e start=100 para a página depois disso e assim por diante. |
| `queryId` | Ao fazer uma consulta ao endpoint /audit/events, a resposta inclui uma propriedade de string queryId. Para fazer a mesma consulta em uma chamada separada, você pode incluir o valor da ID como um único parâmetro de consulta, em vez de configurar manualmente os parâmetros de pesquisa novamente. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os pontos de dados resultantes para as métricas e filtros especificados na solicitação.

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| Propriedade | Descrição |
| --- | --- |
| `customerAuditLogList` | Uma matriz cujos objetos representam cada um dos eventos especificados na solicitação. Cada objeto contém informações sobre a configuração de filtro e os dados de evento retornados. |
| `userEmail` | O email do usuário que executou o evento. |
| `eventType` | O tipo de evento. Os tipos de eventos incluem `Core` e `Enhanced`. |
| `imsOrgId` | A ID da organização em que o evento ocorreu. |
| `permissionResource` | O produto ou recurso que forneceu a permissão executa a ação. Um recurso pode ser qualquer um dos seguintes: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | O tipo de permissão envolvido com a ação. |
| `assetType` | O tipo de recurso da Plataforma no qual a ação foi executada. |
| `assetId` | Um identificador exclusivo para o recurso Plataforma no qual a ação foi executada. |
| `assetName` | O nome do recurso Plataforma no qual a ação foi executada. |
| `action` | O tipo de ação que foi gravada para o evento. Uma ação pode ser qualquer um dos seguintes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | O status da ação. Um status pode ser qualquer um dos seguintes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style=&quot;table-layout:auto&quot;}
