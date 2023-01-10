---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, modelo de dados, ui, espaço de trabalho, matriz, campo;
solution: Experience Platform
title: Definir campos de matriz na interface do usuário
description: Saiba como definir um campo de matriz na interface do usuário do Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# Definir campos de matriz na interface do usuário

Ao definir um campo do Experience Data Model (XDM) na interface do usuário do Adobe Experience Platform, você pode designar esse campo como uma matriz.

O conteúdo da matriz depende do [!UICONTROL Tipo] selecionado para esse campo. Por exemplo, se um campo [!UICONTROL Tipo] está definida como &quot;[!UICONTROL String]&quot;, definir esse campo como um array designará o campo como uma matriz de strings. Se o campo [!UICONTROL Tipo] está definida como um tipo de dados de vários campos, como &quot;[!UICONTROL Endereço postal]&quot;, se tornaria uma matriz de objetos de endereço postal que estão em conformidade com o tipo de dados.

Depois de [definição de um novo campo na interface do usuário](./overview.md#define), você pode defini-lo como um campo de matriz selecionando o **[!UICONTROL Matriz]** caixa de seleção no painel direito.

![](../../images/ui/fields/special/array.png)

Depois que a caixa de seleção for selecionada, os controles adicionais aparecerão no painel direito, permitindo que você opcionalmente restrinja ainda mais o storage. Se não quiser impor uma restrição específica, deixe o campo em branco.

Os controles de configuração adicionais para arrays são os seguintes:

| Propriedade do campo | Descrição |
| --- | --- |
| [!UICONTROL Comprimento mínimo] | O número mínimo de itens que a matriz deve conter para que a assimilação seja bem-sucedida. |
| [!UICONTROL Tamanho máximo] | O número máximo de itens que a matriz deve conter para que a assimilação seja bem-sucedida. |
| [!UICONTROL Somente itens únicos] | Se definido como &quot;[!UICONTROL Verdadeiro]&quot;, cada item na matriz deve ser exclusivo para que a assimilação seja bem-sucedida. |

{style=&quot;table-layout:auto&quot;}

Depois de concluir a configuração do campo, selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao schema.

![](../../images/ui/fields/special/array-config.png)

A tela é atualizada para refletir as alterações feitas no campo. Observe que o tipo de dados exibido ao lado do nome do campo na tela é anexado com um par de colchetes (`[]`), indicando que o campo representa uma matriz desse tipo de dados.

![](../../images/ui/fields/special/array-applied.png)

## Próximas etapas

Este guia abordou como definir um campo de matriz na interface do usuário do . Consulte a visão geral em [definição de campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
