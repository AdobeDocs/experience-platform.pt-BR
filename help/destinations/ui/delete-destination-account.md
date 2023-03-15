---
keywords: excluir conta de destino, contas de destino, como excluir contas
title: Excluir contas de destino
type: Tutorial
description: Este tutorial lista as etapas para excluir contas de destino na interface do usuário do Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 2ea56957e122140fbc68c727e36666f8f9a71dd8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Excluir contas de destino

## Visão geral {#overview}

A variável **[!UICONTROL Contas]** A guia mostra detalhes sobre as conexões estabelecidas com vários destinos. Consulte a [Visão geral das contas](../ui/destinations-workspace.md#accounts) para obter todas as informações que você pode obter em cada conta de destino.

Este tutorial aborda as etapas para excluir contas de destino que não são mais necessárias usando a interface do usuário do Experience Platform.

![Guia Contas](../assets/ui/update-accounts/destination-accounts.png)

## Excluir contas {#delete}

>[!TIP]
>
>Antes de excluir a conta de destino, primeiro você deve excluir todos os fluxos de dados existentes associados à conta de destino. Para excluir fluxos de dados de destino existentes, consulte o tutorial em [exclusão de fluxos de dados de destino na interface do](./delete-destinations.md).

Siga as etapas abaixo para excluir contas de destino existentes.

1. Faça logon no [IU DO EXPERIENCE PLATFORM](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecionar **[!UICONTROL Contas]** no cabeçalho superior para exibir as contas existentes.

   ![Guia Contas](../assets/ui/delete-accounts/accounts-tab.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../assets/ui/update-accounts/filter.png) na parte superior esquerda para iniciar o painel classificar. O painel de classificação fornece uma lista de todos os seus destinos. É possível selecionar mais de um destino na lista para ver uma seleção filtrada de contas associadas aos destinos selecionados.

   ![Filtrar destinos](../assets/ui/delete-accounts/filter-accounts.png)

3. Selecione as reticências (`...`) ao lado do nome da conta que deseja excluir. Um painel pop-up é exibido, fornecendo opções para **[!UICONTROL Ativar segmentos]**, **[!UICONTROL Editar detalhes]**, e **[!UICONTROL Excluir]** a conta. Selecione o ![Botão Excluir](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Excluir]** botão para excluir a conta desejada.

   ![Excluir conta de destino](../assets/ui/delete-accounts/delete-accounts.png)

4. Uma caixa de diálogo de confirmação final é exibida, selecione **[!UICONTROL Excluir]** para concluir o processo.

![Confirmar exclusão da conta](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho de destinos para excluir contas existentes.

Para obter etapas sobre como executar essas operações de forma programática usando o [!DNL Flow Service] , consulte o tutorial em [exclusão de conexões usando a API de serviço de fluxo](../api/delete-destination-account.md)
