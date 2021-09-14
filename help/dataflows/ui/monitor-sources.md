---
keywords: Experience Platform, home, tópicos populares, monitorar contas, monitorar fluxos de dados, fluxos de dados, fontes
description: Este tutorial fornece etapas para monitorar o fluxo de dados, usando a visualização de monitoramento agregado e o monitoramento entre serviços.
solution: Experience Platform
title: Monitorar fluxos de dados para fontes na interface do usuário
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Monitorar fluxos de dados para fontes na interface do usuário

>[!IMPORTANT]
>
>Fontes de transmissão, como [HTTP API source](../../sources/connectors/streaming/http.md), não são compatíveis no momento com o painel de monitoramento. Nesse momento, você só pode usar o painel para monitorar fontes em lote.

No Adobe Experience Platform, os dados são assimilados de uma grande variedade de fontes, analisados no Experience Platform, e ativados para uma grande variedade de destinos. A Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear ao fornecer transparência com fluxos de dados.

O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Você pode usar uma visualização de monitoramento agregado e navegar verticalmente do nível de origem, para um fluxo de dados e para uma execução de fluxo de dados, permitindo exibir as métricas correspondentes que contribuem para o sucesso ou a falha de um fluxo de dados. Você também pode usar a capacidade de monitoramento entre serviços do painel de monitoramento para monitorar a jornada de um fluxo de dados de uma fonte, para [!DNL Identity Service] e para [!DNL Profile].

