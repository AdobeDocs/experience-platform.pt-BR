---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;classe;classes;
solution: Experience Platform
title: Criar e editar classes na interface
description: Saiba como criar e editar classes na interface do usuário do Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 02b709c01347c1d03f870132dff437b97f239a9c
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 5%

---

# Criar e editar classes na interface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtro de classe padrão ou personalizada"
>abstract="A lista de classes disponíveis é pré-filtrada com base em como elas foram criadas. Selecione o botão de opção para escolher entre as opções Padrão e Personalizado. A opção Padrão mostra entidades criadas pela Adobe e inclui as classes Perfil individual XDM e Evento de experiência XDM. A opção Personalizado exibe entidades criadas em sua organização. Consulte a documentação para saber mais sobre criação e edição de classes."

Na Adobe Experience Platform, a classe de um esquema define os aspectos comportamentais dos dados que o esquema conterá (registro ou série temporal). Além disso, as classes descrevem o menor número de propriedades comuns que todos os esquemas baseados nessa classe precisariam incluir e fornecem uma maneira de vários conjuntos de dados compatíveis serem mesclados.

O Adobe fornece várias classes padrão (&quot;núcleo&quot;) do Experience Data Model (XDM), incluindo o [Perfil Individual XDM](../../classes/individual-profile.md) e o [XDM ExperienceEvent](../../classes/experienceevent.md). Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos para sua organização.

Este documento fornece uma visão geral de como criar, editar e gerenciar classes personalizadas na interface do usuário do Experience Platform.

## Pré-requisitos {#prerequisites}

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM no ecossistema de Experience Platform e as [noções básicas da composição de esquema](../../schema/composition.md) para saber como as classes contribuem para os esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir o tutorial sobre [composição de um esquema na interface](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do Editor de esquemas.

## Introdução {#getting-started}

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o espaço de trabalho [!UICONTROL Esquemas] e selecione a guia **[!UICONTROL Classes]**. Uma lista de classes disponíveis é exibida.

![O número de classes dentro da guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] [!UICONTROL Classes] e [!UICONTROL Esquemas] destacados.](../../images/ui/resources/classes/available-classes.png)

## Filtrar classes {#filter}

A lista de classes é automaticamente filtrada com base em como foram criadas. A configuração padrão exibe as classes definidas pelo Adobe. Também é possível filtrar a lista para mostrar os criados por sua organização. Selecione o botão de opção para escolher entre as opções [!UICONTROL Padrão] e [!UICONTROL Personalizado]. A opção [!UICONTROL Padrão] mostra entidades criadas pelo Adobe e a opção [!UICONTROL Personalizado] exibe entidades criadas na sua organização.

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com [!UICONTROL Padrão] e [!UICONTROL Personalizado] destacados.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Use os recursos de pesquisa para filtrar ou localizar uma classe com base em seu nome. Consulte o guia em [explorando recursos XDM](../explore.md) para obter mais informações.

## Criar uma nova classe {#create}

Há dois métodos para criar uma classe na interface do usuário da Platform, por meio de **[!UICONTROL Criar classe]** ou **[!UICONTROL Criar esquema]**.

### Criar classe

Selecione **[!UICONTROL Criar classe]** na guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas].

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com [!UICONTROL Criar classe] realçada](../../images/ui/resources/classes/create-class.png)

A caixa de diálogo [!UICONTROL Criar classe] é exibida. Insira um [!UICONTROL Nome de exibição] e uma [!UICONTROL Descrição] para sua classe e escolha o comportamento pretendido para sua classe com os botões de opção. As classes podem ser do tipo [!UICONTROL Registro] ou [!UICONTROL Série temporal]. Selecione **[!UICONTROL Criar]** para confirmar suas escolhas e retornar à guia [!UICONTROL Classes].

![A caixa de diálogo [!UICONTROL Criar classe] com [!UICONTROL Criar] foi realçada.](../../images/ui/resources/classes/create-class-dialog.png)

A classe criada está disponível e listada no modo de exibição [!UICONTROL Classes].

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com a classe criada recentemente realçada.](../../images/ui/resources/classes/new-class-listing.png)

### Criar esquema

Como alternativa, você pode criar uma classe criando um esquema manualmente. Selecione **[!UICONTROL Criar esquema]** na guia [!UICONTROL Classes] no espaço de trabalho [!UICONTROL Esquemas].

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com [!UICONTROL Criar esquema] realçada](../../images/ui/resources/classes/create-schema.png)

