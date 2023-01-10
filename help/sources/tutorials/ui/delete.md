---
keywords: Experience Platform; home; tópicos populares; excluir fluxos de dados
description: O espaço de trabalho de fontes oferece a capacidade de excluir fluxos de dados de lote e fluxo que contenham erros ou se tornaram obsoletos.
solution: Experience Platform
title: Excluir fluxos de dados na interface do usuário
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# Excluir fluxos de dados na interface do usuário

O [!UICONTROL Fontes] o workspace permite excluir fluxos de dados em lote e fluxo que contêm erros ou que se tornaram obsoletos.

Este tutorial fornece etapas para excluir fluxos de dados usando o [!UICONTROL Fontes] espaço de trabalho.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
- [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Excluir fluxos de dados

No [Interface do usuário do Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho e selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior.

![catálogo](../../images/tutorials/delete/catalog.png)

O **[!UICONTROL Fluxos de dados]** será exibida. Nesta página, há uma lista de fluxos de dados visualizáveis, incluindo informações sobre o conjunto de dados de destino, a fonte, o nome da conta e a data de criação.

Selecione o ícone de filtro (![ícone de filtro](../../images/tutorials/delete/filter.png)) na parte superior esquerda para iniciar o painel de classificação.

![fluxo de dados](../../images/tutorials/delete/dataflows.png)

O painel de classificação fornece uma lista de todas as fontes. Você pode selecionar mais de uma fonte na lista para acessar uma seleção filtrada de fluxos de dados associada às fontes específicas selecionadas.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de seus fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja excluir, selecione as reticências (`...`) ao lado do nome do fluxo de dados.

![filtro de fluxo de dados](../../images/tutorials/delete/dataflows-filter.png)

Um menu suspenso é exibido, fornecendo opções para editar a programação do fluxo de dados, desativar o fluxo de dados ou excluí-lo totalmente.

Selecionar **[!UICONTROL Excluir]** para excluir o fluxo de dados.

![excluir](../../images/tutorials/delete/delete.png)

Uma caixa de diálogo de confirmação final é exibida. Selecionar **[!UICONTROL Excluir]** para concluir o processo.

![confirmar](../../images/tutorials/delete/confirm.png)

Após alguns instantes, uma caixa de confirmação será exibida na parte inferior da tela para confirmar uma exclusão bem-sucedida.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável [!UICONTROL Fontes] espaço de trabalho para excluir um fluxo de dados existente.

Veja o tutorial em [exclusão de fluxos de dados usando a API do Serviço de Fluxo](../../tutorials/api/delete-dataflows.md) para obter etapas sobre como executar essas operações programaticamente usando chamadas de API.
