---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, modelo de dados, ui, espaço de trabalho, esquema, esquemas;
solution: Experience Platform
title: Criar e editar esquemas na interface do usuário
description: Saiba mais sobre as noções básicas de como criar e editar esquemas na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 6402499535b71f43c158fcec7e2b0065437bed51
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Criar e editar esquemas na interface do usuário

Este guia fornece uma visão geral de como criar, editar e gerenciar esquemas do Experience Data Model (XDM) para sua organização na interface do usuário do Adobe Experience Platform.

>[!IMPORTANT]
>
>Os esquemas XDM são extremamente personalizáveis e, portanto, as etapas envolvidas na criação de um esquema podem variar dependendo do tipo de dados que você deseja que o esquema capture. Como resultado, este documento cobre apenas as interações básicas que você pode fazer com esquemas na interface do usuário e exclui etapas relacionadas, como personalização de classes, grupos de campos de esquema, tipos de dados e campos.
>
>Para um tour completo do processo de criação do schema, siga o [tutorial de criação de schema](../../tutorials/create-schema-ui.md) para criar um schema de exemplo completo e se familiarizar com os muitos recursos do [!DNL Schema Editor].

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM no ecossistema do Experience Platform e as [noções básicas da composição do schema](../../schema/composition.md) para obter uma visão geral de como os schemas são construídos.

## Criar um novo schema {#create}

