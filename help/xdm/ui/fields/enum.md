---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;enum;campo;
solution: Experience Platform
title: Definir um campo enum na interface do usuário
description: Saiba como definir um campo enum na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Definir um campo enum na interface do usuário

No Experience Data Model (XDM), um campo enum representa um campo que está restrito a uma lista predefinida de valores aceitáveis.

Quando [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, você pode defini-lo como um campo enum selecionando a caixa de seleção **[!UICONTROL Enum]** no painel direito.

![](../../images/ui/fields/special/enum.png)

Os controles adicionais são exibidos depois de marcar a caixa de seleção, permitindo que você especifique as restrições de valor para a enumeração. Na coluna **[!UICONTROL Valor]**, você deve fornecer o valor exato ao qual deseja restringir o campo. Esse valor deve estar em conformidade com [!UICONTROL Type] selecionado para o campo enum. Opcionalmente, você pode fornecer um **[!UICONTROL Label]** amigável para humanos também para a restrição.

Para adicionar restrições adicionais à enumeração, selecione **[!UICONTROL Adicionar linha]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continue a adicionar as restrições desejadas e os rótulos opcionais à enumeração. Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao schema.

![](../../images/ui/fields/special/enum-configured.png)

A tela é atualizada para refletir as alterações. Ao explorar esse schema no futuro, você pode visualização e editar as restrições para o campo enum no painel direito.

![](../../images/ui/fields/special/enum-applied.png)

## Próximas etapas

Este guia abordou como definir um campo enum na interface do usuário. Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].