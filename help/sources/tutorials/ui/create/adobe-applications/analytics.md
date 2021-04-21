---
keywords: Experience Platform, home, tópicos populares, conector de origem do Analytics, conector do Analytics, fonte do Analytics, analytics
solution: Experience Platform
title: Criar uma conexão de origem do Adobe Analytics na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Adobe Analytics na interface do usuário para trazer dados do consumidor para o Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 2%

---

# Criar uma conexão de origem do Adobe Analytics na interface do usuário

Este tutorial fornece etapas para criar uma conexão de origem Adobe Analytics na interface do usuário para trazer dados do consumidor para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil](../../../../../profile/home.md) do cliente em tempo real: Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Criar uma conexão de origem com o Adobe Analytics

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho de origens. A tela **Catalog** exibe as fontes disponíveis para criar conexões de entrada com o e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Adobe applications]**, selecione **[!UICONTROL Adobe Analytics]** para expor uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição da fonte selecionada, bem como opções para se conectar com a fonte ou exibir sua documentação. Para exibir as contas existentes, selecione **[!UICONTROL Accounts]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Selecionar dados

A etapa **[!UICONTROL Adobe Analytics]** é exibida. Os fluxos de conjunto de dados estabelecidos anteriormente para o Analytics são listados nesta tela. Você pode criar um novo fluxo de conjunto de dados clicando em **[!UICONTROL Select data]**.

>[!NOTE]
>
>Várias conexões de entrada para uma fonte podem ser feitas para trazer dados diferentes.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Na lista de conjuntos de relatórios disponíveis, selecione aquele que deseja trazer para a Plataforma e clique em **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Dê um nome ao fluxo do conjunto de dados

A etapa **[!UICONTROL Dataset flow detail]** é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo do conjunto de dados. Selecione **[!UICONTROL Next]** quando terminar.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Revisar o fluxo do conjunto de dados

A etapa **[!UICONTROL Review]** é exibida, permitindo revisar o novo fluxo do conjunto de dados de entrada do Analytics antes de ele ser criado. Os detalhes da conexão são agrupados por categorias, incluindo:

* **[!UICONTROL Connection]**: Mostra o tipo da conexão de origem e o conjunto de relatórios selecionado.
* **[!UICONTROL Assign dataset & map fields]**: Ao criar outros conectores de origem, esse contêiner mostra em qual conjunto de dados os dados de origem estão assimilando, incluindo o esquema ao qual o conjunto de dados adere. O esquema de saída e o conjunto de dados são configurados automaticamente para fluxos de conjunto de dados do Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Monitorar o fluxo do conjunto de dados

Depois que o fluxo do conjunto de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Na tela **[!UICONTROL Catalog]**, selecione **[!UICONTROL Dataset flows]** para visualizar uma lista de fluxos estabelecidos associados à sua conta do Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

A tela **Fluxo do conjunto de dados** é exibida. Nesta página há um par de fluxos de conjunto de dados, incluindo informações sobre seu nome, dados de origem, tempo de criação e status.

O conector instancia dois fluxos de conjunto de dados. Um fluxo representa dados de preenchimento retroativo e o outro é dados em tempo real. Os dados de preenchimento retroativo não são configurados para Perfil, mas são enviados para o lago de dados para casos de uso analíticos e da ciência de dados.

Para obter mais informações sobre preenchimento retroativo, dados em tempo real e suas respectivas latências, consulte a [Visão geral do Conector de dados do Analytics](../../../../connectors/adobe-applications/analytics.md).

Selecione o fluxo do conjunto de dados que deseja visualizar na lista.

![](../../../../images/tutorials/create/analytics/backfill.png)

A página **Atividade do conjunto de dados** é exibida. Essa página exibe a taxa de mensagens que estão sendo consumidas no formato de um gráfico. Selecione *Data governance* no cabeçalho superior para acessar os campos de rotulagem.

![](../../../../images/tutorials/create/analytics/batches.png)

Você pode visualizar os rótulos herdados de um fluxo de conjunto de dados da tela *Data governance*. Para acessar rótulos específicos, selecione o botão de edição na parte superior direita.

![](../../../../images/tutorials/create/analytics/data-gov.png)

O painel **Editar rótulos de governança** é exibido. Essa tela permite que você acesse e edite o contrato, a identidade e os rótulos confidenciais de um fluxo de conjunto de dados.

Para obter mais informações sobre como rotular dados provenientes do Analytics, visite o [guia de rótulos de uso de dados](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## Próximas etapas e recursos adicionais

Depois que a conexão é criada, um esquema de destino e um fluxo de conjunto de dados são criados automaticamente para conter os dados recebidos. Além disso, ocorre o preenchimento retroativo de dados e a assimilação de até 13 meses de dados históricos. Quando a assimilação inicial for concluída, os dados do Analytics e serão usados pelos serviços de downstream da plataforma, como o Perfil do cliente em tempo real e o Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do serviço de segmentação](../../../../../segmentation/home.md)
* [Visão geral do Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Visão geral do Serviço de query](../../../../../query-service/home.md)

O vídeo a seguir é destinado a respaldar a compreensão da assimilação de dados pelo uso do conector do Adobe Analytics Source:

>[!WARNING]
>
> A interface [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
