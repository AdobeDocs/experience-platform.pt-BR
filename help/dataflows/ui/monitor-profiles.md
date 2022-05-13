---
keywords: Experience Platform, home, tópicos populares, monitorar perfis, monitorar fluxos de dados, fluxos de dados, perfil, perfil do cliente em tempo real;
description: O Perfil do cliente em tempo real permite que você visualize uma visualização holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. Este tutorial fornece instruções sobre como você pode monitorar fluxos de dados com perfis usando a interface do usuário do Experience Platform.
title: Monitorar fluxos de dados para perfis na interface do usuário
topic-legacy: overview
type: Tutorial
source-git-commit: 3018ee005c96e3905ae8dab24cca901cf48847ea
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# Monitorar fluxos de dados para perfis na interface do usuário

O Perfil do cliente em tempo real permite que você visualize uma visualização holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

O painel de monitoramento fornece uma representação visual da atividade dos dados no Perfil, incluindo o status dos perfis dos dados. Este tutorial fornece instruções sobre como você pode usar o painel de monitoramento para monitorar os perfis de dados usando a interface do usuário do Experience Platform, permitindo rastrear o status do processamento do perfil.

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fluxos de dados](../home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile]e para [!DNL Destinations].
   - [Execuções do fluxo de dados](../../sources/notifications.md): As execuções de fluxo de dados são trabalhos agendados recorrentes com base na configuração de frequência de fluxos de dados selecionados.
- [Perfil do cliente em tempo real](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Monitoramento do painel de perfis {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Processamento de perfil"
>abstract="A visualização Processamento de perfil contém informações sobre registros assimilados ao serviço de perfil, incluindo o número de fragmentos de perfil criados, fragmentos de perfil atualizados e o número total de fragmentos de perfil."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Detalhes da execução do fluxo de dados"
>abstract="A página Detalhes de execução do fluxo de dados exibe mais informações sobre a execução do fluxo de dados do Perfil, incluindo a ID da organização e a ID de execução do fluxo de dados."

Para acessar o **[!UICONTROL Perfis]** painel, selecione **[!UICONTROL Monitoramento]** no painel de navegação esquerdo. Uma vez no **[!UICONTROL Monitoramento]** selecione o **[!UICONTROL Perfis]** cartão.

![O cartão Perfis . Informações sobre o número de registros recebidos, o número de fragmentos de perfil criados e atualizados e a taxa de sucesso é mostrada.](../assets/ui/monitor-profiles/focus-card.png)

No principal **[!UICONTROL Perfis]** painel, o **[!UICONTROL Perfis]** cartão mostra informações sobre o número total de registros recebidos, o número de fragmentos de perfil criados e atualizados, bem como a taxa de sucesso de fragmentos de perfil criados e atualizados.

O próprio painel contém métricas sobre o processamento do perfil. Por padrão, o painel mostrará os detalhes de processamento do perfil das fontes de sua organização nas últimas 24 horas.

![O painel Perfis . As informações sobre o número de registros do Perfil recebidos por fonte são exibidas.](../assets/ui/monitor-profiles/sources.png)

O [!UICONTROL Processamento de perfil] contém informações sobre registros assimilados a [!DNL Profile], incluindo o número de fragmentos de perfil criados, fragmentos de perfil atualizados e o número total de fragmentos de perfil.

As métricas a seguir estão disponíveis para esta exibição de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Nome da origem]** | O nome da origem. |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do lago de dados. |
| **[!UICONTROL Falha nos registros]** | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Fragmentos de perfil criados]** | O número líquido de [!DNL Profile] fragmentos adicionados. |
| **[!UICONTROL Fragmentos de perfil atualizados]** | O número de [!DNL Profile] fragmentos atualizados. |
| **[!UICONTROL Total de fragmentos de perfil]** | O número total de registros gravados em [!DNL Profile], incluindo todos os [!DNL Profile] fragmentos atualizados e novos [!DNL Profile] fragmentos criados. |
| **[!UICONTROL Total de fluxos de dados com falha]** | O número de execuções de fluxo de dados que falharam. |

