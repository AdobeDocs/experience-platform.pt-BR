---
keywords: Experience Platform, home, tópicos populares, monitoramento, monitoramento, fluxos de dados, ingestão de monitor, assimilação de dados, ingestão de dados, exibir registros, exibir lotes;
solution: Experience Platform
title: Monitoramento da assimilação de dados
topic-legacy: overview
description: Este guia do usuário fornece etapas sobre como monitorar seus dados na interface do usuário do Adobe Experience Platform. Este guia requer uma Adobe ID e acesso ao Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 6bedd5ec0865e858a337155deb80309a54e30892
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Monitoramento da assimilação de dados

A assimilação de dados permite assimilar seus dados na Adobe Experience Platform. Você pode usar a assimilação em lote, que permite inserir seus dados usando vários tipos de arquivo (como CSVs), ou a assimilação de streaming, que permite assimilar seus dados em [!DNL Platform] usando endpoints de streaming em tempo real.

Este guia do usuário fornece etapas sobre como monitorar seus dados na interface do usuário do Adobe Experience Platform. Este guia requer uma Adobe ID e acesso ao Adobe Experience Platform.

## Monitore a assimilação de dados de ponta a ponta de fluxo

No [Experience Platform UI](https://platform.adobe.com), selecione **[!UICONTROL Monitoring]** no menu de navegação esquerdo, seguido por **[!UICONTROL Streaming end-to-end]**.

A página de monitoramento **[!UICONTROL Streaming end-to-end]** é exibida. Este espaço de trabalho fornece um gráfico que exibe a taxa de eventos transmitidos sendo recebidos por [!DNL Platform], um gráfico que exibe a taxa de eventos transmitidos que foram processados com êxito por [[!DNL Real-time Customer Profile]](../../profile/home.md), bem como uma lista detalhada de dados recebidos.

![](../images/quality/monitor-data-flows/list-streams.png)

Por padrão, o gráfico superior mostra a taxa de assimilação dos últimos sete dias. Esse intervalo de datas pode ser ajustado para mostrar vários períodos de tempo selecionando o botão destacado.

![](../images/quality/monitor-data-flows/events-received.png)

O gráfico inferior mostra a taxa de eventos transmitidos processados com êxito por [!DNL Profile] nos últimos sete dias. Esse intervalo de datas pode ser ajustado para mostrar vários períodos de tempo selecionando o botão destacado.

>[!NOTE]
>
>Para que os dados sejam exibidos neste gráfico, os dados devem ser **explicitamente** habilitados para [!DNL Profile]. Para saber como habilitar os dados de transmissão para [!DNL Profile], leia o [guia do usuário dos conjuntos de dados](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Abaixo dos gráficos está uma lista de todos os registros de assimilação de streaming que correspondem ao intervalo de datas exibido acima. Cada lote listado exibe sua ID, o nome do conjunto de dados, quando foi atualizado pela última vez, o número de registros no lote, bem como o número de erros (se houver). Você pode selecionar qualquer um dos registros para obter informações mais detalhadas sobre esse registro.

![](../images/quality/monitor-data-flows/streams.png)

### Exibição de registros de transmissão

Ao visualizar os detalhes de um registro simplificado bem-sucedido, informações como o número de registros assimilados, o tamanho do arquivo e as horas de início e término da assimilação são mostradas.

![](../images/quality/monitor-data-flows/successful-streaming.png)

Os detalhes de um registro de transmissão com falha exibem as mesmas informações de um registro bem-sucedido.

![](../images/quality/monitor-data-flows/failed-batch.png)

Além disso, registros com falha fornecem detalhes sobre os erros que ocorreram ao processar o lote. No exemplo abaixo, ocorreu um erro de análise ao converter ou validar os dados.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Monitorar a assimilação de dados de ponta a ponta do lote

No [[!DNL Experience Platform UI]](https://platform.adobe.com), selecione **[!UICONTROL Monitoring]** no menu de navegação esquerdo.

A página de monitoramento **[!UICONTROL Batch end-to-end]** é exibida, exibindo uma lista dos lotes assimilados anteriormente. Você pode selecionar qualquer um dos lotes para obter informações mais detalhadas sobre esse registro.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Exibindo lotes

Ao visualizar os detalhes de um lote bem-sucedido, informações como o número de registros assimilados, o tamanho do arquivo e as horas de início e término da assimilação são mostradas.

![](../images/quality/monitor-data-flows/successful-batch.png)

Os detalhes de um lote com falha exibem as mesmas informações de um lote bem-sucedido, com a adição do número de registros com falha.

![](../images/quality/monitor-data-flows/failed-batch.png)

Além disso, os lotes com falha fornecem detalhes sobre os erros que ocorreram durante o processamento do lote. No exemplo abaixo, ocorreu um erro com o lote assimilado porque ele tem o número máximo de identidades da pessoa.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
