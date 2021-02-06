---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;array;field;
solution: Experience Platform
title: Definir campos de matriz na interface do usuário
description: Saiba como definir um campo de matriz na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---


# Definir campos de matriz na interface do usuário

Ao definir um campo do Modelo de dados de experiência (XDM) na interface do usuário do Adobe Experience Platform, você pode designar esse campo como um storage.

O conteúdo da matriz depende do [!UICONTROL Tipo] selecionado para esse campo. Por exemplo, se [!UICONTROL Type] de um campo estiver definido como &quot;[!UICONTROL String]&quot;, definir esse campo como uma matriz designará o campo como uma matriz de strings. Se [!UICONTROL Type] do campo estiver definido como um tipo de dados de vários campos, como &quot;[!UICONTROL Endereço postal]&quot;, então ele se tornaria uma matriz de objetos de endereço postal que estão em conformidade com o tipo de dados.

Depois de [definir um novo campo na interface do usuário](./overview.md#define), você pode defini-lo como um campo de matriz selecionando a caixa de seleção **[!UICONTROL Array]** no painel direito.

![](../../images/ui/fields/special/array.png)

Depois que a caixa de seleção é selecionada, os controles adicionais são exibidos no painel direito, o que permite que você, opcionalmente, restrinja o storage ainda mais. Caso não deseje aplicar uma restrição específica, deixe o campo em branco.

Os controles de configuração adicionais para arrays são os seguintes:

| Propriedade de campo | Descrição |
| --- | --- |
| [!UICONTROL Comprimento mínimo] | O número mínimo de itens que a matriz deve conter para que a ingestão seja bem-sucedida. |
| [!UICONTROL Tamanho máximo] | O número máximo de itens que a matriz deve conter para que a ingestão seja bem-sucedida. |
| [!UICONTROL Somente itens únicos] | Se definido como &quot;[!UICONTROL True]&quot;, cada item na matriz deve ser exclusivo para que a ingestão seja bem-sucedida. |

Quando terminar de configurar o campo, selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao schema.

![](../../images/ui/fields/special/array-config.png)

A tela é atualizada para refletir as alterações feitas no campo. Observe que o tipo de dados exibido ao lado do nome do campo na tela é anexado com um par de colchetes (`[]`), indicando que o campo representa uma matriz desse tipo de dados.

![](../../images/ui/fields/special/array-applied.png)

## Próximas etapas

Este guia aborda como definir um campo de matriz na interface do usuário. Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].