Selecione **[!UICONTROL Manual]** na caixa de diálogo [!UICONTROL Criar um esquema] exibida.

>[!NOTE]
>
>Se você usar o fluxo de trabalho de criação do esquema assistido por aprendizado de máquina, será possível fazer upload de um arquivo e usar algoritmos de aprendizado de máquina para gerar um esquema recomendado. Nesse fluxo de trabalho de criação de esquema, não é necessário especificar a classe base do esquema. Para saber como o ML pode recomendar uma estrutura de esquema com base em um arquivo csv, consulte o [guia de criação de esquema assistido por aprendizado de máquina](../ml-assisted-schema-creation.md).

![A caixa de diálogo Criar um esquema com as opções de fluxo de trabalho e selecione realçada.](../../images/ui/resources/classes/manually-create-a-schema.png)

O workflow de criação do schema é exibido. Na seção [!UICONTROL Detalhes do esquema], selecione **[!UICONTROL Outros]**. Uma lista de classes disponíveis é exibida. Selecione **[!UICONTROL Criar classe]**.

![O fluxo de trabalho [!UICONTROL Criar esquema] com [!UICONTROL Outros] realçado na seção [!UICONTROL Detalhes do esquema].](../../images/ui/resources/classes/other-schema-details.png)

A caixa de diálogo [!UICONTROL Criar classe] é exibida. Insira um [!UICONTROL Nome de exibição] e uma [!UICONTROL Descrição] para sua classe e escolha o comportamento pretendido para sua classe com os botões de opção. As classes podem ser do tipo [!UICONTROL Registro] ou [!UICONTROL Série temporal]. Selecione **[!UICONTROL Criar]** para confirmar suas escolhas e retornar à guia [!UICONTROL Classes].

![A caixa de diálogo [!UICONTROL Criar classe] com [!UICONTROL Criar] foi realçada.](../../images/ui/resources/classes/create-class-from-schema.png)

A lista de classes é atualizada na seção [!UICONTROL Detalhes do esquema], e sua classe recém-criada é selecionada automaticamente. Selecione **[!UICONTROL Avançar]** para continuar criando seu esquema.

![A seção [!UICONTROL Detalhes do esquema] com a nova classe selecionada e [!UICONTROL Próximo] realçado.](../../images/ui/resources/classes/select-new-class.png)

Após selecionar uma classe, a seção [!UICONTROL Nome e revisão] é exibida. Nesta seção, você fornece um nome e uma descrição para identificar o esquema. &#x200B;A estrutura base do esquema (fornecida pela classe) é mostrada na tela para que você revise e verifique a classe selecionada e a estrutura do esquema.

Insira um [!UICONTROL Nome para exibição do esquema] amigável no campo de texto. Em seguida, insira uma descrição adequada para ajudar a identificar seu esquema. Quando tiver revisado a estrutura do esquema e estiver satisfeito com as configurações, selecione **[!UICONTROL Concluir]** para criar o esquema.

![A seção [!UICONTROL Nome e revisão] do fluxo de trabalho [!UICONTROL Criar esquema] com o [!UICONTROL Nome para exibição do esquema], [!UICONTROL Descrição] e [!UICONTROL Término] realçados.](../../images/ui/resources/classes/schema-details.png)

## Adicionar campos a uma classe {#add-fields}

Depois que você tiver um esquema que emprega uma classe personalizada aberta no Editor de esquemas, poderá começar a adicionar campos à classe. Para adicionar um novo campo, selecione o ícone **de adição (+)** ao lado do nome do esquema.

