---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; objeto; campo;
solution: Experience Platform
title: Definir campos de objeto na interface do usuário
description: Saiba como definir um campo do tipo objeto na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Definir campos de objeto na interface do usuário

O Adobe Experience Platform permite personalizar totalmente a estrutura de suas classes personalizadas do Experience Data Model (XDM), grupos de campos de esquema e tipos de dados. Para organizar e aninhar campos relacionados em recursos XDM personalizados, você pode definir campos do tipo objeto que podem conter subcampos adicionais.

When [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, use a variável **[!UICONTROL Tipo]** e selecione &quot;[!UICONTROL Objeto]&quot; na lista.

![](../../images/ui/fields/special/object.png)

Selecionar **[!UICONTROL Aplicar]** para adicionar o objeto ao schema. A tela é atualizada para mostrar o novo campo com a variável [!UICONTROL Objeto] tipo de dados aplicado, incluindo controles para editar e adicionar subcampos ao objeto.

![](../../images/ui/fields/special/object-applied.png)

Para adicionar um subcampo, selecione o **mais (+)** ícone ao lado do campo de objeto na tela. Um novo campo é exibido abaixo do objeto, com controles para configurar o subcampo no painel direito.

![](../../images/ui/fields/special/object-add-field.png)

Depois de configurar o subcampo e selecionar **[!UICONTROL Aplicar]**, é possível continuar a adicionar campos ao objeto usando o mesmo processo. Também é possível adicionar subcampos que são objetos, permitindo aninhar campos da maneira mais profunda que desejar.

Depois de concluir a construção do objeto, você pode descobrir que deseja reutilizar sua estrutura em diferentes classes e grupos de campos. Nesse caso, é possível optar por converter o objeto em um tipo de dados. Consulte a seção sobre [conversão de objetos em tipos de dados](../resources/data-types.md#convert) no guia da interface do usuário de tipos de dados para obter mais informações.

## Próximas etapas

Este guia cobriu como definir um campo de objeto na interface do usuário do . Consulte a visão geral em [definição de campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
