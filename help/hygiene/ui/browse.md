---
title: Procurar Ordens de Serviço de Higiene de Dados
description: Saiba como visualizar e gerenciar ordens de trabalho de higiene de dados existentes na interface do usuário do Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 25%

---

# Procurar ordens de trabalho de higiene de dados {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs de ordem de trabalho"
>abstract="Quando uma solicitação de higiene de dados é enviada para o sistema, uma ordem de trabalho é criada para executar a tarefa solicitada. Em outras palavras, uma ordem de trabalho representa um processo específico de higiene de dados, que inclui seu status atual e outros detalhes relacionados. Cada ordem de trabalho recebe automaticamente sua própria ID exclusiva após a criação."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Atualmente, os recursos de higiene de dados na Adobe Experience Platform estão disponíveis apenas para organizações que compraram **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**.

Quando uma solicitação de higiene de dados é enviada para o sistema, uma ordem de trabalho é criada para executar a tarefa solicitada. Uma ordem de serviço representa um processo específico de higiene de dados, como a expiração programada de um conjunto de dados, que inclui o status atual e outros detalhes relacionados.

Este guia aborda como exibir e gerenciar ordens de serviço existentes na interface do usuário do Adobe Experience Platform.

## Listar e filtrar ordens de serviço existentes

Ao acessar o pela primeira vez, **[!UICONTROL Higiene de dados]** espaço de trabalho na interface, uma lista de ordens de serviço existentes é mostrada junto com seus detalhes básicos.

![Imagem mostrando o [!UICONTROL Higiene de dados] espaço de trabalho na interface do usuário da Platform](../images/ui/browse/work-order-list.png)

A lista mostra somente ordens de serviço para uma categoria de cada vez. Selecionar **[!UICONTROL Consumidor]** para exibir uma lista de tarefas de deleção de registro e **[!UICONTROL Conjunto de dados]** para visualizar uma lista de expirações programadas do conjunto de dados.

![Imagem mostrando o [!UICONTROL Conjunto de dados] guia](../images/ui/browse/dataset-tab.png)

Selecione o ícone de funil (![Imagem do ícone de funil](../images/ui/browse/funnel-icon.png)) para exibir uma lista de filtros para as ordens de serviço exibidas.

![Imagem dos filtros de ordem de trabalho exibidos](../images/ui/browse/filters.png)

Dependendo do tipo de ordem de serviço que você está exibindo, diferentes opções de filtro estarão disponíveis.

### Filtros para exclusões de registro

Os filtros a seguir se aplicam às solicitações de exclusão de registro:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Status] | Filtrar com base no status atual da ordem de serviço:<ul><li>**[!UICONTROL Concluído]**: O trabalho foi concluído.</li><li>**[!UICONTROL Failed]**: o trabalho encontrou um erro e não pôde ser concluído.</li><li>**[!UICONTROL Processando]**: a solicitação foi iniciada e está sendo processada.</li></ul> |
| [!UICONTROL Data de criação] | Filtrar com base em quando a ordem de serviço foi feita. |
| [!UICONTROL Data da atualização] | Filtrar com base em quando a ordem de serviço foi atualizada pela última vez. As criações são contadas como atualizações. |

### Filtros para expirações de conjunto de dados

Os filtros a seguir se aplicam às solicitações de expiração do conjunto de dados:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Status] | Filtrar com base no status atual da ordem de serviço:<ul><li>**[!UICONTROL Concluído]**: O trabalho foi concluído.</li><li>**[!UICONTROL Pending]**: A tarefa foi criada, mas ainda não foi executada. A [solicitação de expiração do conjunto de dados](./dataset-expiration.md) O assume esse status antes da data de exclusão programada. Quando a data de exclusão chegar, o status será atualizado para [!UICONTROL Execução] a menos que a tarefa seja cancelada antecipadamente.</li><li>**[!UICONTROL Execução]**: a solicitação de expiração do conjunto de dados foi iniciada e está sendo processada.</li><li>**[!UICONTROL Cancelado]**: o trabalho foi cancelado como parte de uma solicitação manual do usuário.</li></ul> |
| [!UICONTROL Data de criação] | Filtrar com base em quando a ordem de serviço foi feita. |
| [!UICONTROL Data de validade] | Filtre solicitações de expiração do conjunto de dados com base na data de exclusão agendada para o conjunto de dados em questão. |
| [!UICONTROL Data da atualização] | Filtrar com base em quando a ordem de serviço foi atualizada pela última vez. Criações e expirações são contadas como atualizações. |

{style="table-layout:auto"}

## Exibir os detalhes de uma ordem de serviço {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Status por serviço"
>abstract="As solicitações de higiene de dados são processadas de maneira independente por vários serviços da Experience Platform. Esta seção descreve o status de processamento atual da solicitação para cada serviço respectivo. Para saber mais, consulte o guia da interface de higiene de dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Número de identidades"
>abstract="O número de identidades cujos registros foram solicitados a serem atualizados ou excluídos como parte dessa ordem de trabalho. As identidades incluídas na contagem podem não existir necessariamente nos conjuntos de dados afetados. Para saber mais, consulte o guia da interface de higiene de dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Registrar resposta de exclusão"
>abstract="Quando um processo de exclusão de registro recebe uma resposta do sistema, essas mensagens são exibidas na seção **[!UICONTROL Resultado]**. Se ocorrer um problema enquanto uma ordem de trabalho está sendo processada, qualquer mensagem de erro relevante será exibida nessa seção para ajudar você a solucionar o problema. Para saber mais, consulte o guia da interface de higiene de dados."

Selecione a ID de uma ordem de serviço listada para exibir seus detalhes.

![Imagem mostrando uma ID de ordem de trabalho sendo selecionada](../images/ui/browse/select-work-order.png)

Dependendo do tipo de ordem de serviço selecionada, informações e controles diferentes serão fornecidos. Elas são abordadas nas seções abaixo.

### Detalhes de exclusão de registro {#record-delete}

Os detalhes de uma solicitação de exclusão de registro incluem o status atual e o tempo decorrido desde a solicitação. Cada solicitação também inclui um **[!UICONTROL Status por serviço]** seção que fornece detalhes de status individuais em cada serviço downstream envolvido na exclusão. No painel direito, você pode usar controles para atualizar o nome e a descrição da ordem de serviço.

![Imagem mostrando a página de detalhes de uma ordem de serviço de exclusão de registro](../images/ui/browse/record-delete-details.png)

### Detalhes de expiração do conjunto de dados {#dataset-expiration}

A página de detalhes de uma expiração de conjunto de dados fornece informações sobre seus atributos básicos, incluindo a data de expiração programada nos dias restantes antes de ocorrer a exclusão. No painel direito, é possível usar os controles para editar ou cancelar a expiração.

![Imagem mostrando a página de detalhes de uma ordem de trabalho de expiração do conjunto de dados](../images/ui/browse/ttl-details.png)

## Próximas etapas

Este guia abordou como visualizar e gerenciar ordens de trabalho de higiene de dados existentes na interface do usuário da plataforma. Para obter informações sobre como criar suas próprias ordens de serviço, consulte a seguinte documentação:

* [Gerenciar expirações do conjunto de dados](./dataset-expiration.md)
<!-- * [Manage record deletes](./record-delete.md) -->
