---
keywords: Experience Platform;página inicial;tópicos populares;monitorar contas;monitorar fluxos de dados;fluxos de dados;fontes
description: Este tutorial fornece etapas para monitorar seu fluxo de dados, usando a visualização de monitoramento agregado e o monitoramento entre serviços.
solution: Experience Platform
title: Monitorar fluxos de dados para fontes na interface do usuário
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 8%

---

# Monitorar fluxos de dados para fontes na interface

>[!IMPORTANT]
>
>Fontes de transmissão, como o [Fonte da API HTTP](../../sources/connectors/streaming/http.md) atualmente, não são compatíveis com o painel de monitoramento. Nesse momento, você só pode usar o painel para monitorar origens de lote.

No Adobe Experience Platform, os dados são assimilados de uma grande variedade de fontes, analisados no Experience Platform e ativados para uma grande variedade de destinos. O Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear, fornecendo transparência aos fluxos de dados.

O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Você pode usar uma exibição de monitoramento agregada e navegar verticalmente do nível da origem, até um fluxo de dados e até uma execução de fluxo de dados, permitindo visualizar as métricas correspondentes que contribuem para o sucesso ou a falha de um fluxo de dados. Você também pode usar a capacidade de monitoramento entre serviços do painel de monitoramento para monitorar a jornada de um fluxo de dados de uma origem para [!DNL Identity Service], e para [!DNL Profile].

