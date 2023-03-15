---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;políticas de mesclagem;interface do usuário;carimbo de data/hora ordenado;precedência do conjunto de dados
title: Guia da interface de políticas de mesclagem
type: Documentation
description: Ao reunir dados de várias fontes no Experience Platform, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar a visualização unificada. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# Guia da interface de políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] O usa o para determinar como os dados serão priorizados e quais dados serão combinados para criar a visualização unificada.

Usando APIs RESTful ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform.

Para saber mais sobre as políticas de mesclagem e a função que elas desempenham no Experience Platform, comece lendo o [visão geral das políticas de mesclagem](overview.md).

## Introdução

Este guia requer uma compreensão funcional de vários [!DNL Experience Platform] recursos. Antes de seguir este guia, consulte a documentação dos seguintes serviços:

* [Perfil do cliente em tempo real](../home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): habilita o Perfil do cliente em tempo real unindo identidades de diferentes fontes de dados que estão sendo assimiladas na [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

## Exibir políticas de mesclagem {#view-merge-policies}

No prazo de [!DNL Experience Platform] Você pode começar a trabalhar com políticas de mesclagem selecionando **[!UICONTROL Perfis]** no painel de navegação esquerdo e, em seguida, selecione a **[!UICONTROL Políticas de mesclagem]** guia. Essa guia inclui uma lista de todas as políticas de mesclagem existentes para sua organização, bem como detalhes para cada política de mesclagem, incluindo o nome da política, se a política de mesclagem é ou não a política de mesclagem padrão e a classe de esquema à qual a política de mesclagem está relacionada.

![Página de aterrissagem das políticas de mesclagem](../images/merge-policies/landing.png)

Para selecionar quais detalhes estão visíveis ou para adicionar outras colunas à exibição, selecione **[!UICONTROL Configurar colunas]** e clique em um nome de coluna para adicioná-la ou removê-la da exibição.

![](../images/merge-policies/adjust-view.png)

## Criar uma política de mesclagem {#create-a-merge-policy}

Para criar uma nova política de mesclagem, selecione **[!UICONTROL Criar política de mesclagem]** na guia políticas de mesclagem para inserir o novo fluxo de trabalho da política de mesclagem.

![Página de aterrissagem de políticas de mesclagem com o botão criar realçado.](../images/merge-policies/create-new.png)

A variável **[!UICONTROL Nova política de mesclagem]** fluxo de trabalho, exige que você forneça informações importantes para sua nova política de mesclagem por meio de uma série de etapas guiadas. Essas etapas são descritas nas seções a seguir.

![O novo fluxo de trabalho da política de mesclagem.](../images/merge-policies/create.png)

## [!UICONTROL Configurar] {#configure}

A primeira etapa do fluxo de trabalho permite configurar a política de mesclagem fornecendo informações básicas. Essas informações incluem:

* **[!UICONTROL Nome]**: o nome da sua política de mesclagem deve ser descritivo, mas conciso.
* **[!UICONTROL Classe do esquema]**: a classe de esquema XDM associada à política de mesclagem. Especifica a classe de esquema para a qual essa política de mesclagem é criada. As organizações podem criar várias políticas de mesclagem por classe de esquema. Atualmente, somente o [!UICONTROL Perfil individual XDM] está disponível na interface do usuário do. Você pode visualizar o esquema de união para a classe de esquema selecionando **[!UICONTROL Exibir esquema de união]**. Para obter mais informações, consulte a seção sobre [exibição do esquema de união](#view-union-schema) a seguir.
* **[!UICONTROL Identificação de ID]**: esse campo define como determinar as identidades relacionadas de um cliente. Há dois valores possíveis para a compilação de identidade, e é importante entender como o tipo de compilação de identidade que você seleciona afetará seus dados. Para saber mais, consulte o [visão geral das políticas de mesclagem](overview.md).
   * **[!UICONTROL Nenhum]**: não executa compilação de identidade.
   * **[!UICONTROL Gráfico privado]**: execute a compilação de identidade com base no seu gráfico de identidade privado.
* **[!UICONTROL Política de mesclagem padrão]**: um botão que permite selecionar se essa política de mesclagem será ou não o padrão da sua organização. Se o seletor estiver ativado, um aviso será exibido solicitando que você confirme se deseja alterar a política de mesclagem padrão da organização. Consulte a [visão geral das políticas de mesclagem](overview.md) para saber mais sobre as políticas de mesclagem padrão.
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Política de mesclagem ativa na borda]**: um botão que permite selecionar se essa política de mesclagem estará ou não ativa na borda. Para garantir que todos os consumidores de perfil estejam trabalhando com a mesma exibição nas bordas, as políticas de mesclagem podem ser marcadas como ativas na borda. Para que um segmento seja ativado na borda (marcado como um segmento de borda), ele deve estar vinculado a uma política de mesclagem marcada como ativa na borda. Se um segmento for **não** vinculado a uma política de mesclagem marcada como ativa na borda, o segmento não será marcado como ativo na borda e será marcado como um segmento de transmissão. Além disso, cada sandbox em uma organização só pode ter **um** política de mesclagem ativa no edge.

Depois que os campos obrigatórios forem preenchidos, você poderá selecionar **[!UICONTROL Próxima]** para continuar com o fluxo de trabalho.

![Uma tela Configurar completa com o botão Avançar realçado.](../images/merge-policies/create-complete.png)

## [!UICONTROL Exibir esquema de união] {#view-union-schema}

Ao criar ou editar uma política de mesclagem, você pode visualizar o esquema de união para a classe de esquema escolhida selecionando **[!UICONTROL Exibir esquema de união]**.

![](../images/merge-policies/view-union-schema.png)

Isso abre o [!UICONTROL Exibir esquema de união] , mostrando todos os esquemas de contribuição, identidades e relacionamentos associados ao esquema de união. Você pode usar a caixa de diálogo para explorar o esquema de união da mesma maneira que faria ao acessar a [!UICONTROL Esquema de união] na guia [!UICONTROL Perfis] seção da interface do usuário da Platform.

Para obter informações detalhadas sobre esquemas de união, incluindo como interagir com eles no [!UICONTROL Esquema de união] ou na guia [!UICONTROL Exibir esquema de união] caixa de diálogo mostrada no fluxo de trabalho das políticas de mesclagem, visite o [guia da interface do esquema de união](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Selecionar conjuntos de dados do perfil] {#select-profile-datasets}

No **[!UICONTROL Selecionar conjuntos de dados do perfil]** , você deve selecionar o **[!UICONTROL Método de mesclagem]** que você deseja usar para a política de mesclagem. Também exibido na tela é o número total de [!UICONTROL Conjuntos de dados do perfil] em sua organização que estão relacionados à classe de esquema selecionada na tela anterior.

Dependendo do método de mesclagem escolhido, todos os conjuntos de dados do Perfil serão mesclados pela ordem em que foram atualizados pela última vez (carimbo de data e hora ordenado) ou você precisará selecionar quais conjuntos de dados do Perfil incluir na política de mesclagem e a ordem em que eles serão mesclados (precedência do conjunto de dados).

Para obter mais informações sobre métodos de mesclagem, consulte o [visão geral das políticas de mesclagem](overview.md).

### Carimbo de data e hora ordenado {#timestamp-ordered-profile}

Selecionar **[!UICONTROL Carimbo de data e hora ordenado]** como o método de mesclagem significa que os atributos dos conjuntos de dados atualizados mais recentemente terão prioridade. Isso se aplica a todos os conjuntos de dados do Perfil.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL Conjuntos de dados do perfil]** (por exemplo, `(37)` na imagem mostrada) mostra o número total de conjuntos de dados de perfil que serão incluídos.

![](../images/merge-policies/timestamp-ordered.png)

### Prioridade de conjunto de dados {#dataset-precedence-profile}

Selecionar **[!UICONTROL Prioridade de conjunto de dados]** como o método de mesclagem exige que você selecione Conjuntos de dados do perfil e os priorize manualmente. Cada conjunto de dados listado também inclui o status do último lote assimilado ou exibe um aviso de que nenhum lote foi assimilado nesse conjunto de dados.

É possível selecionar até 50 conjuntos de dados na lista de conjuntos de dados para incluir na política de mesclagem.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL Conjuntos de dados do perfil]** (por exemplo, `(37)` na imagem mostrada) mostra o número total de conjuntos de dados de perfil disponíveis para seleção.