>[!IMPORTANT]
>
>Ao criar um esquema que implementa uma classe definida por sua organização, lembre-se de que os grupos de campos de esquema estão disponíveis para uso somente com classes compatíveis. Como a classe definida é nova, não há grupos de campos compatíveis listados na caixa de diálogo **[!UICONTROL Adicionar grupo de campos]**. Em vez disso, você precisará [criar novos grupos de campos](./field-groups.md#create) para usar com essa classe. Na próxima vez que você compor um schema que implementa a nova classe, os grupos de campos definidos serão listados e estarão disponíveis para uso.

![O Editor de Esquemas com o botão Adicionar realçado.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Lembre-se de que todos os campos adicionados a uma classe serão usados em todos os esquemas que empregam essa classe. Portanto, você deve considerar cuidadosamente quais campos serão úteis em todos os casos de uso do schema. Se você estiver pensando em adicionar um campo que só pode ser usado em alguns esquemas nesta classe, considere adicioná-lo a esses esquemas [criando um grupo de campos](./field-groups.md#create).

Um espaço reservado para **[!UICONTROL Campo sem título]** aparece na tela e o painel direito atualiza para mostrar controles que configuram as propriedades do campo. Em **[!UICONTROL Atribuir a]**, selecione **[!UICONTROL Classe]**.

![Um campo sem título na tela do Editor de Esquemas com a propriedade de campo Atribuir à [!UICONTROL Classe] selecionada e realçada.](../../images/ui/resources/classes/assign-to-class.png)

Consulte o manual sobre [definição de campos na interface](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo à classe. Continue a adicionar quantos campos forem necessários à classe. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o esquema e a classe.

![O esquema recém-criado na tela do Editor de Esquemas, com [!UICONTROL Salvar] realçado.](../../images/ui/resources/classes/save.png)

Se você tiver criado esquemas que empregam essa classe, os campos recém-adicionados aparecerão automaticamente nesses esquemas.

## Editar uma classe (#edit-a-class)

>[!NOTE]
>
>Somente as classes personalizadas definidas por sua organização podem ser totalmente editadas e personalizadas. Para classes principais definidas por Adobe, somente os nomes de exibição de seus campos podem ser editados no contexto de esquemas individuais. Consulte a seção sobre [edição de nomes para exibição para campos de esquema](./schemas.md#display-names) para obter detalhes.
>
>Depois que uma classe personalizada é salva e usada na assimilação de dados, somente alterações aditivas podem ser feitas nela a partir de então. Consulte as [regras de evolução do esquema](../../schema/composition.md#evolution) para obter mais informações.

Você pode editar uma classe por meio do workflow do esquema editando um esquema existente que estende a classe ou criando manualmente um esquema. Não é possível editar uma classe diretamente. Dentro da guia [!UICONTROL Procurar] no espaço de trabalho [!UICONTROL Esquemas], selecione uma classe existente ou **[!UICONTROL Criar um esquema]**.

![O Editor de Esquemas com uma classe existente e o [!UICONTROL Criar um esquema] realçado.](../../images/ui/resources/classes/edit-class-options.png)

Se você optar por criar um novo esquema, consulte a seção sobre [criação de um esquema](#create-schema) para obter detalhes. Quando terminar de criar o esquema (ou após selecionar um esquema existente), o Editor de esquemas será exibido. Para atualizar um campo de classe existente, selecione o campo na estrutura do esquema. As informações do campo aparecerão no painel direito. Assegure a [!UICONTROL Atribuir a]
a opção **[!UICONTROL Classe]** está selecionada ou suas atualizações não afetarão a classe.

![O Editor de Esquemas com um campo selecionado e realçado, e o painel direito exposto, realçando [!UICONTROL Atribuir a].](../../images/ui/resources/classes/edit-existing-field.png)

Faça as alterações desejadas no campo, rolando para baixo no painel direito para selecionar **[!UICONTROL Aplicar]** para salvar as alterações.

>[!IMPORTANT]
>
> Quaisquer atualizações feitas em campos serão aplicadas em todos os esquemas que empregam essa classe, seguindo as [regras de evolução de esquema](../../schema/composition.md#evolution).

![O Editor de Esquemas com um campo selecionado e o painel direito exposto, destacando [!UICONTROL Aplicar].](../../images/ui/resources/classes/save-changes.png)

Para adicionar novos campos, siga o guia [adicionar campos a uma classe](#add-fields-to-a-class). Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o esquema e a classe.

![O Editor de Esquemas com [!UICONTROL Salvar] realçado.](../../images/ui/resources/classes/save-schema.png)

## Alterar a classe de um esquema {#schema}

Você pode alterar a classe do schema em qualquer momento durante o processo de criação inicial, antes que ele seja salvo. No entanto, isso deve ser feito com cuidado, pois os grupos de campo são compatíveis apenas com determinadas classes. Alterar a classe redefine a tela de desenho e quaisquer campos adicionados.
Consulte o manual sobre [criação e edição de esquemas](./schemas.md#change-class) para obter mais informações.

## Próximas etapas {#next-steps}

Este documento abordou como criar e editar classes usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Esquemas], consulte a [[!UICONTROL visão geral do espaço de trabalho de ]](../overview.md).

Para saber como gerenciar classes usando a API do Registro de Esquema, consulte o [manual de ponto de extremidade de classes](../../api/classes.md).