Este tutorial fornece etapas para monitorar seu fluxo de dados, usando a visualização de monitoramento agregado e o monitoramento entre serviços.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino para [!DNL Identity] e [!DNL Profile], e para [!DNL Destinations].
   * [O fluxo de dados é executado](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
* [Origens](../../sources/home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Serviço de identidade](../../identity-service/home.md): obtenha uma melhor visualização dos clientes individuais e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
* [Perfil do cliente em tempo real](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Exibição de monitoramento agregada {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Ingestão de origem"
>abstract="A visualização da ingestão de origem contém informações sobre o status da atividade de dados e métricas no serviço do data lake, incluindo registros assimilados e registros que falharam. Consulte o guia de definição de métricas para saber mais sobre métricas e gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Detalhes de execução do fluxo de dados"
>abstract="O processamento de fontes contém informações sobre o status da atividade de dados e métricas no serviço do data lake, incluindo registros assimilados e registros que falharam. Consulte o guia de definição de métricas para saber mais sobre métricas e gráficos."
>text="Learn more in documentation"

No [Interface do Platform](https://platform.adobe.com), selecione **[!UICONTROL Monitoramento]** na navegação à esquerda, para acessar a [!UICONTROL Monitoramento] painel. A variável [!UICONTROL Monitoramento] O painel contém métricas e informações sobre todos os fluxos de dados de origens, incluindo insights sobre a integridade do tráfego de dados de uma origem para [!DNL Identity Service], e para [!DNL Profile].

No centro do painel está a variável [!UICONTROL Assimilação de origem] painel, que contém métricas e gráficos que exibem dados sobre registros assimilados e registros com falha.

![monitoring-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Por padrão, os dados exibidos contêm taxas de assimilação das últimas 24 horas. Selecionar **[!UICONTROL Últimas 24 horas]** para ajustar o intervalo de tempo dos registros exibidos.

![data de alteração](../assets/ui/monitor-sources/change-date.png)

Uma janela pop-up de calendário é exibida, fornecendo opções para intervalos de tempo de assimilação alternativos. Selecionar **[!UICONTROL Últimos 30 dias]** e selecione **[!UICONTROL Aplicar]**

![ajustar intervalo de tempo](../assets/ui/monitor-sources/adjust-timeframe.png)

Os gráficos são ativados por padrão e você pode desativá-los para expandir a lista de fontes abaixo. Selecione o **[!UICONTROL Métricas e gráficos]** ativar para desativar os gráficos.

![métricas e gráficos](../assets/ui/monitor-sources/metrics-graphs.png)

| Ingestão de origem | Descrição |
| ---------------- | ----------- |
| [!UICONTROL Registros assimilados ] | O número total de registros assimilados. |
| [!UICONTROL Registros com falha] | O número total de registros que não foram assimilados devido a erros nos dados. |
| [!UICONTROL Total de fluxos de dados com falha] | O número total de fluxos de dados com um `failed` status. |

A lista de assimilação de origem exibe todas as origens que contêm pelo menos uma conta existente. A lista também inclui informações sobre a taxa de assimilação de cada origem, o número de registros com falha e o número total de fluxos de dados com falha com base no período aplicado.

![source-ingestion](../assets/ui/monitor-sources/source-ingestion.png)

Para classificar pela lista de fontes, selecione **[!UICONTROL Minhas fontes]** e, em seguida, selecione a categoria de sua escolha no menu suspenso. Por exemplo, para se concentrar em armazenamentos na nuvem, selecione  **[!UICONTROL armazenamento na nuvem]**

![classificar por categoria](../assets/ui/monitor-sources/sort-by-category.png)

Para exibir todos os fluxos de dados existentes em todas as fontes, selecione **[!UICONTROL Fluxos de dados]**.

![exibir todos os fluxos de dados](../assets/ui/monitor-sources/view-all-dataflows.png)

Como alternativa, você pode informar uma origem na barra de pesquisa para isolar uma única origem. Depois de identificar a fonte, selecione o ícone de filtro ![filtro](../assets/ui/monitor-sources/filter.png) ao lado dele para ver uma lista de seus fluxos de dados ativos.

![pesquisa](../assets/ui/monitor-sources/search.png)

Uma lista de fluxos de dados é exibida. Para restringir a lista e se concentrar em fluxos de dados com erros, selecione **[!UICONTROL Mostrar somente falhas]**.

![show-failures-only](../assets/ui/monitor-sources/show-failures-only.png)

Localize o fluxo de dados que deseja monitorar e selecione o ícone de filtro ![filtro](../assets/ui/monitor-sources/filter.png) ao lado dele, para ver mais informações sobre o status de execução.

![fluxo de dados](../assets/ui/monitor-sources/dataflow.png)

A página de execução do fluxo de dados exibe informações sobre a data de início da execução do fluxo de dados, o tamanho dos dados, o status e a duração do tempo de processamento. Selecione o ícone de filtro ![filtro](../assets/ui/monitor-sources/filter.png) ao lado da hora de início da execução do fluxo de dados para ver os detalhes da execução do fluxo de dados.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

A variável [!UICONTROL Detalhes da execução do fluxo de dados] A página exibe informações sobre os metadados do fluxo de dados, status de assimilação parcial e resumo do erro. O resumo de erros contém o erro de nível superior específico que mostra em qual etapa o processo de assimilação encontrou um erro.

Role para baixo para ver informações mais específicas sobre o erro que ocorreu.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

A variável [!UICONTROL Erros de execução de fluxo de dados] exibe o erro específico e o código de erro que resultou na falha de assimilação do fluxo de dados. Nesse cenário, ocorreu um erro de transformação do mapeador, resultando na falha de 24 registros.

Selecionar **[!UICONTROL Arquivos]** para obter mais informações.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

A variável [!UICONTROL Arquivos] contém informações sobre o nome e o caminho do arquivo.

Para obter uma representação mais granular do erro, selecione **[!UICONTROL Visualizar diagnóstico de erro]**.

![arquivos](../assets/ui/monitor-sources/files.png)

A variável [!UICONTROL Visualização do diagnóstico de erro] é exibida, exibindo uma visualização de até 100 erros no fluxo de dados. É possível selecionar **[!UICONTROL Baixar]** para recuperar um comando curl, que permite baixar os diagnósticos de erro.

Quando terminar, selecione **[!UICONTROL Fechar]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

Você pode usar o sistema de navegação estrutural no cabeçalho superior para navegar de volta para a [!UICONTROL Monitoramento] painel. Selecionar **[!UICONTROL Início da execução: 14/02/2021, 21:47]** para retornar à página anterior, e selecione **[!UICONTROL Fluxo de dados: Demonstração da assimilação de dados de fidelidade - Falha]** para retornar à página fluxos de dados.

![navegações estruturais](../assets/ui/monitor-sources/breadcrumbs.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você monitorou com sucesso o fluxo de dados de assimilação no nível da origem usando o **[!UICONTROL Monitoramento]** painel. Você também identificou com sucesso erros que contribuíram para a falha dos fluxos de dados durante o processo de assimilação. Consulte os seguintes documentos para obter mais detalhes:

* [Monitoramento de identidades em fluxos de dados](./monitor-identities.md)
* [Monitoramento de perfis em fluxos de dados](./monitor-profiles.md)
