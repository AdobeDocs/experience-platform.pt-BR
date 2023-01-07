---
keywords: Experience Platform, home, tópicos populares, interface do usuário, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, editor de esquema, Editor de esquema, esquema, esquemas, esquemas, esquemas, criar, relacionamento, Relação, referência, Referência;
solution: Experience Platform
title: Definir uma relação entre dois esquemas usando o editor de esquema
description: Este documento fornece um tutorial para definir uma relação entre dois schemas usando o Editor de esquemas na interface do usuário do Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 3b16c0766c7d54b18ceea4c9f40ccb370b9f9685
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---

# Defina uma relação um para um entre dois schemas usando o [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Relacionamentos de esquema"
>abstract="Os esquemas pertencentes a classes diferentes podem ser vinculados contextualmente por meio de campos de relação, permitindo a criação de regras de segmentação mais complexas. Consulte a documentação para obter mais informações sobre relações de esquema."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Esquema de referência"
>abstract="Selecione o schema com o qual deseja estabelecer uma relação. Esse schema pode ser uma classe diferente do schema atual. Consulte a documentação para obter mais informações sobre relações de esquema."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Namespace da identidade de referência"
>abstract="O namespace (tipo) do campo de identidade principal do esquema de referência. O schema de referência deve ter um campo de identidade primário estabelecido para participar de um relacionamento. Consulte a documentação para obter mais informações sobre relações de esquema."

A capacidade de entender os relacionamentos entre seus clientes e suas interações com a marca em vários canais é uma parte importante do Adobe Experience Platform. Definir esses relacionamentos dentro da estrutura de [!DNL Experience Data Model] Os esquemas (XDM) permitem que você obtenha insights complexos sobre os dados do cliente.

Embora os relacionamentos de schema possam ser inferidos por meio do uso do schema de união e [!DNL Real-Time Customer Profile], isso se aplica somente a esquemas que compartilham a mesma classe. Para estabelecer uma relação entre dois schemas pertencentes a classes diferentes, um campo de relacionamento dedicado deve ser adicionado a um schema de origem, que faz referência à identidade do outro schema relacionado.

Este documento fornece um tutorial para definir uma relação entre dois esquemas usando o Editor de esquemas na [!DNL Experience Platform] interface do usuário. Para obter etapas sobre como definir relações de esquema usando a API, consulte o tutorial em [definição de um relacionamento usando a API do Registro de Esquema](relationship-api.md).

>[!NOTE]
>
>Para obter etapas sobre como criar uma relação muitos para um no Adobe Real-time Customer Data Platform B2B Edition, consulte o guia sobre [criação de relações B2B](./relationship-b2b.md).

## Introdução

Este tutorial requer uma compreensão funcional do [!DNL XDM System] e o Editor de esquemas na [!DNL Experience Platform] IU. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no [!DNL Experience Platform].
* [Noções básicas da composição do schema](../schema/composition.md): Uma introdução dos blocos de construção dos esquemas XDM.
* [Crie um schema usando o [!DNL Schema Editor]](create-schema-ui.md): Um tutorial sobre as noções básicas para trabalhar com a [!DNL Schema Editor].

## Definir um schema de referência e de origem

