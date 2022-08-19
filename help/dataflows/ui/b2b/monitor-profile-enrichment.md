---
description: Use o [!UICONTROL Enriquecimento de perfil] painel para entender se os trabalhos de enriquecimento de perfil foram executados e concluídos com êxito, e para visualizar as métricas básicas para medir a eficácia dos enriquecimentos.
solution: Experience Platform
title: Monitorar trabalhos de enriquecimento de perfil
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 1fed0cf37e7297c21330ebf51ae15054aa21c781
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# Monitorar trabalhos de enriquecimento de perfil na interface do usuário {#monitor-profile-enrichment}

Use o [!UICONTROL Enriquecimento de perfil] painel para entender se os trabalhos de enriquecimento de perfil foram executados e concluídos com êxito, e para visualizar as métricas básicas para medir a eficácia dos enriquecimentos.

No [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Monitoramento]** na navegação à esquerda para acessar o [!UICONTROL Monitoramento] painel. No seletor de exibições, selecione **Fluxo B2B** para visualizar os elementos do painel específicos para [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  O [!UICONTROL Monitoramento] o painel inclui as métricas básicas da última execução bem-sucedida e o status diário da tarefa em até 90 dias no passado.

## Enriquecimento de perfil de contas relacionadas {#related-accounts}

O [!UICONTROL Contas relacionadas] o painel mostra as métricas básicas e o status da tarefa diária específica do [Contas Relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) enriquecimento do perfil.

![Indicação visual de como chegar à tela de monitoramento de trabalhos de enriquecimento de perfil na interface do usuário do Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Os dados no **[!UICONTROL Métricas]** O cartão inclui as métricas básicas da última execução bem-sucedida do trabalho de Contas Relacionadas.

As métricas a seguir estão disponíveis para contas relacionadas e trabalhos de enriquecimento de perfil:

| Métrica | Descrição |
| --------- | ---------- |
| **[!UICONTROL Total de perfis da conta]** | Indica o total de perfis de conta que sua organização tem acesso. |
| **[!UICONTROL Grupos de contas]** | Indica o número de grupos de contas agrupados pelo trabalho de aprendizado de máquina das contas relacionadas. |
| **[!UICONTROL Grupos de conta única]** | Indica o número de contas que não estão agrupadas com outras contas. |
| **[!UICONTROL Tamanho do grupo maior]** | Indica o tamanho do maior grupo de contas relacionadas. O tamanho máximo permitido para o grupo é 30. |
| **[!UICONTROL Dimensão média do grupo]** | Indica o tamanho mediano dos grupos de contas relacionados em sua organização. |
| **[!UICONTROL Última execução bem-sucedida]** | Indica a data e a hora da última execução bem-sucedida do trabalho de contas relacionadas. |
| **[!UICONTROL Status]** | Indica o status (bem-sucedido, com falha ou em processamento) da ordem de produção das contas relacionadas. |
| **[!UICONTROL Mensagem]** | Indica uma mensagem de erro ou de aviso para uma execução de tarefa específica. |

## Lead para o enriquecimento do perfil de correspondência da conta {#lead-to-account-matching}

O [!UICONTROL Lead para correspondência da conta] o painel mostra as métricas básicas e o status diário de execução da tarefa específico da [Lead para correspondência da conta](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) enriquecimento do perfil.

![Lead para o enriquecimento do perfil de correspondência da conta](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

As seguintes métricas estão disponíveis para lead para os trabalhos de enriquecimento de perfil correspondentes a contas:

| Métrica | Descrição |
| --------- | ---------- |
| **[!UICONTROL Total de pessoas com contas]** | Indica o número total de pessoas associadas a uma conta. |
| **[!UICONTROL Total de contas]** | Indica o número total de contas. |
| **[!UICONTROL Pessoas existentes com contabilidade]** | Indica o número de pessoas que já estão associadas a uma conta nas fontes de dados. |
| **[!UICONTROL Pessoas equiparadas]** | Indica o número de pessoas que corresponderam a uma conta. |
| **[!UICONTROL Pessoas sem correspondência]** | Indica o número de pessoas que não corresponderam a uma conta. |
| **[!UICONTROL Última execução bem-sucedida]** | Indica a data e a hora do último lead bem-sucedido para a execução do trabalho de correspondência da conta. |
| **[!UICONTROL Status]** | Indica o status (bem-sucedido, com falha ou processamento) do lead para o trabalho de correspondência da conta. |

## Potencial preditivo e enriquecimento do perfil de pontuação de conta {#predictive-lead-to-account-scoring}

O [!UICONTROL Lead preditivo e pontuação de conta] o painel mostra as métricas básicas e o status diário de execução da tarefa específico da [Lead preditivo e pontuação de conta](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) enriquecimento do perfil.

![Potencial preditivo e enriquecimento do perfil de pontuação de conta](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

As métricas a seguir estão disponíveis para trabalhos preditivos de enriquecimento de perfil de lead e pontuação de conta:

| Métrica | Descrição |
| --------- | ---------- |
| **[!UICONTROL Início da tarefa]** | Indica a data e a hora de início da execução preditiva do trabalho de pontuação de conta e lead. |
| **[!UICONTROL Tempo de processamento]** | O tempo total necessário para a conclusão do trabalho. |
| **[!UICONTROL Nome da pontuação]** | O nome da pontuação do trabalho. |
| **[!UICONTROL Tipo de perfil]** | O tipo da pontuação: <ul><li>Pessoa</li><li>Conta</li></ul>. |
| **[!UICONTROL Tipo de tarefa]** | O tipo da tarefa:<ul><li>Pontuação</li><li>Treinamento</li>. |
| **[!UICONTROL Status]** | Indica o status (sucesso, falha ou processamento) do lead preditivo e do trabalho de pontuação da conta. |

## Controles da interface do usuário {#ui-controls}

Esta seção descreve várias opções da interface do usuário na interface de monitoramento, que permitem filtrar as métricas exibidas na página.

Use o ícone de seta (![ícone de seta](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) para expandir ou descartar o cartão na parte superior da tela, que mostra informações instantâneas sobre os trabalhos de enriquecimento de perfil.

![Gravação de tela que mostra o controle da interface do usuário do ícone de seta.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Use o **[!UICONTROL Métricas e gráficos]** alterne para ignorar a exibição que exibe as métricas mais recentes.

![Gravação de tela que mostra as métricas e os gráficos alternados.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Use o **[!UICONTROL Mostrar somente falhas]** alternar para exibir somente os trabalhos de enriquecimento de perfil com falha.

![Gravação de tela que mostra o botão Mostrar falhas somente alternar.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você pode agora monitorar e entender com êxito as métricas para trabalhos de enriquecimento de perfil. Consulte os seguintes documentos para obter mais detalhes:

* [Contas relacionadas na CDP em tempo real B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Guia contas relacionadas no guia da interface do usuário do perfil da conta](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead para a correspondência de contas na CDP em tempo real B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Lead preditivo e pontuação de conta na CDP em tempo real B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
