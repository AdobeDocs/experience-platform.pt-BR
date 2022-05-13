---
keywords: Experience Platform, home, tópicos populares, monitorar contas, monitorar fluxos de dados, fluxos de dados, fontes
description: Este tutorial fornece etapas para monitorar o fluxo de dados, usando a visualização de monitoramento agregado e o monitoramento entre serviços.
solution: Experience Platform
title: Monitorar fluxos de dados para fontes na interface do usuário
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: ed88ebe7822f60ace2babd7d5a04d2d92d83cf49
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Monitorar fluxos de dados para fontes na interface do usuário

>[!IMPORTANT]
>
>Fontes de transmissão, como [Fonte da API HTTP](../../sources/connectors/streaming/http.md) no momento, não são compatíveis com o painel de monitoramento. Nesse momento, você só pode usar o painel para monitorar fontes em lote.

No Adobe Experience Platform, os dados são assimilados de uma grande variedade de fontes, analisados no Experience Platform, e ativados para uma grande variedade de destinos. A Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear ao fornecer transparência com fluxos de dados.

O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Você pode usar uma visualização de monitoramento agregado e navegar verticalmente do nível de origem, para um fluxo de dados e para uma execução de fluxo de dados, permitindo exibir as métricas correspondentes que contribuem para o sucesso ou a falha de um fluxo de dados. Você também pode usar a capacidade de monitoramento entre serviços do painel de monitoramento para monitorar a jornada de um fluxo de dados de uma fonte para [!DNL Identity Service]e para [!DNL Profile].

Este tutorial fornece etapas para monitorar o fluxo de dados, usando a visualização de monitoramento agregado e o monitoramento entre serviços.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fluxos de dados](../home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile]e para [!DNL Destinations].
   * [Execuções do fluxo de dados](../../sources/notifications.md): As execuções de fluxo de dados são trabalhos agendados recorrentes com base na configuração de frequência de fluxos de dados selecionados.
