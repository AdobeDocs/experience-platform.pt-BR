---
keywords: Experience Platform;página inicial;tópicos populares;monitorar perfis;monitorar fluxos de dados;fluxos de dados;perfil;perfil do cliente em tempo real;
description: O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. Este tutorial fornece instruções sobre como monitorar fluxos de dados com Perfis usando a interface do usuário Experience Platform.
title: Monitorar fluxos de dados para perfis na interface
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 9%

---

# Monitorar fluxos de dados para perfis na interface

O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

O painel de monitoramento fornece uma representação visual da atividade dos dados no Perfil, incluindo o status dos Perfis dos dados. Este tutorial fornece instruções sobre como usar o painel de monitoramento para monitorar os perfis de dados usando a interface do usuário do Experience Platform, permitindo que você acompanhe o status do processamento do Perfil.

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino para [!DNL Identity] e [!DNL Profile], e para [!DNL Destinations].
   - [O fluxo de dados é executado](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
- [Perfil do cliente em tempo real](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

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

Para acessar o **[!UICONTROL Perfis]** painel, selecione **[!UICONTROL Monitoramento]** no painel de navegação esquerdo. Uma vez no **[!UICONTROL Monitoramento]** selecione a **[!UICONTROL Perfis]** cartão.

![O cartão Perfis. As informações sobre o número de registros recebidos, o número de fragmentos de perfil criados e atualizados e a taxa de sucesso são mostradas.](../assets/ui/monitor-profiles/focus-card.png)

No principal **[!UICONTROL Perfis]** painel, o **[!UICONTROL Perfis]** O cartão mostra informações sobre o número total de registros recebidos, o número de fragmentos de perfil criados e atualizados, bem como a taxa de sucesso de fragmentos de perfil criados e atualizados.

O próprio painel contém métricas sobre o Processamento de perfis. Por padrão, o painel mostrará os detalhes de processamento do Perfil das fontes da sua organização nas últimas 24 horas.

![O painel Perfis. As informações sobre o número de registros do Perfil recebidos por origem são exibidas.](../assets/ui/monitor-profiles/sources.png)

A variável [!UICONTROL Processamento de perfil] contém informações sobre os registros assimilados em [!DNL Profile], incluindo o número de fragmentos de perfil criados, os fragmentos de perfil atualizados e o número total de fragmentos de perfil.

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Nome de origem]** | O nome da origem. |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Registros com falha]** | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Fragmentos de perfil criados]** | O número de novas [!DNL Profile] fragmentos adicionados. |
| **[!UICONTROL Fragmentos de perfil atualizados]** | O número de registros existentes [!DNL Profile] fragmentos atualizados. |
| **[!UICONTROL Total de fragmentos de perfil]** | O número total de registros gravados em [!DNL Profile], incluindo todos os existentes [!DNL Profile] fragmentos atualizados e novos [!DNL Profile] fragmentos criados. |
| **[!UICONTROL Total de fluxos de dados com falha]** | O número de execuções de fluxo de dados que falharam. |

É possível selecionar o ícone de filtro ![Ícone Filtrar](../assets/ui/monitor-profiles/filter.png) ao lado do nome da origem para ver as informações de processamento do perfil dos fluxos de dados da origem selecionada.

![O ícone de filtro é realçado. Selecionar esse ícone permite exibir os fluxos de dados da origem selecionada.](../assets/ui/monitor-profiles/sources-filter.png)

Como alternativa, você pode selecionar **[!UICONTROL Fluxos de dados]** Clique no botão para ver os detalhes de processamento do perfil para os fluxos de dados da sua organização nas últimas 24 horas.

![O painel Perfis. As informações sobre o número de registros do Perfil recebidos por fluxo de dados são exibidas.](../assets/ui/monitor-profiles/dataflows.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Fluxo de dados]** | O nome do fluxo de dados. |
| **[!UICONTROL Conjunto de dados]** | O nome do conjunto de dados no qual o fluxo de dados está inserindo. |
| **[!UICONTROL Nome de origem]** | O nome da origem à qual o fluxo de dados pertence. |
| **[!UICONTROL Registros recebidos**] | O número de registros recebidos do data lake. |
| **[!UICONTROL Registros com falha]** | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Fragmentos de perfil criados]** | O número de novas [!DNL Profile] fragmentos adicionados. |
| **[!UICONTROL Fragmentos de perfil atualizados]** | O número de registros existentes [!DNL Profile] fragmentos atualizados |
| **[!UICONTROL Total de fragmentos de perfil]** | O número total de registros gravados em [!DNL Profile], incluindo todos os existentes [!DNL Profile] fragmentos atualizados e novos [!DNL Profile] fragmentos criados. |
| **[!UICONTROL Total de execuções de fluxo com falha]** | O número de execuções de fluxo de dados que falharam. |
| **[!UICONTROL Última atividade]** | O carimbo de data/hora no qual o fluxo de dados foi executado pela última vez. |

Selecione o ícone de filtro ![filtro](../assets/ui/monitor-profiles/filter.png) ao lado da hora de início da execução do fluxo de dados para ver mais informações sobre [!DNL Profile] execução do fluxo de dados.

![O ícone de filtro é realçado. Selecionar esse ícone permite exibir detalhes sobre o fluxo de dados selecionado.](../assets/ui/monitor-profiles/dataflows-filter.png)

A variável [!UICONTROL Detalhes da execução do fluxo de dados] A página exibe mais informações sobre [!DNL Profile] execução do fluxo de dados, incluindo a ID da organização e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos pelo [!DNL Profile], se ocorrerem erros no processo de assimilação.

![Um painel que mostra informações detalhadas sobre o fluxo de dados selecionado é exibido.](../assets/ui/monitor-profiles/dataflow-run-details.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Registros com falha]** | O número de registros que foram assimilados, mas não em [!DNL Profile] devido a erros. |
| **[!UICONTROL Fragmentos de perfil criados]** | O número de novas [!DNL Profile] fragmentos adicionados. |
| **[!UICONTROL Fragmentos de perfil atualizados]** | O número de registros existentes [!DNL Profile] fragmentos atualizados. |
| **[!UICONTROL Status]** | Define o status geral de um fluxo de dados. Os valores possíveis de status são: <ul><li>`Success`: indica que um fluxo de dados está ativo e está assimilando dados de acordo com a programação fornecida.</li><li>`Failed`: indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |
| **[!UICONTROL Início da execução do fluxo de dados]** | A data e a hora em que o fluxo de dados começou a ser executado. |
| **[!UICONTROL Última atualização]** | A data e a hora da última atualização do fluxo de dados. |
| **[!UICONTROL Resumo do erro]** | Se a execução do fluxo de dados falhar, isso exibirá um código de erro e um resumo do por que a execução do fluxo de dados falhou. |
| **[!UICONTROL ID de execução do fluxo de dados]** | A ID da execução do fluxo de dados. |
| **[!UICONTROL ID da Organização IMS]** | A ID da organização à qual a execução do fluxo de dados pertence. |

Além disso, você pode selecionar a opção para visualizar os registros com falha ou os registros ignorados. A seção de erros inclui detalhes sobre o código de erro e o número de registros com falha ou excluídos.
