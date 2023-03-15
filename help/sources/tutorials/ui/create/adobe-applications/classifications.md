---
keywords: Experience Platform;página inicial;tópicos populares; análises;classificações
description: Saiba como criar um conector de origem do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.
solution: Experience Platform
title: Criar uma conexão de origem do Adobe Analytics para dados de classificações na interface
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 6%

---

# Criar uma conexão de origem do Adobe Analytics para dados de classificações na interface

Este tutorial fornece etapas para a criação de uma conexão da fonte de dados de classificações do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O Conector de dados de classificações do Analytics requer que seus dados tenham sido migrados para a nova [!DNL Classifications] infraestrutura da Adobe Analytics antes do uso. Para confirmar o status de migração de seus dados, entre em contato com o Gerente de sucesso do cliente do Adobe.

## Selecione suas classificações

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação à esquerda para acessar o espaço de trabalho de origens. A variável **[!UICONTROL Catálogo]** exibe as fontes disponíveis com as quais criar conexões de entrada. Cada cartão de origem mostra uma opção para configurar uma nova conta ou adicionar dados a uma conta existente.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL aplicativos Adobe]** , selecione a **[!UICONTROL Adobe Analytics]** e selecione **[!UICONTROL Adicionar dados]** para começar a trabalhar com Dados de classificações do Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

A variável **[!UICONTROL Adicionar dados da fonte do Analytics]** é exibida. Selecionar **[!UICONTROL Classificações]** no cabeçalho superior para ver uma lista de [!DNL Classifications] conjuntos de dados, incluindo informações sobre sua ID de dimensão, nome do conjunto de relatórios e ID do conjunto de relatórios.

Cada página exibe até dez páginas diferentes [!DNL Classifications] conjuntos de dados que você pode escolher. Selecionar **[!UICONTROL Próxima]** na parte inferior da página para procurar mais opções. O painel à direita mostra o número total de [!DNL Classifications] conjuntos de dados selecionados, bem como seus nomes. Esse painel também permite remover qualquer [!DNL Classifications] conjuntos de dados que você pode ter selecionado por engano ou desmarque todas as seleções com uma ação.

É possível selecionar até 30 opções diferentes [!DNL Classifications] conjuntos de dados para trazer para o [!DNL Platform].

Depois de selecionar o [!DNL Classifications] conjuntos de dados, selecione **[!UICONTROL Próxima]** na parte superior direita da página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revise suas classificações

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise o conteúdo selecionado [!DNL Classifications] conjuntos de dados antes de serem criados. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Tipo de dados]**: mostra o número de selecionados [!DNL Classifications].
* **[!UICONTROL Agendamento]**: mostra a frequência de sincronização de [!DNL Classifications] dados.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorar o fluxo de dados de classificações

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. No **[!UICONTROL Catálogo]** , selecione **[!UICONTROL Fluxos de dados]** para exibir uma lista de fluxos estabelecidos associados ao seu [!DNL Classifications] conta.

![](../../../../images/tutorials/create/classifications/dataflows.png)

A variável **[!UICONTROL Fluxos de dados]** é exibida. Nesta página, há uma lista de fluxos de dados, incluindo informações sobre seu nome, dados de origem e status de execução do fluxo de dados. À direita, está o **[!UICONTROL Propriedades]** painel que contém metadados relacionados à [!DNL Classifications] fluxo de dados.

Selecione o **[!UICONTROL Conjunto de dados de destino]** que deseja acessar.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

A variável **[!UICONTROL Atividade do conjunto de dados]** A página exibe informações sobre o conjunto de dados de destino selecionado, incluindo detalhes sobre o status do lote, a ID do conjunto de dados e o esquema.

>[!IMPORTANT]
>
>Embora a exclusão de conjuntos de dados seja possível para outros conectores de origem, no momento não há suporte para o Conector de dados de classificações do Analytics. Se você excluir um conjunto de dados por engano, entre em contato com o Atendimento ao cliente da Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Próximas etapas

Seguindo este tutorial, você criou um Conector de dados de classificações do Analytics que traz [!DNL Classifications] entrada de dados [!DNL Platform]. Consulte os seguintes documentos para obter mais informações sobre [!DNL Analytics] e [!DNL Classifications] dados:

* [Visão geral do conector de dados do Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Criar uma conexão de dados do Analytics na interface](./analytics.md)
* [Sobre as classificações](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=pt-BR)
