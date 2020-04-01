---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Métricas disponíveis
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Lista de métricas disponíveis

Abaixo está uma lista de métricas que são expostas pelo Observability Insights, cada uma com seu serviço de Plataforma, descrição e parâmetro de query de ID aceito.

| Métrica de insights | Serviço de plataforma | Descrição | Parâmetro do query de ID |
| ---- | ---- | ---- | ---- |
| time.ingestão.dataset.new.count | Ingestão de dados | Número total de conjuntos de dados criados. | N/D |
| time.ingestão.dataset.size | Ingestão de dados | Tamanho cumulativo de todos os dados ingeridos para um conjunto de dados para ou todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.ingestão.dataset.dailysize | Ingestão de dados | Tamanho dos dados ingeridos diariamente para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.ingestão.dataset.batchfailed.count | Ingestão de dados | O número de lotes falhou para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.ingestão.dataset.batchsuccess.count | Ingestão de dados | Número de lotes ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.ingestão.dataset.recordsuccess.count | Ingestão de dados | Número de registros ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.total.messages.rate | Ingestão de dados (streaming) | Número total de mensagens para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.valid.messages.rate | Ingestão de dados (streaming) | Número total de mensagens válidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.invalid.messages.rate | Ingestão de dados (streaming) | Número total de mensagens inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.type.count | Ingestão de dados (streaming) | O número total de mensagens de &quot;tipo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.range.count | Ingestão de dados (streaming) | Número total de mensagens de &quot;intervalo&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.format.count | Ingestão de dados (streaming) | Número total de mensagens de &quot;formato&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.pattern.count | Ingestão de dados (streaming) | Número total de mensagens &quot;padrão&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.presence.count | Ingestão de dados (streaming) | Número total de mensagens de &quot;presença&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.enum.count | Ingestão de dados (streaming) | Número total de mensagens &quot;enum&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.unclassified.count | Ingestão de dados (streaming) | Número total de mensagens &quot;não classificadas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.data.collection.validation.categoria.unknown.count | Ingestão de dados (streaming) | Número total de mensagens &quot;desconhecidas&quot; inválidas para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timesries.data.collection.inlet.total.messages.receive | Ingestão de dados (streaming) | Número total de mensagens recebidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| time.data.collection.inlet.total.messages.size.receive | Ingestão de dados (streaming) | Tamanho total dos dados recebidos para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| timesries.data.collection.inlet.success | Ingestão de dados (streaming) | Número total de chamadas HTTP bem-sucedidas para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| timesries.data.collection.inlet.failure | Ingestão de dados (streaming) | Número total de chamadas HTTP com falha para uma entrada de dados ou para todas as entradas de dados. | ID de entrada (opcional) |
| time.perfil.dataset.recordread.count | Perfil do cliente em tempo real | Número de registros lidos do lago de dados por Perfil, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timesries.perfis.dataset.recordsuccess.count | Perfil do cliente em tempo real | Número de registros gravados em sua fonte de dados por Perfil, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.perfil.dataset.recordfailed.count | Perfil do cliente em tempo real | Número de registros falhados por Perfil, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.perfil.dataset.batchsuccess.count | Perfil do cliente em tempo real | Número de lotes de Perfis ingeridos para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| time.perfil.dataset.batchfailed.count | Perfil do cliente em tempo real | O número de lotes de Perfis falhou para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timesries.identity.dataset.recordsuccess.count | Serviço de identidade | Número de registros gravados em sua fonte de dados pelo Serviço de identidade, para um conjunto de dados ou todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timesries.identity.dataset.recordfailed.count | Serviço de identidade | Número de registros falhados pelo Serviço de Identidade, para um conjunto de dados ou para todos os conjuntos de dados. | ID do conjunto de dados (opcional) |
| timesries.identity.dataset.namespacecode.recordsuccess.count | Serviço de identidade | Número de registros de identidade ingeridos com êxito para uma namespace. | ID da Namespace (**obrigatório**) |
| timesries.identity.dataset.namespacecode.recordfailed.count | Serviço de identidade | Número de registros de identidade falhados por uma namespace. | ID da Namespace (**obrigatório**) |
| timesries.identity.dataset.namespacecode.recordskipped.count | Serviço de identidade | Número de registros de identidade ignorados por uma namespace. | ID da Namespace (**obrigatório**) |
| timesries.identity.graph.imsorg.uniqueidentities.count | Serviço de identidade | Número de identidades exclusivas armazenadas no gráfico de identidade para sua Organização IMS. | N/D |
| timesries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Serviço de identidade | Número de identidades exclusivas armazenadas no gráfico de identidade de uma namespace. | ID da Namespace (**obrigatório**) |
| timesries.identity.graph.imsorg.numidogramas.count | Serviço de identidade | Número de identidades de gráfico exclusivas armazenadas no gráfico de identidade para a sua Organização IMS. | N/D |
| timesries.identity.graph.imsorg.grafstrong.uniqueidentities.count | Serviço de identidade | Número de identidades exclusivas armazenadas no gráfico de identidade para sua Organização IMS para uma determinada intensidade do gráfico (&quot;desconhecido&quot;, &quot;fraco&quot; ou &quot;forte&quot;). | Intensidade do gráfico (**obrigatório**) |
| timesries.gdpr.jobs.totaljobs.count | GDPR | Número total de empregos criados a partir do RGPD. | ENV (**obrigatório**) |
| timesries.gdpr.jobs.complete.jobs.count | GDPR | Número total de trabalhos concluídos do RGPD. | ENV (**obrigatório**) |
| timesries.gdpr.jobs.errorjobs.count | GDPR | Número total de trabalhos de erro do RGPD. | ENV (**obrigatório**) |
| timesries.queryservice.query.Scheduleonce.count | Serviço de Query | Número total de query agendados não recorrentes. | N/D |
| timesries.queryservice.query.Scheduledrecurring.count | Serviço de Query | Número total de query programados recorrentes. | N/D |
| time.queryservice.query.batchquery.count | Serviço de Query | Número total de query em lote executados. | N/D |
| timesries.queryservice.query.Scheduledquery.count | Serviço de Query | Número total de query programados executados. | N/D |
| timesries.queryservice.query.interativequery.count | Serviço de Query | Número total de query interativos executados. | N/D |
| timesries.queryservice.query.batchfrompsqlquery.count | Serviço de Query | Número total de query em lote executados do PSQL. | N/D |