Você pode selecionar o ícone de filtro ![Ícone Filtro](../assets/ui/monitor-profiles/filter.png) ao lado do nome de origem para ver as informações de processamento do perfil dos fluxos de dados da origem selecionada.

![O ícone de filtro é realçado. Selecionar esse ícone permite exibir os fluxos de dados da fonte selecionada.](../assets/ui/monitor-profiles/sources-filter.png)

Como alternativa, você pode selecionar **[!UICONTROL Fluxos de dados]** no botão de alternância para ver os detalhes de processamento do perfil dos fluxos de dados da sua organização das últimas 24 horas.

![O painel Perfis . As informações sobre o número de registros do Perfil recebidos por fluxo de dados são exibidas.](../assets/ui/monitor-profiles/dataflows.png)

As métricas a seguir estão disponíveis para esta exibição de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Fluxo de dados]** | O nome do fluxo de dados. |
| **[!UICONTROL Conjunto de dados]** | O nome do conjunto de dados ao qual o fluxo de dados está sendo inserido. |
| **[!UICONTROL Nome da origem]** | O nome da origem à qual o fluxo de dados pertence. |
| **[!UICONTROL Registros recebidos**] | O número de registros recebidos do lago de dados. |
| **[!UICONTROL Falha nos registros]** | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Fragmentos de perfil criados]** | O número líquido de [!DNL Profile] fragmentos adicionados. |
| **[!UICONTROL Fragmentos de perfil atualizados]** | O número de [!DNL Profile] fragmentos atualizados |
| **[!UICONTROL Total de fragmentos de perfil]** | O número total de registros gravados em [!DNL Profile], incluindo todos os [!DNL Profile] fragmentos atualizados e novos [!DNL Profile] fragmentos criados. |
| **[!UICONTROL Total de execuções de fluxo com falha]** | O número de execuções de fluxo de dados que falharam. |
| **[!UICONTROL Última atividade]** | O carimbo de data e hora em que o fluxo de dados foi executado pela última vez. |

Selecione o ícone de filtro ![filter](../assets/ui/monitor-profiles/filter.png) além do tempo de início da execução do fluxo de dados para ver mais informações sobre o [!DNL Profile] execução do fluxo de dados.

![O ícone de filtro é realçado. Selecionar esse ícone permite exibir detalhes sobre o fluxo de dados selecionado.](../assets/ui/monitor-profiles/dataflows-filter.png)

O [!UICONTROL Detalhes da execução do fluxo de dados] página exibe mais informações sobre sua [!DNL Profile] execução do fluxo de dados, incluindo a ID da organização e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos pelo [!DNL Profile], caso ocorra algum erro no processo de ingestão.

![Um painel que mostra informações detalhadas sobre o fluxo de dados selecionado é exibido.](../assets/ui/monitor-profiles/dataflow-run-details.png)

As métricas a seguir estão disponíveis para esta exibição de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do lago de dados. |
| **[!UICONTROL Falha nos registros]** | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Fragmentos de perfil criados]** | O número líquido de [!DNL Profile] fragmentos adicionados. |
| **[!UICONTROL Fragmentos de perfil atualizados]** | O número de [!DNL Profile] fragmentos atualizados. |
| **[!UICONTROL Status]** | Define o status geral de um fluxo de dados. Os valores de status possíveis são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com o cronograma que foi fornecido.</li><li>`Failed`: Indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: Indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |
| **[!UICONTROL Início da execução do fluxo de dados]** | A data e a hora em que o fluxo de dados começou a ser executado. |
| **[!UICONTROL Última atualização]** | A data e a hora em que o fluxo de dados foi atualizado pela última vez. |
| **[!UICONTROL Resumo do erro]** | Se a execução do fluxo de dados falhar, isso exibirá um código de erro e um resumo de por que a execução do fluxo de dados falhou. |
| **[!UICONTROL ID de execução do fluxo de dados]** | A ID da execução do fluxo de dados. |
| **[!UICONTROL ID da organização IMS]** | A ID da organização à qual a execução do fluxo de dados pertence. |

Além disso, você pode selecionar a alternância para exibir os registros que falharam ou os registros ignorados. A seção errors inclui detalhes sobre o código de erro e o número de registros que falharam ou foram excluídos.