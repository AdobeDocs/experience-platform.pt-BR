---
description: Saiba como usar o painel de monitoramento para monitorar dados assimilados no data lake.
title: Monitorar assimilação do data lake
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 75970d41a316c97d98ebf6cefd3bfa0e58173030
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 10%

---

# Monitorar assimilação do data lake

>[!IMPORTANT]
>
>As fontes de transmissão, como a [fonte de API HTTP](../../sources/connectors/streaming/http.md), não têm suporte atualmente no painel de monitoramento. Nesse momento, você só pode usar o painel para monitorar origens de lote.

Você pode usar o painel de monitoramento na interface do usuário do Adobe Experience Platform para recuperar métricas sobre os processos de assimilação e retenção de dados no data lake. Use os gráficos na interface para monitorar as tendências de assimilação e retenção ao longo do tempo e resumir o desempenho em todos os fluxos de dados de suas origens.

Leia este documento para saber como você pode usar o painel de monitoramento para monitorar todo o processamento de dados no data lake, incluindo a assimilação e a retenção.

## Introdução {#get-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Experience Platform. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   * [Execuções de fluxo de dados](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
* [Fontes](../../sources/home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Serviço de identidade](../../identity-service/home.md): obtenha uma melhor visão dos clientes individuais e de seu comportamento unindo as identidades de vários dispositivos e sistemas.
* [Perfil de cliente em tempo real](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Usar o painel de monitoramento para assimilação do data lake

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

Selecione **[!UICONTROL Data lake]** no cabeçalho principal do painel de monitoramento para exibir sua taxa de assimilação do data lake.

![O painel de monitoramento com o cartão de origens selecionado.](../assets/ui/monitor-sources/data-lake.png)

O gráfico [!UICONTROL Ingestion rate] exibe a taxa de assimilação de dados com base no intervalo de tempo configurado. Por padrão, o painel de monitoramento exibe taxas de assimilação das últimas 24 horas. Para obter etapas sobre como configurar seu intervalo de tempo, leia o guia em [configurando o intervalo de tempo de monitoramento](monitor.md#configure-monitoring-time-frame).

O gráfico é ativado para exibir por padrão. Para ocultar o gráfico, selecione **[!UICONTROL Metrics and graphs]** para desabilitar a alternância e ocultar o gráfico.

![O gráfico de métricas da taxa de assimilação.](../assets/ui/monitor-sources/metrics-graph.png)

A parte inferior do painel exibe uma tabela que descreve o relatório de métricas atuais para todos os fluxos de dados de fontes existentes.

![A tabela de métricas do painel de monitoramento.](../assets/ui/monitor-sources/metrics-table.png)

| Métricas | Descrição |
| --- | --- |
| Registros recebidos | O número total de registros recebidos de uma determinada fonte. |
| Registros assimilados | O número total de registros assimilados no data lake. |
| Registros excluídos | O número total de registros excluídos devido às configurações de retenção do data lake ou às operações de captura de dados de alteração. |
| Registros ignorados | O número total de registros ignorados. Um registro ignorado se refere a campos que foram ignorados porque não foram necessários para assimilação. Por exemplo, se você criar um fluxo de dados de origens com a assimilação parcial ativada, poderá configurar um limite de taxa de erro aceitável. Durante o processo de assimilação, a assimilação ignorará registros de campos que não são obrigatórios, como campos de identidade, desde que estejam dentro do limite de erro. |
| Registros com falha | O número total de registros que não puderam ser assimilados devido a erros. |
| Taxa de assimilação | A porcentagem de registros assimilados com base no número total de registros recebidos. |
| Total de fluxos de dados com falha | O número total de fluxos de dados que falharam. |

{style="table-layout:auto"}

Você pode filtrar ainda mais seus dados usando as opções fornecidas acima da tabela de métricas:

| Opções de filtro | Descrição |
| --- | --- |
| Pesquisa | Use a barra de pesquisa para filtrar sua exibição para um único tipo de origem. |
| Origens | Selecione **[!UICONTROL Sources]** para filtrar sua exibição e exibir dados de métrica por tipo de origem. Essa é a exibição padrão que o painel de monitoramento usa. |
| Fluxos de dados | Selecione **[!UICONTROL Dataflows]** para filtrar sua visualização e exibir dados de métrica por fluxo de dados. |
| Mostrar somente falhas | Selecione **[!UICONTROL Show failures only]** para filtrar sua visualização e exibir apenas os fluxos de dados que relataram falhas de assimilação. |
| Minhas fontes | Você pode filtrar ainda mais sua exibição usando o menu suspenso [!UICONTROL My sources]. Use o menu suspenso para filtrar sua visualização por categoria. Como alternativa, você pode selecionar **[!UICONTROL All sources]** para exibir métricas em todas as fontes ou selecionar **[!UICONTROL My sources]** para exibir somente as fontes com as quais você tem uma conta correspondente. |

{style="table-layout:auto"}

Para personalizar a exibição da coluna, selecione o ícone de configurações de coluna ![column-icon](/help/images/icons/column-settings.png).

![O painel de monitoramento com o ícone de configurações de coluna selecionado.](../assets/ui/monitor-sources/edit-columns.png)

Em seguida, use a janela *[!UICONTROL Customize table]* para selecionar as colunas que deseja que o painel exiba. Quando terminar, selecione **[!UICONTROL Apply]**.

![A janela pop-up personalizar coluna no painel de monitoramento.](../assets/ui/monitor-sources/customize-table.png)

Para monitorar os dados que estão sendo assimilados em um fluxo de dados específico, selecione o ícone de filtro ![filtro](/help/images/icons/filter-add.png) ao lado de uma origem.

>[!TIP]
>
>Você pode usar o painel de monitoramento para monitorar métricas de exclusão de dados para registros excluídos usando políticas de retenção de dados. Para obter mais informações sobre retenção de dados, leia o guia em [definindo políticas de retenção de dados](../../catalog/datasets/user-guide.md#data-retention-policy).

![Monitore um fluxo de dados específico selecionando o ícone de filtro ao lado de uma determinada fonte.](../assets/ui/monitor-sources/monitor-dataflow.png)

A tabela de métricas é atualizada para uma tabela de fluxos de dados ativos que correspondem à origem selecionada. Durante essa etapa, você pode visualizar informações adicionais sobre os fluxos de dados, incluindo o conjunto de dados e o tipo de dados correspondentes, bem como um carimbo de data e hora para indicar quando eles estavam ativos pela última vez.

Para inspecionar ainda mais um fluxo de dados, selecione o ícone de filtro ![filtro](/help/images/icons/filter-add.png) ao lado de um fluxo de dados.

![A tabela de fluxos de dados no painel de monitoramento.](../assets/ui/monitor-sources/select-dataflow.png)

Em seguida, você é direcionado a uma interface que lista todas as iterações de execução do fluxo de dados selecionado.

As execuções de fluxo de dados representam uma instância da execução do fluxo de dados. Por exemplo, se um fluxo de dados estiver agendado para ser executado por hora às 9h00, 10h10 e 11h20, você terá três instâncias de um fluxo em execução. :00:00:00 As execuções de fluxo são específicas para sua organização específica.

Para inspecionar métricas de uma iteração de execução de fluxo de dados específica, selecione o ícone de filtro ![filtro](/help/images/icons/filter-add.png) ao lado do fluxo de dados.

![A página de métrica de execução do fluxo de dados.](../assets/ui/monitor-sources/dataflow-page.png)

Use a página de detalhes da execução do fluxo de dados para exibir métricas e informações da iteração de execução selecionada.

![A página de detalhes da execução do fluxo de dados.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Detalhes de execução do fluxo de dados | Descrição |
| --- | --- |
| Registros assimilados | O número total de registros assimilados da execução do fluxo de dados. |
| Registros com falha | O número total de registros que não foram assimilados devido a erros na execução do fluxo de dados. |
| Total de arquivos | O número total de arquivos na execução do fluxo de dados. |
| Tamanho dos dados | O tamanho total dos dados contidos na execução do fluxo de dados. |
| ID de execução do fluxo de dados | A ID da iteração de execução do fluxo de dados. |
| ID da organização | A ID da organização na qual a execução do fluxo de dados foi criada. |
| Status | O status da execução do fluxo de dados. |
| Início da execução do fluxo de dados | Um carimbo de data e hora que indica quando a execução do fluxo de dados foi iniciada. |
| Término da execução do fluxo de dados | Um carimbo de data e hora que indica quando a execução do fluxo de dados terminou. |
| Conjunto de dados | O conjunto de dados usado para criar o fluxo de dados. |
| Tipo de dados | O tipo de dados que estava no fluxo de dados. |
| Ingestão parcial | A assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros até um determinado limite configurável. Esse recurso permite assimilar com sucesso todos os seus dados precisos na Experience Platform, enquanto todos os seus dados incorretos são armazenados em lote separadamente com informações sobre por que são inválidos. Você pode ativar a assimilação parcial durante o processo de criação do fluxo de dados. |
| Diagnóstico de erro | O diagnóstico de erro instrui a origem a produzir diagnósticos de erro que você poderá consultar posteriormente ao monitorar a atividade do conjunto de dados e o status do fluxo de dados. Você pode habilitar diagnósticos de erro durante o processo de criação do fluxo de dados. |
| Resumo do erro | Dada uma execução de fluxo de dados com falha, o resumo do erro exibe um código e uma descrição do erro para resumir por que a iteração de execução falhou. |

{style="table-layout:auto"}

Se o fluxo de dados executar erros, você pode rolar para baixo até a parte inferior da página usar a interface [!UICONTROL Dataflow run errors].

Use a seção [!UICONTROL Records failed] para exibir métricas em registros que não foram assimilados devido a erros. Para exibir um relatório de erros abrangente, selecione **[!UICONTROL Preview error diagnostics]**. Para baixar uma cópia do diagnóstico de erros e do manifesto de arquivo, selecione **[!UICONTROL Download]** e copie a chamada de API de exemplo a ser usada com a API [!DNL Data Access].

>[!NOTE]
>
>Você só poderá usar diagnósticos de erro se o recurso tiver sido habilitado durante o processo de criação da conexão de origem.

## Próximas etapas {#next-steps}

Seguindo este tutorial, você aprendeu a monitorar a taxa de assimilação do data lake usando o painel **[!UICONTROL Monitoring]**. Você também aprendeu a identificar erros que causam falhas de fluxo de dados durante a assimilação. Consulte os seguintes documentos para obter mais detalhes:

* [Monitorando dados de identidade](./monitor-identities.md).
* [Monitorando dados do perfil](./monitor-profiles.md).
