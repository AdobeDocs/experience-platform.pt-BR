---
keywords: Experience Platform;página inicial;tópicos populares;monitorar segmentos;monitorar fluxos de dados;fluxos de dados;segmentação
description: A segmentação permite criar segmentos e públicos a partir dos dados do Perfil do cliente em tempo real. Este tutorial fornece instruções sobre como monitorar fluxos de dados durante a segmentação usando a interface do usuário Experience Platform.
title: Monitorar fluxos de dados para segmentos na interface do
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 5%

---

# Monitorar fluxos de dados para segmentos na interface do

O Serviço de segmentação permite criar segmentos e públicos a partir dos dados do Perfil do cliente em tempo real na Adobe Experience Platform. A Platform fornece fluxos de dados para rastrear de forma transparente esse fluxo de dados de origens para destinos.

O painel de monitoramento fornece uma representação visual da atividade dos dados em um segmento, incluindo o status da segmentação dos dados. Este tutorial fornece instruções sobre como usar o painel de monitoramento para monitorar a segmentação de dados usando a interface do usuário do Experience Platform, permitindo rastrear o status de ativação de segmentos, avaliação e trabalhos de exportação.

## Introdução {#getting-started}

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino para [!DNL Identity] e [!DNL Profile], e para [!DNL Destinations].
   - [O fluxo de dados é executado](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
- [Segmentação](../../segmentation/home.md): a segmentação permite criar segmentos e públicos a partir dos dados do Perfil do cliente em tempo real.
   - [Trabalhos de ativação](../../destinations/ui/activation-overview.md): um trabalho de ativação é usado para ativar seu segmento para um destino especificado.
   - [Trabalhos de avaliação](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): um trabalho de avaliação é um processo assíncrono que é executado e cria um segmento de público-alvo com base no segmento especificado.
   - [Exportar trabalhos](../../segmentation/api/export-jobs.md): um trabalho de exportação é um processo assíncrono usado para manter membros do segmento de público-alvo para conjuntos de dados.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Painel de monitoramento de segmentos {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Segmentos"
>abstract="A visualização de segmentos contém informações sobre todos os segmentos da sua Organização, com mais informações sobre os processos de ativação e avaliação."

Para acessar o **[!UICONTROL Segmentos]** painel, selecione **[!UICONTROL Monitoramento]** no painel de navegação esquerdo. Uma vez no **[!UICONTROL Monitoramento]** selecione a **[!UICONTROL Segmentos]** cartão.

![O cartão Segmentos. As informações sobre o último trabalho de avaliação e o último trabalho de exportação são mostradas.](../assets/ui/monitor-segments/segment-card-monitoring.png)

No principal **[!UICONTROL Segmentos]** painel, o **[!UICONTROL Segmentos]** mostra o status e a data do último trabalho de avaliação e do último trabalho de exportação.

O painel em si contém métricas para segmentos e trabalhos de segmento. Por padrão, o painel exibirá as métricas de segmento das últimas 24 horas. Para saber mais sobre a visualização de trabalhos do segmento, leia a [monitoramento de trabalhos do segmento](#monitoring-segment-jobs-dashboard) seção.

>[!IMPORTANT]
>
>Atualmente, somente os segmentos ativados para [destinos em lote (baseados em arquivo)](../../destinations/destination-types.md#file-based) são compatíveis com o painel de segmentos de monitoramento.

![O painel de segmentos. As informações sobre os diferentes segmentos em sua organização e sandbox são exibidas.](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Nome do segmento]** | O nome do segmento. |
| **[!UICONTROL Carimbo de data e hora da última avaliação]** | A data e a hora em que o último trabalho de avaliação do segmento foi executado. |
| **[!UICONTROL Status da última avaliação]** | O status do último trabalho de avaliação do segmento. Os valores possíveis incluem **[!UICONTROL Sucesso]**, **[!UICONTROL Nenhuma execução]**, e **[!UICONTROL Failed]**. |
| **[!UICONTROL Últimos perfis de avaliação]** | O número de perfis que foram avaliados no último trabalho de avaliação do segmento. |
| **[!UICONTROL Carimbo de data/hora da última ativação]** | A data e a hora em que o último trabalho de ativação do segmento foi executado. |
| **[!UICONTROL Status da última ativação]** | O status do último trabalho de ativação do segmento. Os valores possíveis incluem **[!UICONTROL Sucesso]**, **[!UICONTROL Nenhuma execução]**, e **[!UICONTROL Failed]**. |
| **[!UICONTROL Identidades da última ativação]** | O número de identidades que foram ativadas no último trabalho de ativação do segmento. |
| **[!UICONTROL Destino da última ativação]** | O nome do destino em que o último trabalho de ativação do segmento foi ativado. |

Você pode filtrar os resultados para um segmento específico e visualizar seus trabalhos de segmento selecionando o ícone de filtro (![O ícone de filtro.](../assets/ui/monitor-segments/filter-icon.png)). Os trabalhos de segmento são classificados em ordem cronológica, com os trabalhos de segmento mais recentes aparecendo primeiro.

![O ícone de filtro é realçado. Selecionar essa opção permite exibir os trabalhos de segmento para o segmento especificado.](../assets/ui/monitor-segments/filter-segment.png)

O painel de segmentos filtrados é exibido. A variável **[!UICONTROL Segmentos]** mostra o status e a data do último trabalho de avaliação e do último trabalho de ativação.

![O cartão Segmentos. As informações sobre o último trabalho de avaliação e o último trabalho de ativação são mostradas.](../assets/ui/monitor-segments/specified-segment-card.png)

O próprio painel exibe a hora e o status dos últimos trabalhos de avaliação e ativação, um gráfico que mostra a contagem de perfis da avaliação do segmento e as métricas para os trabalhos do segmento que foram executados. Por padrão, o painel mostra as métricas de trabalho do segmento das últimas 24 horas.

![O painel do segmento filtrado. As informações sobre os vários trabalhos de segmento que foram executados para este segmento são exibidas.](../assets/ui/monitor-segments/filter-specified-segment.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Início do trabalho]** | A data e a hora em que o trabalho de segmento começou. |
| **[!UICONTROL Tipo]** | Indica o tipo de trabalho do segmento. Os dois tipos de trabalho compatíveis são **ativação** e **avaliação** tarefas. |
| **[!UICONTROL Trabalho concluído]** | A data e a hora em que o trabalho do segmento foi concluído. |
| **[!UICONTROL Tempo de processamento]** | O tempo necessário para a conclusão do trabalho do segmento. |
| **[!UICONTROL Status da tarefa]** | O status do trabalho do segmento. Os valores compatíveis incluem **[!UICONTROL Sucesso]**, **[!UICONTROL Em andamento]**, e **[!UICONTROL Failed]**. |
| **[!UICONTROL Contagem de perfis]** | O número de perfis que o trabalho de segmento está avaliando. Cada usuário deve ter um perfil exclusivo. |
| **[!UICONTROL Contagem de identidades]** | O número de identidades que o trabalho do segmento está ativando. Cada perfil pode ter várias identidades. Por exemplo, um perfil pode ter um email, um número de telefone e um número de fidelidade como identidades. |
| **[!UICONTROL Nome do destino]** | O nome do destino em que o trabalho de segmento está sendo ativado. |

Você pode filtrar ainda mais para um trabalho de segmento específico e ver seus detalhes selecionando o ícone de filtro (![O ícone de filtro.](../assets/ui/monitor-segments/filter-icon.png)). Há dois tipos diferentes de trabalhos de segmento que podem ser filtrados: trabalhos de ativação e trabalhos de avaliação.

### Detalhes do trabalho de ativação {#activation-job-details}

A página de detalhes da execução do fluxo de dados do trabalho de ativação mostra informações sobre as métricas de execução, os erros de execução do fluxo de dados e os segmentos relacionados ao trabalho do segmento. Um trabalho de ativação é usado para ativar seu segmento para um destino especificado. Por padrão, a página de detalhes mostra os erros de execução do fluxo de dados.

![O painel do segmento filtrado. As informações sobre os vários trabalhos de segmento que foram executados para este segmento são exibidas.](../assets/ui/monitor-segments/activation-job-details.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Perfis recebidos]** | O número total de perfis recebidos no fluxo de ativação. |
| **[!UICONTROL Identidades ativadas]** | O número total de identidades ativadas com êxito para o destino, com base nos perfis recebidos. |
| **[!UICONTROL Identidades excluídas]** | O número total de identidades que foram excluídas de serem ativadas para o destino, com base nos perfis recebidos. Essas identidades podem ser excluídas devido à ausência de atributos ou violações de consentimento. |
| **[!UICONTROL Tamanho dos dados]** | O tamanho do fluxo de dados que está sendo ativado. |
| **[!UICONTROL Total de arquivos]** | O número total de arquivos ativados no fluxo de dados. |
| **[!UICONTROL Status]** | O status atual do trabalho de ativação. |
| **[!UICONTROL Início da execução do fluxo de dados]** | A data e a hora em que o trabalho de ativação foi iniciado. |
| **[!UICONTROL Fim da execução do fluxo de dados]** | A data e a hora em que o trabalho de ativação terminou. |
| **[!UICONTROL ID de execução do fluxo de dados]** | A ID do trabalho de ativação atual. |
| **[!UICONTROL ID da Organização IMS]** | A ID da organização à qual o trabalho de ativação pertence. |
| **[!UICONTROL Nome do destino]** | O nome do destino no qual os dados estão sendo ativados. |

Abaixo das métricas, é exibido um botão para alternar entre os erros de execução do fluxo de dados e os segmentos.

![O painel de segmentos filtrados. A alternância usada para alternar entre os erros de execução do fluxo de dados e a exibição dos segmentos é realçada.](../assets/ui/monitor-segments/activation-job-details-toggle.png)

Na seção erros de execução do fluxo de dados, selecione a alternância para exibir as identidades que falharam ou os campos de identidades excluídos. A seção de erros inclui detalhes sobre o código de erro e o número de identidades que falharam ou foram excluídas.

![O painel do segmento filtrado. As informações sobre as identidades que falharam ou foram excluídas são destacadas.](../assets/ui/monitor-segments/activation-job-details.png)

Na seção segmentos, é possível ver uma lista de segmentos que foram ativados como parte do trabalho de ativação. Use a barra de pesquisa para filtrar a lista de segmentos por nome.

![O painel do segmento filtrado. As informações sobre as identidades que falharam ou foram excluídas são destacadas.](../assets/ui/monitor-segments/activation-job-details-segments.png)

Para a seção segmentos, as seguintes métricas estão disponíveis:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Nome]** | O nome do segmento que foi ativado. |
| **[!UICONTROL Identidades ativadas]** | O número total de identidades ativadas com êxito para o destino, com base nos perfis recebidos. |
| **[!UICONTROL Identidades excluídas]** | O número total de identidades que foram excluídas de serem ativadas para o destino, com base nos perfis recebidos. Essas identidades podem ser excluídas devido à ausência de atributos ou violação de consentimento. |
| **[!UICONTROL Status da última execução do fluxo de dados]** | O status do último trabalho de ativação executado para esse segmento. |
| **[!UICONTROL Data da última execução do fluxo de dados]** | A data e a hora do último trabalho de ativação executado para esse segmento. |

### Detalhes do trabalho de avaliação {#evaluation-job-details}

A página de detalhes da execução do fluxo de dados do trabalho de avaliação mostra informações sobre as métricas de execução e os segmentos relacionados ao trabalho do segmento. Um trabalho de avaliação é um processo assíncrono que cria um segmento de público-alvo com base no segmento especificado. Para saber mais sobre tarefas de avaliação, leia o tutorial em [avaliação de um segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![O painel de tarefas de avaliação. As informações sobre o trabalho de avaliação do segmento são exibidas.](../assets/ui/monitor-segments/evaluation-job-details.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Total de perfis]** | O número total de perfis que estão sendo avaliados. |
| **[!UICONTROL Status]** | O status do trabalho de avaliação. Os possíveis status do trabalho de avaliação incluem **[!UICONTROL Sucesso]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Início do trabalho]** | A data e a hora em que o trabalho de avaliação foi iniciado. |
| **[!UICONTROL Fim do trabalho]** | A data e a hora em que o trabalho de avaliação terminou. |
| **[!UICONTROL Tipo de trabalho]** | O tipo de trabalho do segmento. Nesse caso, sempre será um trabalho de avaliação de segmento. |
| **[!UICONTROL Tipo de avaliação]** | O tipo de avaliação que está sendo feita. Isso pode ser **[!UICONTROL Lote]** ou **[!UICONTROL Streaming]**. |
| **[!UICONTROL ID da tarefa]** | A ID do trabalho de avaliação. |
| **[!UICONTROL ID da Organização IMS]** | A ID da organização à qual o trabalho de avaliação pertence. |
| **[!UICONTROL Nome do segmento]** | O nome do segmento que está sendo avaliado. |
| **[!UICONTROL ID do segmento]** | A ID do segmento que está sendo avaliado. |

Na seção segmentos, você pode ver uma lista de segmentos que estão sendo avaliados como parte do trabalho de avaliação. Você pode filtrar a lista de segmentos por nome usando a barra de pesquisa.

>[!IMPORTANT]
>
>No momento, essa visualização de painel aceita até 800 métricas de segmento.

Para a seção segmentos, as seguintes métricas estão disponíveis:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Nome]** | O nome do segmento que está sendo avaliado. |
| **[!UICONTROL Contagem de perfis]** | O número de perfis que estão sendo avaliados. |

## Painel de monitoramento de processos do segmento {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Processos de segmento"
>abstract="A visualização de processos de segmento contém informações sobre os processos de avaliação e exportação para todos os seus segmentos."

Para acessar o **[!UICONTROL Trabalhos do segmento]** painel, selecione **[!UICONTROL Monitoramento]** (![ícone de monitoramento](../assets/ui/monitor-destinations/monitoring-icon.png)) na navegação à esquerda. Uma vez no [!UICONTROL Monitoramento] selecione **[!UICONTROL Trabalhos do segmento]**. A variável [!UICONTROL Monitoramento] o painel contém métricas e informações sobre os trabalhos de avaliação e exportação de segmentos.

>[!NOTE]
>
>Somente **trabalhos de avaliação de segmento** são compatíveis com monitoramento por segmento. Os trabalhos de exportação de segmento só oferecem suporte ao monitoramento no nível da organização.

![Painel de monitoramento de trabalhos do segmento](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

Use o [!UICONTROL Trabalhos do segmento] painel para entender se a avaliação e a exportação de perfis ocorrem no prazo e sem exceções, de modo que os serviços downstream para ativação de destino possam ter os dados de perfil avaliados mais recentemente.

As seguintes métricas estão disponíveis para trabalhos de segmento:

| Métrica | Descrição |
---------|----------|
| **[!UICONTROL Trabalho de segmento]** | Indica o nome do trabalho de segmento. |
| **[!UICONTROL Tipo]** | Indica o tipo de trabalho do segmento - exportação ou avaliação. Observe que, em ambos os casos, o trabalho do segmento avalia ou exporta **all** segmentos pertencentes a uma organização. Para saber mais sobre processos de exportação, leia o guia no [exportar ponto de extremidade de trabalhos](../../segmentation/api/export-jobs.md). Para saber mais sobre tarefas de avaliação, leia o tutorial em [avaliação de um segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Início do trabalho]** | A data e a hora em que o trabalho de segmento começou. |
| **[!UICONTROL Fim do trabalho]** | A data e a hora em que o trabalho do segmento foi concluído. |
| **[!UICONTROL Status]** | O status do trabalho concluído. Os status possíveis para o trabalho de segmento incluem sucesso ou falha. |
