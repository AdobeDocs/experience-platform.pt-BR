---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Definir uma relação entre dois schemas usando o Editor de Schemas de Schemas
description: Este documento fornece um tutorial para definir uma relação entre dois schemas usando o Editor de Schemas na interface do usuário do Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# Defina uma relação entre dois schemas usando a variável [!DNL Schema Editor]

A capacidade de entender as relações entre seus clientes e suas interações com a sua marca em vários canais é uma parte importante da Adobe Experience Platform. A definição desses relacionamentos dentro da estrutura dos schemas [!DNL Experience Data Model] (XDM) permite obter insights complexos sobre os dados do cliente.

Embora as relações com os schemas possam ser inferidas com o uso do schema da união e [!DNL Real-time Customer Profile], isso se aplica somente aos schemas que compartilham a mesma classe. Para estabelecer uma relação entre dois schemas pertencentes a classes diferentes, um campo de relacionamento dedicado deve ser adicionado a um schema de origem, que faz referência à identidade de um schema de destino.

Este documento fornece um tutorial para definir uma relação entre dois schemas usando o Editor de Schemas na interface do [!DNL Experience Platform] usuário. Para obter etapas sobre como definir relações de schema usando a API, consulte o tutorial sobre como [definir uma relação usando a API](relationship-api.md)de Registro de Schemas.

## Introdução

Este tutorial requer uma compreensão funcional do Editor de Schemas [!DNL XDM System] na [!DNL Experience Platform] interface do usuário. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação em [!DNL Experience Platform].
* [Noções básicas da composição](../schema/composition.md)do schema: Uma introdução dos blocos de construção dos schemas XDM.
* [Crie um schema usando [!DNL Schema Editor]](create-schema-ui.md): Um tutorial que aborda as noções básicas de como trabalhar com o [!DNL Schema Editor].

## Definir um schema de origem e de destino

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Para fins de demonstração, este tutorial cria uma relação entre os membros do programa de fidelidade de uma organização (definido em um &quot;[!DNL Loyalty Members]&quot; schema) e seu hotel favorito (definido em um schema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Para estabelecer uma relação, ambos os schemas devem ter identidades primárias definidas e estar habilitados para [!DNL Real-time Customer Profile]. Consulte a seção sobre como [ativar um schema para uso no Perfil](./create-schema-ui.md#profile) no tutorial de criação do schema se precisar de orientação sobre como configurar seus schemas de acordo.

As relações com o schema são representadas por um campo dedicado dentro de um schema **de** origem que se refere a outro campo dentro de um schema **de** destino. Nas etapas a seguir, &quot;[!DNL Loyalty Members]&quot; será o schema de origem, enquanto &quot;[!DNL Hotels]&quot; atuará como o schema de destino.

Para fins de referência, as seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que uma relação seja definida.

### [!DNL Loyalty Members] schema

O schema de origem &quot;[!DNL Loyalty Members]&quot; é baseado na [!DNL XDM Individual Profile] classe e é o schema que foi construído no tutorial para [criar um schema na interface do usuário](create-schema-ui.md). Inclui um `loyalty` objeto sob sua `_tenantId` namespace, que inclui vários campos específicos para a fidelidade. Um desses campos, `loyaltyId`, serve como a principal identidade do schema sob a namespace [!UICONTROL Email] . Conforme visto em Propriedades **[!UICONTROL do]** Schema, este schema foi habilitado para uso em [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

O schema de destino &quot;[!DNL Hotels]&quot; é baseado em uma classe &quot;[!DNL Hotels]&quot; personalizada e contém campos que descrevem um hotel. O `hotelId` campo serve como a identidade principal do schema sob uma `hotelId` namespace personalizada. Como o [!DNL Loyalty Members] schema, este schema também foi ativado para [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Criar uma mistura de relacionamento

>[!NOTE]
>
>Essa etapa só é necessária se o schema de origem não tiver um campo de tipo de string dedicado para ser usado como referência ao schema de destino. Se esse campo já estiver definido no schema de origem, pule para a próxima etapa da [definição de um campo](#relationship-field)de relação.

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado para ser usado como referência ao schema de destino. É possível adicionar esse campo ao schema de origem criando uma nova combinação.

Start selecionando **[!UICONTROL Adicionar]** na seção **[!UICONTROL Misturas]** .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

A caixa de diálogo [!UICONTROL Adicionar mistura] é exibida. Aqui, selecione **[!UICONTROL Criar nova mixagem]**. Nos campos de texto exibidos, insira um nome de exibição e uma descrição para a nova combinação. Selecione **[!UICONTROL Adicionar mistura]** ao terminar.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

A tela reaparece com &quot;[!DNL Favorite Hotel]&quot; aparecendo na seção **[!UICONTROL Misturas]** . Selecione o nome da combinação e, em seguida, selecione **[!UICONTROL Adicionar campo]** ao lado do campo de nível raiz `Loyalty Members` .

![](../images/tutorials/relationship/loyalty-add-field.png)

Um novo campo é exibido na tela abaixo da `_tenantId` namespace. Em Propriedades **[!UICONTROL de]** campo, forneça um nome de campo e de exibição para o campo e defina seu tipo como &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Quando terminar, selecione **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

O `favoriteHotel` campo atualizado é exibido na tela. Selecione **[!UICONTROL Salvar]** para finalizar as alterações no schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir um campo de relacionamento para o schema de origem {#relationship-field}

Depois que o schema de origem tiver um campo de referência dedicado definido, você poderá designá-lo como um campo de relacionamento.

Selecione o `favoriteHotel` campo na tela e role para baixo em Propriedades **[!UICONTROL de]** campo até que a caixa de seleção **[!UICONTROL Relacionamento]** seja exibida. Marque a caixa de seleção para revelar os parâmetros necessários para configurar um campo de relação.

![](../images/tutorials/relationship/relationship-checkbox.png)

Selecione a lista suspensa para schema **[!UICONTROL de]** referência e selecione o schema de destino para a relação (&quot;[!DNL Hotels]&quot; neste exemplo). Se o schema de destino estiver ativado para [!DNL Profile], o campo **[!UICONTROL Referência da namespace]** de identidade será automaticamente definido para a namespace da identidade principal do schema de destino. Se o schema não tiver uma identidade primária definida, você deverá selecionar manualmente a namespace que planeja usar no menu suspenso. Selecione **[!UICONTROL Aplicar]** ao terminar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

O `favoriteHotel` campo agora é destacado como uma relação na tela, exibindo o nome e a namespace de identidade de referência do schema de destino. Selecione **[!UICONTROL Salvar]** para salvar as alterações e concluir o fluxo de trabalho.

![](../images/tutorials/relationship/relationship-save.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas usando o [!DNL Schema Editor]. Para obter etapas sobre como definir relações usando a API, consulte o tutorial sobre como [definir uma relação usando a API](relationship-api.md)do Registro de Schemas.