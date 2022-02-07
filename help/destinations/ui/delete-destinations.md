---
keywords: excluir destinos, como excluir destinos, excluir destino
title: Excluir destinos
type: Tutorial
description: Este tutorial lista as etapas para excluir um destino existente na interface do usuário do Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Excluir destinos {#delete-destinations}

## Visão geral {#overview}

Na interface do usuário do Adobe Experience Platform, é possível excluir conexões existentes para destinos.

A exclusão de um destino remove todos os fluxos de dados existentes para esse destino. Todos os segmentos ativados para os destinos excluídos são não mapeados antes da exclusão do fluxo de dados.

Há duas maneiras de excluir destinos do [!DNL Platform] [!DNL UI]. É possível:

* [Exclua destinos do [!UICONTROL Procurar] guia](#delete-browse-tab)
* [Excluir destinos da página de detalhes do destino](#delete-destination-details-page)

## Excluir destinos na guia Procurar{#delete-browse-tab}

Siga as etapas abaixo para excluir um destino do [!UICONTROL Procurar] guia .

1. Faça logon no [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Para exibir seus destinos existentes, selecione **[!UICONTROL Procurar]** no cabeçalho superior.

   ![Procurar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone Filtro](../assets/ui/delete-destinations/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecione o ![Botão Mais](../assets/ui/delete-destinations/more-icon.png) na coluna Nome e selecione ![Botão Excluir](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Excluir]** para remover uma conexão de destino existente.
   ![Excluir destinos](../assets/ui/delete-destinations/delete-destinations.png)

4. Selecionar **[!UICONTROL Excluir]** para confirmar a remoção da conexão de destino.

   ![Confirmar exclusão de destino](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Excluir destinos da página de detalhes do destino{#delete-destination-details-page}

Siga as etapas abaixo para excluir um destino da página de detalhes do destino.

1. Faça logon no [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Para exibir seus destinos existentes, selecione **[!UICONTROL Procurar]** no cabeçalho superior.

   ![Procurar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone Filtro](../assets/ui/delete-destinations/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecione o nome do destino que deseja excluir.

   ![Selecionar destino](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se o destino tiver fluxos de dados existentes, você será direcionado para o [!UICONTROL Execuções do fluxo de dados] guia .

      ![Guia de execuções do fluxo de dados](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se o destino não tiver fluxos de dados existentes, você será direcionado para uma página vazia, onde poderá começar a ativar públicos-alvo.

      ![Detalhes do destino](../assets/ui/delete-destinations/destination-details-empty.png)

4. Selecionar **[!UICONTROL Excluir]** no painel direito.

   ![Excluir destino](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Selecionar **[!UICONTROL Excluir]** na caixa de diálogo de confirmação para remover o destino.

   ![Excluir confirmação de destino](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Dependendo da carga do servidor, pode levar alguns minutos para [!DNL Platform] para excluir o destino.
