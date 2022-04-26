---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; classe; classes;
solution: Experience Platform
title: Criar e editar classes na interface do usuário
description: Saiba como criar e editar classes na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c83b5616f46f6f7d752979fa66a66fad16f16102
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---

# Criar e editar classes na interface do usuário

No Experience Data Model (XDM), as classes definem os aspectos comportamentais dos dados que um schema conterá (registro ou série de tempo). Além disso, as classes descrevem o menor número de propriedades comuns que todos os esquemas baseados nessa classe precisariam incluir e fornecer uma maneira de vários conjuntos de dados compatíveis serem mesclados.

O Adobe fornece várias classes XDM padrão (&quot;core&quot;), incluindo [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos da sua organização.

Este documento fornece uma visão geral de como criar, editar e gerenciar classes personalizadas na interface do usuário do Adobe Experience Platform.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para uma introdução ao papel do XDM no ecossistema do Experience Platform, e [noções básicas da composição do schema](../../schema/composition.md) para saber como as classes contribuem com os esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir também o tutorial em [composição de um esquema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Criar uma nova classe {#create}

No **[!UICONTROL Esquemas]** espaço de trabalho, selecione **[!UICONTROL Criar esquema]**, em seguida selecione **[!UICONTROL Procurar]** na lista suspensa.

![](../../images/ui/resources/classes/browse-classes.png)

Uma caixa de diálogo é exibida e permite selecionar a partir de uma lista de classes disponíveis. Na parte superior da caixa de diálogo, selecione **[!UICONTROL Criar nova classe]**. Em seguida, você pode fornecer um nome de exibição para a nova classe (um nome curto, descritivo, exclusivo e amigável para a classe), uma descrição e um comportamento para os dados que o schema definirá (&quot;[!UICONTROL Registro]&quot; ou &quot;[!UICONTROL Série cronológica]&quot;).

Quando terminar, selecione **[!UICONTROL Atribuir classe]**.

![](../../images/ui/resources/classes/class-details.png)

O [!DNL Schema Editor] for exibido, mostrando um novo schema na tela com base na classe personalizada que você acabou de criar. Como nenhum campo foi adicionado à classe ainda, o schema contém apenas um `_id` , que representa o identificador exclusivo gerado pelo sistema aplicado automaticamente a todos os recursos no [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Ao criar um schema que implementa uma classe definida pela organização, lembre-se de que os grupos de campos de esquema estão disponíveis para uso somente com classes compatíveis. Como a classe que você definiu é nova, não há grupos de campos compatíveis listados na **[!UICONTROL Adicionar grupo de campos]** caixa de diálogo. Em vez disso, será necessário [criar novos grupos de campos](./field-groups.md#create) para uso com essa classe. Na próxima vez que você compor um schema que implementa a nova classe, os grupos de campos definidos serão listados e estarão disponíveis para uso.

Agora você pode começar [adicionar campos à classe](#add-fields), que será compartilhado por todos os schemas que empregam a classe .

## Editar uma classe existente {#edit}

>[!IMPORTANT]
>
>As classes personalizadas criadas após 30 de abril de 2022 não podem ser editadas diretamente e uma correção está em desenvolvimento no momento. Como solução alternativa, você pode [criar um grupo de campos personalizado](./field-groups.md) e reutilize-o para cada schema que usa a classe personalizada que deseja estender. As classes personalizadas criadas antes de 30 de abril de 2022 não são afetadas por essa limitação.

>[!NOTE]
>
>Somente as classes personalizadas definidas pela sua organização podem ser totalmente editadas e personalizadas. Para classes principais definidas por Adobe, somente os nomes de exibição de seus campos podem ser editados no contexto de schemas individuais. Consulte a seção sobre [edição de nomes de exibição para campos de esquema](./schemas.md#display-names) para obter detalhes.
>
>Depois que uma classe personalizada é salva e usada na assimilação de dados, somente alterações aditivas podem ser feitas a ela depois. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar uma classe existente, selecione a **[!UICONTROL Procurar]** e selecione o nome de um schema que emprega a classe que deseja editar.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para ajudar a encontrar o esquema mais fácil. Consulte o guia sobre [exploração de recursos XDM](../explore.md) para obter mais informações.

O [!DNL Schema Editor] for exibida, com a estrutura do esquema mostrada na tela. Agora você pode começar [adicionar campos à classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Adicionar campos a uma classe {#add-fields}

>[!IMPORTANT]
>
>As classes personalizadas criadas após 30 de abril de 2022 não podem ser editadas diretamente e uma correção está em desenvolvimento no momento. Como solução alternativa, você pode [criar um grupo de campos personalizado](./field-groups.md) e reutilize-o para cada schema que usa a classe personalizada que deseja estender. As classes personalizadas criadas antes de 30 de abril de 2022 não são afetadas por essa limitação.

Depois de ter um schema que emprega uma classe personalizada aberta no [!UICONTROL Editor de esquema], você pode começar a adicionar campos à classe . Para adicionar um novo campo, selecione o **mais (+)** ícone ao lado do nome do schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Lembre-se de que quaisquer campos adicionados a uma classe serão usados em todos os esquemas que empregam essa classe. Portanto, você deve considerar cuidadosamente quais campos serão úteis em todos os casos de uso do schema. Se estiver pensando em adicionar um campo que pode ver o uso somente em alguns schemas desta classe, considere adicioná-lo a esses esquemas por [criação de um grupo de campos](./field-groups.md#create) em vez disso.

A **[!UICONTROL Novo campo]** aparece na tela e o painel direito é atualizado para mostrar controles para configurar as propriedades do campo. Consulte o guia sobre [definição de campos na interface do usuário](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo à classe .

Continue a adicionar quantos campos forem necessários à classe. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o schema e a classe .

![](../../images/ui/resources/classes/save.png)

Se você tiver criado esquemas que empregam essa classe anteriormente, os campos recém-adicionados aparecerão automaticamente nesses esquemas.

## Alterar a classe de um schema {#schema}

Você pode alterar a classe do schema em qualquer ponto durante o processo de criação inicial antes que ele seja salvo. Consulte o guia sobre [criação e edição de schemas](./schemas.md#change-class) para obter mais informações.

## Próximas etapas

Este documento cobriu como criar e editar classes usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos da [!UICONTROL Esquemas] espaço de trabalho, consulte o [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar classes usando o [!DNL Schema Registry] API, consulte o [guia de endpoint de classes](../../api/classes.md).
