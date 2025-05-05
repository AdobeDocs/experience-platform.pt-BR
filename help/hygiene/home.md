---
title: Visão geral do gerenciamento avançado do ciclo de vida dos dados
description: O Gerenciamento avançado do ciclo de vida dos dados permite gerenciar o ciclo de vida dos dados atualizando ou removendo registros desatualizados ou imprecisos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---

# Gerenciamento avançado do ciclo de vida dos dados no Adobe Experience Platform

O Adobe Experience Platform fornece um conjunto robusto de ferramentas para gerenciar operações de dados grandes e complicadas para orquestrar as experiências do consumidor. À medida que os dados são assimilados no sistema ao longo do tempo, torna-se cada vez mais importante gerenciar seus armazenamentos de dados para que eles sejam usados conforme o esperado, sejam atualizados quando dados incorretos precisarem de correção e sejam excluídos quando as políticas organizacionais considerarem necessário.

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Estas atividades podem ser executadas usando o [[!UICONTROL espaço de trabalho da interface do usuário do Ciclo de Vida de Dados]](#ui) ou a [API de Higiene de Dados](#api). Quando um trabalho do ciclo de vida dos dados é executado, o sistema fornece atualizações de transparência em cada etapa do processo. Consulte a seção sobre [linhas do tempo e transparência](#timelines-and-transparency) para obter mais informações sobre como cada tipo de trabalho é representado no sistema.

>[!NOTE]
>
>O Gerenciamento Avançado do Ciclo de Vida dos Dados suporta exclusões de conjuntos de dados por meio do [ponto de extremidade de expiração do conjunto de dados](./api/dataset-expiration.md) e exclusões de ID (dados em nível de linha) usando identidades primárias por meio do [ponto de extremidade da ordem de trabalho](./api/workorder.md). Também é possível gerenciar [expirações do conjunto de dados](./ui/dataset-expiration.md) e [exclusões de registros](./ui/record-delete.md) por meio da interface do usuário do Experience Platform. Consulte a documentação vinculada para obter mais informações. Observe que o ciclo de vida dos dados não oferece suporte à exclusão de lotes.

## Espaço de trabalho da interface do usuário do [!UICONTROL Ciclo de Vida de Dados] {#ui}

O espaço de trabalho [!UICONTROL Ciclo de Vida de Dados] na interface do usuário do Experience Platform permite configurar e agendar operações de ciclo de vida de dados, ajudando a garantir que seus registros sejam mantidos conforme esperado.

Para obter etapas detalhadas sobre como gerenciar tarefas do ciclo de vida de dados na interface, consulte o [guia da interface do ciclo de vida de dados](./ui/overview.md).

## API de higiene de dados {#api}

A interface do [!UICONTROL Ciclo de vida dos dados] foi criada com base na API de Higiene de Dados, cujos endpoints estão disponíveis para você usar diretamente, caso prefira automatizar as atividades do ciclo de vida dos dados. Consulte o [Guia da API de higiene de dados](./api/overview.md) para obter mais informações.

## Linhas de tempo e transparência {#timelines-and-transparency}

[As solicitações de exclusão de registro](./ui/record-delete.md) e de expiração de conjunto de dados têm suas próprias linhas do tempo de processamento e fornecem atualizações de transparência em pontos-chave em seus respectivos fluxos de trabalho.

O seguinte ocorre quando uma [solicitação de expiração do conjunto de dados](./ui/dataset-expiration.md) é criada:

| Estágio | Tempo após a expiração programada | Descrição |
| --- | --- | --- |
| A solicitação foi enviada | 0 horas | Um administrador de dados ou analista de privacidade envia uma solicitação para que um conjunto de dados expire em um determinado momento. A solicitação está visível na [!UICONTROL Interface do Usuário do Ciclo de Vida de Dados] após ser enviada e permanece com o status pendente até o horário de expiração agendado, após o qual a solicitação será executada. |
| O conjunto de dados está sinalizado para exclusão | 0-2 horas | Depois que a solicitação é executada, o conjunto de dados é sinalizado para exclusão. Se estiver usando o armazenamento de dados do Amazon Web Services (AWS), esse processo levará até duas horas. Durante esse tempo, operações como segmentação em lote e por transmissão, pré-visualização ou estimativa, exportação e acesso desconsideram esse conjunto de dados. |
| Conjunto de dados descartado | 3 horas | **Uma hora depois que o conjunto de dados for sinalizado para exclusão**, ele será totalmente removido do sistema. Neste ponto, o conjunto de dados é descartado da [página de inventário do conjunto de dados](../catalog/datasets/user-guide.md) na interface. No entanto, os dados no data lake são excluídos apenas por software neste estágio e permanecerão assim até que o processo de exclusão permanente seja concluído. |
| Contagem de perfis atualizada | 30 horas | Dependendo do conteúdo do conjunto de dados que está sendo excluído, alguns perfis podem ser removidos do sistema se todos os atributos do componente estiverem vinculados a esse conjunto de dados. 30 horas após a exclusão do conjunto de dados, as alterações resultantes na contagem geral dos perfis são refletidas nos [widgets do painel](../dashboards/guides/profiles.md#profile-count-trend) e outros relatórios. |
| Públicos atualizados | 48 horas | Depois que todos os perfis afetados forem atualizados, todos os [públicos-alvo](../segmentation/home.md) relacionados serão atualizados para refletir seu novo tamanho. Dependendo do conjunto de dados removido e dos atributos nos quais você está segmentando, o tamanho de cada público pode aumentar ou diminuir como resultado da exclusão. |
| Jornadas e destinos atualizados | 50 horas | [Jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=pt-BR), [campanhas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=pt-BR) e [destinos](../destinations/home.md) são atualizados de acordo com as alterações nos segmentos relacionados. |
| Exclusão forçada concluída | 15 dias | Todos os dados relacionados ao conjunto de dados são excluídos permanentemente do data lake. O [status do trabalho do ciclo de vida dos dados](./ui/browse.md#view-details) que excluiu o conjunto de dados foi atualizado para refletir isso. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>As exclusões de conjuntos de dados na Amazon Web Services (AWS) estão sujeitas a uma latência de cerca de três horas antes de as alterações serem totalmente aplicadas. Isso inclui até duas horas para que o conjunto de dados seja sinalizado para exclusão, seguidas por uma hora adicional antes de ser totalmente descartado do sistema. Por outro lado, as solicitações de exclusão para instâncias do Experience Platform que usam o Azure Data Lake resultam em alterações imediatas em funções comerciais.
>
>Para usuários do AWS, esse atraso pode afetar a segmentação em lote, a segmentação por transmissão, as visualizações, as estimativas, as exportações e o acesso aos dados. Essa latência afeta apenas os clientes que usam o AWS, já que os usuários do Azure Data Lake experimentam atualizações imediatas. Para usuários do AWS, pode levar até três horas para que as solicitações de exclusão se propaguem totalmente em todos os sistemas afetados. Ajuste suas expectativas de acordo.


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=pt-BR), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=pt-BR), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Próximas etapas

Este documento forneceu uma visão geral dos recursos de ciclo de vida dos dados da Experience Platform. Para começar a fazer solicitações de higiene de dados na interface do usuário, consulte o [manual da interface](./ui/overview.md). Para saber como criar trabalhos do Ciclo de Vida de Dados de forma programática, consulte o [guia da API de Higiene de Dados](./api/overview.md)