Este tutorial fornece etapas para monitorar o fluxo de dados, usando a visualização de monitoramento agregado e o monitoramento entre serviços.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fluxos de dados](../home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   * [O fluxo de dados é executado](../../sources/notifications.md): As execuções de fluxo de dados são trabalhos agendados recorrentes com base na configuração de frequência de fluxos de dados selecionados.
* [Fontes](../../sources/home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Serviço](../../identity-service/home.md) de identidade: Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
* [Perfil](../../profile/home.md) do cliente em tempo real: Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Exibição de monitoramento agregada

Na [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Monitoring]** no painel de navegação esquerdo para acessar o [!UICONTROL Monitoring] painel. O painel [!UICONTROL Monitoring] contém métricas e informações sobre todos os fluxos de dados de fontes, incluindo insights sobre a integridade do tráfego de dados de uma fonte para [!DNL Identity Service] e para [!DNL Profile].

No centro do painel está o painel [!UICONTROL Assimilação de origem], que contém métricas e gráficos que exibem dados em registros assimilados e que falharam.

![painel de monitoramento](../assets/ui/monitor-sources/monitoring-dashboard.png)

Por padrão, os dados exibidos contêm taxas de ingestão das últimas 24 horas. Selecione **[!UICONTROL Last 24 horas]** para ajustar o intervalo de tempo dos registros exibidos.

![data de alteração](../assets/ui/monitor-sources/change-date.png)

Uma janela pop-up do calendário é exibida, fornecendo opções para intervalos de tempo de ingestão alternativos. Selecione **[!UICONTROL Últimos 30 dias]** e selecione **[!UICONTROL Aplicar]**

![ajuste-horário](../assets/ui/monitor-sources/adjust-timeframe.png)

Os gráficos são ativados por padrão e você pode desativá-los para expandir a lista de fontes abaixo. Selecione a opção **[!UICONTROL Métricas e gráficos]** para desativar os gráficos.

![métricas e gráficos](../assets/ui/monitor-sources/metrics-graphs.png)

| Assimilação de origem | Descrição |
| ---------------- | ----------- |
| [!UICONTROL Registros assimilados  ] | O número total de registros assimilados. |
| [!UICONTROL Falha nos registros] | O número total de registros que não foram assimilados devido a erros nos dados. |
| [!UICONTROL Total de fluxos de dados com falha] | O número total de fluxos de dados com um status `failed`. |

A lista de assimilação de origem exibe todas as fontes que contêm pelo menos uma conta existente. A lista também inclui informações sobre a taxa de ingestão de cada fonte, o número de registros com falha e o número total de fluxos de dados com falha com base no período aplicado.

![ingestão de origem](../assets/ui/monitor-sources/source-ingestion.png)

Para classificar pela lista de fontes, selecione **[!UICONTROL Minhas fontes]** e selecione sua categoria de escolha no menu suspenso. Por exemplo, para se concentrar nos armazenamentos de nuvem, selecione **[!UICONTROL Cloud storage]**

![classificar por categoria](../assets/ui/monitor-sources/sort-by-category.png)

Para exibir todos os fluxos de dados existentes em todas as fontes, selecione **[!UICONTROL Fluxos de dados]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Como alternativa, você pode inserir uma fonte na barra de pesquisa para isolar uma única fonte. Depois de identificar a fonte, selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele para ver uma lista de seus fluxos de dados ativos.

![pesquisa](../assets/ui/monitor-sources/search.png)

Uma lista de fluxos de dados é exibida. Para restringir a lista e concentrar-se nos fluxos de dados com erros, selecione **[!UICONTROL Mostrar falhas somente]**.

![show-failed-only](../assets/ui/monitor-sources/show-failures-only.png)

Localize o fluxo de dados que deseja monitorar e selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele, para ver mais informações sobre o status de execução.

![fluxo de dados](../assets/ui/monitor-sources/dataflow.png)

A página de execução do fluxo de dados exibe informações sobre a data de início da execução do fluxo de dados, o tamanho dos dados, o status e a duração do tempo de processamento. Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de início da execução do fluxo de dados para ver os detalhes de execução do fluxo de dados.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

A página [!UICONTROL Detalhes de execução do fluxo de dados] exibe informações sobre os metadados do fluxo de dados, o status de assimilação parcial e o resumo do erro. O resumo do erro contém o erro de nível superior específico que mostra em qual etapa o processo de assimilação encontrou um erro.

Role para baixo para ver informações mais específicas sobre o erro que ocorreu.

![detalhes de execução do fluxo de dados](../assets/ui/monitor-sources/dataflow-run-details.png)

O painel [!UICONTROL Dataflow run errors] exibe o erro específico e o código de erro que resultaram na falha de assimilação do fluxo de dados. Nesse cenário, ocorreu um erro de transformação do mapeador, resultando na falha de 24 registros.

Selecione **[!UICONTROL Arquivos]** para obter mais informações.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

O painel [!UICONTROL Arquivos] contém informações sobre o nome e o caminho do arquivo.

Para obter uma representação mais granular do erro, selecione **[!UICONTROL Preview error diagnostics]**.

![arquivos](../assets/ui/monitor-sources/files.png)

A janela [!UICONTROL Error diagnostics preview] é exibida, exibindo uma visualização de até 100 erros no fluxo de dados. Você pode selecionar **[!UICONTROL Download]** para recuperar um comando curl, o que permite baixar o diagnóstico de erro.

Quando terminar, selecione **[!UICONTROL Fechar]**

![diagnóstico de erros](../assets/ui/monitor-sources/error-diagnostics.png)

Você pode usar o sistema de navegação estrutural no cabeçalho superior para navegar de volta para o painel [!UICONTROL Monitoring]. Selecione **[!UICONTROL Executar início: 14/2/2021, 21:47 PM]** para retornar à página anterior e, em seguida, selecionar **[!UICONTROL Fluxo de dados: Demonstração da assimilação de dados de fidelidade - Falha]** ao retornar à página de fluxos de dados.

![navegação estrutural](../assets/ui/monitor-sources/breadcrumbs.png)

## Monitoramento entre serviços

A parte superior do painel contém uma representação do fluxo de assimilação do nível de origem, para [!DNL Identity Service] e para [!DNL Profile]. Cada célula inclui um marcador de ponto que indica a presença de erros que ocorreram nesse estágio de assimilação. Um ponto verde significa uma ingestão sem erros, enquanto um ponto vermelho significa que ocorreu um erro nessa determinada etapa de ingestão.

![monitoramento entre serviços](../assets/ui/monitor-sources/cross-service-monitoring.png)

Na página de fluxos de dados, localize um fluxo de dados bem-sucedido e selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele, para ver suas informações de execução do fluxo de dados.

![sucesso do fluxo de dados](../assets/ui/monitor-sources/dataflow-success.png)

A página [!UICONTROL Assimilação de origem] contém informações que confirmam a assimilação bem-sucedida do seu fluxo de dados. A partir daqui, você pode começar a monitorar a jornada do seu fluxo de dados do nível de origem para [!DNL Identity Service] e depois para [!DNL Profile].

Selecione **[!UICONTROL Identities]** para ver a assimilação no estágio [!UICONTROL Identities].

![fontes](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] métricas

A página [!UICONTROL Processamento de identidade] contém informações sobre registros assimilados a [!DNL Identity Service], incluindo o número de identidades adicionadas, gráficos criados e gráficos atualizados.

Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de início da execução do fluxo de dados para ver mais informações sobre a [!DNL Identity] execução do fluxo de dados.

![identidades](../assets/ui/monitor-sources/identities.png)

| Métricas de identidade | Descrição |
| ---------------- | ----------- |
| [!UICONTROL Registros recebidos] | O número de registros recebidos de [!DNL Data Lake]. |
| [!UICONTROL Falha nos registros] | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| [!UICONTROL Registros ignorados] | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| [!UICONTROL Registros assimilados] | O número de registros assimilados em [!DNL Identity Service]. |
| [!UICONTROL Total de registros] | A contagem total de todos os registros, incluindo registros com falha, registros ignorados, [!DNL Identities] adicionados e registros duplicados. |
| [!UICONTROL Identidades adicionadas] | O número de novos identificadores líquidos adicionados a [!DNL Identity Service]. |
| [!UICONTROL Gráficos criados] | O número de novos gráficos de identidade criados em [!DNL Identity Service]. |
| [!UICONTROL Gráficos atualizados] | O número de gráficos de identidade existentes atualizados com novas bordas. |
| [!UICONTROL Falha na execução do fluxo de dados] | O número de execuções de fluxo de dados que falharam. |
| [!UICONTROL Tempo de processamento] | O carimbo de data e hora desde o início da assimilação até a conclusão. |
| [!UICONTROL Status] | Define o status geral de um fluxo de dados. Os valores de status possíveis são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com o cronograma que foi fornecido.</li><li>`Failed`: Indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: Indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |

A página [!UICONTROL Detalhes de execução do fluxo de dados] exibe mais informações sobre a [!DNL Identity] execução do fluxo de dados, incluindo a ID de organização IMS e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos por [!DNL Identity Service], caso ocorra algum erro no processo de assimilação.

Selecione **[!UICONTROL Executar início: 14/2/2021, 21:47 PM]** para retornar à página anterior.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Na página [!UICONTROL Identity processing], selecione **[!UICONTROL Profiles]** para ver o status da assimilação de registros na etapa [!UICONTROL Profiles].

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] métricas

