---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Endpoint da API de métricas
topic: developer guide
description: Saiba como recuperar métricas de observabilidade no Experience Platform usando a API do Observability Insights .
translation-type: tm+mt
source-git-commit: 136c75f56c2ba4d61fef7981ff8a7889a0ade3d1
workflow-type: tm+mt
source-wordcount: '2056'
ht-degree: 2%

---


# Ponto de extremidade de métricas

As métricas de capacidade de observação fornecem informações sobre estatísticas de uso, tendências históricas e indicadores de desempenho para vários recursos no Adobe Experience Platform. O terminal `/metrics` no [!DNL Observability Insights API] permite recuperar programaticamente os dados de métrica da atividade da organização em [!DNL Platform].

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API [!DNL Experience Platform].

## Recuperar métricas de observabilidade

Há dois métodos compatíveis para recuperar dados de métrica usando a API:

* [Versão 1](#v1): Especifique métricas usando parâmetros de consulta.
* [Versão 2](#v2): Especifique e aplique filtros a métricas usando uma carga JSON.

### Versão 1 {#v1}

Você pode recuperar dados de métricas fazendo uma solicitação GET para o terminal `/metrics`, especificando métricas por meio do uso de parâmetros de consulta.

**Formato da API**

Pelo menos uma métrica deve ser fornecida no parâmetro `metric` . Outros parâmetros de consulta são opcionais para filtrar resultados.

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
| `{ID}` | O identificador de um recurso [!DNL Platform] específico cujas métricas você deseja expor. Essa ID pode ser opcional, obrigatória ou não aplicável, dependendo das métricas que estão sendo usadas. Consulte o [apêndice](#available-metrics) para obter uma lista de métricas disponíveis, incluindo as IDs suportadas (obrigatórias e opcionais) para cada métrica. |
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

Uma resposta bem-sucedida retorna uma lista de objetos, cada um contendo um carimbo de data e hora no `dateRange` fornecido e os valores correspondentes para as métricas especificadas no caminho da solicitação. Se `id` de um recurso [!DNL Platform] estiver incluído no caminho da solicitação, os resultados serão aplicados somente a esse recurso específico. Se `id` for omitido, os resultados serão aplicados a todos os recursos aplicáveis em sua Organização IMS.

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

### Versão 2 {#v2}

Você pode recuperar dados de métricas fazendo uma solicitação de POST ao endpoint `/metrics`, especificando as métricas que deseja recuperar no payload.

**Formato da API**

```http
POST /metrics
```

**Solicitação**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `start` | A data/hora mais antiga a partir da qual recuperar dados de métrica. |
| `end` | A data/hora mais recente da qual recuperar dados de métrica. |
| `granularity` | Um campo opcional que indica o intervalo de tempo para dividir os dados da métrica. Por exemplo, um valor `DAY` retorna métricas para cada dia entre as datas `start` e `end`, enquanto um valor `MONTH` agruparia os resultados da métrica por mês. Ao usar esse campo, uma propriedade `downsample` correspondente também deve ser fornecida para indicar a função de agregação pela qual agrupar dados. |
| `metrics` | Uma matriz de objetos, um para cada métrica que você deseja recuperar. |
| `name` | O nome de uma métrica reconhecida pelos Insights de capacidade de observação. Consulte o [apêndice](#available-metrics) para obter uma lista completa dos nomes de métricas aceitas. |
| `filters` | Um campo opcional que permite filtrar métricas por conjuntos de dados específicos. O campo é uma matriz de objetos (um para cada filtro), com cada objeto contendo as seguintes propriedades: <ul><li>`name`: O tipo de entidade para o qual filtrar métricas. Atualmente, somente `dataSets` é suportado.</li><li>`value`: A ID de um ou mais conjuntos de dados. Várias IDs de conjunto de dados podem ser fornecidas como uma única string, com cada ID separada por caracteres de barra vertical (`|`).</li><li>`groupBy`: Quando definido como verdadeiro, indica que o correspondente  `value` representa vários conjuntos de dados cujos resultados da métrica devem ser retornados separadamente. Se definido como falso, os resultados da métrica desses conjuntos de dados serão agrupados.</li></ul> |
| `aggregator` | Especifica a função de agregação que deve ser usada para agrupar vários registros de séries de tempo em resultados únicos. Para obter informações detalhadas sobre agregadores disponíveis, consulte a [documentação do OpenTSDB](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html). |
| `downsample` | Um campo opcional que permite especificar uma função de agregação para reduzir a taxa de amostragem de dados de métrica, classificando campos em intervalos (ou &quot;buckets&quot;). O intervalo para a amostragem decrescente é determinado pela propriedade `granularity`. Para obter informações detalhadas sobre o downsampling, consulte a [documentação do OpenTSDB](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html). |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os pontos de dados resultantes para as métricas e filtros especificados na solicitação.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `metricResponses` | Uma matriz cujos objetos representam cada uma das métricas especificadas na solicitação. Cada objeto contém informações sobre a configuração de filtro e os dados de métrica retornados. |
| `metric` | O nome de uma das métricas fornecidas na solicitação. |
| `filters` | A configuração de filtro para a métrica especificada. |
| `datapoints` | Uma matriz cujos objetos representam os resultados da métrica e dos filtros especificados. O número de objetos na matriz depende das opções de filtro fornecidas na solicitação. Se nenhum filtro for fornecido, a matriz conterá apenas um único objeto que represente todos os conjuntos de dados. |
| `groupBy` | Se vários conjuntos de dados foram especificados na propriedade `filter` de uma métrica e a opção `groupBy` foi definida como true na solicitação, esse objeto conterá a ID do conjunto de dados à qual a propriedade `dps` correspondente se aplica.<br><br>Se esse objeto aparecer vazio na resposta, a  `dps` propriedade correspondente se aplica a todos os conjuntos de dados fornecidos na  `filters` matriz (ou a todos os conjuntos de dados em  [!DNL Platform] caso nenhum filtro tenha sido fornecido). |
| `dps` | Os dados retornados para determinada métrica, filtro e intervalo de tempo. Cada chave nesse objeto representa um carimbo de data e hora com um valor correspondente para a métrica especificada. O período entre cada ponto de dados depende do valor `granularity` especificado na solicitação. |

{style=&quot;table-layout:auto&quot;}

## Apêndice

A seção a seguir contém informações adicionais sobre como trabalhar com o endpoint `/metrics`.

### Métricas disponíveis {#available-metrics}

As tabelas a seguir listam todas as métricas expostas por [!DNL Observability Insights], detalhadas pelo serviço [!DNL Platform]. Cada métrica inclui uma descrição e um parâmetro de consulta de ID aceito.

>[!NOTE]
>
>Todos os parâmetros de consulta de ID listados são opcionais, salvo indicação em contrário.

#### [!DNL Data Ingestion] {#ingestion}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Data Ingestion]. Métricas em **bold** são métricas de assimilação de streaming.

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Número total de conjuntos de dados criados. | N/D |
| timeseries.ingestion.dataset.size | Tamanho cumulativo de todos os dados assimilados para um conjunto de dados para ou todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.dailysize | Tamanho dos dados assimilados em uma base de uso diário para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.batchfailed.count | Número de lotes com falha para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes assimilados para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros assimilados para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.total.messages.rate** | Número total de mensagens para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **timesries.data.collection.validation.valid.messages.rate** | Número total de mensagens válidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **timesries.data.collection.validation.invalid.messages.rate** | Número total de mensagens inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.type.count** | Número total de mensagens de &quot;tipo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.range.count** | Número total de mensagens de &quot;intervalo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.format.count** | Número total de mensagens de &quot;formato&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.pattern.count** | Número total de mensagens de &quot;padrão&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **timesries.data.collection.validation.category.presence.count** | Número total de mensagens de &quot;presença&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.enum.count** | Número total de mensagens &quot;enum&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.unclassification.count** | Número total de mensagens &quot;não classificadas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **time.data.collection.validation.category.unknown.count** | Número total de mensagens &quot;desconhecidas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **timesries.data.collection.inlet.total.messages.receive** | Número total de mensagens recebidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timesries.data.collection.inlet.total.messages.size.receive** | Tamanho total dos dados recebidos para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timesries.data.collection.inlet.success** | Número total de chamadas HTTP bem-sucedidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timesries.data.collection.inlet.failure** | Número total de chamadas HTTP com falha para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Identity Service].

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros gravados em sua fonte de dados por [!DNL Identity Service], para um conjunto de dados ou todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.identity.dataset.recordfailed.count | Número de registros falhados por [!DNL Identity Service], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Número de registros de identidade assimilados com êxito para um namespace. | ID de namespace (**Obrigatório**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidade falhados por um namespace. | ID de namespace (**Obrigatório**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidade ignorados por um namespace. | ID de namespace (**Obrigatório**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade da organização IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade de um namespace. | ID de namespace (**Obrigatório**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Número de identidades de gráfico exclusivas armazenadas no gráfico de identidade da organização IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade da sua Organização IMS para uma determinada intensidade de gráfico (&quot;desconhecido&quot;, &quot;fraco&quot; ou &quot;forte&quot;). | Intensidade do gráfico (**Obrigatório**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Privacy Service].

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Número total de tarefas criadas pelo GDPR. | ENV (**Obrigatório**) |
| timeseries.gdpr.jobs.completedjobs.count | Número total de tarefas concluídas do GDPR. | ENV (**Obrigatório**) |
| timeseries.gdpr.jobs.errorjobs.count | Número total de tarefas com erro do GDPR. | ENV (**Obrigatório**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Query Service].

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Número total de consultas agendadas não recorrentes. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Número total de consultas programadas recorrentes. | N/D |
| timeseries.queryservice.query.batchquery.count | Número total de consultas em lote executadas. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Número total de consultas programadas executadas. | N/D |
| timeseries.queryservice.query.interactivequery.count | Número total de consultas interativas executadas. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Número total de consultas em lote executadas do PSQL. | N/D |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

A tabela a seguir descreve as métricas de [!DNL Real-time Customer Profile].

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros lidos a partir de [!DNL Data Lake] por [!DNL Profile], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros gravados em sua fonte de dados por [!DNL Profile], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.recordfailed.count | Número de registros falhados por [!DNL Profile], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.batchsuccess.count | Número de [!DNL Profile] lotes assimilados para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.batchfailed.count | Falha no número de [!DNL Profile] lotes para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| platform.ups.ingest.streaming.request.m1_rate | Taxa de Solicitação de Entrada. | Organização IMS (**Obrigatório**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taxa de sucesso da assimilação. | Organização IMS (**Obrigatório**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Taxa de novos registros assimilados para um conjunto de dados. | ID do conjunto de dados (**Obrigatório**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taxa de registros com carimbo de data e hora fora de ordem para criar solicitação para um conjunto de dados. | ID do conjunto de dados (**Obrigatório**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Carimbo de data e hora da última solicitação de registro de criação para um conjunto de dados. | ID do conjunto de dados (**Obrigatório**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taxa de registros com carimbo de data e hora fora de ordem para a solicitação de atualização de um conjunto de dados. | ID do conjunto de dados (**Obrigatório**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Carimbo de data e hora da última solicitação de registro de atualização para um conjunto de dados. | ID do conjunto de dados (**Obrigatório**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Tamanho médio do registro. | Organização IMS (**Obrigatório**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taxa de solicitações de atualização para registros assimilados de um conjunto de dados. | ID do conjunto de dados (**Obrigatório**) |

{style=&quot;table-layout:auto&quot;}

### Mensagens de erro

Respostas do endpoint `/metrics` podem retornar mensagens de erro sob determinadas condições. Essas mensagens de erro são retornadas no seguinte formato:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `title` | Uma string contendo a mensagem de erro e o possível motivo da sua ocorrência. |
| `report` | Contém informações contextuais sobre o erro, incluindo a sandbox e a IMS Org que estão sendo usadas na operação que o acionou. |

{style=&quot;table-layout:auto&quot;}

A tabela a seguir lista os diferentes códigos de erro que podem ser retornados pela API:

| Código de erro | Title | Descrição |
| --- | --- | --- |
| `INSGHT-1000-400` | Carga de solicitação incorreta | Algo estava errado com a carga da solicitação. Certifique-se de corresponder a formatação de carga exatamente como mostrado [acima](#v2). Qualquer um dos possíveis motivos pode acionar esse erro:<ul><li>Campos obrigatórios ausentes, como `aggregator`</li><li>Métricas inválidas</li><li>A solicitação contém um agregador inválido</li><li>Uma data inicial ocorre após uma data final</li></ul> |
| `INSGHT-1001-400` | Falha na consulta de métricas | Ocorreu um erro ao tentar consultar o banco de dados de métricas, devido a uma solicitação incorreta ou à impossibilidade de análise da consulta propriamente dita. Certifique-se de que sua solicitação esteja formatada corretamente antes de tentar novamente. |
| `INSGHT-1001-500` | Falha na consulta de métricas | Ocorreu um erro ao tentar consultar o banco de dados de métricas devido a um erro de servidor. Tente a solicitação novamente e, se o problema persistir, entre em contato com o suporte ao Adobe. |
| `INSGHT-1002-500` | Erro de serviço | Não foi possível processar a solicitação devido a um erro interno. Tente a solicitação novamente e, se o problema persistir, entre em contato com o suporte ao Adobe. |
| `INSGHT-1003-401` | Erro de validação da sandbox | Não foi possível processar a solicitação devido a um erro de validação de sandbox. Certifique-se de que o nome da sandbox fornecido no cabeçalho `x-sandbox-name` representa uma sandbox válida e ativada para sua organização IMS antes de tentar a solicitação novamente. |

{style=&quot;table-layout:auto&quot;}