Espera-se que você já tenha criado os dois schemas que serão definidos na relação. Para fins de demonstração, este tutorial cria uma relação entre membros do programa de fidelidade de uma organização (definido em um &quot;[!DNL Loyalty Members]&quot; schema) e seu hotel favorito (definido em um &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Para estabelecer uma relação, ambos os esquemas devem ter identidades primárias definidas e devem ser habilitados para [!DNL Real-Time Customer Profile]. Consulte a seção sobre [ativar um esquema para usar no Perfil](./create-schema-ui.md#profile) no tutorial de criação de esquema se você precisar de orientação sobre como configurar seus esquemas adequadamente.

Os relacionamentos de schema são representados por um campo dedicado em um **esquema de origem** que aponta para outro campo dentro de um **schema de referência**. Nas etapas a seguir, &quot;[!DNL Loyalty Members]&quot; será o schema de origem, enquanto &quot;[!DNL Hotels]&quot; atuará como o schema de referência.

As seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que um relacionamento seja definido.

### [!DNL Loyalty Members] schema

O schema de origem &quot;[!DNL Loyalty Members]&quot; se baseia no [!DNL XDM Individual Profile] classe , que contém campo que descreve membros de um programa de fidelidade. Um desses campos, `personalEmail.addess`, serve como a identidade primária do schema no [!UICONTROL Email] namespace. Conforme visto em **[!UICONTROL Propriedades do esquema]**, este esquema foi ativado para uso em [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

O schema de referência &quot;[!DNL Hotels]&quot; se baseia em um &quot; personalizado[!DNL Hotels]&quot; e contém campos que descrevem um hotel. Para participar de um relacionamento, o schema de referência também deve ter uma identidade primária definida e estar habilitado para [!UICONTROL Perfil]. Nesse caso, `_tenantId.hotelId`atua como a identidade primária do esquema, usando um &quot; personalizado[!DNL Hotel ID]&quot; namespace de identidade.

![Ativar para Perfil](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Para saber como criar namespaces de identidade personalizados, consulte [Documentação do Serviço de identidade](../../identity-service/namespaces.md#manage-namespaces).

## Criar um grupo de campos de relação

>[!NOTE]
>
>Essa etapa só será necessária se o esquema de origem não tiver um campo de tipo string dedicado para ser usado como ponteiro para a identidade primária do esquema de referência. Se esse campo já estiver definido no esquema de origem, pule para a próxima etapa de [definição de um campo de relacionamento](#relationship-field).

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado que indicará a identidade primária do schema de referência. É possível adicionar esse campo ao schema de origem criando um novo grupo de campos de esquema ou estendendo um existente.

No caso de [!DNL Loyalty Members] , um novo `preferredHotel` será adicionado para indicar o hotel preferencial do membro do programa de fidelidade para visitas da empresa. Comece selecionando o ícone de adição (**+**) ao lado do nome do schema de origem.

![](../images/tutorials/relationship/loyalty-add-field.png)

Um novo espaço reservado para campo aparece na tela. Em **[!UICONTROL Propriedades do campo]**, forneça um nome de campo e nome de exibição para o campo e defina seu tipo como &quot;[!UICONTROL String]&quot;. Em **[!UICONTROL Atribuir a]**, selecione um grupo de campos existente a ser estendido ou digite um nome exclusivo para criar um novo grupo de campos. Nesse caso, um novo &quot;[!DNL Preferred Hotel]&quot; grupo de campos é criado.

![](../images/tutorials/relationship/relationship-field-details.png)

Quando terminar, selecione **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

O arquivo `preferredHotel` aparece na tela, localizada abaixo de um `_tenantId` desde que seja um campo personalizado. Selecionar **[!UICONTROL Salvar]** para finalizar as alterações no schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir um campo de relacionamento para o schema de origem {#relationship-field}

Depois que o schema de origem tiver um campo de referência dedicado definido, você poderá designá-lo como um campo de relacionamento.

>[!NOTE]
>
>As etapas abaixo abordam como definir um campo de relação usando os controles do painel direito na tela. Se você tiver acesso ao Real-Time CDP B2B Edition, também poderá definir uma relação um para um usando o [mesma caixa de diálogo](./relationship-b2b.md#relationship-field) como ao criar relacionamentos muitos para um.

Selecione o `preferredHotel` na tela, role para baixo **[!UICONTROL Propriedades do campo]** até que o **[!UICONTROL Relação]** será exibida. Marque a caixa de seleção para revelar os parâmetros necessários para configurar um campo de relacionamento.

![](../images/tutorials/relationship/relationship-checkbox.png)

Selecione a lista suspensa para **[!UICONTROL Esquema de referência]** e selecione o schema de referência para o relacionamento (&quot;[!DNL Hotels]&quot; neste exemplo). Em **[!UICONTROL Namespace da identidade de referência]**, selecione o namespace do campo de identidade do schema de referência (neste caso, &quot;[!DNL Hotel ID]&quot;). Selecionar **[!UICONTROL Aplicar]** quando terminar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

O `preferredHotel` agora é destacado como um relacionamento na tela, exibindo o nome do schema de referência. Selecionar **[!UICONTROL Salvar]** para salvar suas alterações e concluir o fluxo de trabalho.

![](../images/tutorials/relationship/relationship-save.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas usando o [!DNL Schema Editor]. Para obter etapas sobre como definir relações usando a API, consulte o tutorial em [definição de um relacionamento usando a API do Registro de Esquema](relationship-api.md).
