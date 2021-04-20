---
keywords: Experience Platform;home;popular tópicos;monitorar contas;monitorar fluxos de dados;fluxos de dados;fontes;;home;popular topics;monitor accounts;monitor dataflows;dataflows;sources
description: Este tutorial fornece etapas para monitorar seu fluxo de dados, usando visualização de monitoramento agregado e monitoramento entre serviços.
solution: Experience Platform
title: Monitorar fluxos de dados para fontes na interface do usuário
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4c668a47e62ba7736dd2d7afe4e71fd015198356
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 0%

---


# Monitorar fluxos de dados para fontes na interface do usuário

No Adobe Experience Platform, os dados são ingeridos de uma grande variedade de fontes, analisados dentro do Experience Platform e ativados para uma grande variedade de destinos. A plataforma facilita o processo de rastreamento desse fluxo potencialmente não linear de dados ao fornecer transparência com fluxos de dados.

O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Você pode usar uma visualização de monitoramento agregada e navegar verticalmente do nível de origem para um fluxo de dados e para uma execução de fluxo de dados, permitindo que você visualização as métricas correspondentes que contribuem para o sucesso ou falha de um fluxo de dados. Você também pode usar a capacidade de monitoramento entre serviços do painel de monitoramento para monitorar a jornada de um fluxo de dados de uma fonte, para [!DNL Identity Service] e para [!DNL Profile].

