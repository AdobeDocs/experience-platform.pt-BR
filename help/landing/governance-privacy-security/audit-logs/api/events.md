---
title: Endpoint da API de eventos de auditoria
description: Saiba como recuperar eventos de auditoria no Experience Platform usando a API de consulta de auditoria.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# Endpoint de eventos de auditoria

Os logs de auditoria são usados para fornecer detalhes da atividade do usuário para vários serviços e recursos. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação. O ponto de extremidade `/audit/events` na API [!DNL Audit Query] permite recuperar programaticamente dados do evento para a atividade de sua organização no [!DNL Experience Platform].

## Introdução

O ponto de extremidade de API usado neste guia faz parte da [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Listar eventos de auditoria

Você pode recuperar dados de eventos fazendo uma solicitação GET para o ponto de extremidade `/audit/events`, especificando os eventos que deseja recuperar na carga.

**Formato da API**

```http
GET /audit/events
```

A API [!DNL Audit Query] oferece suporte ao uso de parâmetros de consulta para página e filtrar resultados ao listar eventos.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. O padrão `limit` é 50. |
| `start` | Um ponteiro para o primeiro item dos resultados da pesquisa retornados. Para acessar a próxima página de resultados, esse parâmetro deve ser incrementado na mesma quantidade indicada pelo limite. Exemplo: para acessar a próxima página de resultados de uma solicitação com limite=50, use o parâmetro start=50, depois start=100 para a página após essa e assim por diante. |
| `queryId` | Ao fazer uma consulta ao endpoint /audit/events, a resposta inclui uma propriedade de sequência de caracteres queryId. Para fazer a mesma consulta em uma chamada separada, você pode incluir o valor da ID como um único parâmetro de consulta em vez de configurar manualmente os parâmetros de pesquisa novamente. |

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

Uma resposta bem-sucedida retorna os pontos de dados resultantes para as métricas e os filtros especificados na solicitação.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Propriedade | Descrição |
| --- | --- |
| `events` | Uma matriz cujos objetos representam cada um dos eventos especificados na solicitação. Cada objeto contém informações sobre a configuração de filtro e os dados do evento retornados. |
| `userEmail` | O email do usuário que executou o evento. |
| `eventType` | O tipo de evento. Os tipos de eventos incluem `Core` e `Enhanced`. |
| `imsOrgId` | A ID da organização na qual o evento ocorreu. |
| `permissionResource` | O produto ou recurso que forneceu a permissão para executar a ação. Um recurso pode ser qualquer um dos seguintes: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | O tipo de permissão envolvido na ação. |
| `assetType` | O tipo de recurso do Experience Platform no qual a ação foi executada. |
| `assetId` | Um identificador exclusivo do recurso do Experience Platform no qual a ação foi executada. |
| `assetName` | O nome do recurso Experience Platform no qual a ação foi executada. |
| `action` | O tipo de ação que foi gravado para o evento. Uma ação pode ser qualquer um dos seguintes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | O status da ação. Um status pode ser qualquer um dos seguintes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
