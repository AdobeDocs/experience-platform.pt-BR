---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Métricas disponíveis
topic: developer guide
translation-type: tm+mt
source-git-commit: ff299a69a81f00cad3e90a83f7411e4b15d4f850

---


# Lista de métricas disponíveis

As tabelas a seguir listas todas as métricas expostas pelos Insights de Observabilidade, detalhadas pelo serviço da Plataforma. Cada métrica inclui uma descrição e um parâmetro de query de ID aceito.

## Ingestão de dados

A tabela a seguir descreve as métricas para a assimilação de dados da plataforma Adobe Experience. Métricas em **negrito** são métricas de ingestão de streaming.

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Número total de conjuntos de dados criados. | N/D |
| timeseries.ingestion.dataset.size | Tamanho cumulativo de todos os dados ingeridos para um conjunto de dados para ou todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.ingestion.dataset.dailysize | Tamanho dos dados ingeridos diariamente para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.ingestion.dataset.batchfailed.count | O número de lotes falhou para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.total.messages.rate** | Número total de mensagens para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.valid.messages.rate** | Número total de mensagens válidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.invalid.messages.rate** | Número total de mensagens inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.type.count** | O número total de mensagens de &quot;tipo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.range.count** | Número total de mensagens de &quot;intervalo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.format.count** | Número total de mensagens de &quot;formato&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.pattern.count** | Número total de mensagens &quot;padrão&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.presence.count** | Número total de mensagens de &quot;presença&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.enum.count** | Número total de mensagens &quot;enum&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.unclassified.count** | Número total de mensagens &quot;não classificadas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **time.data.collection.validation.categoria.unknown.count** | Número total de mensagens &quot;desconhecidas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| **timesries.data.collection.inlet.total.messages.receive** | Número total de mensagens recebidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| **time.data.collection.inlet.total.messages.size.receive** | Tamanho total dos dados recebidos para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| **timesries.data.collection.inlet.success** | Número total de chamadas HTTP bem-sucedidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| **timesries.data.collection.inlet.failure** | Número total de chamadas HTTP com falha para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |

## Serviço de identidade

A tabela a seguir descreve as métricas do Adobe Experience Platform Identity Service.

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros gravados em sua fonte de dados pelo Serviço de identidade, para um conjunto de dados ou todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.identity.dataset.recordfailed.count | Número de registros falhados pelo Serviço de Identidade, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Número de registros de identidade ingeridos com êxito para uma namespace. | ID da Namespace (**obrigatório**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidade falhados por uma namespace. | ID da Namespace (**obrigatório**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidade ignorados por uma namespace. | ID da Namespace (**obrigatório**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade para sua Organização IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade de uma namespace. | ID da Namespace (**obrigatório**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Número de identidades de gráfico exclusivas armazenadas no gráfico de identidade para a sua Organização IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades exclusivas armazenadas no gráfico de identidade para sua Organização IMS para uma determinada intensidade do gráfico (&quot;desconhecido&quot;, &quot;fraco&quot; ou &quot;forte&quot;). | Intensidade do gráfico (**obrigatório**) |

## Privacy Service

A tabela a seguir descreve as métricas do Adobe Experience Platform Privacy Service.

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Número total de empregos criados a partir do RGPD. | ENV (**obrigatório**) |
| timeseries.gdpr.jobs.completedjobs.count | Número total de trabalhos concluídos do RGPD. | ENV (**obrigatório**) |
| timeseries.gdpr.jobs.errorjobs.count | Número total de trabalhos de erro do RGPD. | ENV (**obrigatório**) |

## Serviço de Query

A tabela a seguir descreve as métricas do Adobe Experience Platform Query Service.

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Número total de query agendados não recorrentes. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Número total de query programados recorrentes. | N/D |
| timeseries.queryservice.query.batchquery.count | Número total de query em lote executados. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Número total de query programados executados. | N/D |
| timeseries.queryservice.query.interactivequery.count | Número total de query interativos executados. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Número total de query em lote executados do PSQL. | N/D |

## Perfil do cliente em tempo real

A tabela a seguir descreve as métricas do Perfil do cliente em tempo real.

| Métrica de insights | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros lidos do lago de dados por Perfil, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros gravados em sua fonte de dados por Perfil, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.profiles.dataset.recordfailed.count | Número de registros falhados por Perfil, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.profiles.dataset.batchsuccess.count | Número de lotes de Perfis ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timeseries.profiles.dataset.batchfailed.count | O número de lotes de Perfis falhou para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| platform.ups.ingest.streaming.request.m1_rate | Taxa de Solicitação de Entrada. | Organização IMS |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taxa de sucesso da ingestão. | Organização IMS |
| platform.ups.ingest.streaming.records.created.m15_rate | Taxa de novos registros ingeridos para um conjunto de dados. | ID do conjunto de dados |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taxa de registros com carimbos de data e hora fora de ordem para criar solicitação para um conjunto de dados. | ID do conjunto de dados |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Carimbo de data e hora da última solicitação de criação de registro para um conjunto de dados. | ID do conjunto de dados |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taxa de registros com carimbos de data e hora fora de ordem para solicitação de atualização de um conjunto de dados. | ID do conjunto de dados |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Carimbo de data e hora para a última solicitação de registro de atualização para um conjunto de dados. | ID do conjunto de dados |
| platform.ups.ingest.streaming.record.size.m1_rate | Tamanho médio do registro. | Organização IMS |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taxa de solicitações de atualização para registros ingeridos para um conjunto de dados. | ID do conjunto de dados |
