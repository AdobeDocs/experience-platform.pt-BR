---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;matriz;campo;
solution: Experience Platform
title: Definir campos de matriz na interface
description: Saiba como definir um campo de matriz na interface do usuário do Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definir campos de matriz na interface

Ao definir um campo Experience Data Model (XDM) na interface do usuário do Adobe Experience Platform, você pode designar esse campo como uma matriz.

O conteúdo da matriz depende do [!UICONTROL Tipo] selecionado para esse campo. Por exemplo, se o [!UICONTROL Type] de um campo estiver definido como &quot;[!UICONTROL String]&quot;, definir esse campo como uma matriz designará o campo como uma matriz de cadeias de caracteres. Se o [!UICONTROL Tipo] do campo estiver definido como um tipo de dados de vários campos, como &quot;[!UICONTROL Endereço postal]&quot;, ele se tornará uma matriz de objetos de endereço postal que estão em conformidade com o tipo de dados.

Depois que você tiver [definido um novo campo na interface](./overview.md#define), poderá defini-lo como um campo de matriz marcando a caixa de seleção **[!UICONTROL Matriz]** no painel direito.

![](../../images/ui/fields/special/array.png)

Depois que a caixa de seleção é marcada, controles adicionais são exibidos no painel direito, que permitem, opcionalmente, restringir ainda mais o storage. Se não quiser aplicar uma restrição específica, deixe o campo em branco.

Os controles de configuração adicionais para arrays são os seguintes:

| Propriedade do campo | Descrição |
| --- | --- |
| [!UICONTROL Comprimento mínimo] | O número mínimo de itens que a matriz deve conter para que a assimilação seja bem-sucedida. |
| [!UICONTROL Tamanho máximo] | O número máximo de itens que a matriz deve conter para que a assimilação seja bem-sucedida. |
| [!UICONTROL Somente itens exclusivos] | Se definido como &quot;[!UICONTROL True]&quot;, cada item na matriz deve ser exclusivo para que a assimilação seja bem-sucedida. |

{style="table-layout:auto"}

Quando terminar de configurar o campo, selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao esquema.

![](../../images/ui/fields/special/array-config.png)

A tela é atualizada para refletir as alterações feitas no campo. Observe que o tipo de dados exibido ao lado do nome do campo na tela é anexado com um par de colchetes (`[]`), indicando que o campo representa uma matriz desse tipo de dados.

![](../../images/ui/fields/special/array-applied.png)

## Próximas etapas

Este guia abordou como definir um campo de matriz na interface do usuário. Consulte a visão geral em [definindo campos na interface](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].
