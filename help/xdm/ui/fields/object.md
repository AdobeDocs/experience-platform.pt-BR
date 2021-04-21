---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; objeto; campo;
solution: Experience Platform
title: Definir campos de objeto na interface do usuário
description: Saiba como definir um campo do tipo objeto na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Definir campos de objeto na interface do usuário

O Adobe Experience Platform permite personalizar totalmente a estrutura de suas classes, combinações e tipos de dados personalizados do Experience Data Model (XDM). Para organizar e aninhar campos relacionados em recursos XDM personalizados, você pode definir campos do tipo objeto que podem conter subcampos adicionais.

Ao [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, use a lista suspensa **[!UICONTROL Type]** e selecione &quot;[!UICONTROL Object]&quot; na lista.

![](../../images/ui/fields/special/object.png)

Selecione **[!UICONTROL Apply]** para adicionar o objeto ao esquema. A tela é atualizada para mostrar o novo campo com o tipo de dados [!UICONTROL Object] aplicado, incluindo controles para editar e adicionar subcampos ao objeto.

![](../../images/ui/fields/special/object-applied.png)

Para adicionar um subcampo, selecione o ícone de **mais (+)** ao lado do campo de objeto na tela. Um novo campo é exibido abaixo do objeto, com controles para configurar o subcampo no painel direito.

![](../../images/ui/fields/special/object-add-field.png)

Depois de configurar o subcampo e selecionar **[!UICONTROL Apply]**, você pode continuar a adicionar campos ao objeto usando o mesmo processo. Também é possível adicionar subcampos que são objetos, permitindo aninhar campos da maneira mais profunda que desejar.

![](../../images/ui/fields/special/object-nested.png)

Uma vez terminado de construir o objeto, você pode descobrir que deseja reutilizar sua estrutura em diferentes classes e mixins. Nesse caso, é possível optar por converter o objeto em um tipo de dados. Consulte a seção sobre [conversão de objetos em tipos de dados](../resources/data-types.md#convert) no guia da interface do usuário de tipos de dados para obter mais informações.

## Próximas etapas

Este guia cobriu como definir um campo de objeto na interface do usuário do . Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].
