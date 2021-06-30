---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; grupo de campos; grupos de campos;
solution: Experience Platform
title: Criar e editar grupos de campos de esquema na interface do usuário
description: Saiba como criar e editar grupos de campos de esquema na interface do usuário do Experience Platform.
topic-legacy: user guide
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# Criar e editar grupos de campos de esquema na interface do usuário

No Experience Data Model (XDM), os grupos de campos do esquema são componentes reutilizáveis que definem um ou mais campos que implementam determinadas funções, como detalhes pessoais, preferências de hotel ou endereço. Os grupos de campos devem ser incluídos como parte de um schema que implementa uma classe compatível.

Um grupo de campos define a(s) classe(s) com a qual ele é compatível, com base no comportamento dos dados que o grupo de campos representa (registro ou série de tempo). Isso significa que nem todos os grupos de campos estão disponíveis para uso com todas as classes.

O Adobe Experience Platform fornece vários grupos de campo padrão que abrangem uma grande variedade de casos de uso de marketing. No entanto, também é possível criar e editar seus próprios grupos de campos personalizados para definir conceitos adicionais relacionados à sua empresa nos esquemas XDM. Este guia fornece uma visão geral de como criar, editar e gerenciar grupos de campos personalizados para sua organização na interface do usuário da plataforma.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM no ecossistema do Experience Platform e as [noções básicas da composição do schema](../../schema/composition.md) sobre como os grupos de campos contribuem para os esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir também o tutorial em [composição de um schema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Criar um novo grupo de campos {#create}

Para criar um novo grupo de campos, primeiro selecione um schema ao qual o grupo de campos será adicionado. Você pode optar por [criar um novo schema](./schemas.md#create) ou [selecionar um schema existente para editar](./schemas.md#edit).

Depois de abrir o schema no [!DNL Schema Editor], selecione **[!UICONTROL Adicionar]** ao lado da seção [!UICONTROL Grupos de campos] no painel esquerdo.

![](../../images/ui/resources/field-groups/add-field-group.png)

Uma caixa de diálogo é exibida mostrando uma lista de grupos de campos existentes para sua organização. Próximo à parte superior da caixa de diálogo, selecione **[!UICONTROL Criar novo grupo de campos]**. Aqui você pode fornecer um **[!UICONTROL Display name]** e **[!UICONTROL Description]** para o grupo de campos. Quando terminar, selecione **[!UICONTROL Adicionar grupo de campos]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

O [!DNL Schema Editor] é exibido novamente, com o novo grupo de campos listado no painel esquerdo. Como esse é um grupo de campos totalmente novo, atualmente não fornece campos para o esquema e, portanto, a tela permanece inalterada. Agora você pode iniciar [adicionando campos ao grupo de campos](#add-fields).

## Editar um grupo de campos existente {#edit}

>[!NOTE]
>
>Somente grupos de campos personalizados definidos pela sua organização podem ser totalmente editados e personalizados. Para grupos de campos principais definidos pelo Adobe, somente os nomes de exibição de seus campos podem ser editados no contexto de schemas individuais. Consulte a seção sobre [edição de nomes de exibição para campos de esquema](./schemas.md#display-names) para obter detalhes.
>
>Depois que um grupo de campos personalizado é salvo e usado em um schema para assimilação de dados, somente alterações aditivas podem ser feitas no grupo de campos depois disso. Consulte as [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar um grupo de campos existente, primeiro abra um esquema que empregue o grupo de campos dentro do [!DNL Schema Editor]. Você pode [selecionar um esquema existente para editar](./schemas.md#edit), ou pode [criar um novo esquema](./schemas.md#create) e adicionar o grupo de campos em questão.

Depois de abrir o schema no editor, você pode iniciar [adicionando campos ao grupo de campos](#add-fields).

## Adicionar campos a um grupo de campos {#add-fields}

Para adicionar campos a um grupo de campos no [!DNL Schema Editor], comece selecionando o nome do grupo de campos no painel à esquerda e selecione o ícone de **mais (+)** ao lado do nome do esquema na tela.

![](../../images/ui/resources/field-groups/add-field.png)

Um **[!UICONTROL Novo campo]** aparece na tela e o painel direito é atualizado para mostrar controles para configurar as propriedades do campo. Consulte o guia em [definindo campos na interface do usuário](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo ao grupo de campos.

Continue a adicionar quantos campos forem necessários ao grupo de campos. Quando terminar, selecione **[!UICONTROL Save]** para salvar o esquema e o grupo de campos.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Se o mesmo grupo de campos já estiver empregado em outros schemas, os campos recém-adicionados serão exibidos automaticamente nesses schemas.

## Próximas etapas

Este guia cobriu como criar e editar grupos de campos usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL Visão geral do espaço de trabalho Schemas]](../overview.md).

Para saber como gerenciar grupos de campos usando a API [!DNL Schema Registry], consulte o [guia de ponto de extremidade de grupos de campos](../../api/field-groups.md).