---
keywords: Experience Platform; home; tópicos populares; excluir contas
description: Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para excluir contas do espaço de trabalho Fontes .
solution: Experience Platform
title: Excluir contas de conexão de origem na interface do usuário
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 609f7a5de51840fe657ca72df99c90da56c8f466
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Excluir contas de conexão de origem

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para excluir contas do **[!UICONTROL Fontes]** espaço de trabalho.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Excluir contas usando a interface do usuário

>[!TIP]
>
>Antes de excluir a conta de origem, primeiro exclua qualquer fluxo de dados existente associado à conta de origem. Para excluir fluxos de dados existentes, consulte o tutorial em [exclusão de fluxos de dados de fontes na interface do usuário](./delete.md).

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar contas e fluxos de dados. Cada origem mostra o número de contas e fluxos de dados existentes associados a elas.

Selecionar **[!UICONTROL Contas]** para acessar o **[!UICONTROL Contas]** página.

![contas de catálogo](../../images/tutorials/delete-accounts/catalog.png)

Uma lista de contas existentes é exibida. Nesta página há uma lista de informações classificáveis para contas existentes, como origem, nome de usuário, fluxos de dados associados e data criada. Selecione o **ícone de funil** no canto superior esquerdo para classificar.

![lista de fluxos de dados](../../images/tutorials/delete-accounts/accounts.png)

O painel de classificação é exibido no lado esquerdo da tela, contendo uma lista de fontes disponíveis. Você pode selecionar mais de uma fonte usando a função de classificação .

Selecione a fonte que deseja acessar e localize a conta que deseja excluir da lista de contas na interface principal. No exemplo, a fonte selecionada é **[!DNL Azure Blob Storage]** e o nome da conta é **[!UICONTROL blobTestConnector]**. Ao selecionar várias fontes no painel de classificação, suas contas criadas mais recentemente aparecem primeiro porque a lista é classificada por data criada.

Selecione a conta que pretende eliminar.

![classificação de fluxos de dados](../../images/tutorials/delete-accounts/sort.png)

O **[!UICONTROL Propriedades]** é exibido no lado direito da tela, contendo informações sobre a conta selecionada.

Selecione as reticências (`...`) ao lado do nome da conta que você pretende excluir. Um painel pop-up é exibido, fornecendo opções para **[!UICONTROL Adicionar dados]**, **[!UICONTROL Editar detalhes]** e **[!UICONTROL Excluir]**. Selecionar **[!UICONTROL Excluir]** para excluir a conta.

![classificação de fluxos de dados](../../images/tutorials/delete-accounts/delete.png)

Uma caixa de diálogo de confirmação final é exibida, selecione **[!UICONTROL Excluir]** para concluir o processo.

![excluir](../../images/tutorials/delete-accounts/confirm.png)

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável **[!UICONTROL Fontes]** espaço de trabalho para excluir contas existentes.

Para obter etapas sobre como executar essas operações de forma programática usando o [!DNL Flow Service] Consulte o tutorial em [exclusão de conexões usando a API do Serviço de Fluxo](../../tutorials/api/delete.md)
