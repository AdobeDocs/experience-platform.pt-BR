---
keywords: Experience Platform;home;popular topics; delete dataflows
description: A área de trabalho de fontes oferece a capacidade de excluir fluxos de dados em lote e em fluxo contínuo existentes que contenham erros ou se tenham tornado obsoletos.
solution: Experience Platform
title: Excluir fluxos de dados
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 7cb5862112c80e386e697aa2bd503abe49f11a3f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---


# Excluir fluxos de dados na interface do usuário

A área de trabalho [!UICONTROL Fontes] permite que você exclua fluxos de dados em lote e fluxo contínuo existentes que contêm erros ou se tornaram obsoletos.

Este tutorial fornece etapas para excluir fluxos de dados usando a área de trabalho [!UICONTROL Fontes] .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
- [Caixas de proteção](../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Excluir fluxos de dados

Na interface do usuário [do](https://platform.adobe.com)Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar a área de trabalho [!UICONTROL Fontes] e, em seguida, selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior.

![catálogo](../../images/tutorials/delete/catalog.png)

A página **[!UICONTROL Fluxos de dados]** é exibida. Nesta página há uma lista de fluxos de dados visualizáveis, incluindo informações sobre o conjunto de dados do público alvo, a fonte, o nome da conta e a data de criação.

Selecione o ícone de filtro (ícone![de](../../images/tutorials/delete/filter.png)filtro) na parte superior esquerda para iniciar o painel de classificação.

![fluxo de dados](../../images/tutorials/delete/dataflows.png)

O painel de classificação fornece uma lista de todas as fontes. Você pode selecionar mais de uma fonte da lista para acessar uma seleção filtrada de fluxos de dados associados às fontes específicas que você selecionou.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de seus fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja excluir, selecione as elipses (`...`) ao lado do nome do fluxo de dados.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Um menu suspenso é exibido, fornecendo opções para editar a programação do seu fluxo de dados, desativar o fluxo de dados ou excluí-lo totalmente.

Selecione **[!UICONTROL Excluir]** para excluir o fluxo de dados.

![delete](../../images/tutorials/delete/delete.png)

Uma caixa de diálogo de confirmação final é exibida. Selecione **[!UICONTROL Excluir]** para concluir o processo.

![confirmar](../../images/tutorials/delete/confirm.png)

Após alguns instantes, uma caixa de confirmação será exibida na parte inferior da tela para confirmar uma exclusão bem-sucedida.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito a área de trabalho [!UICONTROL Fontes] para excluir um fluxo de dados existente.

Consulte o tutorial sobre como [excluir fluxos de dados usando a API](../../tutorials/api/delete-dataflows.md) de Serviço de Fluxo para obter etapas sobre como executar essas operações de forma programática usando chamadas de API.