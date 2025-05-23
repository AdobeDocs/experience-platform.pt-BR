---
keywords: excluir destinos, como excluir destinos, excluir destinos
title: Excluir destinos
type: Tutorial
description: Este tutorial lista as etapas para excluir um destino existente na interface do usuário do Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Excluir destinos {#delete-destinations}

## Visão geral {#overview}

Na interface do usuário do Adobe Experience Platform, é possível excluir conexões existentes com destinos.

A exclusão de um destino remove todos os fluxos de dados existentes para esse destino. Todos os públicos ativados para os destinos excluídos são desmapeados antes da exclusão do fluxo de dados.

Há duas maneiras de excluir destinos de [!DNL Experience Platform] [!DNL UI]. É possível:

* [Excluir destinos da guia [!UICONTROL Procurar]](#delete-browse-tab)
* [Excluir destinos da página de detalhes do destino](#delete-destination-details-page)

## Excluir destinos da guia Procurar{#delete-browse-tab}

Siga as etapas abaixo para excluir um destino da guia [!UICONTROL Procurar].

1. Faça logon na [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Para exibir seus destinos existentes, selecione **[!UICONTROL Procurar]** no cabeçalho superior.

   ![Procurar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone de filtro](/help/images/icons/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecione o botão ![Mais botão](/help/images/icons/more.png) na coluna Nome e selecione ![Excluir botão](/help/images/icons/delete.png) **[!UICONTROL Excluir]** para remover uma conexão de destino existente.
   ![Excluir destinos](../assets/ui/delete-destinations/delete-destinations.png)

4. Selecione **[!UICONTROL Excluir]** para confirmar a remoção da conexão de destino.

   ![Confirmar exclusão do destino](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Excluir destinos da página de detalhes do destino{#delete-destination-details-page}

Siga as etapas abaixo para excluir um destino da página de detalhes do destino.

1. Faça logon na [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Para exibir seus destinos existentes, selecione **[!UICONTROL Procurar]** no cabeçalho superior.

   ![Procurar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone de filtro](/help/images/icons/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecione o nome do destino que deseja deletar.

   ![Selecionar destino](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se o destino tiver fluxos de dados existentes, você será direcionado para a guia [!UICONTROL Execuções de fluxo de dados].

     ![Guia Execuções de fluxo de dados](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se o destino não tiver fluxos de dados existentes, você será direcionado para uma página vazia onde poderá começar a ativar públicos.

     ![Detalhes do destino](../assets/ui/delete-destinations/destination-details-empty.png)

4. Selecione **[!UICONTROL Excluir]** no painel direito.

   ![Excluir destino](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Selecione **[!UICONTROL Excluir]** na caixa de diálogo de confirmação para remover o destino.

   ![Excluir confirmação de destino](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Dependendo da carga do servidor, pode levar alguns minutos para [!DNL Experience Platform] excluir o destino.
