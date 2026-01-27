---
keywords: Experience Platform;página inicial;tópicos populares;monitorar perfis;monitorar fluxos de dados;fluxos de dados;perfil;perfil do cliente em tempo real;
description: O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. Este tutorial fornece instruções sobre como monitorar fluxos de dados com Perfis usando a interface do usuário do Experience Platform.
title: Monitorar fluxos de dados para perfis na interface
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1d60afdf486642398a2d31302db339eb9cb45130
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 6%

---

# Monitorar fluxos de dados para perfis na interface

O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

O painel de monitoramento fornece uma representação visual da atividade dos dados no Perfil, incluindo o status dos Perfis dos dados. Este tutorial fornece instruções sobre como usar o painel de monitoramento para monitorar os perfis de dados usando a interface do usuário do Experience Platform, permitindo que você acompanhe o status do processamento do Perfil.

## Introdução {#getting-started}

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Experience Platform. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   - [Execuções de fluxo de dados](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
- [Perfil de cliente em tempo real](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Painel de monitoramento de perfis {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Processamento de perfil"
>abstract="A visualização do processamento de perfil contém informações sobre registros assimilados ao serviço de perfil, incluindo o número de fragmentos de perfil criados, fragmentos de perfil atualizados e o número total de fragmentos de perfil."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Detalhes de execução do fluxo de dados"
>abstract="A página Detalhes de execução do fluxo de dados exibe mais informações sobre a execução do fluxo de dados do Perfil, incluindo a ID da organização e a ID de execução do fluxo de dados."

Para acessar o painel **[!UICONTROL Profiles]**, selecione **[!UICONTROL Monitoring]** na navegação à esquerda. Na página **[!UICONTROL Monitoring]**, selecione o cartão **[!UICONTROL Profiles]**.

![O cartão Perfis. Informações sobre o número de registros recebidos, o número de fragmentos de perfil criados e atualizados, e a taxa de sucesso é mostrada.](../assets/ui/monitor-profiles/focus-card.png)

No painel **[!UICONTROL Profiles]** principal, o cartão **[!UICONTROL Profiles]** mostra informações sobre o número total de registros recebidos, o número de fragmentos de perfil criados e atualizados, bem como a taxa de sucesso de fragmentos de perfil criados e atualizados.

O próprio painel contém métricas sobre o Processamento de perfis. Por padrão, o painel mostrará os detalhes de processamento do Perfil das fontes da sua organização nas últimas 24 horas.

![O painel Perfis. São exibidas informações sobre o número de registros do Perfil recebidos por origem.](../assets/ui/monitor-profiles/sources.png)

A página [!UICONTROL Profile processing] contém informações sobre registros assimilados em [!DNL Profile], incluindo o número de fragmentos de perfil criados, fragmentos de perfil atualizados e o número total de fragmentos de perfil.

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Source name]** | O nome da origem. |
| **[!UICONTROL Records received]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Records failed]** | O número de registros assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Profile fragments created]** | O número de novos fragmentos [!DNL Profile] adicionados. |
| **[!UICONTROL Profile fragments updated]** | O número de fragmentos [!DNL Profile] existentes atualizados. |
| **[!UICONTROL Total Profile fragments]** | O número total de registros gravados em [!DNL Profile], incluindo todos os fragmentos [!DNL Profile] existentes atualizados e os novos fragmentos [!DNL Profile] criados. |
| **[!UICONTROL Total failed dataflows]** | O número de execuções de fluxo de dados que falharam. |

Você pode selecionar o ícone de filtro ![Ícone de filtro](/help/images/icons/filter.png) ao lado do nome de origem para ver as informações de processamento do perfil para os fluxos de dados da origem selecionada.

Como alternativa, você pode selecionar **[!UICONTROL Dataflows]** no botão de alternância para ver os detalhes de processamento do perfil para os fluxos de dados da sua organização nas últimas 24 horas.

![O painel Perfis. São exibidas informações sobre o número de registros do Perfil recebidos por fluxo de dados.](../assets/ui/monitor-profiles/dataflows.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | O nome do fluxo de dados. |
| **[!UICONTROL Dataset]** | O nome do conjunto de dados no qual o fluxo de dados está inserindo. |
| **[!UICONTROL Source name]** | O nome da origem à qual o fluxo de dados pertence. |
| **[!UICONTROL Data type]** | O tipo de dados recebido do conjunto de dados. |
| **[!UICONTROL Records received**] | O número de registros recebidos do data lake. |
| **[!UICONTROL Records failed]** | O número de registros assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Profile fragments created]** | O número de novos fragmentos [!DNL Profile] adicionados. |
| **[!UICONTROL Profile fragments updated]** | O número de fragmentos [!DNL Profile] existentes atualizados |
| **[!UICONTROL Total Profile fragments]** | O número total de registros gravados em [!DNL Profile], incluindo todos os fragmentos [!DNL Profile] existentes atualizados e os novos fragmentos [!DNL Profile] criados. |
| **[!UICONTROL Total failed flow runs]** | O número de execuções de fluxo de dados que falharam. |
| **[!UICONTROL Last active]** | O carimbo de data/hora no qual o fluxo de dados foi executado pela última vez. |

