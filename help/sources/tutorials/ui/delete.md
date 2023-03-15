---
keywords: Experience Platform;página inicial;tópicos populares; excluir fluxos de dados
description: O espaço de trabalho de origens fornece a capacidade de excluir fluxos de dados de batch e streaming existentes que contêm erros ou se tornaram obsoletos.
solution: Experience Platform
title: Excluir fluxos de dados na interface
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# Excluir fluxos de dados na interface do

A variável [!UICONTROL Origens] o workspace permite excluir lotes e fluxos de dados de streaming existentes que contêm erros ou se tornaram obsoletos.

Este tutorial fornece etapas para excluir fluxos de dados usando o [!UICONTROL Origens] espaço de trabalho.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Origens](../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
- [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Excluir fluxos de dados

No [IU DO EXPERIENCE PLATFORM](https://platform.adobe.com), selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] e selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior.

![catálogo](../../images/tutorials/delete/catalog.png)

A variável **[!UICONTROL Fluxos de dados]** é exibida. Nesta página, há uma lista de fluxos de dados visualizáveis, incluindo informações sobre seu conjunto de dados de destino, origem, nome da conta e data de criação.

Selecione o ícone de filtro (![filter-icon](../../images/tutorials/delete/filter.png)) na parte superior esquerda para iniciar o painel de classificação.

![fluxos de dados](../../images/tutorials/delete/dataflows.png)

O painel de classificação fornece uma lista de todas as fontes. Você pode selecionar mais de uma origem na lista para acessar uma seleção filtrada de fluxos de dados associados às origens específicas selecionadas.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja excluir, selecione as reticências (`...`) ao lado do nome do fluxo de dados.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Um menu suspenso é exibido, fornecendo opções para editar a programação do fluxo de dados, desativar o fluxo de dados ou excluí-lo totalmente.

Selecionar **[!UICONTROL Excluir]** para excluir o fluxo de dados.

![excluir](../../images/tutorials/delete/delete.png)

Uma caixa de diálogo de confirmação final é exibida. Selecionar **[!UICONTROL Excluir]** para concluir o processo.

![confirmar](../../images/tutorials/delete/confirm.png)

Após alguns minutos, uma caixa de confirmação é exibida na parte inferior da tela para confirmar uma exclusão bem-sucedida.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o [!UICONTROL Origens] espaço de trabalho para excluir um fluxo de dados existente.

Veja o tutorial sobre [exclusão de fluxos de dados usando a API de serviço de fluxo](../../tutorials/api/delete-dataflows.md) para obter etapas sobre como executar essas operações programaticamente usando chamadas de API.
