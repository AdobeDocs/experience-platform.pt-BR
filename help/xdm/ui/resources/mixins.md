---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;mixin;mixins;
solution: Experience Platform
title: Criar e editar combinações na interface do usuário
description: Saiba como criar e editar mixins na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Criar e editar combinações na interface do usuário

No Experience Data Model (XDM), as combinações são componentes reutilizáveis que definem um ou mais campos que implementam determinadas funções, como detalhes pessoais, preferências de hotel ou endereço. As misturas devem ser incluídas como parte de um schema que implementa uma classe compatível.

Uma mistura define a(s) classe(s) com a qual é compatível, com base no comportamento dos dados que a mistura representa (registro ou série de tempo). Isso significa que nem todas as combinações estão disponíveis para uso com todas as classes.

A Adobe Experience Platform fornece várias combinações padrão que abrangem uma grande variedade de casos de uso de marketing. No entanto, você também pode criar e editar suas próprias misturas personalizadas para definir conceitos adicionais relacionados à sua empresa dentro dos schemas XDM. Este guia fornece uma visão geral de como criar, editar e gerenciar misturas personalizadas para sua organização na interface do usuário da plataforma.

## Pré-requisitos

Este guia requer um entendimento prático do sistema XDM. Consulte [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM dentro do ecossistema do Experience Platform, e as [noções básicas da composição do schema](../../schema/composition.md) para saber como as misturas contribuem para os schemas XDM.

Embora não seja necessário para este guia, é recomendável que você também siga o tutorial sobre [compondo um schema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Criar uma nova mistura {#create}

Para criar uma nova mistura, é necessário selecionar primeiro um schema ao qual a mistura será adicionada. Você pode optar por [criar um novo schema](./schemas.md#create) ou [selecionar um schema existente para editar](./schemas.md#edit).

Depois de abrir o schema na seção [!DNL Schema Editor], selecione **[!UICONTROL Adicionar]** ao lado da seção [!UICONTROL Mixins] no painel esquerdo.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Uma caixa de diálogo é exibida, mostrando uma lista de combinações existentes para sua organização. Próximo à parte superior da caixa de diálogo, selecione **[!UICONTROL Criar nova mistura]**. Aqui você pode fornecer um **[!UICONTROL Nome de exibição]** e **[!UICONTROL Descrição]** para a combinação. Quando terminar, selecione **[!UICONTROL Adicionar mistura]**.

![](../../images/ui/resources/mixins/create-mixin.png)

O [!DNL Schema Editor] reaparece, com a nova combinação listada no painel esquerdo. Como essa é uma mistura totalmente nova, ela não fornece nenhum campo para o schema e, portanto, a tela permanece inalterada. Agora você pode start [adicionando campos ao mixin](#add-fields).

## Editar uma mistura existente {#edit}

>[!NOTE]
>
>Somente misturas personalizadas definidas pela sua organização podem ser editadas.
>
>Além disso, uma vez guardada e utilizada uma mistura num schema para ingestão de dados, só podem ser efetuadas alterações aditivas à mistura a partir daí. Consulte as [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar uma mistura existente, primeiro abra um schema que utilize a mistura dentro de [!DNL Schema Editor]. Você pode [selecionar um schema existente para editar](./schemas.md#edit) ou [criar um novo schema](./schemas.md#create) e adicionar a mistura em questão.

Depois que o schema for aberto no editor, você poderá start [adicionando campos ao mixin](#add-fields).

## Adicionar campos a uma combinação {#add-fields}

Para adicionar campos a uma mistura no start [!DNL Schema Editor], selecione o nome da mistura no painel esquerdo e, em seguida, selecione o ícone **mais (+)** ao lado do nome do schema na tela.

![](../../images/ui/resources/mixins/add-field-button.png)

Um **[!UICONTROL Novo campo]** aparece na tela e o painel direito é atualizado para mostrar controles para configurar as propriedades do campo. Consulte o guia em [definindo campos na interface do usuário](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo ao mixin.

Continue a adicionar quantos campos forem necessários ao mixin. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o schema e o mixin.

![](../../images/ui/resources/mixins/complete-mixin.png)

Se a mesma combinação já estiver empregada em outros schemas, os campos recém-adicionados aparecerão automaticamente nesses schemas.

## Próximas etapas

Este guia aborda como criar e editar misturas usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL visão geral do espaço de trabalho dos Schemas]](../overview.md).

Para saber como gerenciar misturas usando a API [!DNL Schema Registry], consulte o [guia de ponto de extremidade de mixins](../../api/mixins.md).