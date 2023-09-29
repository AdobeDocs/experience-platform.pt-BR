---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;classe;classes;
solution: Experience Platform
title: Criar e editar classes na interface
description: Saiba como criar e editar classes na interface do usuário do Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 4214339c4a661c6bca2cd571919ae205dcb47da1
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 5%

---

# Criar e editar classes na interface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtro de classe padrão ou personalizada"
>abstract="A lista de classes disponíveis é pré-filtrada com base em como elas foram criadas. Selecione o botão de opção para escolher entre as opções Padrão e Personalizado. A opção Padrão mostra entidades criadas pela Adobe e inclui as classes Perfil individual XDM e Evento de experiência XDM. A opção Personalizado exibe entidades criadas em sua organização. Consulte a documentação para saber mais sobre criação e edição de classes."

Na Adobe Experience Platform, a classe de um esquema define os aspectos comportamentais dos dados que o esquema conterá (registro ou série temporal). Além disso, as classes descrevem o menor número de propriedades comuns que todos os esquemas baseados nessa classe precisariam incluir e fornecem uma maneira de vários conjuntos de dados compatíveis serem mesclados.

O Adobe fornece várias classes padrão (&quot;núcleo&quot;) do Experience Data Model (XDM), incluindo [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos para sua organização.

Este documento fornece uma visão geral de como criar, editar e gerenciar classes personalizadas na interface do usuário do Experience Platform.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução ao papel do XDM no ecossistema de Experience Platform, e a [noções básicas da composição do esquema](../../schema/composition.md) para saber como as classes contribuem para esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir o tutorial em [composição de um esquema na interface](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Introdução

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda, para abrir a [!UICONTROL Esquemas] e selecione o **[!UICONTROL Classes]** guia. Uma lista de classes disponíveis é exibida.

## Filtrar classes {#filter}

A lista de classes é automaticamente filtrada com base em como foram criadas. A configuração padrão exibe as classes definidas pelo Adobe. Também é possível filtrar a lista para mostrar os criados por sua organização. Selecione o botão de opção para escolher entre as opções [!UICONTROL Padrão] e [!UICONTROL Personalizado] opções. A variável [!UICONTROL Padrão] mostra entidades criadas por Adobe e a variável [!UICONTROL Personalizado] exibe entidades criadas na organização.

![A variável [!UICONTROL Classes] guia do [!UICONTROL Esquemas] espaço de trabalho com [!UICONTROL Padrão] e [!UICONTROL Personalizado] destacado.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa do espaço de trabalho para ajudar a encontrar o esquema com mais facilidade. Consulte o guia sobre [exploração de recursos XDM](../explore.md) para obter mais informações.

## Criar uma nova classe {#create}

Há dois métodos para criar uma classe na interface do usuário da Platform. Em qualquer guia no **[!UICONTROL Esquemas]** espaço de trabalho, selecione **[!UICONTROL Criar esquema]**, ou do [!UICONTROL Classes] seleção de guia **[!UICONTROL Criar classe]**.

![A variável [!UICONTROL Classes] guia do [!UICONTROL Esquemas] espaço de trabalho com [!UICONTROL Criar esquema] e [!UICONTROL Criar classe] realçado](../../images/ui/resources/classes/create-class-methods.png)

Se você selecionar **[!UICONTROL Criar classe]**, o [!UICONTROL Criar classe] será exibida. Insira um [!UICONTROL Nome] e [!UICONTROL Descrição] para a sua classe e escolha o comportamento pretendido da sua classe com os botões de opção. As classes podem ser séries de registros ou séries de tempo. Selecionar **[!UICONTROL Criar]** para confirmar suas escolhas.

![A variável [!UICONTROL Criar classe] diálogo com [!UICONTROL Criar] destacado.](../../images/ui/resources/classes/create-class-dialog.png)

A variável [!DNL Schema Editor] é exibida, mostrando um novo esquema na tela com base na classe personalizada que você acabou de criar. Como nenhum campo foi adicionado à classe ainda, o esquema contém apenas um `_id` que representa o identificador exclusivo gerado pelo sistema aplicado automaticamente a todos os recursos na [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Ao criar um esquema que implementa uma classe definida por sua organização, lembre-se de que os grupos de campos de esquema estão disponíveis para uso somente com classes compatíveis. Como a classe definida é nova, não há grupos de campos compatíveis listados na **[!UICONTROL Adicionar grupo de campos]** diálogo. Em vez disso, será necessário [criar novos grupos de campos](./field-groups.md#create) para uso com essa classe. Na próxima vez que você compor um schema que implementa a nova classe, os grupos de campos definidos serão listados e estarão disponíveis para uso.

### Criar ou editar uma classe {#create-or-edit}

Se você selecionar **[!UICONTROL Criar esquema]**, o [!UICONTROL Criar esquema] workflow aparece. No [!UICONTROL Detalhes do esquema] , selecione **[!UICONTROL Outro]**. Uma lista de classes disponíveis é exibida. Aqui você pode navegar e filtrar classes pré-existentes nas quais basear sua nova classe.

>[!NOTE]
>
>Somente as classes personalizadas definidas por sua organização podem ser totalmente editadas e personalizadas. Para classes principais definidas por Adobe, somente os nomes de exibição de seus campos podem ser editados no contexto de esquemas individuais. Consulte a seção sobre [edição de nomes de exibição para campos de esquema](./schemas.md#display-names) para obter detalhes.
>
>Depois que uma classe personalizada é salva e usada na assimilação de dados, somente alterações aditivas podem ser feitas nela a partir de então. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

![A variável [!UICONTROL Criar esquema] workflow com [!UICONTROL Outro] destacado no [!UICONTROL Detalhes do esquema] seção.](../../images/ui/resources/classes/other-schema-details.png)

Selecione um botão de opção para filtrar as classes com base no fato de serem classes personalizadas ou padrão. Você também pode filtrar os resultados disponíveis com base em seu setor ou pesquisar por uma classe específica usando o campo de pesquisa.

![A variável [!UICONTROL Criar esquema] workflow com a barra de pesquisa, [!UICONTROL Personalizado], e [!UICONTROL Setores] destacado.](../../images/ui/resources/classes/filter-and-search.png)

Para ajudá-lo a decidir sobre a classe apropriada, há informações (![Um ícone de informações.](../../images/ui/resources/classes/info.png)) e visualização (![Um ícone de visualização.](../../images/ui/resources/classes/preview.png)) para cada classe. O ícone de informações abre uma caixa de diálogo que fornece uma descrição da classe e do setor ao qual ela está associada. O ícone de visualização abre uma caixa de diálogo de visualização para a classe que contém um diagrama de esquema e suas propriedades.

![Uma visualização da classe selecionada com o diagrama de esquema e as propriedades da classe realçadas.](../../images/ui/resources/classes/class-preview.png)

Selecione qualquer linha para escolher uma classe e, em seguida, selecione **[!UICONTROL Próxima]** para confirmar sua escolha.

![A variável [!UICONTROL Criar esquema] fluxo de trabalho com uma classe selecionada na tabela de classes disponíveis e [!UICONTROL Próxima] destacado.](../../images/ui/resources/classes/select-class.png)

A variável [!UICONTROL Nomear e descrever] é exibida. Nesta seção, forneça um nome e uma descrição para identificar seu esquema. &#x200B;A estrutura base do esquema (fornecida pela classe) é mostrada na tela para que você revise e verifique a classe selecionada e a estrutura do esquema.

Insira um nome curto, descritivo, exclusivo e amigável para a classe na [!UICONTROL Nome de exibição do esquema] campo de texto. Em seguida, insira uma descrição adequada para identificar o comportamento dos dados definidos pelo schema. Quando tiver revisado a estrutura do esquema e estiver satisfeito com as configurações, selecione **[!UICONTROL Concluir]** para criar seu esquema.

![A variável [!UICONTROL Nome e revisão] seção do [!UICONTROL Criar esquema] fluxo de trabalho com o [!UICONTROL Nome de exibição do esquema], [!UICONTROL Descrição], e [!UICONTROL Concluir] destacado.](../../images/ui/resources/classes/name-and-review-class.png)

A variável [!DNL Schema Editor] é exibida, com a estrutura do schema mostrada na tela. Agora você pode começar [adicionar campos à classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Adicionar campos a uma classe {#add-fields}

Depois que você tiver um esquema que emprega uma classe personalizada aberta na [!UICONTROL Editor de esquema], você pode começar a adicionar campos à classe. Para adicionar um novo campo, selecione a variável **mais (+)** ícone ao lado do nome do esquema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Lembre-se de que todos os campos adicionados a uma classe serão usados em todos os esquemas que empregam essa classe. Portanto, você deve considerar cuidadosamente quais campos serão úteis em todos os casos de uso do schema. Se estiver pensando em adicionar um campo que só pode ver uso em alguns esquemas nesta classe, você pode considerar adicioná-lo a esses esquemas por [criação de um grupo de campos](./field-groups.md#create) em vez disso.

Um **[!UICONTROL Campo sem título]** o espaço reservado é exibido no na tela, e o painel direito é atualizado para mostrar controles para configurar as propriedades do campo. Em **[!UICONTROL Atribuir a]**, selecione **[!UICONTROL Classe]**.

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

Consulte o guia sobre [definição de campos na interface](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo à classe. Continue a adicionar quantos campos forem necessários à classe. Quando terminar, selecione **[!UICONTROL Salvar]** para salvar o schema e a classe.

![](../../images/ui/resources/classes/save.png)

Se você tiver criado esquemas que empregam essa classe, os campos recém-adicionados aparecerão automaticamente nesses esquemas.

## Alterar a classe de um esquema {#schema}

Você pode alterar a classe do schema em qualquer momento durante o processo de criação inicial, antes que ele seja salvo. Consulte o guia sobre [criação e edição de schemas](./schemas.md#change-class) para obter mais informações.

## Próximas etapas

Este documento abordou como criar e editar classes usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do [!UICONTROL Esquemas] espaço de trabalho, consulte a [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar aulas usando o [!DNL Schema Registry] , consulte a [manual de endpoint de classes](../../api/classes.md).
