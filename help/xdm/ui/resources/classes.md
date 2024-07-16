---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;classe;classes;
solution: Experience Platform
title: Criar e editar classes na interface
description: Saiba como criar e editar classes na interface do usuário do Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 5%

---

# Criar e editar classes na interface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtro de classe padrão ou personalizada"
>abstract="A lista de classes disponíveis é pré-filtrada com base em como elas foram criadas. Selecione o botão de opção para escolher entre as opções Padrão e Personalizado. A opção Padrão mostra entidades criadas pela Adobe e inclui as classes Perfil individual XDM e Evento de experiência XDM. A opção Personalizado exibe entidades criadas em sua organização. Consulte a documentação para saber mais sobre criação e edição de classes."

Na Adobe Experience Platform, a classe de um esquema define os aspectos comportamentais dos dados que o esquema conterá (registro ou série temporal). Além disso, as classes descrevem o menor número de propriedades comuns que todos os esquemas baseados nessa classe precisariam incluir e fornecem uma maneira de vários conjuntos de dados compatíveis serem mesclados.

O Adobe fornece várias classes padrão (&quot;núcleo&quot;) do Experience Data Model (XDM), incluindo o Perfil individual XDM e o XDM ExperienceEvent. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos para sua organização.

Este documento fornece uma visão geral de como criar, editar e gerenciar classes personalizadas na interface do usuário do Experience Platform.

## Pré-requisitos {#prerequisites}

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM no ecossistema de Experience Platform e as [noções básicas da composição de esquema](../../schema/composition.md) para saber como as classes contribuem para os esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir o tutorial sobre [composição de um esquema na interface](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do Editor de esquemas.

## Introdução {#getting-started}

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o espaço de trabalho [!UICONTROL Esquemas] e selecione a guia **[!UICONTROL Classes]**. Uma lista de classes disponíveis é exibida.

## Filtrar classes {#filter}

A lista de classes é automaticamente filtrada com base em como foram criadas. A configuração padrão exibe as classes definidas pelo Adobe. Também é possível filtrar a lista para mostrar os criados por sua organização. Selecione o botão de opção para escolher entre as opções [!UICONTROL Padrão] e [!UICONTROL Personalizado]. A opção [!UICONTROL Padrão] mostra entidades criadas pelo Adobe e a opção [!UICONTROL Personalizado] exibe entidades criadas na sua organização.

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com [!UICONTROL Padrão] e [!UICONTROL Personalizado] destacados.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Use os recursos de pesquisa para filtrar ou localizar uma classe com base em seu nome. Consulte o guia em [explorando recursos XDM](../explore.md) para obter mais informações.

## Criar uma nova classe {#create}

Há dois métodos para criar uma classe na interface do usuário da Platform. Em qualquer guia no espaço de trabalho [!UICONTROL Esquemas], selecione **[!UICONTROL Criar esquema]**, ou na guia [!UICONTROL Classes], selecione **[!UICONTROL Criar classe]**.

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com [!UICONTROL Criar esquema] e [!UICONTROL Criar classe] realçada](../../images/ui/resources/classes/create-class-methods.png)

Se você selecionar **[!UICONTROL Criar classe]**, a caixa de diálogo [!UICONTROL Criar classe] será exibida. Insira um [!UICONTROL Nome de exibição] e uma [!UICONTROL Descrição] para sua classe e escolha o comportamento pretendido para sua classe com os botões de opção. As classes podem ser do tipo, série de registros ou série temporal. Selecione **[!UICONTROL Criar]** para confirmar suas escolhas e retornar à guia [!UICONTROL Classes].

![A caixa de diálogo [!UICONTROL Criar classe] com [!UICONTROL Criar] foi realçada.](../../images/ui/resources/classes/create-class-dialog.png)

A classe criada está disponível e listada no modo de exibição [!UICONTROL Classes].

![A guia [!UICONTROL Classes] do espaço de trabalho [!UICONTROL Esquemas] com a classe criada recentemente realçada.](../../images/ui/resources/classes/new-class-listing.png)

### Criar ou editar uma classe {#create-or-edit}

Como alternativa, se você selecionar **[!UICONTROL Criar esquema]**, o fluxo de trabalho [!UICONTROL Criar esquema] será exibido. Na seção [!UICONTROL Detalhes do esquema], selecione **[!UICONTROL Outros]**. Uma lista de classes disponíveis é exibida. Aqui você pode navegar e filtrar classes pré-existentes nas quais basear sua nova classe.

