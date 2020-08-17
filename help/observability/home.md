---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
description: Observability Insights é uma RESTful API que permite que você exponha as principais métricas de observabilidade no Adobe Experience Platform. Essas métricas fornecem insights sobre as estatísticas de uso da plataforma, verificações de integridade para serviços da plataforma, tendências históricas e indicadores de desempenho para várias funcionalidades da plataforma.
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 2%

---


# Visão geral do Adobe Experience Platform Observability Insights

Observability Insights é uma RESTful API que permite que você exponha as principais métricas de observabilidade no Adobe Experience Platform. Essas métricas fornecem informações sobre as estatísticas de [!DNL Platform] uso, verificações de integridade para [!DNL Platform] serviços, tendências históricas e indicadores de desempenho para várias [!DNL Platform] funcionalidades.

Este documento demonstra uma chamada de exemplo para a API Observability Insights. Para obter uma lista completa dos pontos finais de Observabilidade, consulte a referência [à API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)Observability Insights.

## Introdução

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá. Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../sandboxes/home.md)caixa de proteção.

* x-sandbox-name: `{SANDBOX_NAME}`

## Recuperar métricas de observabilidade

Você pode recuperar métricas de observabilidade fazendo uma solicitação de GET para o `/metrics` terminal na API do Observability Insights.

**Formato da API**

Ao usar o `/metrics` endpoint, pelo menos um parâmetro de solicitação de métrica deve ser fornecido. Outros parâmetros de query são opcionais para filtrar resultados.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{METRIC}` | A métrica que você deseja expor. Ao combinar várias métricas em uma única chamada, você deve usar um E comercial (`&`) para separar métricas individuais. Por exemplo, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | O identificador de um [!DNL Platform] recurso específico cujas métricas você deseja expor. Essa ID pode ser opcional, obrigatória ou não aplicável, dependendo das métricas usadas. Para obter uma lista de métricas disponíveis, bem como IDs compatíveis (obrigatórias e opcionais) para cada métrica, consulte o documento de referência sobre métricas [](metrics.md)disponíveis. |
| `{DATE_RANGE}` | O intervalo de datas das métricas que você deseja expor, no formato ISO 8601 (por exemplo, `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de objetos, cada um contendo um carimbo de data e hora dentro dos valores fornecidos `dateRange` e correspondentes para as métricas especificadas no caminho da solicitação. Se o `id` de um [!DNL Platform] recurso for incluído no caminho da solicitação, os resultados serão aplicados somente a esse recurso específico. Se o `id` for omitido, os resultados serão aplicados a todos os recursos aplicáveis dentro da organização IMS.

```json
{
    "id": "5cf8ab4ec48aba145214abeb",
    "imsOrgId": "{IMS_ORG}",
    "timeseries": {
        "granularity": "MONTH",
        "items": [
            {
                "timestamp": "2019-06-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1125,
                    "timeseries.ingestion.dataset.size": 32320
                }
            },
            {
                "timestamp": "2019-05-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1003,
                    "timeseries.ingestion.dataset.size": 31409
                }
            },
            {
                "timestamp": "2019-04-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-03-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-02-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 390,
                    "timeseries.ingestion.dataset.size": 16801
                }
            }
        ],
        "_page": null,
        "_links": null
    },
    "stats": {}
}
```

## Próximas etapas

Este documento forneceu uma visão geral da API de informações de observação. Consulte o documento das métricas [](metrics.md) disponíveis para obter uma lista completa das métricas que podem ser usadas na API.