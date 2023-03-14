---
title: Visão geral da higiene dos dados
description: A Higiene de dados do Adobe Experience Platform permite gerenciar o ciclo de vida de seus dados ao atualizar ou limpar registros desatualizados ou imprecisos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Higiene de dados no Adobe Experience Platform

>[!IMPORTANT]
>
>Atualmente, a higiene de dados está disponível somente para organizações que compraram **Blindagem do Adobe Healthcare** ou **Privacidade e proteção de segurança do Adobe**.

O Adobe Experience Platform fornece um conjunto robusto de ferramentas para gerenciar operações de dados grandes e complicadas a fim de orquestrar experiências do consumidor. À medida que os dados são assimilados no sistema ao longo do tempo, torna-se cada vez mais importante gerenciar seus armazenamentos de dados para que eles sejam usados conforme esperado, atualizados quando for necessário corrigir dados incorretos e excluídos quando as políticas organizacionais o considerarem necessário.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Essas atividades podem ser executadas usando o [[!UICONTROL Higiene de dados] Espaço de trabalho da interface do usuário](#ui) ou [API de higiene de dados](#api). Quando um trabalho de higiene de dados é executado, o sistema fornece atualizações de transparência em cada etapa do processo. Consulte a seção sobre [prazos e transparência](#timelines-and-transparency) para obter mais informações sobre como cada tipo de trabalho é representado no sistema.

## [!UICONTROL Higiene de dados] Espaço de trabalho da interface do usuário {#ui}

O [!UICONTROL Higiene de dados] A área de trabalho na interface do usuário da plataforma permite configurar e agendar operações de higiene de dados, ajudando a garantir que seus registros sejam mantidos conforme o esperado.

Para obter etapas detalhadas sobre o gerenciamento de tarefas de higiene de dados na interface do usuário, consulte o [Guia da interface do usuário da Higiene de dados](./ui/overview.md).

## API de higiene de dados {#api}

O [!UICONTROL Higiene de dados] A interface do usuário é criada sobre a API de higiene de dados, cujos endpoints estão disponíveis para você usar diretamente se preferir automatizar suas atividades de higiene de dados. Consulte a [Guia da API de higiene de dados](./api/overview.md) para obter mais informações.

## Linhas de tempo e transparência

Registrar solicitações de exclusão e expiração de conjunto de dados têm suas próprias linhas do tempo de processamento e fornecem atualizações de transparência em pontos-chave em seus respectivos fluxos de trabalho.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

O seguinte ocorre quando uma [solicitação de expiração do conjunto de dados](./ui/dataset-expiration.md) é criado:

| Fase | Tempo após a expiração agendada | Descrição |
| --- | --- | --- |
| Solicitação enviada | 0 horas | Um administrador de dados ou analista de privacidade envia uma solicitação para que um conjunto de dados expire em um determinado momento. A solicitação está visível no [!UICONTROL Interface do usuário de hierarquia de dados] após o envio, e permanece em um status pendente até o tempo de expiração agendado, após o qual a solicitação será executada. |
| O conjunto de dados é descartado | 1 hora | O conjunto de dados é descartado do [página de inventário do conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do . Os dados no lago de dados são excluídos apenas de forma suave e permanecerão até o final do processo, após o que serão excluídos permanentemente. |
| Contagem de perfis atualizada | 30 horas | Dependendo do conteúdo do conjunto de dados que está sendo excluído, alguns perfis poderão ser removidos do sistema se todos os atributos de componente estiverem vinculados a esse conjunto de dados. 30 horas após o conjunto de dados ser excluído, todas as alterações resultantes nas contagens gerais de perfil serão refletidas em [widgets de painel](../dashboards/guides/profiles.md#profile-count-trend) e outros relatórios. |
| Segmentos atualizados | 48 horas | Depois que todos os perfis afetados forem atualizados, todos os perfis relacionados [segmentos](../segmentation/home.md) são atualizadas para refletir seu novo tamanho. Dependendo do conjunto de dados que foi removido e dos atributos que você está segmentando, o tamanho de cada segmento pode aumentar ou diminuir como resultado da exclusão. |
| Jornadas e destinos atualizados | 50 horas | [Jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campanhas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)e [destinos](../destinations/home.md) são atualizadas de acordo com as alterações em segmentos relacionados. |
| Exclusão em disco concluída | 14 dias | Todos os dados relacionados ao conjunto de dados são excluídos permanentemente do lago de dados. O [estatuto do trabalho de higiene](./ui/browse.md#view-details) que excluiu o conjunto de dados é atualizado para refletir isso. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Próximas etapas

Este documento forneceu uma visão geral dos recursos de higiene de dados da Platform. Para começar a fazer solicitações de higiene de dados na interface do usuário, consulte o [Guia da interface do usuário](./ui/overview.md). Para saber como criar trabalhos de higiene de dados de forma programática, consulte [Guia da API de higiene de dados](./api/overview.md)
