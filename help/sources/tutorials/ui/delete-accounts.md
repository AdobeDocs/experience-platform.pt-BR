---
keywords: Experience Platform;página inicial;tópicos populares; excluir contas
description: Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para excluir contas do espaço de trabalho de Fontes.
solution: Experience Platform
title: Excluir contas do Source Connection na interface
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Excluir contas de conexão de origem

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para excluir contas do espaço de trabalho **[!UICONTROL Fontes]**.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Tutorial do Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Excluir contas usando a interface

>[!TIP]
>
>Antes de excluir a conta de origem, primeiro você deve excluir todos os fluxos de dados existentes associados à conta de origem. Para excluir fluxos de dados existentes, consulte o tutorial em [exclusão de fluxos de dados de fontes na interface](./delete.md).

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar contas e fluxos de dados. Cada origem mostra o número de contas e fluxos de dados existentes associados a elas.

Selecione **[!UICONTROL Contas]** para acessar a página **[!UICONTROL Contas]**.

![contas-catálogo](../../images/tutorials/delete-accounts/catalog.png)

Uma lista de contas existentes é exibida. Nesta página há uma lista de informações classificáveis para contas existentes, como origem, nome de usuário, fluxos de dados associados e data de criação. Selecione o **ícone de funil** na parte superior esquerda para classificar.

![lista de fluxos de dados](../../images/tutorials/delete-accounts/accounts.png)

O painel de classificação é exibido no lado esquerdo da tela, contendo uma lista de fontes disponíveis. É possível selecionar mais de uma origem usando a função de classificação.

Selecione a fonte que deseja acessar e localize a conta que deseja excluir da lista de contas na interface principal. No exemplo, a origem selecionada é **[!DNL Azure Blob Storage]** e o nome da conta é **[!UICONTROL blobTestConnector]**. Ao selecionar várias fontes no painel de classificação, as contas criadas mais recentemente aparecem primeiro, pois a lista é classificada pela data de criação.

Selecione a conta que deseja excluir.

![classificação de fluxos de dados](../../images/tutorials/delete-accounts/sort.png)

O painel **[!UICONTROL Propriedades]** é exibido no lado direito da tela, contendo informações sobre a conta selecionada.

Selecione as reticências (`...`) ao lado do nome da conta que você deseja excluir. Um painel pop-up é exibido, fornecendo opções para **[!UICONTROL Adicionar dados]**, **[!UICONTROL Editar detalhes]** e **[!UICONTROL Excluir]**. Selecione **[!UICONTROL Excluir]** para excluir a conta.

![classificação de fluxos de dados](../../images/tutorials/delete-accounts/delete.png)

Uma caixa de diálogo de confirmação final é exibida, selecione **[!UICONTROL Excluir]** para concluir o processo.

![excluir](../../images/tutorials/delete-accounts/confirm.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho **[!UICONTROL Fontes]** para excluir contas existentes.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Flow Service], consulte o tutorial em [exclusão de conexões usando a API de Serviço de Fluxo](../../tutorials/api/delete.md)
