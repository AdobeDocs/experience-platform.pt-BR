---
title: Procurar Ordens de Serviço de Higiene de Dados
description: Saiba como visualizar e gerenciar pedidos de higiene de dados existentes na interface do usuário do Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '860'
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
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Healthcare Shield.

Quando uma solicitação de higiene de dados é enviada para o sistema, uma ordem de trabalho é criada para executar a tarefa solicitada. Uma ordem de trabalho representa um processo específico de higiene de dados, como uma expiração programada do conjunto de dados, que inclui seu status atual e outros detalhes relacionados.

Este guia aborda como visualizar e gerenciar pedidos de trabalho existentes na interface do usuário do Adobe Experience Platform.

## Listar e filtrar ordens de trabalho existentes

Ao acessar o **[!UICONTROL Higiene de dados]** na interface do usuário, uma lista de pedidos de trabalho existentes é mostrada junto com os detalhes básicos.

![Imagem que mostra o [!UICONTROL Higiene de dados] espaço de trabalho na interface do usuário da plataforma](../images/ui/browse/work-order-list.png)

A lista mostra somente pedidos de trabalho para uma categoria de cada vez. Selecionar **[!UICONTROL Consumidor]** para exibir uma lista de tarefas de exclusão do consumidor, e **[!UICONTROL Conjunto de dados]** para exibir uma lista de expirações agendadas do conjunto de dados.

![Imagem que mostra o [!UICONTROL Conjunto de dados] guia](../images/ui/browse/dataset-tab.png)

Selecione o ícone de funil (![Imagem do ícone de funil](../images/ui/browse/funnel-icon.png)) para visualizar uma lista de filtros para as ordens de serviço exibidas.

![Imagem dos filtros da ordem de trabalho exibidos](../images/ui/browse/filters.png)

Dependendo do tipo de ordem de trabalho que você estiver visualizando, diferentes opções de filtro estarão disponíveis.

### Filtros para exclusões de consumidores

Os seguintes filtros se aplicam às solicitações de exclusão do consumidor:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Status] | Filtro com base no status atual da ordem de serviço:<ul><li>**[!UICONTROL Concluído]**: O trabalho foi concluído.</li><li>**[!UICONTROL Falha]**: O trabalho encontrou um erro e não pôde ser concluído.</li><li>**[!UICONTROL Processamento]**: A solicitação foi iniciada e está em processamento no momento.</li></ul> |
| [!UICONTROL Data de criação] | Filtrar com base no momento em que a ordem de trabalho foi feita. |
| [!UICONTROL Data de atualização] | Filtrar com base em quando a ordem de trabalho foi atualizada pela última vez. As criações são contadas como atualizações. |

### Filtros para expirações do conjunto de dados

Os seguintes filtros se aplicam às solicitações de expiração do conjunto de dados:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Status] | Filtro com base no status atual da ordem de serviço:<ul><li>**[!UICONTROL Concluído]**: O trabalho foi concluído.</li><li>**[!UICONTROL Pending]**: O trabalho foi criado, mas ainda não foi executado. A [solicitação de expiração do conjunto de dados](./dataset-expiration.md) O assume esse status antes da data de exclusão agendada. Quando a data de exclusão chegar, o status será atualizado para [!UICONTROL Em execução] a menos que a tarefa seja cancelada antecipadamente.</li><li>**[!UICONTROL Em execução]**: A solicitação de expiração do conjunto de dados foi iniciada e está em processamento no momento.</li><li>**[!UICONTROL Cancelado]**: A tarefa foi cancelada como parte de uma solicitação manual do usuário.</li></ul> |
| [!UICONTROL Data de criação] | Filtrar com base no momento em que a ordem de trabalho foi feita. |
| [!UICONTROL Data de validade] | Filtrar solicitações de expiração do conjunto de dados com base na data de exclusão agendada para o conjunto de dados em questão. |
| [!UICONTROL Data de atualização] | Filtrar com base em quando a ordem de trabalho foi atualizada pela última vez. As criações e expirações são contadas como atualizações. |

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
>abstract="Quando um processo de exclusão do consumidor recebe uma resposta do sistema, essas mensagens são exibidas na guia **[!UICONTROL Resultado]** seção. Se ocorrer um problema enquanto uma ordem de trabalho está sendo processada, qualquer mensagem de erro relevante será exibida nesta seção para ajudá-lo a solucionar o problema. Para saber mais, consulte o guia da interface do usuário de higiene de dados."

Selecione a ID de um pedido de trabalho listado para exibir seus detalhes.

![Imagem que mostra uma ID de ordem de trabalho sendo selecionada](../images/ui/browse/select-work-order.png)

Dependendo do tipo de ordem de trabalho selecionada, informações e controles diferentes são fornecidos. Elas são abordadas nas seções abaixo.

### Detalhes de exclusão do consumidor {#consumer-delete}

Os detalhes de uma solicitação de exclusão do consumidor incluem seu status atual e o tempo decorrido desde que a solicitação foi feita. Cada solicitação também inclui uma **[!UICONTROL Status por serviço]** seção que fornece detalhes de status individuais sobre cada serviço de downstream envolvido na exclusão. No painel direito, você pode usar controles para atualizar o nome e a descrição da ordem de trabalho.

![Imagem mostrando a página de detalhes de uma ordem de trabalho de exclusão do consumidor](../images/ui/browse/consumer-delete-details.png)

### Detalhes da expiração do conjunto de dados {#dataset-expiration}

A página de detalhes de uma expiração de conjunto de dados fornece informações sobre seus atributos básicos, incluindo a data de expiração programada nos dias restantes antes da exclusão. No painel direito, você pode usar controles para editar ou cancelar a expiração.

![Imagem que mostra a página de detalhes de uma ordem de trabalho de expiração do conjunto de dados](../images/ui/browse/ttl-details.png)

## Próximas etapas

Este guia cobriu como visualizar e gerenciar pedidos de higiene de dados existentes na interface do usuário da plataforma. Para obter informações sobre como criar seus próprios pedidos de trabalho, consulte a seguinte documentação:

* [Gerenciar expirações do conjunto de dados](./dataset-expiration.md)
* [Gerenciar exclusões de consumidores](./delete-consumer.md)
