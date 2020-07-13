---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Adobe Analytics na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# Criar um conector de origem do Adobe Analytics na interface do usuário

Este tutorial fornece etapas para a criação de um conector de origem do Adobe Analytics na interface do usuário, a fim de trazer os dados do consumidor para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Criar uma conexão de origem com o Adobe Analytics

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho de fontes. A tela *Catálogo* exibe as fontes disponíveis para criar conexões de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria de aplicativos *da* Adobe, selecione **[!UICONTROL Adobe Analytics]** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para visualização de contas existentes, selecione **[!UICONTROL Contas]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Selecionar dados

A etapa *Adobe Analytics* é exibida. Fluxos de conjunto de dados estabelecidos anteriormente para Analytics são listados nesta tela. Você pode criar um novo fluxo de conjunto de dados clicando em **[!UICONTROL Selecionar dados]**.

>[!NOTE]
>
>Várias conexões de entrada para uma fonte podem ser feitas para inserir dados diferentes.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Na lista dos conjuntos de relatórios disponíveis, selecione o que deseja trazer para o Platform e clique em **[!UICONTROL Avançar]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Nomear o fluxo do conjunto de dados

A etapa de detalhes *do fluxo do conjunto de* dados é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo do conjunto de dados. Selecione **[UICONTROL! Próximo]** quando terminar.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Revisar o fluxo do conjunto de dados

A etapa *Revisar* é exibida, permitindo que você reveja seu novo fluxo de conjunto de dados vinculado da Analytics antes de ele ser criado. Os detalhes da conexão são agrupados por categorias, incluindo:

* *Conexão*: Mostra o tipo da conexão de origem e o conjunto de relatórios selecionado.
* *Atribuir campos* do conjunto de dados e mapear: Ao criar outros conectores de origem, esse container mostra em qual conjunto de dados os dados de origem estão assimilando, incluindo o schema ao qual o conjunto de dados está aderindo. O schema de saída e o conjunto de dados são configurados automaticamente para fluxos de conjunto de dados Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Monitorar o fluxo do conjunto de dados

Depois que o fluxo do conjunto de dados for criado, você poderá monitorar os dados que estão sendo assimilados por ele. Na tela *Catálogo* , selecione Fluxos *de* conjunto de dados para visualização de uma lista de fluxos estabelecidos associados à sua conta Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

A tela Fluxos *do* Conjunto de Dados é exibida. Nesta página há um par de fluxos de conjunto de dados, incluindo informações sobre seu nome, dados de origem, tempo de criação e status.

O conector instancia dois fluxos de conjunto de dados. Um fluxo representa dados de preenchimento retroativo e o outro é para dados em tempo real. Os dados de preenchimento retroativo não estão configurados para o Perfil, mas são enviados para o lago de dados para casos de uso analíticos e de ciência de dados.

Para obter mais informações sobre preenchimento retroativo, dados ao vivo e suas respectivas latências, consulte a visão geral [do Conector de dados da](../../../../connectors/adobe-applications/analytics.md)Analytics.

Selecione o fluxo do conjunto de dados que deseja visualização na lista.

![](../../../../images/tutorials/create/analytics/backfill.png)

A página atividade *do Conjunto* de Dados é exibida. Esta página exibe a taxa de mensagens que estão sendo consumidas na forma de um gráfico. Selecione *Controle* de dados no cabeçalho superior para acessar os campos de rotulagem.

![](../../../../images/tutorials/create/analytics/batches.png)

Você pode visualização rótulos herdados de um fluxo de conjunto de dados da tela de controle *de* dados. Para acessar rótulos específicos, selecione o botão de edição na parte superior direita.

![](../../../../images/tutorials/create/analytics/data-gov.png)

O painel *Editar rótulos* de controle é exibido. Essa tela permite acessar e editar o contrato, a identidade e os rótulos confidenciais de um fluxo de conjunto de dados.

Para obter mais informações sobre como rotular dados provenientes da Analytics, visite o guia [de uso de](../../../../../data-governance/labels/user-guide.md)dados.

![](../../../../images/tutorials/create/analytics/labels.png)

## Próximos passos e recursos adicionais

Depois que a conexão é criada, um schema de público alvo e um fluxo de conjunto de dados são criados automaticamente para conter os dados recebidos. Além disso, ocorre o preenchimento retroativo de dados e a assimilação de até 13 meses de dados históricos. Quando a ingestão inicial for concluída, os dados da Analytics e serão usados pelos serviços Platform de downstream, como Perfil do cliente em tempo real e Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do Serviço de segmentação](../../../../../segmentation/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../../../../data-science-workspace/home.md)
* [Visão geral do Serviço de Query](../../../../../query-service/home.md)

O vídeo a seguir é destinado a oferecer suporte à sua compreensão da assimilação de dados usando o conector de origem Analytics da Adobe:

>[!WARNING]
>
> A [!DNL Platform] interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

