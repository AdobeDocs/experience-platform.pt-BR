---
title: Visão geral do gerenciamento avançado do ciclo de vida dos dados
description: O Gerenciamento avançado do ciclo de vida dos dados permite gerenciar o ciclo de vida dos dados atualizando ou removendo registros desatualizados ou imprecisos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: adba9d3cd979f655f477d2d80ed3e55e96fbe486
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 2%

---

# Gerenciamento avançado do ciclo de vida dos dados no Adobe Experience Platform

O Adobe Experience Platform fornece um conjunto robusto de ferramentas para gerenciar operações de dados grandes e complicadas para orquestrar as experiências do consumidor. À medida que os dados são assimilados no sistema ao longo do tempo, torna-se cada vez mais importante gerenciar seus armazenamentos de dados para que eles sejam usados conforme o esperado, sejam atualizados quando dados incorretos precisarem de correção e sejam excluídos quando as políticas organizacionais considerarem necessário.

Estas atividades podem ser realizadas usando o espaço de trabalho [[!UICONTROL Data Lifecycle] da interface](#ui) ou a [API de Higiene de Dados](#api). Quando um trabalho do ciclo de vida dos dados é executado, o sistema fornece atualizações de transparência em cada etapa do processo. Consulte a seção sobre [linhas do tempo e transparência](#timelines-and-transparency) para obter mais informações sobre como cada tipo de trabalho é representado no sistema.

>[!NOTE]
>
>O Gerenciamento Avançado do Ciclo de Vida dos Dados suporta exclusões de conjuntos de dados por meio do [ponto de extremidade de expiração do conjunto de dados](./api/dataset-expiration.md) e exclusões de ID (dados em nível de linha) usando identidades primárias por meio do [ponto de extremidade da ordem de trabalho](./api/workorder.md). Também é possível gerenciar [expirações do conjunto de dados](./ui/dataset-expiration.md) e [exclusões de registros](./ui/record-delete.md) por meio da interface do usuário do Experience Platform. Consulte a documentação vinculada para obter mais informações. Observe que o ciclo de vida dos dados não oferece suporte à exclusão de lotes.

## Espaço de trabalho da interface do usuário [!UICONTROL Data Lifecycle] {#ui}

O espaço de trabalho [!UICONTROL Data Lifecycle] na interface do usuário do Experience Platform permite configurar e agendar operações de ciclo de vida de dados, ajudando a garantir que seus registros sejam mantidos conforme esperado.

Para obter etapas detalhadas sobre como gerenciar tarefas do ciclo de vida de dados na interface, consulte o [guia da interface do ciclo de vida de dados](./ui/overview.md).

## API de higiene de dados {#api}

A interface do usuário do [!UICONTROL Data Lifecycle] é criada com base na API de higiene de dados, cujos endpoints estão disponíveis para você usar diretamente, caso prefira automatizar as atividades do ciclo de vida dos dados. Consulte o [Guia da API de higiene de dados](./api/overview.md) para obter mais informações.

## Linhas de tempo e transparência {#timelines-and-transparency}

[As solicitações de exclusão de registro](./ui/record-delete.md) e de expiração de conjunto de dados têm suas próprias linhas do tempo de processamento e fornecem atualizações de transparência em pontos-chave em seus respectivos fluxos de trabalho.

>[!TIP]
>
>Para obter mais informações de referência:
>- Para monitorar seu uso atual em relação aos limites de cota, consulte o [Guia de referência de cota](./api/quota.md).
>- Para regras de direito, limites mensais, linhas do tempo do SLA e políticas de tratamento de exceções, consulte o [Guia de cota de exclusão de registro (UI)](./ui/record-delete.md#quotas) e o [Guia de cota de ordem de trabalho (API)](./api/workorder.md#quotas).

O seguinte ocorre quando uma [solicitação de expiração do conjunto de dados](./ui/dataset-expiration.md) é criada:

| Preparo | Tempo após a expiração programada | Descrição |
| --- | --- | --- |
| A solicitação foi enviada | 0 horas | Um administrador de dados ou analista de privacidade envia uma solicitação para que um conjunto de dados expire em um determinado momento. A solicitação fica visível no [!UICONTROL Data Lifecycle UI] após ser enviada e permanece com o status pendente até o horário de expiração agendado, após o qual a solicitação será executada. |
| O conjunto de dados é descartado do data lake | 1 hora | O conjunto de dados é descartado da [página de inventário do conjunto de dados](../catalog/datasets/user-guide.md) na interface. Os dados no data lake são excluídos apenas por software e permanecerão assim até o final do processo, após o qual serão excluídos com dificuldade. |
| O conjunto de dados foi removido do serviço de perfil | 3 horas | A partir deste ponto, as operações que incluem segmentação em lote e por transmissão, pré-visualização ou estimativa, exportação e acesso à entidade não lerão mais os dados deste conjunto de dados. Os dados no serviço de perfil são excluídos por software e permanecerão assim até o final do processo, após o qual serão excluídos por hardware. |
| Contagem de perfis e públicos atualizados | 48 horas | Depois que todos os perfis afetados forem atualizados, todos os [públicos-alvo](../segmentation/home.md) relacionados serão atualizados para refletir seu novo tamanho. Dependendo do conjunto de dados removido e dos atributos nos quais você está segmentando, o tamanho de cada público pode aumentar ou diminuir devido à exclusão. Neste ponto, qualquer alteração resultante na contagem geral de perfis é refletida nos [widgets de painel](../dashboards/guides/profiles.md#profile-count-trend) e outros relatórios. |
| Jornadas e destinos atualizados | 50 horas | [Jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=pt-BR), [campanhas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=pt-BR) e [destinos](../destinations/home.md) são atualizados de acordo com as alterações nos segmentos relacionados. |
| Exclusão forçada concluída | 15 dias | Todos os dados relacionados ao conjunto de dados são excluídos permanentemente do data lake e do serviço de perfil. O [status do trabalho do ciclo de vida dos dados](./ui/browse.md#view-details) que excluiu o conjunto de dados foi atualizado para refletir isso. |

{style="table-layout:auto"}

### Registrar linhas do tempo de exclusão {#record-delete-transparency}

O seguinte ocorre após o envio de uma [solicitação de exclusão de registro](./ui/record-delete.md).

>[!NOTE]
>
>Os horários são aproximados e variam de acordo com a carga do sistema, o agendamento em lote e o nível de direito. O SLA completo (padrão de 30 dias, 15 dias para o Privacy and Security Shield ou Healthcare Shield) é o compromisso operacional.

| Preparo | Aproximadamente tempo | Descrição |
| --- | --- | --- |
| Solicitação enviada e em lote | Dias 1 a 15 | Uma ordem de serviço é criada e colocada em fila. As solicitações podem ser enfileiradas e colocadas em lote por até 14 dias antes do início do processamento. A exclusão em lote é o principal motivo pela qual a exclusão não é imediata. |
| Sistemas downstream processam solicitação de exclusão | Dias 16 a 25 | Os serviços downstream recebem e executam a solicitação de exclusão de registro. |
| Buffer — verificações de integridade e reenvios | Dias 25 a 30 | Uma janela de buffer permite a verificação de integridade e o reenvio de trabalhos com falha antes do fechamento da janela do SLA. O status da ordem de trabalho será atualizado para `completed` assim que todos os sistemas confirmarem a exclusão. |

{style="table-layout:auto"}

Para obter durações de fila baseadas em direitos e valores máximos de SLA, consulte [Processando linhas do tempo para envios de identificadores](./ui/record-delete.md#sla-processing-timelines).

## Próximas etapas {#next-steps}

Este documento fornece uma visão geral dos recursos de ciclo de vida dos dados da Experience Platform. Para começar a fazer solicitações de higiene de dados na interface, consulte o [guia da interface do usuário do ciclo de vida dos dados](./ui/overview.md). Para criar trabalhos do Ciclo de Vida de Dados de forma programática, consulte o [guia da API de Higiene de Dados](./api/overview.md).
