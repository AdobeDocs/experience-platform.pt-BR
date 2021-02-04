---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;schema;schemas;
solution: Experience Platform
title: Criar e editar schemas na interface do usuário
description: Saiba mais sobre as noções básicas de como criar e editar schemas na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: babe47cc864d9f79eee28989ca8b658350b9d790
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# Criar e editar schemas na interface do usuário

Este guia fornece uma visão geral de como criar, editar e gerenciar schemas do Modelo de Dados de Experiência (XDM) para sua organização na interface do usuário do Adobe Experience Platform.

>[!IMPORTANT]
>
>Os schemas XDM são extremamente personalizáveis e, portanto, as etapas envolvidas na criação de um schema podem variar dependendo do tipo de dados que você deseja que o schema capture. Como resultado, este documento cobre apenas as interações básicas que você pode fazer com schemas na interface do usuário e exclui etapas relacionadas, como personalização de classes, combinações, tipos de dados e campos.
>
>Para um tour completo do processo de criação do schema, siga o tutorial [de criação do schema](../../tutorials/create-schema-ui.md) para criar um schema de exemplo completo e familiarizar-se com os vários recursos do [!DNL Schema Editor].

## Pré-requisitos

Este guia requer um entendimento prático do sistema XDM. Consulte [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM dentro do ecossistema do Experience Platform, e as [noções básicas da composição do schema](../../schema/composition.md) para obter uma visão geral de como os schemas são construídos.

## Criar um novo schema {#create}

Na área de trabalho [!UICONTROL Schemas], selecione **[!UICONTROL Criar schema]** no canto superior direito. Na lista suspensa que é exibida, você pode escolher entre **[!UICONTROL Perfil individual XDM]** e **[!UICONTROL ExperienceEvent XDM]** como a classe base do schema. Como alternativa, você pode selecionar **[!UICONTROL Procurar]** para selecionar na lista completa das classes disponíveis, ou [criar uma nova classe personalizada](./classes.md#create) em vez disso.

![](../../images/ui/resources/schemas/create-schema.png)

Após selecionar uma classe, [!DNL Schema Editor] será exibido e a estrutura base do schema (fornecida pela classe) será mostrada na tela. Aqui, você pode usar o painel direito para adicionar um **[!UICONTROL Nome de exibição]** e **[!UICONTROL Descrição]** para o schema.

![](../../images/ui/resources/schemas/schema-details.png)

Agora você pode criar o start de criar a estrutura do schema ao adicionar [mixins](#add-mixins).

## Editar um schema existente {#edit}

>[!NOTE]
>
>Depois que um schema é salvo e usado na ingestão de dados, somente alterações aditivas podem ser feitas nele. Consulte as [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar um schema existente, selecione a guia **[!UICONTROL Procurar]** e selecione o nome do schema que deseja editar.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para ajudar a encontrar o schema com mais facilidade. Consulte o guia em [exploração de recursos XDM](../explore.md) para obter mais informações.

Após selecionar um schema, o [!DNL Schema Editor] será exibido com a estrutura do schema mostrada na tela. Agora você pode [adicionar mixins](#add-mixins) ao schema, [editar nomes de exibição de campos](#display-names) ou [editar mixins personalizados existentes](./mixins.md#edit) se o schema empregar algum.

## Adicionar misturas a um schema {#add-mixins}

>[!NOTE]
>
>Esta seção aborda como adicionar misturas existentes a um schema. Se quiser criar uma nova combinação personalizada, consulte o guia em [criar e editar mixins](./mixins.md#create).

Depois de abrir um schema dentro de [!DNL Schema Editor], é possível adicionar campos ao schema por meio do uso de mixins. Para start, selecione **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Mixins]** no painel esquerdo.

![](../../images/ui/resources/schemas/add-mixin-button.png)

Uma caixa de diálogo é exibida mostrando uma lista de combinações que você pode selecionar para o schema. Como as misturas são compatíveis apenas com uma classe, somente as misturas associadas à classe selecionada do schema serão listadas. Por padrão, as misturas listadas são classificadas com base na popularidade de uso dentro da organização.

![](../../images/ui/resources/schemas/mixin-popularity.png)

Você pode usar a barra de pesquisa para ajudar a localizar a combinação desejada. As misturas cujo nome corresponde ao query são exibidas na parte superior da lista. Em **[!UICONTROL Campos padrão]**, as combinações que contêm campos que descrevem os atributos de dados desejados são exibidas.

![](../../images/ui/resources/schemas/mixin-search.png)

Marque a caixa de seleção ao lado do nome da mistura que você deseja adicionar ao schema. É possível selecionar várias combinações na lista, com cada combinação selecionada aparecendo no painel direito.

![](../../images/ui/resources/schemas/add-mixin.png)

>[!TIP]
>
>Para qualquer combinação listada, você pode passar o mouse ou focar no ícone de informações (![](../../images/ui/resources/schemas/info-icon.png)) para visualização de uma breve descrição do tipo de dados capturados pela mistura. Você também pode selecionar o ícone de pré-visualização (![](../../images/ui/resources/schemas/preview-icon.png)) para visualização da estrutura dos campos fornecidos pelo mixin antes de decidir adicioná-lo ao schema.

Depois de escolher suas combinações, selecione **[!UICONTROL Adicionar mixin]** para adicioná-las ao schema.

![](../../images/ui/resources/schemas/add-mixin-finish.png)

O [!DNL Schema Editor] reaparece com os campos fornecidos pela combinação representados na tela.

![](../../images/ui/resources/schemas/mixins-added.png)

## Ative um schema para o Perfil do cliente em tempo real {#profile}

[Os ](../../../profile/home.md) Perfis de clientes em tempo real emergem dados de fontes diferentes para construir uma visualização completa de cada cliente individual. Se quiser que os dados capturados por um schema participem desse processo, ative o schema para uso em [!DNL Profile].

>[!IMPORTANT]
>
>Para habilitar um schema para [!DNL Profile], ele deve ter um campo de identidade primário definido. Consulte o guia em [definindo campos de identidade](../fields/identity.md) para obter mais informações.

Para habilitar o schema, selecione o nome do schema no painel esquerdo e, em seguida, selecione o botão **[!UICONTROL Perfil]** no painel direito.

![](../../images/ui/resources/schemas/profile-toggle.png)

Um schema é exibido, avisando que, uma vez ativado e salvo, ele não pode ser desativado. Selecione **[!UICONTROL Ativar]** para continuar.

![](../../images/ui/resources/schemas/profile-confirm.png)

A tela de desenho é exibida novamente com a alternância [!UICONTROL Perfil] ativada.

>[!IMPORTANT]
>
>Como o schema ainda não foi salvo, este é o ponto de não retorno se você mudar de ideia sobre permitir que o schema participe do Perfil do cliente em tempo real: depois de salvar um schema ativado, ele não poderá mais ser desativado. Selecione a alternância **[!UICONTROL Perfil]** novamente para desativar o schema.

Para concluir o processo, selecione **[!UICONTROL Salvar]** para salvar o schema.

![](../../images/ui/resources/schemas/profile-enabled.png)

O schema agora está habilitado para uso no Perfil do cliente em tempo real. Quando a Platform ingressar dados em conjuntos de dados baseados nesse schema, esses dados serão incorporados aos dados do Perfil agrupado.

## Editar nomes de exibição para campos de schema {#display-names}

Depois de atribuir uma classe e adicionar combinações a um schema, você pode editar os nomes de exibição de qualquer um dos campos do schema, independentemente de esses campos terem sido fornecidos por recursos XDM padrão ou personalizados.

>[!NOTE]
>
>Lembre-se de que os nomes de exibição de campos que pertencem a classes ou combinações padrão só podem ser editados no contexto de um schema específico. Em outras palavras, alterar o nome de exibição de um campo padrão em um schema não afeta outros schemas que usam a mesma classe ou combinação associada.

Para editar o nome de exibição de um campo de schema, selecione o campo na tela. No painel direito, forneça o novo nome em **[!UICONTROL Nome de exibição]**.

![](../../images/ui/resources/schemas/display-name.png)

Selecione **[!UICONTROL Aplicar]** no painel direito e a tela é atualizada para mostrar o novo nome de exibição do campo. Selecione **[!UICONTROL Salvar]** para aplicar as alterações ao schema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Alterar uma classe de schema {#change-class}

É possível alterar a classe de um schema em qualquer ponto durante o processo de composição inicial antes que o schema seja salvo.

>[!WARNING]
>
>A reatribuição da classe para um schema deve ser feita com extrema cautela. Misturas são compatíveis somente com certas classes, e, portanto, alterar a classe redefinirá a tela de desenho e quaisquer campos adicionados.

Para reatribuir uma classe, selecione **[!UICONTROL Atribuir]** no lado esquerdo da tela.

![](../../images/ui/resources/schemas/assign-class-button.png)

Será exibida uma caixa de diálogo que exibe uma lista de todas as classes disponíveis, incluindo qualquer classe definida por sua organização (sendo o proprietário &quot;[!UICONTROL Customer]&quot;), bem como as classes padrão definidas pelo Adobe.

Selecione uma classe na lista para exibir sua descrição no lado direito da caixa de diálogo. Você também pode selecionar **[!UICONTROL estrutura de classe de Pré-visualização]** para ver os campos e metadados associados à classe. Selecione **[!UICONTROL Atribuir classe]** para continuar.

![](../../images/ui/resources/schemas/assign-class.png)

Uma nova caixa de diálogo é aberta, solicitando que você confirme que deseja atribuir uma nova classe. Selecione **[!UICONTROL Atribuir]** para confirmar.

![](../../images/ui/resources/schemas/assign-confirm.png)

Após confirmar a alteração de classe, a tela será redefinida e todo o progresso da composição será perdido.

## Próximas etapas

Este documento abordou as noções básicas de criação e edição de schemas na interface do usuário da plataforma. É altamente recomendável que você reveja o tutorial de [criação de schemas](../../tutorials/create-schema-ui.md) para obter um fluxo de trabalho abrangente para a criação de um schema completo na interface do usuário, incluindo a criação de mixins personalizados e tipos de dados para casos de uso exclusivos.

Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL visão geral do espaço de trabalho dos Schemas]](../overview.md).

Para saber como gerenciar schemas na API [!DNL Schema Registry], consulte o [guia de ponto de extremidade de schemas](../../api/schemas.md).