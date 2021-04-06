---
keywords: excluir destinos; como excluir destinos
title: Excluir destinos
type: Tutorial
description: Este tutorial lista as etapas para excluir um destino existente na interface do usuário do Adobe Experience Platform
translation-type: tm+mt
source-git-commit: ebe2a35e66b78acf6a9ffa20664877913cd35648
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Excluir destinos {#delete-destinations}

## Visão geral {#overview}

Na interface do usuário do Adobe Experience Platform, é possível excluir conexões existentes para destinos.

A exclusão de um destino remove todos os fluxos de dados existentes para esse destino. Todos os segmentos ativados para os destinos excluídos são não mapeados antes da exclusão do fluxo de dados.

Há duas maneiras de excluir destinos do [!DNL Platform] [!DNL UI]. É possível:

* [Excluir destinos na  [!UICONTROL Browse] guia](#delete-browse-tab)
* [Excluir destinos da página de detalhes do destino](#delete-destination-details-page)

## Excluir destinos da guia Procurar{#delete-browse-tab}

Siga as etapas abaixo para excluir um destino da guia [!UICONTROL Browse].

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinations]** na barra de navegação esquerda. Para exibir seus destinos existentes, selecione **[!UICONTROL Browse]** no cabeçalho superior.

   ![Procurar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecione o ícone de filtro ![Filter-icon](../assets/ui/delete-destinations/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecione o botão ![Delete](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]** na coluna **[!UICONTROL Platform]** para remover um destino existente.
   ![Excluir destinos](../assets/ui/delete-destinations/delete-destinations.png)

4. Selecione **[!UICONTROL Delete]** para confirmar a remoção do destino.

   ![Confirmar exclusão de destino](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Excluir destinos da página de detalhes do destino{#delete-destination-details-page}

Siga as etapas abaixo para excluir um destino da página de detalhes do destino.

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinations]** na barra de navegação esquerda. Para exibir seus destinos existentes, selecione **[!UICONTROL Browse]** no cabeçalho superior.

   ![Procurar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecione o ícone de filtro ![Filter-icon](../assets/ui/delete-destinations/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecione o nome do destino que deseja excluir.

   ![Selecionar destino](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se o destino tiver fluxos de dados existentes, você será direcionado para a guia [!UICONTROL Dataflow runs].

      ![Guia de execuções do fluxo de dados](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se o destino não tiver fluxos de dados existentes, você será direcionado para uma página vazia, onde poderá começar a ativar públicos-alvo.

      ![Detalhes do destino](../assets/ui/delete-destinations/destination-details-empty.png)


4. Selecione **[!UICONTROL Delete]** no painel direito.

   ![Excluir destino](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Selecione **[!UICONTROL Delete]** na caixa de diálogo de confirmação para remover o destino.

   ![Excluir confirmação de destino](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Dependendo da carga do servidor, pode levar alguns minutos para [!DNL Platform] excluir o destino.