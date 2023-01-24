---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; grupo de campos; grupos de campos;
solution: Experience Platform
title: Criar e editar grupos de campos de esquema na interface do usuário
description: Saiba como criar e editar grupos de campos de esquema na interface do usuário do Experience Platform.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 542ad49f475ac9586da506a8afa5408e83262121
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Criar e editar grupos de campos de esquema na interface do usuário

No Experience Data Model (XDM), os grupos de campos do esquema são componentes reutilizáveis que definem um ou mais campos que implementam determinadas funções, como detalhes pessoais, preferências de hotel ou endereço. Os grupos de campos devem ser incluídos como parte de um schema que implementa uma classe compatível.

Um grupo de campos define a(s) classe(s) com a qual ele é compatível, com base no comportamento dos dados que o grupo de campos representa (registro ou série de tempo). Isso significa que nem todos os grupos de campos estão disponíveis para uso com todas as classes.

O Adobe Experience Platform fornece vários grupos de campo padrão que abrangem uma grande variedade de casos de uso de marketing. No entanto, também é possível criar e editar seus próprios grupos de campos personalizados para definir conceitos adicionais relacionados à sua empresa nos esquemas XDM. Este guia fornece uma visão geral de como criar, editar e gerenciar grupos de campos personalizados para sua organização na interface do usuário da plataforma.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para uma introdução ao papel do XDM no ecossistema do Experience Platform, e [noções básicas da composição do schema](../../schema/composition.md) para saber como os grupos de campos contribuem para os esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir também o tutorial em [composição de um esquema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Criar um novo grupo de campos {#create}

Para criar um novo grupo de campos, primeiro selecione um schema ao qual o grupo de campos será adicionado. Você pode optar por [criar um novo schema](./schemas.md#create) ou [selecionar um esquema existente para editar](./schemas.md#edit).

Depois de ter o schema aberto no [!DNL Schema Editor], selecione **[!UICONTROL Adicionar]** ao lado do [!UICONTROL Grupos de campos] no painel esquerdo.

![](../../images/ui/resources/field-groups/add-field-group.png)

Na caixa de diálogo exibida, selecione **[!UICONTROL Criar novo grupo de campos]**. Aqui você pode fornecer uma **[!UICONTROL Nome de exibição]** e **[!UICONTROL Descrição]** para o grupo de campos. Quando terminar, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

O [!DNL Schema Editor] será exibido novamente, com o novo grupo de campos listado no painel esquerdo. Como esse é um grupo de campos totalmente novo, atualmente não fornece campos para o esquema e, portanto, a tela permanece inalterada. Agora você pode começar [adição de campos ao grupo de campos](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Editar um grupo de campos existente {#edit}

>[!NOTE]
>
>Somente grupos de campos personalizados definidos pela sua organização podem ser totalmente editados e personalizados. Para grupos de campos principais definidos pelo Adobe, somente os nomes de exibição de seus campos podem ser editados no contexto de schemas individuais. Consulte a seção sobre [edição de nomes de exibição para campos de esquema](./schemas.md#display-names) para obter detalhes.
>
>Depois que um grupo de campos personalizado é salvo e usado em um schema para assimilação de dados, somente alterações aditivas podem ser feitas no grupo de campos depois disso. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar um grupo de campos existente, primeiro abra um esquema que empregue o grupo de campos no [!DNL Schema Editor]. Você pode [selecionar um esquema existente para editar](./schemas.md#edit)ou você pode [criar um novo schema](./schemas.md#create) e adicione o grupo de campos em questão.

Depois de abrir o schema no editor, você pode iniciar [adição de campos ao grupo de campos](#add-fields).

## Adicionar campos a um grupo de campos {#add-fields}

>[!NOTE]
>
>Esta seção foca na adição de campos a grupos de campos personalizados. Para obter informações sobre como adicionar campos personalizados a grupos de campos padrão, consulte [guia da interface do usuário do schemas](./schemas.md#custom-fields-for-standard-groups).

Para adicionar campos a um grupo de campos personalizado, comece selecionando o **mais (+)** ícone ao lado do nome do esquema na tela.

![](../../images/ui/resources/field-groups/add-field.png)

Um **[!UICONTROL Campo sem título]** o espaço reservado aparece na tela e o painel direito é atualizado para mostrar controles para configurar as propriedades do campo. Consulte o guia sobre [definição de campos na interface do usuário](../fields/overview.md#define) para etapas específicas sobre como configurar tipos de campos diferentes.

Em **[!UICONTROL Atribuir a]**, selecione o **[!UICONTROL Grupo de campos]** , em seguida, use a lista suspensa para selecionar o grupo de campos desejado na lista. Você pode começar a digitar o nome do grupo de campos para limitar os resultados.

![](../../images/ui/resources/field-groups/select-field-group.png)

Em **[!UICONTROL Atribuir a]**, selecione o **[!UICONTROL Grupo de campos]** , em seguida, use a lista suspensa para selecionar o grupo de campos desejado na lista. Você pode começar a digitar o nome do grupo de campos para limitar os resultados.

![](../../images/ui/resources/field-groups/select-field-group.png)

Depois que o campo é adicionado ao schema, ele é atribuído ao grupo de campos selecionado. Continue a adicionar quantos campos forem necessários ao grupo de campos. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o schema e o grupo de campos.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Se o mesmo grupo de campos já estiver empregado em outros schemas, os campos recém-adicionados serão exibidos automaticamente nesses schemas.

## Próximas etapas

Este guia cobriu como criar e editar grupos de campos usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos da [!UICONTROL Esquemas] espaço de trabalho, consulte o [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar grupos de campos usando o [!DNL Schema Registry] API, consulte o [guia do ponto de extremidade de grupos de campos](../../api/field-groups.md).
