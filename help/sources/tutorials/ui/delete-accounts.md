---
keywords: Experience Platform;home;popular topics; delete accounts
description: Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para excluir contas da área de trabalho Fontes.
solution: Experience Platform
title: Excluir contas
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: e0168c58e3279f27d45d10b79c130935e46afd3d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Excluir contas

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para excluir contas da área de trabalho **[!UICONTROL Fontes]** .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Excluir contas usando a interface do usuário

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar contas e fluxos de dados. Cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Selecione **[!UICONTROL Contas]** para acessar a página **[!UICONTROL Contas]** .

![contas de catálogo](../../images/tutorials/delete-accounts/catalog.png)

Uma lista das contas existentes é exibida. Nesta página há uma lista de informações classificáveis para contas existentes, como origem, nome de usuário, fluxos de dados associados e data de criação. Selecione o ícone **de** funil na parte superior esquerda para classificar.

![lista de dados](../../images/tutorials/delete-accounts/accounts.png)

O painel de classificação é exibido no lado esquerdo da tela, contendo uma lista de fontes disponíveis. É possível selecionar mais de uma fonte usando a função de classificação.

Selecione a fonte que deseja acessar e localize a conta que deseja excluir da lista de contas na interface principal. No exemplo, a origem selecionada é **[!DNL Azure Blob Storage]** e o nome da conta é **[!UICONTROL blobTestConnector]**. Ao selecionar várias fontes no painel de classificação, suas contas criadas mais recentemente aparecem primeiro porque a lista é classificada por data criada.

Selecione a conta que pretende eliminar.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

O painel **[!UICONTROL Propriedades]** é exibido no lado direito da tela, contendo informações sobre a conta selecionada.

Selecione as elipses (`...`) ao lado do nome da conta que você deseja excluir. Um painel pop-up é exibido, fornecendo opções para **[!UICONTROL Adicionar dados]**, **[!UICONTROL Editar detalhes]** e **[!UICONTROL Excluir]**. Selecione **[!UICONTROL Excluir]** para excluir a conta.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Uma caixa de diálogo de confirmação final é exibida; selecione **[!UICONTROL Excluir]** para concluir o processo.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito a área de trabalho **[!UICONTROL Fontes]** para excluir contas existentes.

Para obter etapas sobre como executar essas operações de forma programática usando a [!DNL Flow Service] API, consulte o tutorial sobre como [excluir conexões usando a API de Serviço de Fluxo](../../tutorials/api/delete.md)