>[!NOTE]
>
>Somente as classes personalizadas definidas por sua organização podem ser totalmente editadas e personalizadas. Para classes principais definidas por Adobe, somente os nomes de exibição de seus campos podem ser editados no contexto de esquemas individuais. Consulte a seção sobre [edição de nomes para exibição para campos de esquema](./schemas.md#display-names) para obter detalhes.
>
>Depois que uma classe personalizada é salva e usada na assimilação de dados, somente alterações aditivas podem ser feitas nela a partir de então. Consulte as [regras de evolução do esquema](../../schema/composition.md#evolution) para obter mais informações.

![O fluxo de trabalho [!UICONTROL Criar esquema] com [!UICONTROL Outros] realçado na seção [!UICONTROL Detalhes do esquema].](../../images/ui/resources/classes/other-schema-details.png)

Selecione um botão de opção para filtrar as classes com base no fato de serem classes personalizadas ou padrão. Você também pode filtrar os resultados disponíveis com base em seu setor ou pesquisar por uma classe específica usando o campo de pesquisa.

![O fluxo de trabalho [!UICONTROL Criar esquema] com a barra de pesquisa [!UICONTROL Personalizado] e [!UICONTROL Setores] foi realçado.](../../images/ui/resources/classes/filter-and-search.png)

Para ajudá-lo a decidir a classe apropriada, há informações (![Um ícone de informações.](../../images/ui/resources/classes/info.png)) e visualização (![Um ícone de visualização.](../../images/ui/resources/classes/preview.png)) ícones para cada classe. O ícone de informações abre uma caixa de diálogo que fornece uma descrição da classe e do setor ao qual ela está associada. O ícone de visualização abre uma caixa de diálogo de visualização para a classe que contém um diagrama de esquema e suas propriedades.

![Uma visualização da classe selecionada com o diagrama de esquema e as propriedades de classe realçadas.](../../images/ui/resources/classes/class-preview.png)

Selecione qualquer linha para escolher uma classe, em seguida, selecione **[!UICONTROL Próximo]** para confirmar sua escolha.

![O fluxo de trabalho [!UICONTROL Criar esquema] com uma classe selecionada da tabela de classes disponíveis e [!UICONTROL Próximo] realçado.](../../images/ui/resources/classes/select-class.png)

A seção [!UICONTROL Nome e revisão] do fluxo de trabalho é exibida. Nesta seção, forneça um nome e uma descrição para identificar seu esquema. &#x200B;A estrutura base do esquema (fornecida pela classe) é mostrada na tela para que você revise e verifique a classe selecionada e a estrutura do esquema.

Insira um nome curto, descritivo, exclusivo e amigável para a classe no campo de texto [!UICONTROL Nome de exibição do esquema]. Em seguida, insira uma descrição adequada para identificar o comportamento dos dados definidos pelo schema. Quando tiver revisado a estrutura do esquema e estiver satisfeito com as configurações, selecione **[!UICONTROL Concluir]** para criar o esquema.

![A seção [!UICONTROL Nome e revisão] do fluxo de trabalho [!UICONTROL Criar esquema] com o [!UICONTROL Nome para exibição do esquema], [!UICONTROL Descrição] e [!UICONTROL Término] realçados.](../../images/ui/resources/classes/name-and-review-class.png)

O Editor de esquemas é exibido com a estrutura do esquema mostrada na tela. Agora você pode começar a [adicionar campos à classe](#add-fields).

![O Editor de Esquemas com a estrutura do esquema mostrada na tela.](../../images/ui/resources/classes/edit.png)

## Adicionar campos a uma classe {#add-fields}

Depois que você tiver um esquema que emprega uma classe personalizada aberta no [!UICONTROL Editor de esquemas], poderá começar a adicionar campos à classe. Para adicionar um novo campo, selecione o ícone **de adição (+)** ao lado do nome do esquema.

>[!IMPORTANT]
>
>Ao criar um esquema que implementa uma classe definida por sua organização, lembre-se de que os grupos de campos de esquema estão disponíveis para uso somente com classes compatíveis. Como a classe definida é nova, não há grupos de campos compatíveis listados na caixa de diálogo **[!UICONTROL Adicionar grupo de campos]**. Em vez disso, você precisará [criar novos grupos de campos](./field-groups.md#create) para usar com essa classe. Na próxima vez que você compor um schema que implementa a nova classe, os grupos de campos definidos serão listados e estarão disponíveis para uso.

![O Editor de Esquemas com o botão Adicionar realçado.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Lembre-se de que todos os campos adicionados a uma classe serão usados em todos os esquemas que empregam essa classe. Portanto, você deve considerar cuidadosamente quais campos serão úteis em todos os casos de uso do schema. Se você estiver pensando em adicionar um campo que só pode ser usado em alguns esquemas nesta classe, considere adicioná-lo a esses esquemas [criando um grupo de campos](./field-groups.md#create).

Um espaço reservado para **[!UICONTROL Campo sem título]** aparece na tela e o painel direito atualiza para mostrar controles que configuram as propriedades do campo. Em **[!UICONTROL Atribuir a]**, selecione **[!UICONTROL Classe]**.

![Um campo sem título na tela do editor de esquemas com a propriedade do campo Atribuir à Classe selecionada e realçada.](../../images/ui/resources/classes/assign-to-class.png)

Consulte o manual sobre [definição de campos na interface](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo à classe. Continue a adicionar quantos campos forem necessários à classe. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o esquema e a classe.

![O esquema recém-criado na tela do Editor de Esquemas, com [!UICONTROL Salvar] realçado.](../../images/ui/resources/classes/save.png)

Se você tiver criado esquemas que empregam essa classe, os campos recém-adicionados aparecerão automaticamente nesses esquemas.

## Alterar a classe de um esquema {#schema}

Você pode alterar a classe do schema em qualquer momento durante o processo de criação inicial, antes que ele seja salvo. No entanto, isso deve ser feito com cuidado, pois os grupos de campo são compatíveis apenas com determinadas classes. Alterar a classe redefine a tela de desenho e quaisquer campos adicionados.
Consulte o manual sobre [criação e edição de esquemas](./schemas.md#change-class) para obter mais informações.

## Próximas etapas {#next-steps}

Este documento abordou como criar e editar classes usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Esquemas], consulte a [[!UICONTROL visão geral do espaço de trabalho de ]](../overview.md).

Para saber como gerenciar classes usando a API do Registro de Esquema, consulte o [manual de ponto de extremidade de classes](../../api/classes.md).
