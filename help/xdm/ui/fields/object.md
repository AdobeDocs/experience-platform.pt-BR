---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;objeto;campo;
solution: Experience Platform
title: Definir campos de objeto na interface
description: Saiba como definir um campo do tipo objeto na interface do usuário do Experience Platform.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Definir campos de objeto na interface

O Adobe Experience Platform permite personalizar totalmente a estrutura de suas classes personalizadas do Experience Data Model (XDM), grupos de campos de esquema e tipos de dados. Para organizar e aninhar campos relacionados em recursos XDM personalizados, você pode definir campos do tipo de objeto que podem conter subcampos adicionais.

Quando [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, use o **[!UICONTROL Tipo]** selecione &quot;[!UICONTROL Objeto]&quot; na lista.

![](../../images/ui/fields/special/object.png)

Selecionar **[!UICONTROL Aplicar]** para adicionar o objeto ao esquema. A tela é atualizada para mostrar o novo campo com a tag [!UICONTROL Objeto] tipo de dados aplicado, incluindo controles para editar e adicionar subcampos ao objeto.

![](../../images/ui/fields/special/object-applied.png)

Para adicionar um subcampo, selecione a variável **mais (+)** ícone ao lado do campo de objeto na tela. Um novo campo é exibido abaixo do objeto, com controles para configurar o subcampo no painel direito.

![](../../images/ui/fields/special/object-add-field.png)

Depois de configurar o subcampo e selecionar **[!UICONTROL Aplicar]**, você pode continuar a adicionar campos ao objeto usando o mesmo processo. Também é possível adicionar subcampos que são objetos, permitindo aninhar campos o quanto desejar.

Depois de concluir a construção do objeto, você pode descobrir que deseja reutilizar sua estrutura em diferentes classes e grupos de campos. Nesse caso, você pode optar por converter o objeto em um tipo de dados. Consulte a seção sobre [conversão de objetos em tipos de dados](../resources/data-types.md#convert) no guia da interface de tipos de dados para obter mais informações.

## Próximas etapas

Este guia abordou como definir um campo de objeto na interface do usuário do. Consulte a visão geral em [definição de campos na interface](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
