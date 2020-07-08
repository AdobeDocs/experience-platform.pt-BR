---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitoramento da ingestão de dados
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Monitoramento da ingestão de dados

A ingestão de dados permite assimilar seus dados ao Adobe Experience Platform. Você pode usar a ingestão em lote, que permite inserir seus dados usando vários tipos de arquivo (como CSVs), ou a assimilação em streaming, que permite a assimilação de seus dados à Platform usando pontos de extremidade de streaming em tempo real.

Este guia do usuário fornece etapas sobre como monitorar seus dados na interface do usuário do Adobe Experience Platform. Este guia exige que você tenha um Adobe ID e acesso ao Adobe Experience Platform.

## Monitorar a assimilação de dados de streaming end-to-end

Na interface do usuário [do](https://platform.adobe.com)Experience Platform, clique em **Monitoramento** no menu de navegação esquerdo e clique em **Streaming end-to-end**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

A página *Streaming end-to-end* de monitoramento é exibida. Este espaço de trabalho fornece um gráfico que mostra a taxa de eventos transmitidos recebidos pela Platform, um gráfico que mostra a taxa de eventos transmitidos que foram processados com êxito pelo Perfil [Cliente em tempo](../../profile/home.md)real, bem como uma lista detalhada dos dados recebidos.

![](../images/quality/monitor-data-flows/list-streams.png)

Por padrão, o gráfico superior mostra a taxa de ingestão nos últimos sete dias. Esse intervalo de datas pode ser ajustado para mostrar vários períodos de tempo clicando no botão realçado.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

O gráfico inferior mostra a taxa de eventos em streaming processados com êxito por Perfil nos últimos sete dias. Esse intervalo de datas pode ser ajustado para mostrar vários períodos de tempo clicando no botão realçado.

>[!NOTE]
>
>Para que os dados sejam exibidos neste gráfico, os dados devem estar **explicitamente** habilitados para o Perfil. Para saber como ativar os dados de transmissão para o Perfil, leia o guia [do usuário dos](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)conjuntos de dados.

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Abaixo dos gráficos há uma lista de todos os registros de ingestão de streaming que correspondem ao intervalo de datas exibido acima. Cada lote listado exibe sua ID, o nome do conjunto de dados, quando foi atualizado pela última vez, o número de registros no lote, bem como o número de erros (se houver). Você pode clicar em qualquer um dos registros para obter informações mais detalhadas sobre esse registro.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Exibição de registros de transmissão

Ao visualizar os detalhes de um registro transmitido com êxito, informações como o número de registros ingeridos, o tamanho do arquivo, o start de ingestão e as horas finais são mostradas.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Os detalhes de um registro de streaming com falha exibem as mesmas informações de um registro bem-sucedido.

![](../images/quality/monitor-data-flows/failed-batch.png)

Além disso, os registros com falha fornecem detalhes sobre os erros que ocorreram durante o processamento do lote. No exemplo abaixo, ocorreu um erro de sistema ao validar o datasetId do catálogo.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Monitorar a ingestão de dados de ponta a ponta em lote

Na interface do usuário do [Experience Platform](https://platform.adobe.com), clique em **Monitoramento** no menu de navegação esquerdo.

![](../images/quality/monitor-data-flows/click-monitoring.png)

A página de monitoramento de **lote completo** é exibida, exibindo uma lista dos lotes ingeridos anteriormente. Você pode clicar em qualquer um dos lotes para obter informações mais detalhadas sobre esse registro.

![](../images/quality/monitor-data-flows/list-batches.png)

### Exibindo lotes

Ao exibir os detalhes de um lote bem-sucedido, informações como o número de registros ingeridos, o tamanho do arquivo, o start de ingestão e as horas finais são mostradas.

![](../images/quality/monitor-data-flows/successful-batch.png)

Os detalhes de um lote com falha exibem as mesmas informações de um lote bem-sucedido, com a adição do número de registros com falha.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Além disso, os lotes com falha fornecem detalhes sobre os erros que ocorreram durante o processamento do lote. No exemplo abaixo, ocorreu um erro com o lote ingerido porque ele usou um campo desconhecido de `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)