A página [!UICONTROL Profile processing] contém informações sobre registros assimilados a [!DNL Profile], incluindo o número de fragmentos de perfil criados, fragmentos de perfil atualizados e o número total de fragmentos de perfil.

Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de início da execução do fluxo de dados para ver mais informações sobre a [!DNL Profile] execução do fluxo de dados.

![perfis](../assets/ui/monitor-sources/profiles.png)

| Métricas de perfil | Descrição |
| --------------- | ----------- |
| [!UICONTROL Registros recebidos] | O número de registros recebidos de [!DNL Data Lake]. |
| [!UICONTROL Falha nos registros  ] | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| [!UICONTROL Fragmentos de perfil adicionados] | O número de novos fragmentos [!DNL Profile] líquidos adicionados. |
| [!UICONTROL Fragmentos de perfil atualizados] | O número de fragmentos [!DNL Profile] existentes atualizados |
| [!UICONTROL Total de fragmentos de perfil] | O número total de registros escritos em [!DNL Profile], incluindo todos os fragmentos [!DNL Profile] existentes atualizados e os novos fragmentos [!DNL Profile] criados. |
| [!UICONTROL Falha na execução do fluxo de dados] | O número de execuções de fluxo de dados que falharam. |
| [!UICONTROL Tempo de processamento] | O carimbo de data e hora desde o início da assimilação até a conclusão. |
| [!UICONTROL Status] | Define o status geral de um fluxo de dados. Os valores de status possíveis são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com o cronograma que foi fornecido.</li><li>`Failed`: Indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: Indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |

A página [!UICONTROL Detalhes de execução do fluxo de dados] exibe mais informações sobre a [!DNL Profile] execução do fluxo de dados, incluindo a ID de organização IMS e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos por [!DNL Profile], caso ocorra algum erro no processo de assimilação.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Próximas etapas

Ao seguir este tutorial, você monitorou com êxito o fluxo de dados de assimilação do nível de origem para [!DNL Identity Service] e para [!DNL Profile], usando o painel **[!UICONTROL Monitoring]**. Você também identificou com sucesso erros que contribuíram para a falha dos fluxos de dados durante o processo de assimilação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do perfil do cliente em tempo real](../../profile/home.md)
* [Visão geral do Data Science Workspace](../../data-science-workspace/home.md)
