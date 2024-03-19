---
title: Definir campos de mapa na interface
description: Saiba como definir um campo de mapa na interface do usuário do Experience Platform.
source-git-commit: 8eea73c91d0671b1ddaeb8da0dc18b3e5e306f57
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Definir campos de mapa na interface

O Adobe Experience Platform permite personalizar totalmente a estrutura de suas classes personalizadas do Experience Data Model (XDM), grupos de campos de esquema e tipos de dados.

Você também pode definir campos de mapa no Editor de esquemas para modelar estruturas de dados flexíveis e dinâmicas ou armazenar uma coleção de pares de valores chave. A estrutura de dados do mapa permite pesquisas, inserções e exclusões rápidas e eficientes onde as informações são organizadas e acessadas com base em identificadores exclusivos.

Ao definir um novo campo na interface do usuário (UI) da Platform, use o **[!UICONTROL Tipo]** selecione &quot;**[!UICONTROL Mapa]**&quot; na lista.

![O Editor de esquemas com a lista suspensa Tipo e o valor Mapa realçados.](../../images/ui/fields/special/map.png)

A [!UICONTROL Mapear tipo de valor] é exibida. Este valor é necessário para [!UICONTROL Mapa] tipos de dados. Os valores disponíveis para o mapa são [!UICONTROL String] e [!UICONTROL Integer]. Selecione um valor na lista suspensa de opções disponíveis.

![O Editor de esquemas com o [!UICONTROL Mapear tipo de valor] lista suspensa realçada.](../../images/ui/fields/special/map-value-type.png)

Depois de configurar o subcampo, você deve atribuí-lo a um grupo de campos. Use o **[!UICONTROL Grupo de campos]** menu suspenso ou campo de pesquisa e selecione **[!UICONTROL Aplicar]**. Você pode continuar a adicionar campos ao objeto usando o mesmo processo ou selecionar **[!UICONTROL Salvar]** para confirmar as configurações.

![Uma gravação da seleção e das configurações do grupo de campos que estão sendo aplicadas.](../../images/ui/fields/special/assign-to-field-group.gif)

>[!NOTE]
>
>A interface do usuário da Platform tem limitações na forma como pode extrair as chaves de campos do tipo mapa. Enquanto os campos do tipo objeto podem ser expandidos, os mapas são exibidos como um único campo. Os campos de mapa criados por meio da API do Registro de esquema que não são do tipo string ou dados inteiros são exibidos como &quot;[!UICONTROL Complexo]&quot; tipos de dados.

## Próximas etapas

Depois de ler este documento, agora é possível definir campos de mapa na interface do usuário da Platform. Lembre-se de que você só pode usar classes e grupos de campos para adicionar campos a esquemas. Para saber mais sobre como gerenciar esses recursos na interface do usuário, consulte os guias sobre criação e edição [classes](../resources/classes.md) e [grupos de campos](../resources/field-groups.md).

Para obter mais informações sobre os recursos do [!UICONTROL Esquemas] espaço de trabalho, consulte a [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).