Este tutorial fornece etapas para monitorar seu fluxo de dados, usando visualização de monitoramento agregado e monitoramento entre serviços.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fluxos de dados](../home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de público alvo, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   * [Execução](../../sources/notifications.md) do Dataflow: Execuções de fluxo de dados são trabalhos programados recorrentes com base na configuração de frequência de fluxos de dados selecionados.
* [Fontes](../../sources/home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Serviço](../../identity-service/home.md) de identidade: Obtenha uma melhor visualização de clientes individuais e de seu comportamento ao unir identidades entre dispositivos e sistemas.
* [Perfil](../../profile/home.md) do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Visualização de monitoramento agregada

Na [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Monitoramento]** no menu de navegação esquerdo para acessar o painel [!UICONTROL Monitoramento]. O painel [!UICONTROL Monitoring] contém métricas e informações sobre todos os fluxos de dados de origem, incluindo informações sobre a integridade do tráfego de dados de uma fonte para [!DNL Identity Service] e para [!DNL Profile].

No centro do painel está o painel [!UICONTROL ingestão de origem], que contém métricas e gráficos que exibem dados em registros assimilados e que falharam.

![painel de monitoramento](../assets/ui/monitor-sources/monitoring-dashboard.png)

Por padrão, os dados exibidos contêm taxas de ingestão das últimas 24 horas. Selecione **[!UICONTROL Últimas 24 horas]** para ajustar o período de tempo dos registros apresentados.

![data de alteração](../assets/ui/monitor-sources/change-date.png)

Uma janela pop-up de calendário é exibida, fornecendo opções para intervalos de tempo de ingestão alternativos. Selecione **[!UICONTROL Últimos 30 dias]** e selecione **[!UICONTROL Aplicar]**

![horário de ajuste](../assets/ui/monitor-sources/adjust-timeframe.png)

Os gráficos são ativados por padrão e você pode desativá-los para expandir a lista de fontes abaixo. Selecione a opção **[!UICONTROL Métricas e gráficos]** para desativar os gráficos.

![métricas e gráficos](../assets/ui/monitor-sources/metrics-graphs.png)

| ingestão de origem | Descrição |
| ---------------- | ----------- |
| [!UICONTROL Registros ingeridos  ] | O número total de registros ingeridos. |
| [!UICONTROL Falha nos registros] | O número total de registros que não foram ingeridos devido a erros nos dados. |
| [!UICONTROL Total de fluxos de dados com falha] | O número total de fluxos de dados com um status `failed`. |

A lista de ingestão de origem exibe todas as fontes que contêm pelo menos uma conta existente. A lista também inclui informações sobre a taxa de ingestão de cada fonte, o número de registros com falha e o número total de fluxos de dados com falha com base no período aplicado.

![ingestão de origem](../assets/ui/monitor-sources/source-ingestion.png)

Para classificar pela lista de fontes, selecione **[!UICONTROL Minhas fontes]** e selecione sua categoria de escolha no menu suspenso. Por exemplo, para focar em armazenamentos em nuvem, selecione **[!UICONTROL armazenamento em nuvem]**

![classificar por categoria](../assets/ui/monitor-sources/sort-by-category.png)

Para visualização de todos os fluxos de dados existentes em todas as fontes, selecione **[!UICONTROL Fluxos de dados]**.

![visualização de todos os fluxos de dados](../assets/ui/monitor-sources/view-all-dataflows.png)

Como alternativa, você pode inserir uma fonte na barra de pesquisa para isolar uma única fonte. Depois que a fonte for identificada, selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele para ver uma lista de seus fluxos de dados ativos.

![pesquisa](../assets/ui/monitor-sources/search.png)

Uma lista de fluxos de dados é exibida. Para restringir a lista e o foco nos fluxos de dados com erros, selecione **[!UICONTROL Mostrar falhas apenas]**.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Localize o fluxo de dados que deseja monitorar e selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele, para ver mais informações sobre o status de execução.

![fluxo de dados](../assets/ui/monitor-sources/dataflow.png)

A página de execução de fluxo de dados exibe informações sobre a data de execução do start do seu fluxo de dados, o tamanho dos dados, o status e a duração do tempo de processamento. Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de start de execução do fluxo de dados para ver os detalhes de execução do fluxo de dados.

![start de execução de fluxo de dados](../assets/ui/monitor-sources/dataflow-run-start.png)

A página [!UICONTROL Detalhes de execução do Fluxo de Dados] exibe informações sobre os metadados do fluxo de dados, o status de ingestão parcial e o resumo do erro. O resumo do erro contém o erro de nível superior específico que mostra em qual etapa o processo de ingestão encontrou um erro.

Role para baixo para ver informações mais específicas sobre o erro ocorrido.

![detalhes da execução do fluxo de dados](../assets/ui/monitor-sources/dataflow-run-details.png)

O painel [!UICONTROL Erros de execução de fluxo de dados] exibe o erro específico e o código de erro que resultaram na falha de ingestão do fluxo de dados. Nesse cenário, ocorreu um erro de transformação do mapeador, resultando na falha de 24 registros.

Selecione **[!UICONTROL Arquivos]** para obter mais informações.

![erros de execução de dataflow](../assets/ui/monitor-sources/dataflow-run-errors.png)

O painel [!UICONTROL Arquivos] contém informações sobre o nome e o caminho do arquivo.

Para obter uma representação mais granular do erro, selecione **[!UICONTROL diagnóstico de erro de Pré-visualização]**.

![arquivos](../assets/ui/monitor-sources/files.png)

A janela [!UICONTROL pré-visualização de diagnóstico de erro] é exibida, exibindo uma pré-visualização de até 100 erros no fluxo de dados. Você pode selecionar **[!UICONTROL Baixar]** para recuperar um comando de ondulação, que permite baixar o diagnóstico de erro.

Quando terminar, selecione **[!UICONTROL Fechar]**

![diagnóstico de erros](../assets/ui/monitor-sources/error-diagnostics.png)

Você pode usar o sistema de navegação estrutural no cabeçalho superior para navegar de volta para o painel [!UICONTROL Monitoring]. Selecione **[!UICONTROL Executar start: 14/2/2021, 21:47 PM]** para retornar à página anterior e selecione **[!UICONTROL Fluxo de dados: Demonstração de ingestão de dados de fidelidade - falha]** para retornar à página de fluxos de dados.

![navegações estruturais](../assets/ui/monitor-sources/breadcrumbs.png)

## Monitorização entre serviços

A parte superior do painel contém uma representação do fluxo de ingestão do nível de origem para [!DNL Identity Service] e para [!DNL Profile]. Cada célula inclui um marcador de ponto que indica a presença de erros que ocorreram nesse estágio de ingestão. Um ponto verde significa uma ingestão sem erros, enquanto um ponto vermelho significa que ocorreu um erro nessa determinada fase de ingestão.

![monitorização entre serviços](../assets/ui/monitor-sources/cross-service-monitoring.png)

Na página de fluxo de dados, localize um fluxo de dados bem-sucedido e selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado dele para ver suas informações de execução de fluxo de dados.

![sucesso do fluxo de dados](../assets/ui/monitor-sources/dataflow-success.png)

A página [!UICONTROL ingestão de origem] contém informações que confirmam a assimilação bem-sucedida do seu fluxo de dados. Desse ponto em diante, é possível monitorar a jornada do seu fluxo de dados do nível de origem para [!DNL Identity Service] e depois para [!DNL Profile].

Selecione **[!UICONTROL Identidades]** para ver a ingestão na etapa [!UICONTROL Identidades].

![fontes](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] métricas

A página [!UICONTROL Processamento de identidade] contém informações sobre registros assimilados a [!DNL Identity Service], incluindo o número de identidades adicionadas, gráficos criados e gráficos atualizados.

Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de start de execução do fluxo de dados para ver mais informações sobre a execução do fluxo de dados [!DNL Identity].

![identidades](../assets/ui/monitor-sources/identities.png)

| Métricas de identidade | Descrição |
| ---------------- | ----------- |
| [!UICONTROL Registros recebidos] | O número de registros recebidos de [!DNL Data Lake]. |
| [!UICONTROL Falha nos registros] | O número de registros que não foram ingeridos na Plataforma devido a erros nos dados. |
| [!UICONTROL Registros ignorados] | O número de registros que foram ingeridos, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| [!UICONTROL Registros ingeridos] | O número de registros ingeridos em [!DNL Identity Service]. |
| [!UICONTROL Total de registros] | A contagem total de todos os registros, incluindo registros com falha, registros ignorados, [!DNL Identities] adicionados e registros duplicados. |
| [!UICONTROL Identidades adicionadas] | O número de novos identificadores líquidos adicionados a [!DNL Identity Service]. |
| [!UICONTROL Gráficos criados] | O número de novos gráficos de identidade criados em [!DNL Identity Service]. |
| [!UICONTROL Gráficos atualizados] | O número de gráficos de identidade existentes atualizados com novas bordas. |
| [!UICONTROL Falha ao executar o fluxo de dados] | O número de execuções de fluxo de dados que falharam. |
| [!UICONTROL Tempo de processamento] | O carimbo de data e hora desde o start da ingestão até a conclusão. |
| [!UICONTROL Status] | Define o status geral de um fluxo de dados. Os possíveis valores de status são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com a programação que foi fornecida.</li><li>`Failed`: Indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: Indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |

A página [!UICONTROL Detalhes de execução do Fluxo de Dados] exibe mais informações sobre a [!DNL Identity] execução do fluxo de dados, incluindo a ID Org IMS e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos por [!DNL Identity Service], caso ocorram erros no processo de ingestão.

Selecione **[!UICONTROL Executar start: 14/2/2021, 21:47 PM]** para retornar à página anterior.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Na página [!UICONTROL Processamento de identidade], selecione **[!UICONTROL Perfis]** para ver o status da ingestão de registros na etapa [!UICONTROL Perfis].

![seleted-perfis](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] métricas

A página [!UICONTROL processamento do Perfil] contém informações sobre registros assimilados a [!DNL Profile], incluindo o número de fragmentos de perfil criados, fragmentos de perfil atualizados e o número total de fragmentos de perfil.

Selecione o ícone de filtro ![filter](../assets/ui/monitor-sources/filter.png) ao lado do tempo de start de execução do fluxo de dados para ver mais informações sobre a execução do fluxo de dados [!DNL Profile].

![perfis](../assets/ui/monitor-sources/profiles.png)

| Métricas de perfil | Descrição |
| --------------- | ----------- |
| [!UICONTROL Registros recebidos] | O número de registros recebidos de [!DNL Data Lake]. |
| [!UICONTROL Falha nos registros  ] | O número de registros que foram ingeridos, mas não em [!DNL Profile] devido a erros. |
| [!UICONTROL Fragmentos de perfil adicionados] | O número de novos fragmentos [!DNL Profile] líquidos adicionados. |
| [!UICONTROL Fragmentos de perfil atualizados] | O número de fragmentos [!DNL Profile] existentes atualizados |
| [!UICONTROL Total de fragmentos de Perfil] | O número total de registros gravados em [!DNL Profile], incluindo todos os fragmentos [!DNL Profile] existentes atualizados e os novos fragmentos [!DNL Profile] criados. |
| [!UICONTROL Falha ao executar o fluxo de dados] | O número de execuções de fluxo de dados que falharam. |
| [!UICONTROL Tempo de processamento] | O carimbo de data e hora desde o start da ingestão até a conclusão. |
| [!UICONTROL Status] | Define o status geral de um fluxo de dados. Os possíveis valores de status são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com a programação que foi fornecida.</li><li>`Failed`: Indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: Indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |

A página [!UICONTROL Detalhes de execução do Fluxo de Dados] exibe mais informações sobre a [!DNL Profile] execução do fluxo de dados, incluindo a ID Org IMS e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos por [!DNL Profile], caso ocorram erros no processo de ingestão.

![perfis-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Próximas etapas

Ao seguir este tutorial, você monitorou com êxito o fluxo de dados de ingestão do nível de origem para [!DNL Identity Service] e para [!DNL Profile], usando o painel **[!UICONTROL Monitoring]**. Você também identificou com êxito erros que contribuíram para a falha dos fluxos de dados durante o processo de ingestão. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../profile/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../data-science-workspace/home.md)
