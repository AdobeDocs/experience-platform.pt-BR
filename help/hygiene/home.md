---
title: Visão geral da higiene dos dados
description: A Higiene de dados do Adobe Experience Platform permite gerenciar o ciclo de vida de seus dados ao atualizar ou limpar registros desatualizados ou imprecisos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 70a2abcc4d6e27a89e77d68e7757e4876eaa4fc0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# Higiene de dados no Adobe Experience Platform

>[!IMPORTANT]
>
>Atualmente, a higiene de dados está disponível somente para organizações que compraram **Blindagem do Adobe Healthcare** ou **Privacidade e proteção de segurança do Adobe**.

O Adobe Experience Platform fornece um conjunto robusto de ferramentas para gerenciar operações de dados grandes e complicadas a fim de orquestrar experiências do consumidor. À medida que os dados são assimilados no sistema ao longo do tempo, torna-se cada vez mais importante gerenciar seus armazenamentos de dados para que eles sejam usados conforme esperado, atualizados quando for necessário corrigir dados incorretos e excluídos quando as políticas organizacionais o considerarem necessário.

Os recursos de higiene de dados da Platform permitem gerenciar os dados armazenados por meio do seguinte:

* Agendamento de expirações automatizadas do conjunto de dados
* Exclusão de registros individuais de um ou todos os conjuntos de dados

>[!IMPORTANT]
>
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles são **not** a ser usado para solicitações de direitos do titular de dados (conformidade) como parte de regulamentos de privacidade como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) em vez disso.

Essas atividades podem ser executadas usando o [[!UICONTROL Higiene de dados] Espaço de trabalho da interface do usuário](#ui) ou [API de higiene de dados](#api). Quando um trabalho de higiene de dados é executado, o sistema fornece atualizações de transparência em cada etapa do processo. Consulte a seção sobre [prazos e transparência](#timelines-and-transparency) para obter mais informações sobre como cada tipo de trabalho é representado no sistema.

## [!UICONTROL Higiene de dados] Espaço de trabalho da interface do usuário {#ui}

O [!UICONTROL Higiene de dados] A área de trabalho na interface do usuário da plataforma permite configurar e agendar operações de higiene de dados, ajudando a garantir que seus registros sejam mantidos conforme o esperado.

Para obter etapas detalhadas sobre o gerenciamento de tarefas de higiene de dados na interface do usuário, consulte o [Guia da interface do usuário da Higiene de dados](./ui/overview.md).

## API de higiene de dados {#api}

O [!UICONTROL Higiene de dados] A interface do usuário é criada sobre a API de higiene de dados, cujos endpoints estão disponíveis para você usar diretamente se preferir automatizar suas atividades de higiene de dados. Consulte a [Guia da API de higiene de dados](./api/overview.md) para obter mais informações.

## Linhas de tempo e transparência

Registrar solicitações de exclusão e expiração de conjunto de dados têm suas próprias linhas do tempo de processamento e fornecem atualizações de transparência em pontos-chave em seus respectivos fluxos de trabalho. Consulte as seções abaixo para obter detalhes sobre cada tipo de trabalho.

### Expirações do conjunto de dados {#dataset-expiration-transparency}

O seguinte ocorre quando uma [solicitação de expiração do conjunto de dados](./ui/dataset-expiration.md) é criado:

| Fase | Tempo após a expiração agendada | Descrição |
| --- | --- | --- |
| Solicitação enviada | 0 horas | Um administrador de dados ou analista de privacidade envia uma solicitação para que um conjunto de dados expire em um determinado momento. A solicitação está visível no [!UICONTROL Interface do usuário de hierarquia de dados] após o envio, e permanece em um status pendente até o tempo de expiração agendado, após o qual a solicitação será executada. |
| O conjunto de dados é descartado | 1 hora | O conjunto de dados é descartado do [página de inventário do conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do . Os dados no lago de dados são excluídos apenas de forma suave e permanecerão até o final do processo, após o que serão excluídos permanentemente. |
| Contagem de perfis atualizada | 30 horas | Dependendo do conteúdo do conjunto de dados que está sendo excluído, alguns perfis poderão ser removidos do sistema se todos os atributos de componente estiverem vinculados a esse conjunto de dados. 30 horas após o conjunto de dados ser excluído, todas as alterações resultantes nas contagens gerais de perfil serão refletidas em [widgets de painel](../dashboards/guides/profiles.md#profile-count-trend) e outros relatórios. |
| Segmentos atualizados | 48 horas | Depois que todos os perfis afetados forem atualizados, todos os perfis relacionados [segmentos](../segmentation/home.md) são atualizadas para refletir seu novo tamanho. Dependendo do conjunto de dados que foi removido e dos atributos que você está segmentando, o tamanho de cada segmento pode aumentar ou diminuir como resultado da exclusão. |
| Jornadas e destinos atualizados | 50 horas | [Jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campanhas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)e [destinos](../destinations/home.md) são atualizadas de acordo com as alterações em segmentos relacionados. |
| Exclusão em disco concluída | 14 dias | Todos os dados relacionados ao conjunto de dados são excluídos permanentemente do lago de dados. O [estatuto do trabalho de higiene](./ui/browse.md#view-details) que excluiu o conjunto de dados é atualizado para refletir isso. |

{style=&quot;table-layout:auto&quot;}

### Exclusões de registro {#record-delete-transparency}

>[!IMPORTANT]
>
>As exclusões de registros só estão disponíveis para organizações que compraram o Adobe Healthcare Shield.

O seguinte ocorre quando uma [solicitação de exclusão de registro](./ui/record-delete.md) é criado:

| Fase | Tempo após o envio da solicitação | Descrição |
| --- | --- | --- |
| Solicitação enviada | 0 horas | Um administrador de dados ou analista de privacidade envia uma solicitação de exclusão de registro. A solicitação está visível no [!UICONTROL Interface do usuário de hierarquia de dados] após a sua apresentação. |
| Pesquisas de perfil atualizadas | 3 horas | A alteração nas contagens de perfil causada pela identidade excluída é refletida em [widgets de painel](../dashboards/guides/profiles.md#profile-count-trend) e outros relatórios. |
| Segmentos atualizados | 24 horas | Depois que os perfis forem removidos, todos os [segmentos](../segmentation/home.md) são atualizadas para refletir seu novo tamanho. |
| Jornadas e destinos atualizados | 26 horas | [Jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campanhas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)e [destinos](../destinations/home.md) são atualizadas de acordo com as alterações em segmentos relacionados. |
| Registros suaves excluídos no lago de dados | 7 dias | Os dados são excluídos facilmente do lago de dados. |
| Extração de dados concluída | 14 dias | O [estatuto do trabalho de higiene](./ui/browse.md#view-details) Atualizações para indicar que o trabalho foi concluído, o que significa que o vazamento de dados foi concluído no lago de dados e que os registros relevantes foram eliminados. |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Este documento forneceu uma visão geral dos recursos de higiene de dados da Platform. Para começar a fazer solicitações de higiene de dados na interface do usuário, consulte o [Guia da interface do usuário](./ui/overview.md). Para saber como criar trabalhos de higiene de dados de forma programática, consulte [Guia da API de higiene de dados](./api/overview.md)
