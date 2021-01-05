---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;object;field;
solution: Experience Platform
title: Definir um campo de objeto na interface do usuário
description: Saiba como definir um campo de tipo de objeto na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Definir um campo de objeto na interface do usuário

A Adobe Experience Platform permite que você personalize completamente a estrutura de suas classes personalizadas do Experience Data Model (XDM), combinações e tipos de dados. Para organizar e aninhar campos relacionados em recursos XDM personalizados, é possível definir campos de tipo de objeto que podem conter subcampos adicionais.

Quando [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, use a lista suspensa **[!UICONTROL Tipo]** e selecione &quot;[!UICONTROL Objeto]&quot; na lista.

![](../../images/ui/fields/special/object.png)

Selecione **[!UICONTROL Aplicar]** para adicionar o objeto ao schema. A tela é atualizada para mostrar o novo campo com o tipo de dados [!UICONTROL Object] aplicado, incluindo controles para editar e adicionar subcampos ao objeto.

![](../../images/ui/fields/special/object-applied.png)

Para adicionar um subcampo, selecione o ícone **mais (+)** ao lado do campo de objeto na tela de desenho. Um novo campo é exibido abaixo do objeto, com controles para configurar o subcampo no painel direito.

![](../../images/ui/fields/special/object-add-field.png)

Depois de configurar o subcampo e selecionar **[!UICONTROL Aplicar]**, você pode continuar a adicionar campos ao objeto usando o mesmo processo. Também é possível adicionar subcampos que são objetos, permitindo aninhar os campos tão profundamente quanto desejar.

![](../../images/ui/fields/special/object-nested.png)

Após terminar de construir o objeto, talvez você descubra que deseja reutilizar sua estrutura em diferentes classes e misturas. Nesse caso, é possível optar por converter o objeto em um tipo de dados. Consulte a seção sobre [conversão de objetos em tipos de dados](../resources/data-types.md#convert) no guia da interface do usuário de tipos de dados para obter mais informações.

## Próximas etapas

Este guia aborda como definir um campo de objeto na interface do usuário. Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].