* [Fontes](../../sources/home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Serviço de identidade](../../identity-service/home.md): Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
* [Perfil do cliente em tempo real](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Exibição de monitoramento agregada {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Assimilação de origem"
>abstract="A exibição de assimilação de origem contém informações sobre o status e as métricas da atividade de dados no serviço de lago de dados, incluindo registros assimilados e registros que falharam. Consulte o guia de definição de métricas para saber mais sobre métricas e gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Detalhes da execução do fluxo de dados"
>abstract="O processamento de fontes contém informações sobre o status da atividade de dados e métricas no serviço do data lake, incluindo registros assimilados e registros que falharam. Consulte o guia de definição de métricas para saber mais sobre métricas e gráficos."
>text="Learn more in documentation"

No [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Monitoramento]** na navegação à esquerda para acessar o [!UICONTROL Monitoramento] painel. O [!UICONTROL Monitoramento] o painel contém métricas e informações sobre todos os fluxos de dados de fontes, incluindo insights sobre a integridade do tráfego de dados de uma fonte para o [!DNL Identity Service]e para [!DNL Profile].

No centro do painel há [!UICONTROL Assimilação de origem] , que contém métricas e gráficos que exibem dados em registros assimilados e que falharam.

![painel de monitoramento](../assets/ui/monitor-sources/monitoring-dashboard.png)

Por padrão, os dados exibidos contêm taxas de ingestão das últimas 24 horas. Selecionar **[!UICONTROL Últimas 24 horas]** para ajustar o período de tempo dos registros exibidos.

![data de alteração](../assets/ui/monitor-sources/change-date.png)

Uma janela pop-up do calendário é exibida, fornecendo opções para intervalos de tempo de ingestão alternativos. Selecionar **[!UICONTROL Últimos 30 dias]** e depois selecione **[!UICONTROL Aplicar]**

![ajuste-horário](../assets/ui/monitor-sources/adjust-timeframe.png)

Os gráficos são ativados por padrão e você pode desativá-los para expandir a lista de fontes abaixo. Selecione o **[!UICONTROL Métricas e gráficos]** para desativar os gráficos.

![métricas e gráficos](../assets/ui/monitor-sources/metrics-graphs.png)

| Assimilação de origem | Descrição |
| ---------------- | ----------- |
| [!UICONTROL Registros assimilados ] | O número total de registros assimilados. |
| [!UICONTROL Falha nos registros] | O número total de registros que não foram assimilados devido a erros nos dados. |
| [!UICONTROL Total de fluxos de dados com falha] | O número total de fluxos de dados com um `failed` status. |

A lista de assimilação de origem exibe todas as fontes que contêm pelo menos uma conta existente. A lista também inclui informações sobre a taxa de ingestão de cada fonte, o número de registros com falha e o número total de fluxos de dados com falha com base no período aplicado.

![ingestão de origem](../assets/ui/monitor-sources/source-ingestion.png)

Para classificar a lista de fontes, selecione **[!UICONTROL Minhas fontes]** e selecione a categoria escolhida no menu suspenso. Por exemplo, para se concentrar nos armazenamentos de nuvem, selecione  **[!UICONTROL armazenamento na nuvem]**

![classificar por categoria](../assets/ui/monitor-sources/sort-by-category.png)

Para exibir todos os fluxos de dados existentes em todas as fontes, selecione **[!UICONTROL Fluxos de dados]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Como alternativa, você pode inserir uma fonte na barra de pesquisa para isolar uma única fonte. Depois de identificar a fonte, selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele para ver uma lista de seus fluxos de dados ativos.

![pesquisa](../assets/ui/monitor-sources/search.png)

Uma lista de fluxos de dados é exibida. Para restringir a lista e se concentrar nos fluxos de dados com erros, selecione **[!UICONTROL Mostrar somente falhas]**.

![show-failed-only](../assets/ui/monitor-sources/show-failures-only.png)

Localize o fluxo de dados que deseja monitorar e selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele, para ver mais informações sobre seu status de execução.

![fluxo de dados](../assets/ui/monitor-sources/dataflow.png)

A página de execução do fluxo de dados exibe informações sobre a data de início da execução do fluxo de dados, o tamanho dos dados, o status e a duração do tempo de processamento. Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de início da execução do fluxo de dados para ver seus detalhes de execução do fluxo de dados.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

O [!UICONTROL Detalhes da execução do fluxo de dados] exibe informações sobre os metadados do fluxo de dados, o status parcial da assimilação e o resumo do erro. O resumo do erro contém o erro de nível superior específico que mostra em qual etapa o processo de assimilação encontrou um erro.

Role para baixo para ver informações mais específicas sobre o erro que ocorreu.

![detalhes de execução do fluxo de dados](../assets/ui/monitor-sources/dataflow-run-details.png)

O [!UICONTROL Erros de execução do fluxo de dados] O painel exibe o erro específico e o código de erro que resultaram na falha de assimilação do fluxo de dados. Nesse cenário, ocorreu um erro de transformação do mapeador, resultando na falha de 24 registros.

Selecionar **[!UICONTROL Arquivos]** para obter mais informações.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

O [!UICONTROL Arquivos] O painel contém informações sobre o nome e o caminho do arquivo.

Para obter uma representação mais granular do erro, selecione **[!UICONTROL Visualizar diagnósticos de erro]**.

![arquivos](../assets/ui/monitor-sources/files.png)

O [!UICONTROL Visualização do diagnóstico de erros] for exibida, exibindo uma pré-visualização de até 100 erros no fluxo de dados. Você pode selecionar **[!UICONTROL Baixar]** para recuperar um comando curl, que permite baixar o diagnóstico de erro.

Quando terminar, selecione **[!UICONTROL Fechar]**

![diagnóstico de erros](../assets/ui/monitor-sources/error-diagnostics.png)

Você pode usar o sistema de navegação estrutural no cabeçalho superior para retornar ao [!UICONTROL Monitoramento] painel. Selecionar **[!UICONTROL Executar início: 14/2/2021, 21:47]** para retornar à página anterior e, em seguida, selecione **[!UICONTROL Fluxo de dados: Demonstração da Ingestão de Dados de Fidelidade - Falha]** para retornar à página de fluxos de dados.

![navegação estrutural](../assets/ui/monitor-sources/breadcrumbs.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você monitorou com sucesso o fluxo de dados de assimilação do nível de origem usando o **[!UICONTROL Monitoramento]** painel. Você também identificou com sucesso erros que contribuíram para a falha dos fluxos de dados durante o processo de assimilação. Consulte os seguintes documentos para obter mais detalhes:

* [Monitoramento de identidades em fluxos de dados](./monitor-identities.md)
* [Monitoramento de perfis em fluxos de dados](./monitor-profiles.md)