À medida que os conjuntos de dados são selecionados, eles são adicionados ao **[!UICONTROL Selecionar conjuntos de dados]** , permitindo arrastar e soltar os conjuntos de dados e ordená-los de acordo com a precedência desejada. À medida que os conjuntos de dados são ajustados na lista, o ordinal (1, 2, 3 etc.) ao lado do conjunto de dados será atualizado, exibindo a prioridade (1 tendo a prioridade mais alta, depois 2 e adiante).

Selecionar um conjunto de dados também atualiza o **[!UICONTROL Esquema de união]** , mostrando os campos no esquema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre esquemas de união, incluindo como interagir com as visualizações na interface, consulte a [guia da interface do esquema de união](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Selecionar conjuntos de dados ExperienceEvent] {#select-experienceevent-datasets}

A próxima etapa do fluxo de trabalho requer que você selecione conjuntos de dados ExperienceEvent. Essa tela é influenciada pelo método de mesclagem selecionado na [[!UICONTROL Selecionar conjuntos de dados do perfil]](#select-profile-datasets) tela.

### Carimbo de data e hora ordenado {#timestamp-ordered-experienceevent}

Se você selecionou **[!UICONTROL Carimbo de data e hora ordenado]** como o método de mesclagem para conjuntos de dados do Perfil, os atributos dos conjuntos de dados ExperienceEvent atualizados mais recentemente também terão prioridade aqui.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL Conjuntos de dados ExperienceEvent]** (por exemplo, `(20)` na imagem mostrada) mostra o número total de conjuntos de dados ExperienceEvent criados pela sua organização relacionados à classe de esquema selecionada na tela de configuração da política de mesclagem.

![](../images/merge-policies/timestamp-experienceevent.png)

### Prioridade de conjunto de dados {#dataset-precedence-experienceevent}

Se você selecionou **[!UICONTROL Prioridade de conjunto de dados]** como o método de mesclagem para conjuntos de dados de Perfil, será necessário selecionar conjuntos de dados ExperienceEvent para incluir. É possível selecionar até 50 conjuntos de dados ExperienceEvent na lista de conjuntos de dados.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL Conjuntos de dados ExperienceEvent]** (por exemplo, `(20)` na imagem mostrada) mostra o número total de conjuntos de dados ExperienceEvent criados pela sua organização relacionados à classe de esquema selecionada na tela de configuração da política de mesclagem.

