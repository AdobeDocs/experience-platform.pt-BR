---
description: Use o [!UICONTROL Enriquecimento de perfil] painel para entender se os trabalhos de enriquecimento de perfil foram executados e concluídos com êxito, e para visualizar as métricas básicas para medir a eficácia dos enriquecimentos.
solution: Experience Platform
title: Monitorar trabalhos de enriquecimento de perfil
type: Tutorial
source-git-commit: f3389ef2c2bd9ff52ecde2a4f5fd55e5b86783fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Monitorar trabalhos de enriquecimento de perfil na interface do usuário

Use o [!UICONTROL Enriquecimento de perfil] painel para entender se os trabalhos de enriquecimento de perfil foram executados e concluídos com êxito, e para visualizar as métricas básicas para medir a eficácia dos enriquecimentos.

No [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Monitoramento]** na navegação à esquerda para acessar o [!UICONTROL Monitoramento] painel. No seletor de exibições, selecione **Fluxo B2B** para visualizar os elementos do painel específicos para [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  O [!UICONTROL Monitoramento] o painel inclui as métricas básicas da última execução bem-sucedida e o status diário da tarefa em até 90 dias no passado. O [!UICONTROL Contas relacionadas] o painel mostra as métricas básicas e o status diário da tarefa específico da [Contas Relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) enriquecimento do perfil.

![Indicação visual de como chegar à tela de monitoramento de trabalhos de enriquecimento de perfil na interface do usuário do Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Os dados no **[!UICONTROL Métricas]** O cartão inclui as métricas básicas da última execução bem-sucedida do trabalho de Contas Relacionadas.

As métricas a seguir estão disponíveis para contas relacionadas e trabalhos de enriquecimento de perfil:

| Métrica | Descrição |
---------|----------|
| **[!UICONTROL Total de perfis da conta]** | Indica o total de perfis de conta que sua organização tem acesso. |
| **[!UICONTROL Grupos de contas]** | Indica o número de grupos de contas agrupados pelo trabalho de aprendizado de máquina de Contas Relacionadas. |
| **[!UICONTROL Grupos de conta única]** | Indica o número de contas que não estão agrupadas com outras contas. |
| **[!UICONTROL Tamanho do grupo maior]** | Indica o tamanho do maior grupo de contas relacionadas. O tamanho máximo permitido para o grupo é 30. |
| **[!UICONTROL Dimensão média do grupo]** | Indica o tamanho mediano dos grupos de contas relacionados em sua organização. |
| **[!UICONTROL Última execução bem-sucedida]** | Indica a data e a hora da última execução bem-sucedida do trabalho de Contas Relacionadas. |
| **[!UICONTROL Status]** | Indica o status (bem-sucedido, com falha ou em processamento) do trabalho de Contas Relacionadas. |
| **[!UICONTROL Mensagem]** | Indica uma mensagem de erro ou de aviso para uma execução de tarefa específica. |

## Controles da interface do usuário {#ui-controls}

Esta seção descreve várias opções da interface do usuário na interface de monitoramento, que permitem filtrar as métricas exibidas na página.

Use o ícone de seta (![ícone de seta](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) para expandir ou descartar o cartão na parte superior da tela, que mostra informações instantâneas sobre os trabalhos de enriquecimento de perfil.

![Gravação de tela que mostra o controle da interface do usuário do ícone de seta.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Use o **[!UICONTROL Métricas e gráficos]** alterne para ignorar a exibição que exibe as métricas mais recentes.

![Gravação de tela que mostra as métricas e os gráficos alternados.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Use o **[!UICONTROL Mostrar somente falhas]** alternar para exibir somente os trabalhos de enriquecimento de perfil com falha.

![Gravação de tela que mostra o botão Mostrar falhas somente alternar.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, agora é possível monitorar e entender com êxito as métricas de contas relacionadas e trabalhos de enriquecimento de perfil. Consulte os seguintes documentos para obter mais detalhes:

* [Contas relacionadas na CDP em tempo real B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Guia contas relacionadas no guia da interface do usuário do perfil da conta](/help/rtcdp/accounts/account-profile-ui-guide.md)