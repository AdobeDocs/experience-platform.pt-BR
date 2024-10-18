---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Endpoint da API de métricas
description: Saiba como recuperar métricas de observabilidade no Experience Platform usando a API de insights de observação.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: a029d503d37d7e705897ce8efca98674ccf21780
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 4%

---

# Endpoint de métricas

As métricas de observação fornecem insights sobre estatísticas de uso, tendências históricas e indicadores de desempenho para vários recursos no Adobe Experience Platform. O ponto de extremidade `/metrics` no [!DNL Observability Insights API] permite recuperar programaticamente dados de métrica para a atividade da sua organização no [!DNL Platform].

>[!NOTE]
>
>A versão anterior do endpoint de métricas (V1) foi descontinuada. Este documento se concentra exclusivamente na versão atual (V2). Para obter detalhes sobre o ponto de extremidade V1 para implementações herdadas, consulte a [Referência da API](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Introdução

O ponto de extremidade de API usado neste guia faz parte da [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Recuperar métricas de observabilidade

Você pode recuperar dados de métricas fazendo uma solicitação POST para o ponto de extremidade `/metrics`, especificando as métricas que deseja recuperar na carga.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "aggregator": "sum"
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
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `start` | A data/hora mais antiga da qual recuperar dados de métrica. |
| `end` | A data/hora mais recente da qual recuperar dados de métrica. |
| `granularity` | Um campo opcional que indica o intervalo de tempo pelo qual dividir os dados de métrica. Por exemplo, um valor de `DAY` retorna métricas para cada dia entre as datas `start` e `end`, enquanto um valor de `MONTH` agruparia os resultados da métrica por mês. |
| `metrics` | Uma matriz de objetos, um para cada métrica que você deseja recuperar. |
| `name` | O nome de uma métrica reconhecida pelos Insights de capacidade de observação. Consulte o [apêndice](#available-metrics) para obter uma lista completa dos nomes de métricas aceitos. |
| `filters` | Um campo opcional que permite filtrar métricas por conjuntos de dados específicos. O campo é uma matriz de objetos (um para cada filtro), com cada objeto contendo as seguintes propriedades: <ul><li>`name`: O tipo de entidade para filtrar métricas. Atualmente, somente `dataSets` é suportado.</li><li>`value`: A ID de um ou mais conjuntos de dados. Várias IDs de conjunto de dados podem ser fornecidas como uma única cadeia de caracteres, com cada ID separada por caracteres de barra vertical (`\|`).</li><li>`groupBy`: Quando definido como verdadeiro, indica que o `value` correspondente representa vários conjuntos de dados cujos resultados de métrica devem ser retornados separadamente. Se definido como falso, os resultados da métrica para esses conjuntos de dados serão agrupados.</li></ul> |
| `aggregator` | Especifica a função de agregação que deve ser usada para agrupar vários registros de séries temporais em resultados únicos. Os agregadores atualmente compatíveis são mín., máx., soma e média, dependendo da definição da métrica. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os pontos de dados resultantes para as métricas e os filtros especificados na solicitação.

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
| `datapoints` | Uma matriz cujos objetos representam os resultados da métrica e dos filtros especificados. O número de objetos na matriz depende das opções de filtro fornecidas na solicitação. Se nenhum filtro for fornecido, a matriz conterá apenas um único objeto que representa todos os conjuntos de dados. |
| `groupBy` | Se vários conjuntos de dados tiverem sido especificados na propriedade `filter` para uma métrica e a opção `groupBy` tiver sido definida como verdadeira na solicitação, esse objeto conterá a ID do conjunto de dados ao qual a propriedade `dps` correspondente se aplica.<br><br>Se este objeto parecer vazio na resposta, a propriedade `dps` correspondente será aplicada a todos os conjuntos de dados fornecidos na matriz `filters` (ou a todos os conjuntos de dados em [!DNL Platform] se nenhum filtro tiver sido fornecido). |
| `dps` | Os dados retornados para a métrica, o filtro e o intervalo de tempo fornecidos. Cada chave nesse objeto representa um carimbo de data e hora com um valor correspondente para a métrica especificada. O período entre cada ponto de dados depende do valor `granularity` especificado na solicitação. |

{style="table-layout:auto"}

## Apêndice

A seção a seguir contém informações adicionais sobre como trabalhar com o ponto de extremidade `/metrics`.

### Métricas disponíveis {#available-metrics}

As tabelas a seguir listam todas as métricas expostas por [!DNL Observability Insights], detalhadas pelo serviço [!DNL Platform]. Cada métrica inclui uma descrição e um parâmetro de consulta de ID aceito.

>[!NOTE]
>
>Todos os parâmetros de consulta de ID listados são opcionais, a menos que declarado o contrário.

#### [!DNL Data Ingestion] {#ingestion}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Data Ingestion]. As métricas em **bold** são métricas de assimilação de streaming.

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Tamanho cumulativo de todos os dados assimilados de um conjunto de dados para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.dailysize | Tamanho dos dados assimilados com base no uso diário para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.batchfailed.count | Número de lotes com falha para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes assimilados para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros assimilados para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **série.dados.coleção.validação.categoria.presença.contagem** | Número total de mensagens de &quot;presença&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| **timeseries.data.collection.inlet.total.messages.received** | Número total de mensagens recebidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timeseries.data.collection.inlet.total.messages.size.received** | Tamanho total dos dados recebidos para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timeseries.data.collection.inlet.success** | Número total de chamadas HTTP bem-sucedidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |
| **timeseries.data.collection.inlet.failure** | Número total de chamadas HTTP com falha para uma entrada de dados ou para todas as entradas de dados. | ID de entrada |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

A tabela a seguir descreve as métricas do Adobe Experience Platform [!DNL Identity Service].

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros gravados na fonte de dados por [!DNL Identity Service], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.identity.dataset.recordfailed.count | Número de registros com falha por [!DNL Identity Service], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidade ignorados. | ID da organização |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade de sua organização. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade de um namespace. | ID de Namespace (**Obrigatório**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade de sua organização para uma determinada intensidade de gráfico (&quot;desconhecido&quot;, &quot;fraco&quot; ou &quot;forte&quot;). | Intensidade do gráfico (**Obrigatório**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

A tabela a seguir descreve as métricas para [!DNL Real-Time Customer Profile].

| Métrica de insights | Descrição | Parâmetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros lidos de [!DNL Data Lake] por [!DNL Profile], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros gravados na fonte de dados por [!DNL Profile], para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |
| timeseries.profiles.dataset.batchsuccess.count | Número de [!DNL Profile] lotes assimilados para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados |

{style="table-layout:auto"}

### Mensagens de erro

As respostas do ponto de extremidade `/metrics` podem retornar mensagens de erro sob determinadas condições. Essas mensagens de erro são retornadas no seguinte formato:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
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
| `title` | Uma string que contém a mensagem de erro e o possível motivo pelo qual ela ocorreu. |
| `report` | Contém informações contextuais sobre o erro, incluindo a sandbox e a organização em uso na operação que o acionou. |

{style="table-layout:auto"}

A tabela a seguir lista os diferentes códigos de erro que podem ser retornados pela API:

| Código de erro | Título | Descrição |
| --- | --- | --- |
| `INSGHT-1000-400` | Conteúdo de solicitação inválido | Algo deu errado com a carga da solicitação. Verifique se você corresponde exatamente à formatação da carga conforme mostrado [acima](#v2). Qualquer um dos possíveis motivos pode acionar esse erro:<ul><li>Campos obrigatórios ausentes, como `aggregator`</li><li>Métricas inválidas</li><li>A solicitação contém um agregador inválido</li><li>Uma data inicial ocorre após uma data final</li></ul> |
| `INSGHT-1001-400` | Falha na consulta de métricas | Ocorreu um erro ao tentar consultar o banco de dados de métricas devido a uma solicitação inválida ou a própria consulta não pode ser analisada. Verifique se a solicitação está formatada corretamente antes de tentar novamente. |
| `INSGHT-1001-500` | Falha na consulta de métricas | Ocorreu um erro ao tentar consultar o banco de dados de métricas devido a um erro no servidor. Tente a solicitação novamente e, se o problema persistir, entre em contato com o suporte ao Adobe. |
| `INSGHT-1002-500` | Erro de serviço | A solicitação não pôde ser processada devido a um erro interno. Tente a solicitação novamente e, se o problema persistir, entre em contato com o suporte ao Adobe. |
| `INSGHT-1003-401` | Erro de validação de sandbox | A solicitação não pôde ser processada devido a um erro de validação de sandbox. Verifique se o nome da sandbox fornecido no cabeçalho `x-sandbox-name` representa uma sandbox válida e habilitada para sua organização antes de tentar a solicitação novamente. |

{style="table-layout:auto"}