À medida que os conjuntos de dados são selecionados, eles aparecem no [!UICONTROL Selecionar conjuntos de dados] seção.

Os conjuntos de dados ExperienceEvent não podem ser ordenados manualmente, em vez disso, os atributos nos conjuntos de dados ExperienceEvent são anexados aos conjuntos de dados do Perfil se fizerem parte do mesmo fragmento de perfil.

Semelhante à seleção de conjuntos de dados de Perfil, a seleção de um conjunto de dados ExperienceEvent também atualiza a **[!UICONTROL Esquema de união]** , mostrando os campos no esquema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre esquemas de união, incluindo como interagir com as visualizações na interface, consulte a [guia da interface do esquema de união](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Consulte a seção] {#review}

A etapa final do fluxo de trabalho é revisar a política de mesclagem. A variável **[!UICONTROL Revisão]** A tela exibe informações sobre a política de mesclagem, incluindo o método de compilação de ID selecionado, o método de mesclagem selecionado e os conjuntos de dados incluídos. (Para exibir todos os conjuntos de dados de Perfil ou ExperienceEvent incluídos, selecione o número de conjuntos de dados para expandir a lista suspensa.)

Também está incluído na tela de revisão o **[!UICONTROL Visualizar dados]** tabela que mostra registros de perfil de exemplo usando sua política de mesclagem. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar a política de mesclagem.

Revise a configuração da política de mesclagem e visualize os dados cuidadosamente antes de selecionar **[!UICONTROL Concluir]** para concluir o workflow de criação.

### Carimbo de data e hora ordenado {#timestamp-ordered-review}

Se você selecionou **[!UICONTROL Carimbo de data e hora ordenado]** como o método de mesclagem para sua política de mesclagem, a lista de conjuntos de dados do Perfil inclui todos os conjuntos de dados que foram criados por sua organização relacionados à classe de esquema, em ordem de carimbo de data e hora. A lista de conjuntos de dados ExperienceEvent inclui todos os conjuntos de dados que sua organização criou para a classe de esquema escolhida e serão anexados aos conjuntos de dados do Perfil.

A variável **[!UICONTROL Visualizar dados]** A tabela mostra registros de perfil de amostra com base em uma ordem de carimbo de data e hora dos conjuntos de dados. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar a política de mesclagem.

![](../images/merge-policies/timestamp-review.png)

### Prioridade de conjunto de dados {#dataset-precedence-review}

Se você selecionou **[!UICONTROL Prioridade de conjunto de dados]** como o método de mesclagem para sua política de mesclagem, as listas de conjuntos de dados Profile e ExperienceEvent incluem apenas os conjuntos de dados Profile e ExperienceEvent selecionados durante o fluxo de trabalho de criação, respectivamente. A ordem dos conjuntos de dados do Perfil deve corresponder à precedência especificada durante a criação. Caso contrário, use o [!UICONTROL Voltar] para retornar às etapas anteriores do fluxo de trabalho e ajustar a prioridade.

A variável **[!UICONTROL Visualizar dados]** A tabela mostra registros de perfil de exemplo usando os conjuntos de dados selecionados. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar a política de mesclagem.

![](../images/merge-policies/dataset-precedence-review.png)

### Lista atualizada de políticas de mesclagem {#updated-list}

Após concluir o fluxo de trabalho para criar uma nova política de mesclagem, você retornará ao **[!UICONTROL Políticas de mesclagem]** guia. A lista de políticas de mesclagem para sua organização agora deve incluir a política de mesclagem recém-criada.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar uma política de mesclagem

No [!UICONTROL Políticas de mesclagem] você pode modificar uma política de mesclagem existente criada para o [!DNL XDM Individual Profile] selecionando a classe **[!UICONTROL Nome da política]** para a política de mesclagem que deseja editar.

![Página de aterrissagem das políticas de mesclagem](../images/merge-policies/select-edit.png)

Quando a variável **[!UICONTROL Editar política de mesclagem]** for exibida, você poderá fazer alterações no nome e no [!UICONTROL Identificação de ID] , bem como alterar se essa política é ou não a política de mesclagem padrão para sua organização.

Selecionar **[!UICONTROL Próxima]** para continuar o fluxo de trabalho da política de mesclagem para atualizar o método de mesclagem e os conjuntos de dados incluídos na política de mesclagem.

![](../images/merge-policies/edit-screen.png)

Depois de fazer as alterações necessárias, revise a política de mesclagem e selecione **[!UICONTROL Concluir]** para salvar suas alterações e retornar à [!UICONTROL Políticas de mesclagem] guia.

>[!WARNING]
>
>Alterar uma política de mesclagem pode afetar a segmentação e os resultados do perfil, pois alterará a maneira como os conflitos de dados são resolvidos. Certifique-se de revisar cuidadosamente as alterações em suas políticas de mesclagem antes de salvá-las.

![](../images/merge-policies/edit-review.png)

## Violações da política de governança de dados

Ao criar ou atualizar uma política de mesclagem, uma verificação é executada para determinar se a política de mesclagem viola qualquer uma das políticas de uso de dados definidas pela organização. As políticas de uso de dados fazem parte da Governança de dados do Adobe Experience Platform e são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição de realizar em [!DNL Platform] dados. Por exemplo, se uma política de mesclagem fosse usada para criar um segmento que fosse ativado para um destino de terceiros e sua organização tivesse uma política de uso de dados que impedia a exportação de dados específicos para terceiros, você receberia uma **[!UICONTROL Violação da política de governança de dados detectada]** ao tentar salvar sua política de mesclagem.

Esta notificação inclui uma lista de políticas de uso de dados que foram violadas e permite exibir os detalhes da violação selecionando uma política na lista. Ao selecionar uma política violada, a **[!UICONTROL Linhagem de dados]** A guia fornece o motivo da violação e as ativações afetadas, cada uma fornecendo mais detalhes sobre como a política de uso de dados foi violada.

Para saber mais sobre como o controle de dados é executado no Adobe Experience Platform, comece lendo o [Visão geral da governança de dados](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Próximas etapas

Agora que você criou e configurou políticas de mesclagem para sua organização, é possível usá-las para ajustar a visualização de perfis de clientes na Platform e para criar segmentos de público-alvo com base nos dados do perfil. Consulte a [visão geral da segmentação](../../segmentation/home.md) para obter mais informações sobre como criar e trabalhar com segmentos usando o [!DNL Experience Platform] Interface do usuário e APIs.
