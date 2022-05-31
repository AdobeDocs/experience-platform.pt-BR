---
title: Procurar Ordens de Serviço de Higiene de Dados
description: Saiba como visualizar e gerenciar pedidos de higiene de dados existentes na interface do usuário do Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: c24aa700eb425770266bbee5c187e2e87b15a9ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# Procurar ordens de trabalho de higiene de dados {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs de ordem de trabalho"
>abstract="Quando uma solicitação de higiene de dados é enviada para o sistema, uma ordem de trabalho é criada para executar a tarefa solicitada. Em outras palavras, uma ordem de trabalho representa um processo específico de higiene de dados, que inclui seu status atual e outros detalhes relacionados. Cada ordem de trabalho recebe automaticamente sua própria ID exclusiva após a criação."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Shield for Healthcare.

Quando uma solicitação de higiene de dados é enviada para o sistema, uma ordem de trabalho é criada para executar a tarefa solicitada. Uma ordem de trabalho representa um processo específico de higiene de dados, como o TTL (tempo agendado para vida útil) de um conjunto de dados, que inclui seu status atual e outros detalhes relacionados.

Este guia aborda como visualizar e gerenciar pedidos de trabalho existentes na interface do usuário do Adobe Experience Platform.

## Listar e filtrar ordens de trabalho existentes

Ao acessar o **[!UICONTROL Higiene de dados]** na interface do usuário, uma lista de pedidos de trabalho existentes é mostrada junto com os detalhes básicos.

![Imagem que mostra o [!UICONTROL Higiene de dados] espaço de trabalho na interface do usuário da plataforma](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Selecione o ícone de funil (![Imagem do ícone de funil](../images/ui/browse/funnel-icon.png)) para visualizar uma lista de filtros para as ordens de serviço exibidas.

![Imagem dos filtros da ordem de trabalho exibidos](../images/ui/browse/filters.png)

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Status] | Filtrar com base no status atual da ordem de trabalho. |
| [!UICONTROL Data de criação] | Filtre com base em quando a solicitação TTL do conjunto de dados foi feita. |
| [!UICONTROL Data de exclusão] | Filtro com base na data de exclusão agendada pelo TTL. |
| [!UICONTROL Data de atualização] | Filtrar com base em quando o TTL do conjunto de dados foi atualizado pela última vez. As criações e as consultas TTL são contadas como atualizações. |

{style=&quot;table-layout:auto&quot;}

## Exibir os detalhes de uma ordem de serviço

Selecione a ID de um pedido de trabalho listado para exibir seus detalhes.

![Imagem que mostra uma ID de ordem de trabalho sendo selecionada](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

A página de detalhes de um TTL de conjunto de dados fornece informações sobre seus atributos básicos, incluindo a data de expiração programada nos dias restantes antes da exclusão. No painel direito, você pode usar controles para editar ou cancelar o TTL.

![Imagem que mostra a página de detalhes de uma ordem de serviço do TTL do conjunto de dados](../images/ui/browse/ttl-details.png)

## Próximas etapas

Este guia cobriu como visualizar e gerenciar pedidos de higiene de dados existentes na interface do usuário da plataforma. Para obter informações sobre como criar seus próprios pedidos de trabalho, consulte o guia em [agendamento de um TTL de conjunto de dados](./ttl.md).