Selecione o ícone de filtro ![filtro](/help/images/icons/filter.png) ao lado da hora de início da execução do fluxo de dados para ver mais informações sobre sua execução do fluxo de dados [!DNL Profile].

Um painel de controle exibindo todas as execuções de fluxo de dados é exibido. Esse painel contém métricas sobre as execuções do fluxo de dados, bem como gráficos que mostram a taxa de sucesso, os fragmentos de perfil criados e os fragmentos de perfil atualizados.

![O fluxo de dados executa o painel. As informações sobre as execuções de fluxo de dados são exibidas.](../assets/ui/monitor-profiles/dataflow-run.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

>[!NOTE]
>
>Quando o fluxo de dados for executado no estado **[!UICONTROL Processing]**, você poderá ver as informações sobre a preparação ao ver os status dos pontos de verificação no processo de assimilação.
>
>![A bolha de preparação de assimilação de perfil é exibida.](../assets/ui/monitor-profiles/profile-ingestion-readiness.png){zoomable="yes" width="300"}

| Métrica | Descrição |
| ------ | ----------- |
| **[!UICONTROL Dataflow run start]** | A hora em que a execução do fluxo de dados começou em UTC. |
| **[!UICONTROL Data type]** | O tipo de dados recebido pelo fluxo de dados. |
| **[!UICONTROL Records received]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Records failed]** | O número de registros assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Profile fragments created]** | O número de novos fragmentos [!DNL Profile] adicionados. |
| **[!UICONTROL Profile fragments updated]** | O número de fragmentos [!DNL Profile] existentes atualizados. |
| **[!UICONTROL Total profile fragments]** | O número total de registros gravados em [!DNL Profile], incluindo todos os fragmentos [!DNL Profile] existentes atualizados e os novos fragmentos [!DNL Profile] criados. |
| **[!UICONTROL Processing time]** | O tempo necessário para a execução do fluxo de dados ser processada. |
| **[!UICONTROL Status]** | O status da execução do fluxo de dados. Os valores possíveis incluem [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] e [!UICONTROL Processing]. |
| **[!UICONTROL Ready for customer segmentation]** | Um status que mostra se os registros assimilados estão prontos para serem usados na segmentação do cliente. Os valores possíveis incluem [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] e [!UICONTROL Processing]. Mesmo se o **Status** do fluxo de dados estiver sendo processado, se o valor desse campo for Sim, você poderá usar os perfis na segmentação do cliente. |
| **[!UICONTROL Ready for lookup]** | Um status que mostra se os registros assimilados estão prontos para uso na pesquisa do Adobe Journey Optimizer.  Os valores possíveis incluem [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] e [!UICONTROL Processing]. Mesmo que o **Status** do fluxo de dados esteja processando, se o valor desse campo for Sim, você poderá usar os perfis na pesquisa do Journey Optimizer. |

A página [!UICONTROL Dataflow run details] exibe mais informações sobre a execução do fluxo de dados [!DNL Profile], incluindo a ID da organização e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos por [!DNL Profile], caso ocorram erros no processo de assimilação.

![Um painel que mostra informações detalhadas sobre o fluxo de dados selecionado é exibido.](../assets/ui/monitor-profiles/dataflow-run-details.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Records received]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Records failed]** | O número de registros assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Profile fragments created]** | O número de novos fragmentos [!DNL Profile] adicionados. |
| **[!UICONTROL Profile fragments updated]** | O número de fragmentos [!DNL Profile] existentes atualizados. |
| **[!UICONTROL Status]** | Define o status geral de um fluxo de dados. Os valores possíveis de status são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com o agendamento fornecido.</li><li>`Failed`: indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |
| **[!UICONTROL Dataflow run start]** | A data e a hora em que o fluxo de dados começou a ser executado. |
| **[!UICONTROL Last updated]** | A data e a hora da última atualização do fluxo de dados. |
| **[!UICONTROL Error summary]** | Se a execução do fluxo de dados falhar, isso exibirá um código de erro e um resumo do por que a execução do fluxo de dados falhou. |
| **[!UICONTROL Dataflow run ID]** | A ID da execução do fluxo de dados. |
| **[!UICONTROL IMS org ID]** | A ID da organização à qual a execução do fluxo de dados pertence. |

Além disso, você pode selecionar a opção para visualizar os registros com falha ou os registros ignorados. A seção de erros inclui detalhes sobre o código de erro e o número de registros com falha ou excluídos.
