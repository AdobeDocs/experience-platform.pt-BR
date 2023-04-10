---
keywords: Experience Platform; home; tópicos populares; analytics, classificações
description: Saiba como criar um conector de origem do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.
solution: Experience Platform
title: Criar uma conexão de origem do Adobe Analytics para dados de classificações na interface do usuário
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 6%

---

# Criar uma conexão de origem do Adobe Analytics para dados de classificações na interface do usuário

Este tutorial fornece etapas para criar uma conexão de fonte de dados de classificações do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O Conector de dados de classificações do Analytics requer que os dados tenham sido migrados para o novo [!DNL Classifications] infraestrutura do Adobe Analytics antes do uso. Para confirmar o status de migração de seus dados, entre em contato com a equipe de conta do Adobe.

## Selecione suas classificações

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho de origens. O **[!UICONTROL Catálogo]** exibe as fontes disponíveis para criar conexões de entrada com o . Cada cartão de origem mostra uma opção para configurar uma nova conta ou adicionar dados a uma conta existente.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Aplicativos Adobe]** , selecione a **[!UICONTROL Adobe Analytics]** e selecione **[!UICONTROL Adicionar dados]** para começar a trabalhar com os dados de classificações do Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

O **[!UICONTROL Adicionar dados de origem do Analytics]** será exibida. Selecionar **[!UICONTROL Classificações]** no cabeçalho superior para ver uma lista de [!DNL Classifications] conjuntos de dados, incluindo informações sobre a ID da dimensão, o nome do conjunto de relatórios e a ID do conjunto de relatórios.

Cada página exibe até dez diferentes [!DNL Classifications] conjuntos de dados que você pode escolher. Selecionar **[!UICONTROL Próximo]** na parte inferior da página para procurar mais opções. O painel à direita mostra o número total de [!DNL Classifications] conjuntos de dados selecionados, bem como seus nomes. Esse painel também permite remover qualquer [!DNL Classifications] conjuntos de dados que você pode ter selecionado por engano ou apagar todas as seleções com uma ação.

Você pode selecionar até 30 diferentes [!DNL Classifications] conjuntos de dados a serem trazidos para o [!DNL Platform].

Depois de selecionar o [!DNL Classifications] conjuntos de dados, selecione **[!UICONTROL Próximo]** na parte superior direita da página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revisar suas classificações

O **[!UICONTROL Revisão]** será exibida, permitindo que você revise a etapa selecionada [!DNL Classifications] conjuntos de dados antes de ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Tipo de dados]**: Mostra o número de [!DNL Classifications].
* **[!UICONTROL Agendamento]**: Mostra a frequência de sincronização para [!DNL Classifications] dados.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorar o fluxo de dados de classificações

Depois que o fluxo de dados for criado, é possível monitorar os dados que estão sendo assimilados por meio dele. No **[!UICONTROL Catálogo]** , selecione **[!UICONTROL Fluxos de dados]** para visualizar uma lista de fluxos estabelecidos associados a [!DNL Classifications] conta.

![](../../../../images/tutorials/create/classifications/dataflows.png)

O **[!UICONTROL Fluxos de dados]** será exibida. Nesta página há uma lista de fluxos de dados, incluindo informações sobre seu nome, dados de origem e status de execução do fluxo de dados. À direita, está o **[!UICONTROL Propriedades]** painel que contém metadados relacionados ao seu [!DNL Classifications] fluxo de dados.

Selecione o **[!UICONTROL Conjunto de dados do Target]** você deseja acessar o .

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

O **[!UICONTROL Atividade do conjunto de dados]** exibe informações sobre o conjunto de dados de destino selecionado, incluindo detalhes sobre o status do lote, a ID do conjunto de dados e o esquema.

>[!IMPORTANT]
>
>Embora a exclusão de conjuntos de dados seja possível para outros conectores de origem, no momento não há suporte para o Conector de dados de classificações do Analytics. Se você excluir um conjunto de dados por engano, entre em contato com o Atendimento ao cliente da Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Próximas etapas

Ao seguir este tutorial, você criou um conector de dados de classificações do Analytics que traz [!DNL Classifications] dados em [!DNL Platform]. Consulte os seguintes documentos para obter mais informações sobre [!DNL Analytics] e [!DNL Classifications] dados:

* [Visão geral do Data Connector do Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Criar uma conexão de dados do Analytics na interface do usuário](./analytics.md)
* [Sobre as classificações](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=pt-BR)
