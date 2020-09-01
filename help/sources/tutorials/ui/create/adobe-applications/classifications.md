---
keywords: Experience Platform;home;popular topics; analytics;classifications
description: Este tutorial fornece etapas para a criação de um conector de dados de classificações da Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.
solution: Experience Platform
title: Criar um conector de dados de classificações da Adobe Analytics na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 0da686743e8bc57d310f7eff6f1bf812a8f31238
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---


# Criar um conector de dados de classificações da Adobe Analytics na interface do usuário

Este tutorial fornece etapas para a criação de um conector de dados de classificações da Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Selecione suas classificações

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho de fontes. A tela **[!UICONTROL Catálogo]** exibe as fontes disponíveis para criar conexões de entrada. Cada cartão de origem mostra uma opção para configurar uma nova conta ou adicionar dados a uma conta existente.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria de aplicativos **[!UICONTROL do]** Adobe, selecione o cartão **[!UICONTROL Adobe Analytics]** e, em seguida, selecione **[!UICONTROL Adicionar dados]** ao start que trabalha com dados de classificações do Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

A etapa de adição de dados **[!UICONTROL de origem do]** Analytics é exibida. Selecione **[!UICONTROL Classificações]** no cabeçalho superior para ver uma lista de [!DNL Classifications] conjuntos de dados, incluindo informações sobre a ID **[!UICONTROL de]** Dimension, o nome **[!UICONTROL do Conjunto de]** relatórios e a ID **[!UICONTROL do Conjunto de]** relatórios.

Cada página exibe até dez [!DNL Classifications] conjuntos de dados diferentes dos quais você pode escolher. Selecione **[!UICONTROL Próximo]** na parte inferior da página para procurar mais opções. O painel à direita mostra o número total de [!DNL Classifications] conjuntos de dados selecionados, bem como seus nomes. Esse painel também permite remover quaisquer [!DNL Classifications] conjuntos de dados selecionados por engano ou apagar todas as seleções com uma única ação.

Você pode selecionar até 30 [!DNL Classifications] conjuntos de dados diferentes para serem incluídos [!DNL Platform].

Depois de selecionar seus [!DNL Classifications] conjuntos de dados, selecione **[!UICONTROL Avançar]** na parte superior direita da página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revisar suas classificações

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você revise seus [!DNL Classifications] conjuntos de dados selecionados antes de criá-los. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Tipo]** de dados: Mostra o número de selecionados [!DNL Classifications].
* **[!UICONTROL Agendamento]**: Mostra a frequência de sincronização dos [!DNL Classifications] dados.

Depois de revisar seu fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitore seu fluxo de dados de classificações

Depois que o seu fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Na tela **[!UICONTROL Catálogo]** , selecione **[!UICONTROL Fluxos de dados]** para visualização de uma lista de fluxos estabelecidos associados à sua [!DNL Classifications] conta.

![](../../../../images/tutorials/create/classifications/dataflows.png)

A tela **[!UICONTROL Dataflows]** é exibida. Nesta página há uma lista de fluxos de dados, incluindo informações sobre o nome, os dados de origem e o status de execução do fluxo de dados. À direita, está o painel **[!UICONTROL Propriedades]** que contém metadados referentes ao [!DNL Classifications] fluxo de dados.

Selecione o conjunto de dados **[!UICONTROL de]** Públicos alvos que deseja acessar.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

A página atividade **** do conjunto de dados exibe informações sobre o conjunto de dados do público alvo selecionado, incluindo detalhes sobre o status do lote, a ID do conjunto de dados e o schema.

>[!IMPORTANT]
>
>Embora a exclusão de conjuntos de dados seja possível para outros conectores de origem, no momento não é compatível com o conector de dados de classificações do Analytics. Se você excluir um conjunto de dados por engano, entre em contato com o Atendimento ao cliente da Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Próximas etapas

Ao seguir este tutorial, você criou um conector de Dados de classificações do Analytics que traz [!DNL Classifications] dados para [!DNL Platform]. Consulte os seguintes documentos para obter mais informações sobre [!DNL Analytics] e [!DNL Classifications] dados:

* [Visão geral do Conector de dados do Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Criar um conector de dados do Analytics na interface do usuário](./analytics.md)
* [Sobre as classificações](https://docs.adobe.com/content/help/pt-BR/analytics/components/classifications/c-classifications.html#)