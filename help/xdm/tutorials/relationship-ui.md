---
keywords: Experience Platform, home, tópicos populares, interface do usuário, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, editor de esquema, Editor de esquema, esquema, esquemas, esquemas, esquemas, criar, relacionamento, Relação, referência, Referência;
solution: Experience Platform
title: Definir uma relação entre dois esquemas usando o editor de esquema
description: Este documento fornece um tutorial para definir uma relação entre dois schemas usando o Editor de esquemas na interface do usuário do Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Defina uma relação entre dois schemas usando o [!DNL Schema Editor]

A capacidade de entender os relacionamentos entre seus clientes e suas interações com a marca em vários canais é uma parte importante do Adobe Experience Platform. Definir esses relacionamentos dentro da estrutura de seus esquemas [!DNL Experience Data Model] (XDM) permite que você obtenha insights complexos sobre os dados do cliente.

Embora os relacionamentos de esquema possam ser inferidos por meio do uso do schema de união e [!DNL Real-time Customer Profile], isso se aplica somente a esquemas que compartilham a mesma classe. Para estabelecer uma relação entre dois schemas pertencentes a classes diferentes, um campo de relacionamento dedicado deve ser adicionado a um schema de origem, que faz referência à identidade de um schema de destino.

Este documento fornece um tutorial para definir uma relação entre dois esquemas usando o Editor de esquemas na interface do usuário [!DNL Experience Platform]. Para obter etapas sobre como definir relações de esquema usando a API, consulte o tutorial em [definindo uma relação usando a API do Registro de Esquema](relationship-api.md).

## Introdução

Este tutorial requer uma compreensão funcional de [!DNL XDM System] e do Editor de esquemas na interface do usuário [!DNL Experience Platform]. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no  [!DNL Experience Platform].
* [Noções básicas da composição](../schema/composition.md) do schema: Uma introdução dos blocos de construção dos esquemas XDM.
* [Crie um schema usando o [!DNL Schema Editor]](create-schema-ui.md): Um tutorial sobre as noções básicas para trabalhar com a  [!DNL Schema Editor].

## Definir um esquema de origem e de destino

Espera-se que você já tenha criado os dois schemas que serão definidos na relação. Para fins de demonstração, este tutorial cria uma relação entre membros do programa de fidelidade de uma organização (definido em um schema &quot;[!DNL Loyalty Members]&quot;) e seu hotel favorito (definido em um schema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Para estabelecer uma relação, ambos os esquemas devem ter identidades primárias definidas e devem ser habilitados para [!DNL Real-time Customer Profile]. Consulte a seção [ativando um schema para uso em Profile](./create-schema-ui.md#profile) no tutorial de criação de schema se precisar de orientação sobre como configurar seus schemas de acordo.

As relações de esquema são representadas por um campo dedicado dentro de um **schema de origem** que se refere a outro campo dentro de um **schema de destino**. Nas etapas a seguir, &quot;[!DNL Loyalty Members]&quot; será o schema de origem, enquanto &quot;[!DNL Hotels]&quot; atuará como o schema de destino.

Para fins de referência, as seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que um relacionamento seja definido.

### [!DNL Loyalty Members] schema

O schema de origem &quot;[!DNL Loyalty Members]&quot; é baseado na classe [!DNL XDM Individual Profile] e é o schema que foi construído no tutorial para [criar um schema na interface do usuário](create-schema-ui.md). Ele inclui um objeto `loyalty` em seu namespace `_tenantId`, que inclui vários campos específicos de fidelidade. Um desses campos, `loyaltyId`, serve como a identidade primária para o schema no namespace [!UICONTROL Email]. Conforme visto em **[!UICONTROL Schema Properties]**, este esquema foi ativado para uso em [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

O esquema de destino &quot;[!DNL Hotels]&quot; é baseado em uma classe personalizada &quot;[!DNL Hotels]&quot; e contém campos que descrevem um hotel. O campo `hotelId` serve como a identidade primária para o esquema em um namespace `hotelId` personalizado. Como o schema [!DNL Loyalty Members], esse schema também foi ativado para [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Criar um grupo de campos do schema de relacionamento

>[!NOTE]
>
>Essa etapa só será necessária se o schema de origem não tiver um campo do tipo string dedicado a ser usado como referência para o schema de destino. Se esse campo já estiver definido no esquema de origem, pule para a próxima etapa de [definição de um campo de relação](#relationship-field).

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado para ser usado como referência para o schema de destino. É possível adicionar esse campo ao schema de origem criando um novo grupo de campos de esquema.

Comece selecionando **[!UICONTROL Add]** na seção **[!UICONTROL Field groups]**.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

A caixa de diálogo [!UICONTROL Add field group] é exibida. Aqui, selecione **[!UICONTROL Create new field group]**. Nos campos de texto exibidos, insira um nome de exibição e uma descrição para o novo grupo de campos. Selecione **[!UICONTROL Add field groups]** quando terminar.

![](../images/tutorials/relationship/create-field-group.png)

A tela reaparece com &quot;[!DNL Favorite Hotel]&quot; aparecendo na seção **[!UICONTROL Field groups]**. Selecione o nome do grupo de campos e selecione **[!UICONTROL Add field]** ao lado do campo de nível raiz `Loyalty Members`.

![](../images/tutorials/relationship/loyalty-add-field.png)

Um novo campo aparece na tela sob o namespace `_tenantId`. Em **[!UICONTROL Field properties]**, forneça um nome de campo e nome de exibição para o campo e defina seu tipo como &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Quando terminar, selecione **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

O campo atualizado `favoriteHotel` aparece na tela. Selecione **[!UICONTROL Save]** para finalizar as alterações no schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir um campo de relação para o schema de origem {#relationship-field}

Depois que o schema de origem tiver um campo de referência dedicado definido, você poderá designá-lo como um campo de relacionamento.

Selecione o campo `favoriteHotel` na tela e role para baixo em **[!UICONTROL Field properties]** até que a caixa de seleção **[!UICONTROL Relationship]** seja exibida. Marque a caixa de seleção para revelar os parâmetros necessários para configurar um campo de relacionamento.

![](../images/tutorials/relationship/relationship-checkbox.png)

Selecione a lista suspensa para **[!UICONTROL Reference schema]** e selecione o schema de destino para a relação (&quot;[!DNL Hotels]&quot; neste exemplo). Se o schema de destino estiver ativado para [!DNL Profile], o campo **[!UICONTROL Reference identity namespace]** será automaticamente definido para o namespace da identidade primária do schema de destino. Se o schema não tiver uma identidade primária definida, você deverá selecionar manualmente o namespace que planeja usar no menu suspenso. Selecione **[!UICONTROL Apply]** quando terminar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

O campo `favoriteHotel` agora é destacado como uma relação na tela, exibindo o nome e o namespace de identidade de referência do schema de destino. Selecione **[!UICONTROL Save]** para salvar suas alterações e concluir o fluxo de trabalho.

![](../images/tutorials/relationship/relationship-save.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas usando o [!DNL Schema Editor]. Para obter etapas sobre como definir relações usando a API, consulte o tutorial em [definindo uma relação usando a API do Registro de Schema](relationship-api.md).
