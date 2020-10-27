---
keywords: Experience Platform;home;popular topics; delete dataflows
description: Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para excluir fluxos de dados da área de trabalho Fontes.
solution: Experience Platform
title: Excluir fluxos de dados
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: cbd9b3ed0cf43d582d734098b9ce58fc074fb375
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Excluir fluxos de dados

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para excluir fluxos de dados da área de trabalho **[!UICONTROL Fontes]** .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Excluir fluxos de dados usando a interface do usuário

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar contas e fluxos de dados. Cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Selecione **[!UICONTROL Fluxos de dados]** para acessar a página **[!UICONTROL Fluxos de dados]** .

![dataset-flow-atividade](../../images/tutorials/delete/dataflows.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página há uma lista de informações classificáveis para fluxos de dados existentes, como origem, nome de usuário, status de execução e data da última execução. Selecione o ícone **de** funil na parte superior esquerda para classificar.

![lista de dados](../../images/tutorials/delete/dataflows-list.png)

O painel de classificação é exibido no lado esquerdo da tela, contendo uma lista de fontes disponíveis.
É possível selecionar mais de uma fonte usando a função de classificação.

Selecione a fonte que deseja acessar e localize o fluxo de dados que deseja excluir da lista de fluxos de dados na interface principal. No exemplo, a fonte selecionada é **[!DNL Azure Blob Storage]** e o nome do fluxo de dados é o fluxo de dados de perfis **[!UICONTROL do cliente]**. Ao selecionar várias fontes do painel de classificação, seus fluxos de dados criados mais recentemente aparecem primeiro porque a lista é classificada por data criada.

Selecione o fluxo de dados que você deseja excluir.

![dataflows-sort](../../images/tutorials/delete/dataflows-sort.png)

O painel **[!UICONTROL Propriedades]** é exibido no lado direito da tela, contendo informações relacionadas ao fluxo de dados selecionado, bem como uma opção para **[!UICONTROL Editar agendamento]**.

Para excluir o fluxo de dados, selecione **[!UICONTROL Excluir]**.

![dataflows-sort](../../images/tutorials/delete/dataflows-properties.png)

Uma caixa de diálogo de confirmação final é exibida; selecione **[!UICONTROL Excluir]** para concluir o processo.

![delete](../../images/tutorials/delete/delete.png)

Após alguns instantes, uma caixa de confirmação verde é exibida na parte inferior da tela para confirmar a exclusão bem-sucedida.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito a área de trabalho **[!UICONTROL Fontes]** para excluir os fluxos de dados existentes.

Para obter etapas sobre como executar essas operações de forma programática usando a [!DNL Flow Service] API, consulte o tutorial sobre como [excluir conexões usando a API de Serviço de Fluxo](../../tutorials/api/delete.md)