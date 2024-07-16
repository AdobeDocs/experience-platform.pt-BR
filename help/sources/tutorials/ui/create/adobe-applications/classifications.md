---
keywords: Experience Platform;página inicial;tópicos populares; análises;classificações
description: Saiba como criar um conector de origem do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.
solution: Experience Platform
title: Criar uma conexão do Adobe Analytics Source para dados de classificações na interface
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# Criar uma conexão de origem do Adobe Analytics para dados de classificações na interface

Este tutorial fornece etapas para a criação de uma conexão da fonte de dados de classificações do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O Conector de dados de classificações do Analytics requer que seus dados tenham sido migrados para a nova infraestrutura do [!DNL Classifications] do Adobe Analytics antes de serem usados. Para confirmar o status de migração dos dados, entre em contato com a equipe de conta do Adobe.

## Selecione suas classificações

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho de fontes. A tela **[!UICONTROL Catálogo]** exibe as fontes disponíveis para criar conexões de entrada. Cada cartão de origem mostra uma opção para configurar uma nova conta ou adicionar dados a uma conta existente.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL aplicativos de Adobe]**, selecione o cartão **[!UICONTROL Adobe Analytics]** e selecione **[!UICONTROL Adicionar dados]** para começar a trabalhar com os Dados de classificações do Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

A etapa **[!UICONTROL Adicionar dados]** da origem do Analytics é exibida. Selecione **[!UICONTROL Classificações]** no cabeçalho superior para ver uma lista de [!DNL Classifications] conjuntos de dados, incluindo informações sobre sua ID de dimensão, nome do conjunto de relatórios e ID do conjunto de relatórios.

Cada página mostra até dez conjuntos de dados [!DNL Classifications] diferentes entre os quais você pode escolher. Selecione **[!UICONTROL Avançar]** na parte inferior da página para procurar mais opções. O painel à direita mostra o número total de [!DNL Classifications] conjuntos de dados selecionados, bem como seus nomes. Esse painel também permite remover qualquer conjunto de dados do [!DNL Classifications] que você tenha selecionado por engano ou limpar todas as seleções com uma ação.

Você pode selecionar até 30 conjuntos de dados [!DNL Classifications] diferentes para serem trazidos para [!DNL Platform].

Depois de selecionar seus conjuntos de dados do [!DNL Classifications], selecione **[!UICONTROL Avançar]** na parte superior direita da página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revise suas classificações

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise os conjuntos de dados [!DNL Classifications] selecionados antes de criá-los. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Tipo de dados]**: mostra o número de [!DNL Classifications] selecionados.
* **[!UICONTROL Agendamento]**: mostra a frequência de sincronização dos dados [!DNL Classifications].

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorar o fluxo de dados de classificações

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Na tela **[!UICONTROL Catálogo]**, selecione **[!UICONTROL Fluxos de Dados]** para exibir uma lista de fluxos estabelecidos associados à sua conta do [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

A tela **[!UICONTROL Fluxos de Dados]** é exibida. Nesta página, há uma lista de fluxos de dados, incluindo informações sobre seu nome, dados de origem e status de execução do fluxo de dados. À direita está o painel **[!UICONTROL Propriedades]**, que contém metadados relacionados ao fluxo de dados [!DNL Classifications].

Selecione o **[!UICONTROL Conjunto de dados de destino]** que você deseja acessar.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

A página **[!UICONTROL Atividade do conjunto de dados]** exibe informações sobre o conjunto de dados de destino selecionado, incluindo detalhes sobre o status do lote, a ID do conjunto de dados e o esquema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Próximas etapas

Seguindo este tutorial, você criou um Conector de dados de classificações do Analytics que traz dados do [!DNL Classifications] para o [!DNL Platform]. Consulte os seguintes documentos para obter mais informações sobre dados de [!DNL Analytics] e [!DNL Classifications]:

* [Visão geral do conector de dados do Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Criar uma conexão de dados do Analytics na interface](./analytics.md)
* [Sobre as classificações](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
