---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;classe;classes;
solution: Experience Platform
title: Criar e editar classes na interface do usuário
description: Saiba como criar e editar classes na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 5bf729197de53e9d24675c8a1d0455e807fb90c5
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Criar e editar classes na interface do usuário

No Experience Data Model (XDM), as classes definem os aspectos comportamentais dos dados que um schema conterá (registro ou série de tempo). Além disso, as classes descrevem o menor número de propriedades comuns que todos os schemas baseados nessa classe precisariam incluir e fornecer uma maneira de vários conjuntos de dados compatíveis serem mesclados.

O Adobe fornece várias classes XDM padrão (&quot;core&quot;), incluindo [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos para sua organização.

Este documento fornece uma visão geral de como criar, editar e gerenciar classes personalizadas na interface do usuário do Adobe Experience Platform.

## Pré-requisitos

Este guia requer um entendimento prático do sistema XDM. Consulte [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM dentro do ecossistema do Experience Platform, e as [noções básicas da composição do schema](../../schema/composition.md) para saber como as classes contribuem para os schemas XDM.

Embora não seja necessário para este guia, é recomendável que você também siga o tutorial sobre [compondo um schema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Criar uma nova classe {#create}

Na área de trabalho **[!UICONTROL Schemas]**, selecione **[!UICONTROL Criar schema]** e selecione **[!UICONTROL Procurar]** na lista suspensa.

![](../../images/ui/resources/classes/browse-classes.png)

Uma caixa de diálogo é exibida permitindo que você selecione uma lista de classes disponíveis. Na parte superior da caixa de diálogo, selecione **[!UICONTROL Criar nova classe]**. Em seguida, você pode dar um nome de exibição à sua nova classe (um nome curto, descritivo, exclusivo e amigável para a classe), uma descrição e um comportamento para os dados que o schema definirá (&quot;[!UICONTROL Record]&quot; ou &quot;[!UICONTROL Séries de tempo]&quot;).

Quando terminar, selecione **[!UICONTROL Atribuir classe]**.

![](../../images/ui/resources/classes/class-details.png)

O [!DNL Schema Editor] é exibido, mostrando um novo schema na tela que é baseado na classe personalizada que você acabou de criar. Como nenhum campo foi adicionado à classe ainda, o schema contém apenas um campo `_id`, que representa o identificador exclusivo gerado pelo sistema que é automaticamente aplicado a todos os recursos no [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Ao criar um schema que implemente uma classe definida pela sua organização, lembre-se de que as combinações estão disponíveis para uso somente com classes compatíveis. Como a classe definida é nova, não há combinações compatíveis listadas na caixa de diálogo **[!UICONTROL Adicionar mixin]**. Em vez disso, será necessário [criar novas mixins](./mixins.md#create) para usar com essa classe. Na próxima vez que você redigir um schema que implementa a nova classe, as combinações definidas serão listadas e estarão disponíveis para uso.

Agora você pode start [adicionar campos à classe](#add-fields), que será compartilhada por todos os schemas que empregam a classe.

## Editar uma classe existente {#edit}

>[!NOTE]
>
>Somente as classes personalizadas definidas por sua organização podem ser totalmente editadas e personalizadas. Para as classes principais definidas pelo Adobe, somente os nomes para exibição de seus campos podem ser editados no contexto de schemas individuais. Consulte a seção sobre [edição de nomes de exibição para campos de schema](./schemas.md#display-names) para obter detalhes.
>
>Depois que uma classe personalizada é salva e usada na ingestão de dados, somente alterações aditivas podem ser feitas nela posteriormente. Consulte as [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar uma classe existente, selecione a guia **[!UICONTROL Procurar]** e selecione o nome de um schema que emprega a classe que deseja editar.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para ajudar a encontrar o schema com mais facilidade. Consulte o guia em [exploração de recursos XDM](../explore.md) para obter mais informações.

O [!DNL Schema Editor] é exibido, com a estrutura do schema mostrada na tela. Agora você pode start [adicionando campos à classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Adicionar campos a uma classe {#add-fields}

Depois que você tiver um schema que emprega uma classe personalizada aberta no [!UICONTROL Editor de Schemas], poderá start adicionando campos à classe. Para adicionar um novo campo, selecione o ícone **mais (+)** ao lado do nome do schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Lembre-se de que todos os campos adicionados a uma classe serão usados em todos os schemas que empregam essa classe. Portanto, você deve considerar cuidadosamente quais campos serão úteis em todos os casos de uso de schemas. Se você estiver pensando em adicionar um campo que pode ver o uso somente em alguns schemas desta classe, talvez você queira adicionar o campo a esses schemas ao criar uma combinação](./mixins.md#create).[

Um **[!UICONTROL Novo campo]** aparece na tela e o painel direito é atualizado para mostrar controles para configurar as propriedades do campo. Consulte o guia em [definindo campos na interface do usuário](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo à classe.

Continue a adicionar quantos campos forem necessários à classe. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o schema e a classe.

![](../../images/ui/resources/classes/save.png)

Se você tiver criado schemas que empregam essa classe, os campos recém-adicionados aparecerão automaticamente nesses schemas.

## Alterar a classe de um schema {#schema}

É possível alterar a classe do schema em qualquer ponto durante o processo de criação inicial antes que ele seja salvo. Consulte o guia em [criar e editar schemas](./schemas.md#change-class) para obter mais informações.

## Próximas etapas

Este documento abordou a criação e edição de classes usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL visão geral do espaço de trabalho dos Schemas]](../overview.md).

Para saber como gerenciar classes usando a API [!DNL Schema Registry], consulte o [guia de ponto de extremidade de classes](../../api/classes.md).