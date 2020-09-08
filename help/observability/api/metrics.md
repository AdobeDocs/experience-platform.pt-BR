---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Métricas disponíveis
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# Ponto de extremidade de métricas

Métricas de observabilidade fornecem insights sobre estatísticas de uso, tendências históricas e indicadores de desempenho para vários recursos no Adobe Experience Platform. O `/metrics` endpoint no [!DNL Observability Insights API] permite recuperar dados de métrica programaticamente para a atividade de sua organização no [!DNL Platform].

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Antes de continuar, reveja o guia [de](./getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Recuperar métricas de observabilidade

Você pode recuperar métricas de observabilidade, fazendo uma solicitação de GET para o `/metrics` terminal na [!DNL Observability Insights] API.

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
| `{ID}` | O identificador de um [!DNL Platform] recurso específico cujas métricas você deseja expor. Essa ID pode ser opcional, obrigatória ou não aplicável, dependendo das métricas usadas. Consulte o [apêndice](#available-metrics) para obter uma lista de métricas disponíveis, bem como IDs compatíveis (obrigatórias e opcionais) para cada métrica. |
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

## Apêndice

A seção a seguir contém informações adicionais sobre como trabalhar com o `/metrics` endpoint.

### Métricas disponíveis {#available-metrics}

As tabelas a seguir listas todas as métricas expostas por [!DNL Observability Insights], detalhadas por [!DNL Platform] serviço. Cada métrica inclui uma descrição e um parâmetro de query de ID aceito.

>[!NOTE]
>
>Todos os parâmetros de query de ID listados são opcionais, a menos que seja indicado o contrário.

#### [!DNL Data Ingestion] {#ingestion}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Data Ingestion]. Métricas em **negrito** são métricas de ingestão de streaming.

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Número total de conjuntos de dados criados. | N/D |
| timeseries.ingestion.dataset.size | Tamanho cumulativo de todos os dados ingeridos para um conjunto de dados para ou todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.dailysize | Tamanho dos dados ingeridos diariamente para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.batchfailed.count | O número de lotes falhou para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.total.messages.rate** | Número total de mensagens para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.valid.messages.rate** | Número total de mensagens válidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.invalid.messages.rate** | Número total de mensagens inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.type.count** | O número total de mensagens de &quot;tipo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.range.count** | Número total de mensagens de &quot;intervalo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.format.count** | Número total de mensagens de &quot;formato&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.pattern.count** | Número total de mensagens &quot;padrão&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.presence.count** | Número total de mensagens de &quot;presença&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.enum.count** | Número total de mensagens &quot;enum&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.unclassified.count** | Número total de mensagens &quot;não classificadas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.categoria.unknown.count** | Número total de mensagens &quot;desconhecidas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **timesries.data.collection.inlet.total.messages.receive** | Número total de mensagens recebidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **time.data.collection.inlet.total.messages.size.receive** | Tamanho total dos dados recebidos para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timesries.data.collection.inlet.success** | Número total de chamadas HTTP bem-sucedidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timesries.data.collection.inlet.failure** | Número total de chamadas HTTP com falha para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |

#### [!DNL Identity Service] {#identity}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Identity Service].

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros gravados em sua fonte de dados por, [!DNL Identity Service]para um conjunto de dados ou todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.identity.dataset.recordfailed.count | Número de registros falhados por, [!DNL Identity Service]para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Número de registros de identidade ingeridos com êxito para uma namespace. | ID da namespace (**obrigatório**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidade falhados por uma namespace. | ID da namespace (**obrigatório**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidade ignorados por uma namespace. | ID da namespace (**obrigatório**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade para sua Organização IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade de uma namespace. | ID da namespace (**obrigatório**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Número de identidades de gráfico exclusivas armazenadas no gráfico de identidade para a sua Organização IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade para sua Organização IMS para uma determinada intensidade do gráfico (&quot;desconhecido&quot;, &quot;fraco&quot; ou &quot;forte&quot;). | Intensidade do gráfico (**obrigatório**) |

#### [!DNL Privacy Service] {#privacy}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Privacy Service].

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Número total de empregos criados a partir do RGPD. | ENV (**obrigatório**) |
| timeseries.gdpr.jobs.completedjobs.count | Número total de trabalhos concluídos do RGPD. | ENV (**obrigatório**) |
| timeseries.gdpr.jobs.errorjobs.count | Número total de trabalhos de erro do RGPD. | ENV (**obrigatório**) |

#### [!DNL Query Service] {#query}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Query Service].

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Número total de query agendados não recorrentes. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Número total de query programados recorrentes. | N/D |
| timeseries.queryservice.query.batchquery.count | Número total de query em lote executados. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Número total de query programados executados. | N/D |
| timeseries.queryservice.query.interactivequery.count | Número total de query interativos executados. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Número total de query em lote executados do PSQL. | N/D |

#### [!DNL Real-time Customer Profile] {#profile}

A tabela a seguir descreve as métricas para [!DNL Real-time Customer Profile].

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros lidos do [!DNL Data Lake] por, [!DNL Profile]para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros gravados em sua fonte de dados por [!DNL Profile], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.recordfailed.count | Número de registros falhados por, [!DNL Profile]para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.batchsuccess.count | Número de [!DNL Profile] lotes ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.batchfailed.count | O número de [!DNL Profile] lotes falhou para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| platform.ups.ingest.streaming.request.m1_rate | Taxa de Solicitação de Entrada. | Organização IMS (**obrigatório**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taxa de sucesso da ingestão. | Organização IMS (**obrigatório**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Taxa de novos registros ingeridos para um conjunto de dados. | ID do conjunto de dados (**obrigatório**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taxa de registros com carimbos de data e hora fora de ordem para criar solicitação para um conjunto de dados. | ID do conjunto de dados (**obrigatório**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Carimbo de data e hora da última solicitação de criação de registro para um conjunto de dados. | ID do conjunto de dados (**obrigatório**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taxa de registros com carimbos de data e hora fora de ordem para solicitação de atualização de um conjunto de dados. | ID do conjunto de dados (**obrigatório**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Carimbo de data e hora para a última solicitação de registro de atualização para um conjunto de dados. | ID do conjunto de dados (**obrigatório**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Tamanho médio do registro. | Organização IMS (**obrigatório**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taxa de solicitações de atualização para registros ingeridos para um conjunto de dados. | ID do conjunto de dados (**obrigatório**) |