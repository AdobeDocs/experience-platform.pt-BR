---
title: Procurar Ordens de Serviço de Higiene de Dados
description: Saiba como visualizar e gerenciar pedidos de higiene de dados existentes na interface do usuário do Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: f246a014de7869b627a677ac82e98d4556065010
workflow-type: tm+mt
source-wordcount: '616'
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
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Healthcare Shield.

Quando uma solicitação de higiene de dados é enviada para o sistema, uma ordem de trabalho é criada para executar a tarefa solicitada. Uma ordem de trabalho representa um processo específico de higiene de dados, como uma expiração programada do conjunto de dados, que inclui seu status atual e outros detalhes relacionados.

Este guia aborda como visualizar e gerenciar pedidos de trabalho existentes na interface do usuário do Adobe Experience Platform.

## Listar e filtrar ordens de trabalho existentes

Ao acessar o **[!UICONTROL Higiene de dados]** na interface do usuário, uma lista de pedidos de trabalho existentes é mostrada junto com os detalhes básicos.

![Imagem que mostra o [!UICONTROL Higiene de dados] espaço de trabalho na interface do usuário da plataforma](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Selecione o ícone de funil (![Imagem do ícone de funil](../images/ui/browse/funnel-icon.png)) para visualizar uma lista de filtros para as ordens de serviço exibidas.

![Imagem dos filtros da ordem de trabalho exibidos](../images/ui/browse/filters.png)

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Status] | Filtro com base no status atual da ordem de serviço:<ul><li>**[!UICONTROL Concluído]**: O trabalho foi concluído.</li><li>**[!UICONTROL Pending]**: O trabalho foi criado, mas ainda não foi executado. A [solicitação de expiração do conjunto de dados](./dataset-expiration.md) O assume esse status antes da data de exclusão agendada. Quando a data de exclusão chegar, o status será atualizado para [!UICONTROL Em execução] a menos que a tarefa seja cancelada antecipadamente.</li><li>**[!UICONTROL Em execução]**: A solicitação de expiração do conjunto de dados foi iniciada e está em processamento no momento.</li><li>**[!UICONTROL Cancelado]**: A tarefa foi cancelada como parte de uma solicitação manual do usuário.</li></ul> |
| [!UICONTROL Data de criação] | Filtrar com base no momento em que a ordem de trabalho foi feita. |
| [!UICONTROL Data de validade] | Filtrar solicitações de expiração do conjunto de dados com base na data de exclusão agendada para o conjunto de dados em questão. |
| [!UICONTROL Data de atualização] | Filtrar solicitações de expiração do conjunto de dados com base em quando a ordem de trabalho foi atualizada pela última vez. As criações e expirações são contadas como atualizações. |

{style=&quot;table-layout:auto&quot;}

## Exibir os detalhes de uma ordem de serviço {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Status por serviço"
>abstract="As solicitações de higiene de dados são processadas de maneira independente por vários serviços de Experience Platform. Esta seção descreve o status de processamento atual da solicitação para cada serviço respectivo. Para saber mais, consulte o guia da interface do usuário de higiene de dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Número de identidades"
>abstract="O número de identidades que foram solicitadas a serem excluídas como parte desta ordem de trabalho. As identidades incluídas na contagem podem não existir necessariamente nos conjuntos de dados afetados. Para saber mais, consulte o guia da interface do usuário de higiene de dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Resposta de exclusão do consumidor"
>abstract="Quando um processo de exclusão do consumidor recebe uma resposta do sistema, essas mensagens são exibidas na variável **[!UICONTROL Resultado]** seção. Se ocorrer um problema enquanto uma ordem de trabalho está sendo processada, qualquer mensagem de erro relevante será exibida nesta seção para ajudá-lo a solucionar o problema. Para saber mais, consulte o guia da interface do usuário de higiene de dados."

Selecione a ID de um pedido de trabalho listado para exibir seus detalhes.

![Imagem que mostra uma ID de ordem de trabalho sendo selecionada](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details {#consumer-delete}

The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details {#dataset-expiration} -->

A página de detalhes de uma expiração de conjunto de dados fornece informações sobre seus atributos básicos, incluindo a data de expiração programada nos dias restantes antes da exclusão. No painel direito, você pode usar controles para editar ou cancelar a expiração.

![Imagem que mostra a página de detalhes de uma ordem de trabalho de expiração do conjunto de dados](../images/ui/browse/ttl-details.png)

## Próximas etapas

Este guia cobriu como visualizar e gerenciar pedidos de higiene de dados existentes na interface do usuário da plataforma. Para obter informações sobre como criar seus próprios pedidos de trabalho, consulte o guia em [agendamento de uma expiração de conjunto de dados](./dataset-expiration.md).