No espaço de trabalho [!UICONTROL Schemas], selecione **[!UICONTROL Criar esquema]** no canto superior direito. Na lista suspensa que aparece, você pode escolher entre **[!UICONTROL Perfil individual XDM]** e **[!UICONTROL XDM ExperienceEvent]** como a classe base do esquema. Como alternativa, você pode selecionar **[!UICONTROL Procurar]** para selecionar na lista completa de classes disponíveis, ou [criar uma nova classe personalizada](./classes.md#create) em vez disso.

![](../../images/ui/resources/schemas/create-schema.png)

Depois de selecionar uma classe, o [!DNL Schema Editor] aparece e a estrutura base do esquema (fornecida pela classe) é mostrada na tela. Aqui, você pode usar o painel direito para adicionar um **[!UICONTROL Display name]** e **[!UICONTROL Description]** ao schema.

![](../../images/ui/resources/schemas/schema-details.png)

Agora é possível começar a criar a estrutura do schema adicionando [grupos de campos de esquema](#add-field-groups).

## Editar um esquema existente {#edit}

>[!NOTE]
>
>Depois que um schema é salvo e usado na assimilação de dados, somente alterações aditivas podem ser feitas nele. Consulte as [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar um schema existente, selecione a guia **[!UICONTROL Browse]** e selecione o nome do schema que deseja editar.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para ajudar a encontrar o esquema mais fácil. Consulte o guia sobre [exploração de recursos XDM](../explore.md) para obter mais informações.

Depois de selecionar um schema, o [!DNL Schema Editor] aparece com a estrutura do schema mostrada na tela. Agora é possível [adicionar grupos de campos](#add-field-groups) ao esquema, [editar nomes de exibição de campos](#display-names) ou [editar grupos de campos personalizados existentes](./field-groups.md#edit) se o esquema empregar algum.

## Adicionar grupos de campos a um schema {#add-field-groups}

>[!NOTE]
>
>Esta seção aborda como adicionar grupos de campos existentes a um schema. Se quiser criar um novo grupo de campos personalizado, consulte o guia em [criar e editar grupos de campos](./field-groups.md#create).

Após abrir um schema dentro do [!DNL Schema Editor], é possível adicionar campos ao schema por meio do uso de grupos de campos. Para iniciar, selecione **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]** no painel esquerdo.

![](../../images/ui/resources/schemas/add-field-group-button.png)

Uma caixa de diálogo é exibida mostrando uma lista de grupos de campos que você pode selecionar para o esquema. Como os grupos de campos são compatíveis apenas com uma classe, somente os grupos de campos associados à classe selecionada do esquema serão listados. Por padrão, os grupos de campos listados são classificados com base em sua popularidade de uso em sua organização.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Se você souber a atividade geral ou a área comercial dos campos que deseja adicionar, selecione uma ou mais categorias verticais do setor no painel à esquerda para filtrar a lista exibida de grupos de campo.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Para obter mais informações sobre as práticas recomendadas para modelagem de dados específica do setor no XDM, consulte a documentação sobre [modelos de dados do setor](../../schema/industries/overview.md).

Também é possível usar a barra de pesquisa para ajudar a localizar o grupo de campos desejado. Os grupos de campos cujo nome corresponde ao query são exibidos na parte superior da lista. Em **[!UICONTROL Campos padrão]**, grupos de campos contendo campos que descrevem os atributos de dados desejados são exibidos.

![](../../images/ui/resources/schemas/field-group-search.png)

Marque a caixa de seleção ao lado do nome do grupo de campos que deseja adicionar ao schema. É possível selecionar vários grupos de campos na lista, com cada grupo de campos selecionado aparecendo no painel direito.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Para qualquer grupo de campos listado, você pode passar o mouse ou focar no ícone de informações (![](../../images/ui/resources/schemas/info-icon.png)) para exibir uma breve descrição do tipo de dados que o grupo de campos captura. Você também pode selecionar o ícone de visualização (![](../../images/ui/resources/schemas/preview-icon.png)) para exibir a estrutura dos campos que o grupo de campos fornece antes de decidir adicioná-lo ao schema.

Depois de escolher os grupos de campos, selecione **[!UICONTROL Add field groups]** para adicioná-los ao esquema.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

O [!DNL Schema Editor] é exibido novamente com os campos fornecidos pelo grupo de campos representados na tela.

![](../../images/ui/resources/schemas/field-groups-added.png)

## Ativar um esquema para o Perfil do cliente em tempo real {#profile}

[Os ](../../../profile/home.md) Perfis do cliente em tempo real emergem dados de fontes diferentes para construir uma visualização completa de cada cliente individual. Se desejar que os dados capturados por um schema participem neste processo, é necessário habilitar o schema para uso em [!DNL Profile].

>[!IMPORTANT]
>
>Para habilitar um schema para [!DNL Profile], ele deve ter um campo de identidade primário definido. Consulte o guia em [definindo campos de identidade](../fields/identity.md) para obter mais informações.

Para ativar o schema, comece selecionando o nome do schema no painel à esquerda e selecione o botão **[!UICONTROL Profile]** no painel à direita.

![](../../images/ui/resources/schemas/profile-toggle.png)

Um provedor é exibido, avisando que, uma vez que um esquema foi ativado e salvo, ele não poderá ser desativado. Selecione **[!UICONTROL Ativar]** para continuar.

![](../../images/ui/resources/schemas/profile-confirm.png)

A tela é exibida novamente com a opção [!UICONTROL Profile] ativada.

>[!IMPORTANT]
>
>Como o esquema ainda não foi salvo, esse é o ponto de não retorno se você mudar de ideia sobre permitir que o esquema participe do Perfil do cliente em tempo real: depois de salvar um schema ativado, ele não poderá mais ser desativado. Selecione a opção **[!UICONTROL Profile]** novamente para desativar o esquema.

Para concluir o processo, selecione **[!UICONTROL Save]** para salvar o esquema.

![](../../images/ui/resources/schemas/profile-enabled.png)

O esquema agora está ativado para uso no Perfil do cliente em tempo real. Quando a Platform assimila dados em conjuntos de dados com base nesse esquema, esses dados serão incorporados aos dados do Perfil amalgamado.

## Editar nomes de exibição para campos de esquema {#display-names}

Depois de atribuir uma classe e adicionar grupos de campos a um esquema, você pode editar os nomes de exibição de qualquer um dos campos do esquema, independentemente desses campos terem sido fornecidos por recursos XDM padrão ou personalizados.

>[!NOTE]
>
>Lembre-se de que os nomes de exibição dos campos que pertencem a classes ou grupos de campos padrão só podem ser editados no contexto de um schema específico. Em outras palavras, alterar o nome de exibição de um campo padrão em um schema não afeta outros esquemas que empregam a mesma classe ou grupo de campos associado.
>
>Depois de fazer alterações nos nomes de exibição dos campos de um esquema, essas alterações são refletidas imediatamente em qualquer conjunto de dados existente com base nesse esquema.

Para editar o nome de exibição de um campo de esquema, selecione o campo na tela. No painel direito, forneça o novo nome em **[!UICONTROL Display name]**.

![](../../images/ui/resources/schemas/display-name.png)

Selecione **[!UICONTROL Aplicar]** no painel à direita e a tela será atualizada para mostrar o novo nome de exibição do campo. Selecione **[!UICONTROL Save]** para aplicar as alterações ao esquema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Alterar a classe de um esquema {#change-class}

Você pode alterar a classe de um schema em qualquer ponto durante o processo de composição inicial antes que o schema tenha sido salvo.

>[!WARNING]
>
>A reatribuição da classe para um schema deve ser feita com extremo cuidado. Os grupos de campos são compatíveis apenas com determinadas classes e, portanto, alterar a classe redefinirá a tela e quaisquer campos adicionados.

Para reatribuir uma classe, selecione **[!UICONTROL Assign]** no lado esquerdo da tela.

![](../../images/ui/resources/schemas/assign-class-button.png)

Uma caixa de diálogo é exibida mostrando uma lista de todas as classes disponíveis, incluindo qualquer classe definida por sua organização (o proprietário sendo &quot;[!UICONTROL Customer]&quot;), bem como classes padrão definidas pelo Adobe.

Selecione uma classe na lista para exibir sua descrição no lado direito da caixa de diálogo. Você também pode selecionar **[!UICONTROL Visualizar estrutura de classe]** para ver os campos e metadados associados à classe. Selecione **[!UICONTROL Atribuir classe]** para continuar.

![](../../images/ui/resources/schemas/assign-class.png)

Uma nova caixa de diálogo é aberta, solicitando que você confirme que deseja atribuir uma nova classe. Selecione **[!UICONTROL Atribuir]** para confirmar.

![](../../images/ui/resources/schemas/assign-confirm.png)

Após confirmar a alteração de classe, a tela será redefinida e todo o progresso da composição será perdido.

## Próximas etapas

Este documento abordou as noções básicas para a criação e edição de schemas na interface do usuário da plataforma. É altamente recomendável revisar o [tutorial de criação de esquema](../../tutorials/create-schema-ui.md) para obter um fluxo de trabalho abrangente para criar um schema completo na interface do usuário, incluindo a criação de grupos de campos personalizados e tipos de dados para casos de uso exclusivos.

Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL Visão geral do espaço de trabalho Schemas]](../overview.md).

Para saber como gerenciar schemas na API [!DNL Schema Registry], consulte o [guia de ponto de extremidade de schemas](../../api/schemas.md).
