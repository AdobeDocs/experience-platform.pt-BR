---
description: Saiba como monitorar os fluxos de dados durante a segmentação usando a interface do usuário do Experience Platform.
title: Monitorar fluxos de dados para públicos na interface
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 4%

---

# Monitorar fluxos de dados para públicos na interface

O Serviço de Segmentação permite criar públicos-alvo por meio de definições de segmento ou outras fontes de seus dados do [!DNL Real-Time Customer Profile]. O Experience Platform fornece fluxos de dados para rastrear de forma transparente esse fluxo de dados de origens para destinos.

Use o painel de monitoramento para ver uma representação visual da atividade dos dados em um público-alvo, incluindo o status da segmentação dos seus dados. Leia o tutorial para obter instruções sobre como usar o painel de monitoramento para monitorar a segmentação de dados usando a interface do usuário do Experience Platform, permitindo acompanhar o status dos trabalhos de ativação, avaliação e exportação de público-alvo.

## Introdução {#getting-started}

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Experience Platform. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   - [Execuções de fluxo de dados](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
- [Segmentação](../../segmentation/home.md): a segmentação permite criar públicos a partir dos dados do Perfil do cliente em tempo real.
   - [Trabalhos de ativação](../../destinations/ui/activation-overview.md): um trabalho de ativação é usado para ativar seu público para um destino especificado.
   - [Trabalhos de avaliação](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): um trabalho de avaliação é um processo assíncrono que avalia o público-alvo.
   - [Trabalhos de exportação](../../segmentation/api/export-jobs.md): um trabalho de exportação é um processo assíncrono usado para manter membros do público-alvo em conjuntos de dados.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Monitorar o painel de públicos-alvo {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Públicos-alvo"
>abstract="A exibição de públicos-alvo contém informações sobre todos os públicos-alvo da organização, com mais informações sobre os processos de ativação e avaliação."

Para acessar o painel **[!UICONTROL Audiences]**, selecione **[!UICONTROL Monitoring]** na navegação à esquerda. Na página **[!UICONTROL Monitoring]**, selecione o cartão **[!UICONTROL Audiences]**.

![O cartão Públicos-alvo. São mostradas informações sobre o último trabalho de avaliação e o último trabalho de exportação.](../assets/ui/monitor-audiences/audience-card.png)

No painel **[!UICONTROL Audiences]** principal, o cartão **[!UICONTROL Audiences]** mostra o status e a data do último trabalho de avaliação e do último trabalho de exportação.

O próprio painel contém métricas para públicos-alvo e trabalhos de segmentação. Por padrão, o painel mostra as métricas de público-alvo das últimas 24 horas. Para saber mais sobre a exibição de trabalhos de segmentação, leia a seção [trabalhos de segmentação de monitoramento](#monitoring-segmentation-jobs-dashboard).

>[!IMPORTANT]
>
>Atualmente, somente os públicos-alvo ativados para [destinos em lote (baseados em arquivo)](../../destinations/destination-types.md#file-based) têm suporte no painel de monitoramento de públicos-alvo.

![O painel de públicos-alvo. Informações sobre os diferentes públicos-alvo na sua organização e sandbox são exibidas.](../assets/ui/monitor-audiences/audience-dashboard.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Audience name]** | O nome do público. |
| **[!UICONTROL Data type]** | O tipo de dados do público. Os valores possíveis incluem **[!UICONTROL Customer]**, **[!UICONTROL Account]** e **[!UICONTROL Prospect]**. Você pode visualizar públicos-alvo de um tipo de dados especificado usando o filtro [!UICONTROL Data type] acima da faixa de opções de cartões. |
| **[!UICONTROL Last evaluation timestamp]** | A data e a hora em que o último trabalho de avaliação do público-alvo foi executado. |
| **[!UICONTROL Last evaluation status]** | O status do último trabalho de avaliação do público-alvo. Os valores possíveis incluem **[!UICONTROL Success]**, **[!UICONTROL No runs]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Last evaluation method]** | O método de avaliação do público. Como só há suporte para segmentação em lote, o único valor possível é **[!UICONTROL Batch]**. |
| **[!UICONTROL Last evaluation profiles]** | O número de perfis que foram avaliados no último trabalho de avaliação do público-alvo. |
| **[!UICONTROL Last activation timestamp]** | A data e a hora em que o último trabalho de ativação do público-alvo foi executado. |
| **[!UICONTROL Last activation status]** | O status do último trabalho de ativação do público-alvo. Os valores possíveis incluem **[!UICONTROL Success]**, **[!UICONTROL No runs]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Last activation identities]** | O número de identidades que foram ativadas no último trabalho de ativação do público-alvo. |
| **[!UICONTROL Last activation destination]** | O nome do destino em que o último trabalho de ativação do público-alvo foi ativado. |

Você pode filtrar os resultados para um público-alvo específico e exibir seus trabalhos de segmentação selecionando o ícone de filtro (![O ícone de filtro.](/help/images/icons/filter-add.png)). Os trabalhos de segmentação são classificados em ordem cronológica, com os trabalhos de segmentação mais recentes aparecendo primeiro.

![O ícone de filtro está realçado. Selecionar essa opção permite exibir os trabalhos de segmentação para o público-alvo especificado.](../assets/ui/monitor-audiences/filter-audience.png)

O painel de público-alvo filtrado é exibido. O cartão **[!UICONTROL Audiences]** mostra o status e a data do último trabalho de avaliação e do último trabalho de ativação.

![O cartão Públicos-alvo. São mostradas informações sobre o último trabalho de avaliação e o último trabalho de ativação.](../assets/ui/monitor-audiences/specified-audience-card.png)

O próprio painel exibe a hora e o status dos últimos trabalhos de avaliação e ativação, um gráfico que mostra a contagem de perfis da avaliação de público-alvo e as métricas para os trabalhos de segmentação que foram executados. Por padrão, o painel mostra as métricas de trabalho de segmentação das últimas 24 horas.

![O painel do público-alvo filtrado. São exibidas informações sobre os vários trabalhos de segmentação executados para este público-alvo.](../assets/ui/monitor-audiences/filter-audience.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Job start]** | A data e a hora em que o trabalho de segmentação foi iniciado. |
| **[!UICONTROL Type]** | Indica o tipo do trabalho de segmentação. Os dois tipos de trabalho com suporte são trabalhos de **ativação** e **avaliação**. |
| **[!UICONTROL Job complete]** | A data e a hora em que o trabalho de segmentação foi concluído. |
| **[!UICONTROL Processing time]** | O tempo necessário para a conclusão do trabalho de segmentação. |
| **[!UICONTROL Job status]** | O status do trabalho de segmentação. Os valores suportados incluem **[!UICONTROL Success]**, **[!UICONTROL In Progress]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Profile count]** | O número de perfis que o trabalho de segmentação está avaliando. Cada usuário deve ter um perfil exclusivo. |
| **[!UICONTROL Identity activated]** | O número de identidades que o trabalho de segmentação está ativando. Cada perfil pode ter várias identidades. Por exemplo, um perfil pode ter um email, um número de telefone e um número de fidelidade como identidades. |
| **[!UICONTROL Destination name]** | O nome do destino em que o trabalho de segmentação está sendo ativado. |

Você pode filtrar ainda mais para um trabalho de segmentação específico e ver seus detalhes selecionando o ícone de filtro (![O ícone de filtro.](/help/images/icons/filter.png)). Há dois tipos diferentes de trabalhos de segmentação que podem ser filtrados: trabalhos de ativação e trabalhos de avaliação.

### Detalhes do trabalho de ativação {#activation-job-details}

A página de detalhes da execução do fluxo de dados do trabalho de ativação mostra informações sobre as métricas de execução, os erros de execução do fluxo de dados e os públicos-alvo relacionados ao trabalho de segmentação. Um trabalho de ativação é usado para ativar seu público-alvo para um destino especificado.

![O painel do trabalho de ativação. São exibidas informações sobre os vários trabalhos de segmentação executados para este público-alvo.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Profiles received]** | O número total de perfis recebidos no fluxo de ativação. |
| **[!UICONTROL Identities activated]** | O número total de identidades ativadas com êxito para o destino, com base nos perfis recebidos. |
| **[!UICONTROL Identities excluded]** | O número total de identidades que foram excluídas de serem ativadas para o destino, com base nos perfis recebidos. Essas identidades podem ser excluídas devido à ausência de atributos ou violações de consentimento. |
| **[!UICONTROL Size of data]** | O tamanho do fluxo de dados que está sendo ativado. |
| **[!UICONTROL Total files]** | O número total de arquivos ativados no fluxo de dados. |
| **[!UICONTROL Status]** | O status atual do trabalho de ativação. |
| **[!UICONTROL Dataflow run start]** | A data e a hora em que o trabalho de ativação foi iniciado. |
| **[!UICONTROL Dataflow run end]** | A data e a hora em que o trabalho de ativação terminou. |
| **[!UICONTROL Dataflow run ID]** | A ID do trabalho de ativação atual. |
| **[!UICONTROL IMS org ID]** | A ID da organização à qual o trabalho de ativação pertence. |
| **[!UICONTROL Destination name]** | O nome do destino no qual os dados estão sendo ativados. |

Na seção públicos-alvo, é possível ver uma lista de públicos-alvo que foram ativados como parte do trabalho de ativação.

![O painel do trabalho de ativação. As informações sobre as identidades que falharam ou foram excluídas são destacadas.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Para a seção Públicos-alvo, as seguintes métricas estão disponíveis:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Name]** | O nome do público-alvo que foi ativado. |
| **[!UICONTROL Identities activated]** | O número total de identidades ativadas com êxito para o destino, com base nos perfis recebidos. |
| **[!UICONTROL Identities excluded]** | O número total de identidades que foram excluídas de serem ativadas para o destino, com base nos perfis recebidos. Essas identidades podem ser excluídas devido à ausência de atributos ou violação de consentimento. |
| **[!UICONTROL Last dataflow run status]** | O status do último trabalho de ativação executado para esse público-alvo. |
| **[!UICONTROL Last dataflow run date]** | A data e a hora do último trabalho de ativação executado para esse público-alvo. |

Além disso, você pode exibir detalhes sobre os erros de execução do fluxo de dados. Na seção erros de execução do fluxo de dados, é possível exibir as identidades que falharam ou que foram excluídas. A seção de erros inclui detalhes sobre o código de erro e o número de identidades que falharam ou foram excluídas.

![O painel do trabalho de ativação. As informações sobre as identidades que falharam ou foram excluídas são destacadas.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Detalhes do trabalho de avaliação {#evaluation-job-details}

A página de detalhes da execução do fluxo de dados do trabalho de avaliação mostra informações sobre as métricas e os públicos-alvo da execução relacionados ao trabalho de segmentação.

![O painel de trabalho de avaliação. Informações sobre o trabalho de avaliação do público são exibidas.](../assets/ui/monitor-audiences/evaluation-job-details.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Total profiles]** | O número total de perfis que estão sendo avaliados. |
| **[!UICONTROL Status]** | O status do trabalho de avaliação. Os possíveis status do trabalho de avaliação incluem **[!UICONTROL Success]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Job start]** | A data e a hora em que o trabalho de avaliação foi iniciado. |
| **[!UICONTROL Job end]** | A data e a hora em que o trabalho de avaliação terminou. |
| **[!UICONTROL Job type]** | O tipo de trabalho de segmentação. Nesse caso, sempre será um trabalho **[!UICONTROL Segment evaluation]**. |
| **[!UICONTROL Evaluation type]** | O tipo de avaliação que está sendo feita. Pode ser **[!UICONTROL Batch]** ou **[!UICONTROL Streaming]**. |
| **[!UICONTROL Job ID]** | A ID do trabalho de avaliação. |
| **[!UICONTROL IMS org ID]** | A ID da organização à qual o trabalho de avaliação pertence. |
| **[!UICONTROL Audience name]** | O nome do público-alvo que está sendo avaliado. |
| **[!UICONTROL Audience ID]** | A ID do público-alvo que está sendo avaliado. |

Na seção [!UICONTROL Audiences], você pode ver uma lista de públicos-alvo que estão sendo avaliados como parte do trabalho de avaliação. Você pode filtrar a lista de públicos-alvo por nome usando a barra de pesquisa.

>[!IMPORTANT]
>
>Atualmente, essa visualização de painel aceita até 800 métricas de público-alvo.

Para a seção [!UICONTROL Audiences], as seguintes métricas estão disponíveis:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Name]** | O nome do público-alvo que está sendo avaliado. |
| **[!UICONTROL Profile count]** | O número de perfis que estão sendo avaliados. |

## Monitorar o painel de processos de segmentação {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Processos de segmentação"
>abstract="A exibição de processos de segmentação contém informações sobre os processos de avaliação e exportação para todos os seus públicos-alvo."

Para acessar o painel **[!UICONTROL Segmentation Jobs]**, selecione **[!UICONTROL Segmentation jobs]** no painel [!UICONTROL Audiences]. O painel [!UICONTROL Monitoring] contém métricas e informações sobre os trabalhos de avaliação e exportação.

>[!NOTE]
>
>Somente **trabalhos de avaliação de segmentação** têm suporte para monitoramento por público. Os trabalhos de exportação de segmentação só oferecem suporte ao monitoramento no nível da organização.

![O painel de monitoramento dos trabalhos de segmentação é exibido. A opção para alternar entre Públicos-alvo e trabalhos de Segmentação está realçada.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Use o painel [!UICONTROL Segmentation Jobs] para entender se a avaliação e a exportação de perfil ocorrem no prazo e sem exceções, de modo que os serviços downstream para ativação de destino possam ter os dados de perfil avaliados mais recentemente.

As seguintes métricas estão disponíveis para trabalhos de segmentação:

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Segmentation job]** | Indica o nome do trabalho de segmentação. |
| **[!UICONTROL Type]** | Indica o tipo de trabalho de segmentação - exportação ou avaliação. Observe que, em ambos os casos, o trabalho de segmentação avalia ou exporta **todos** públicos-alvo pertencentes a uma organização. Para saber mais sobre trabalhos de exportação, leia o manual no [ponto de extremidade de trabalhos de exportação](../../segmentation/api/export-jobs.md). Para saber mais sobre tarefas de avaliação, leia o tutorial em [avaliação de uma definição de segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Job start]** | A data e a hora em que o trabalho de segmentação foi iniciado. |
| **[!UICONTROL Job end]** | A data e a hora em que o trabalho de segmentação foi concluído. |
| **[!UICONTROL Status]** | O status do trabalho concluído. Os possíveis status do trabalho de segmentação incluem sucesso ou falha. |
