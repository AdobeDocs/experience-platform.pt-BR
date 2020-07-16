---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definir uma relação entre dois schemas usando o Editor de Schemas de Schemas
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# Defina uma relação entre dois schemas usando a variável [!DNL Schema Editor]

A capacidade de entender os relacionamentos entre seus clientes e suas interações com a sua marca em vários canais é uma parte importante do Adobe Experience Platform. A definição desses relacionamentos dentro da estrutura dos schemas [!DNL Experience Data Model] (XDM) permite obter insights complexos sobre os dados do cliente.

Este documento fornece um tutorial para definir uma relação um para um entre dois schemas definidos pela sua organização usando o [!DNL Schema Editor] na interface do [!DNL Experience Platform] usuário. Para obter etapas sobre como definir relações de schema usando a API, consulte o tutorial sobre como [definir uma relação usando a API](relationship-api.md)de Registro de Schemas.

## Introdução

Este tutorial requer uma compreensão funcional de [!DNL XDM System] e da [!DNL Schema Editor] [!DNL Experience Platform] interface do usuário. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no Experience Platform.
* [Noções básicas da composição](../schema/composition.md)do schema: Uma introdução dos blocos de construção dos schemas XDM.
* [Crie um schema usando o Editor](create-schema-ui.md)de Schemas: Um tutorial que aborda as noções básicas de como trabalhar com o [!DNL Schema Editor].

## Definir um schema de origem e de destino

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Para fins de demonstração, este tutorial cria uma relação entre os membros do programa de fidelidade de uma organização (definido em um schema &quot;Membros[!UICONTROL de]fidelidade&quot;) e seus hotéis favoritos (definido em um schema &quot;Hotéis&quot;).

As relações de Schema são representadas por um schema **[!UICONTROL de]** origem com um campo que se refere a outro campo dentro de um schema **[!UICONTROL de]** destino. Nas etapas a seguir, &quot;Membros[!UICONTROL de]fidelidade&quot; será o schema de origem, enquanto &quot;Hotéis&quot; atuará como o schema de destino.

Para fins de referência, as seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que uma relação seja definida.

### [!UICONTROL schema de Membros] de Fidelidade

O schema de origem &quot;Membros[!UICONTROL de]fidelidade&quot; é o schema que foi construído no tutorial para [criar um schema na interface do usuário](create-schema-ui.md). Ele inclui um objeto &quot;[!UICONTROL fidelidade]&quot; na namespace &quot;[!UICONTROL \_locatárioId]&quot;, que inclui vários campos específicos de fidelidade. Um desses campos, &quot;[!UICONTROL loyaltyId]&quot;, serve como a principal identidade para o schema sob a namespace &quot;[!UICONTROL Email]&quot;. Conforme visto em Propriedades _do_ Schema, este schema foi habilitado para uso em [!DNL Real-time Customer Profile](../../profile/home.md).

![](../images/tutorials/relationship/loyalty-members.png)

### schema Hotéis

O schema de destino &quot;[!UICONTROL Hotéis]&quot; contém campos que descrevem um hotel, incluem seu endereço, marca, número de salas e classificação de estrelas. O campo &quot;[!UICONTROL hotelId]&quot; serve como a principal identidade do schema sob a namespace &quot;ECID&quot;. Ao contrário de &quot;Membros[!UICONTROL de]Fidelidade&quot;, este schema não foi ativado para [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Criar uma mistura de relacionamento

>[!NOTE]
>
>Essa etapa só é necessária se o schema de origem não tiver um campo do tipo string dedicado para ser usado como referência a outro schema. Se esse campo já estiver definido no schema de origem, pule para a próxima etapa da [definição de um campo](#relationship-field)de relação.

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado para ser usado como referência ao schema de destino. É possível adicionar esse campo ao schema de origem criando uma nova combinação.

Start clicando em **[!UICONTROL Adicionar]** na seção _Misturas_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

A caixa de diálogo [!UICONTROL _Adicionar mistura _]é exibida. Aqui, clique em**[!UICONTROL  Criar nova mistura ]**. Nos campos de texto exibidos, insira um nome de exibição e uma descrição para a nova combinação. Clique em**[!UICONTROL  Adicionar mistura ]**quando terminar.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

A tela reaparece com &quot;Relacionamento de[!UICONTROL fidelidade]&quot; na seção _Misturas_ . Clique no nome da combinação e, em seguida, clique em **[!UICONTROL Adicionar campo]** ao lado do campo de nível raiz &quot;Membros[!UICONTROL de]fidelidade&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Um novo campo é exibido na tela sob a namespace &quot;[!UICONTROL \_locatárioId]&quot;. Em Propriedades [!UICONTROL _do _]campo, forneça um nome de campo e de exibição para o campo e defina seu tipo como &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Quando terminar, clique em **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

O campo atualizado &quot;[!UICONTROL loyaltyRelationship]&quot; aparece na tela. Clique em **[!UICONTROL Salvar]** para finalizar as alterações no schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir um campo de relacionamento para o schema de origem {#relationship-field}

Depois que o schema de origem tiver um campo de referência dedicado definido, você poderá designá-lo como um campo de relacionamento.

Clique no campo de referência na tela e role para baixo em Propriedades _[!UICONTROL do]_campo até que a caixa de seleção**[!UICONTROL  Relacionamento ]**seja exibida. Marque a caixa de seleção para revelar os parâmetros necessários para configurar um campo de relação.

![](../images/tutorials/relationship/relationship-checkbox.png)

Clique na lista suspensa para Schema **[!UICONTROL de]** referência e selecione o schema de destino para a relação (&quot;[!UICONTROL Hotéis]&quot; neste exemplo). Se o schema de destino estiver habilitado para união, o campo Namespace **[!UICONTROL de identidade de]** referência será automaticamente definido para a namespace da identidade principal do schema de destino. Se o schema não tiver uma identidade primária definida, você deverá selecionar manualmente a namespace que planeja usar no menu suspenso. Click **[!UICONTROL Apply]** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

O campo aparece como uma relação na tela, exibindo o nome e a namespace de identidade de referência do schema de destino. Clique em **[!UICONTROL Salvar]** para salvar suas alterações e concluir o fluxo de trabalho.

![](../images/tutorials/relationship/relationship-save.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas usando o [!DNL Schema Editor]. Para obter etapas sobre como definir relações usando a API, consulte o tutorial sobre como [definir uma relação usando a API](relationship-api.md)do Registro de Schemas.