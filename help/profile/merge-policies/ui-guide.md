---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, políticas de mesclagem, interface do usuário, interface do usuário, carimbo de data e hora solicitado, precedência do conjunto de dados
title: Guia da interface do usuário de políticas de mesclagem
type: Documentation
description: Ao reunir dados de várias fontes no Experience Platform, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar a exibição unificada. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: e0a75a75e5dbb0318ec8785d887d7a156d28f5bd
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 0%

---


# Guia da interface do usuário de políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao unir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] O usa o para determinar como os dados serão priorizados e quais dados serão combinados para criar a visualização unificada.

Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform (UI).

Para saber mais sobre as políticas de mesclagem e sobre o papel que desempenham no Experience Platform, por favor comece lendo o [visão geral das políticas de mesclagem](overview.md).

## Introdução

Este guia requer uma compreensão funcional de vários [!DNL Experience Platform] recursos. Antes de seguir este guia, reveja a documentação dos seguintes serviços:

* [Perfil do cliente em tempo real](../home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): Habilita o Perfil do cliente em tempo real ao unir identidades de fontes de dados diferentes que estão sendo assimiladas no [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

## Exibir políticas de mesclagem {#view-merge-policies}

No [!DNL Experience Platform] IU, você pode começar a trabalhar com políticas de mesclagem selecionando **[!UICONTROL Perfis]** na navegação à esquerda e, em seguida, selecionando o **[!UICONTROL Políticas de Mesclagem]** guia . Esta guia inclui uma lista de todas as políticas de mesclagem existentes para sua organização, bem como detalhes de cada política de mesclagem, incluindo o nome da política, se a política de mesclagem é ou não a política de mesclagem padrão e a classe de schema à qual a política de mesclagem está relacionada.

![Página inicial de políticas de mesclagem](../images/merge-policies/landing.png)

Para selecionar quais detalhes estão visíveis ou para adicionar mais colunas à exibição, selecione **[!UICONTROL Configurar colunas]** e clique no nome de uma coluna para adicioná-la ou removê-la da exibição.

![](../images/merge-policies/adjust-view.png)

## Criar uma política de mesclagem {#create-a-merge-policy}

Para criar uma nova política de mesclagem, selecione **[!UICONTROL Criar política de mesclagem]** na guia merge policies para inserir o novo workflow de política de mesclagem.

![Mesclar a landing page de políticas com o botão criar destacado.](../images/merge-policies/create-new.png)

O **[!UICONTROL Nova política de mesclagem]** , requer que você forneça informações importantes para sua nova política de mesclagem por meio de uma série de etapas guiadas. Essas etapas são descritas nas seções a seguir.

![O novo fluxo de trabalho da política de mesclagem.](../images/merge-policies/create.png)

## [!UICONTROL Configurar] {#configure}

A primeira etapa do fluxo de trabalho permite configurar a política de mesclagem fornecendo informações básicas. Essas informações incluem:

* **[!UICONTROL Nome]**: O nome da sua política de mesclagem deve ser descritivo, mas conciso.
* **[!UICONTROL Classe de esquema]**: A classe de esquema XDM associada à política de mesclagem. Especifica a classe de schema para a qual essa política de mesclagem é criada. As organizações podem criar várias políticas de mesclagem por classe de esquema. Atualmente, somente o [!UICONTROL Perfil individual XDM] A classe está disponível na interface do usuário do . Você pode visualizar o schema de união para a classe de esquema selecionando **[!UICONTROL Exibir Esquema de União]**. Para obter mais informações, consulte a seção em [visualização do schema de união](#view-union-schema) o que se segue.
* **[!UICONTROL Compilação de ID]**: Este campo define como determinar as identidades relacionadas de um cliente. Há dois valores possíveis para a identificação e é importante entender como o tipo de identificação selecionada afetará seus dados. Para saber mais, consulte o [visão geral das políticas de mesclagem](overview.md).
   * **[!UICONTROL Nenhum]**: Não execute nenhum agrupamento de identidade.
   * **[!UICONTROL Gráfico privado]**: Realize a identificação com base no gráfico de identidade privado.
* **[!UICONTROL Política de mesclagem padrão]**: Um botão de alternância que permite selecionar se essa política de mesclagem será ou não o padrão para sua organização. Se o seletor estiver ligado, será exibido um aviso solicitando que você confirme que deseja alterar a política de mesclagem padrão da sua organização. Consulte a [visão geral das políticas de mesclagem](overview.md) para saber mais sobre as políticas de mesclagem padrão.
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Política de Mesclagem Ativa On-Edge]**: Um botão de alternância que permite selecionar se essa política de mesclagem estará ou não ativa no Edge. Para garantir que todos os consumidores de perfil estejam trabalhando com a mesma exibição nas bordas, as políticas de mesclagem podem ser marcadas como ativas na borda. Para que um segmento seja ativado na borda (marcado como um segmento de borda), ele deve ser vinculado a uma política de mesclagem marcada como ativa na borda. Se um segmento for **not** vinculado a uma política de mesclagem marcada como ativa na borda, o segmento não será marcado como ativo na borda e será marcado como um segmento de streaming. Além disso, cada Organização IMS só pode ter **one** política de mesclagem ativa no edge.

Depois que os campos obrigatórios forem preenchidos, é possível selecionar **[!UICONTROL Próximo]** para continuar com o workflow.

![Uma tela Configure (Configurar) completa com o botão Next (Avançar) é realçada.](../images/merge-policies/create-complete.png)

## [!UICONTROL Exibir Esquema de União] {#view-union-schema}

Ao criar ou editar uma política de mesclagem, você pode exibir o schema de união para a classe de schema escolhida selecionando **[!UICONTROL Exibir Esquema de União]**.

![](../images/merge-policies/view-union-schema.png)

Isso abre o [!UICONTROL Exibir Esquema de União] , mostrando todos os esquemas, identidades e relações de contribuição associados ao esquema de união. Você pode usar a caixa de diálogo para explorar o schema da união da mesma maneira que faria acessando a variável [!UICONTROL Esquema de união] na guia no [!UICONTROL Perfis] da interface do usuário da plataforma.

Para obter informações detalhadas sobre schemas da união, incluindo como interagir com eles no [!UICONTROL Esquema de união] ou a guia [!UICONTROL Exibir Esquema de União] exibida no fluxo de trabalho das políticas de mesclagem, visite o [guia da interface do usuário do schema de união](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Selecionar conjuntos de dados do perfil] {#select-profile-datasets}

No **[!UICONTROL Selecionar conjuntos de dados do perfil]** , você deve selecionar a variável **[!UICONTROL Método de mesclagem]** que você deseja usar para a política de mesclagem. Também é exibido na tela o número total de [!UICONTROL Conjuntos de dados de perfil] na organização relacionada à classe de esquema selecionada na tela anterior.

Dependendo do método de mesclagem escolhido, todos os conjuntos de dados do Perfil serão mesclados pela ordem em que foram atualizados pela última vez (carimbo de data e hora solicitado) ou será necessário selecionar quais conjuntos de dados do Perfil serão incluídos na política de mesclagem e na ordem em que serão mesclados (precedência do conjunto de dados).

Para obter mais informações sobre métodos de mesclagem, consulte [visão geral das políticas de mesclagem](overview.md).

### Carimbo de data e hora ordenado {#timestamp-ordered-profile}

Selecionar **[!UICONTROL Carimbo de data e hora ordenado]** como o método de mesclagem significa que os atributos dos conjuntos de dados atualizados mais recentemente terão prioridade. Isso se aplica a todos os conjuntos de dados do Perfil.

>[!NOTE]
>
>O número entre colchetes ao lado de **[!UICONTROL Conjuntos de dados de perfil]** (por exemplo, `(37)` na imagem exibida) mostra o número total de conjuntos de dados de perfil que serão incluídos.

![](../images/merge-policies/timestamp-ordered.png)

### Precedência do conjunto de dados {#dataset-precedence-profile}

Selecionar **[!UICONTROL Precedência do conjunto de dados]** como o método merge requer a seleção de Conjuntos de dados de perfil e a priorização manual deles. Cada conjunto de dados listado também inclui o status do último lote assimilado ou exibe um aviso de que nenhum lote foi assimilado nesse conjunto de dados.

É possível selecionar até 50 conjuntos de dados na lista de conjuntos de dados para incluir na política de mesclagem.

>[!NOTE]
>
>O número entre colchetes ao lado de **[!UICONTROL Conjuntos de dados de perfil]** (por exemplo, `(37)` na imagem exibida) mostra o número total de conjuntos de dados de perfil disponíveis para seleção.

À medida que os conjuntos de dados são selecionados, eles são adicionados à variável **[!UICONTROL Selecionar conjuntos de dados]** , permitindo arrastar e soltar os conjuntos de dados e ordená-los de acordo com a precedência desejada. Conforme os conjuntos de dados são ajustados na lista, o ordinal (1, 2, 3, etc) ao lado do conjunto de dados será atualizado, exibindo a prioridade (1 sendo atribuída a prioridade mais alta, depois 2 e depois).

A seleção de um conjunto de dados também atualiza o **[!UICONTROL Schema da União]** , mostrando os campos no schema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre schemas de união, incluindo como interagir com as visualizações na interface do usuário, consulte o [guia da interface do usuário do schema de união](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Selecionar conjuntos de dados do ExperienceEvent] {#select-experienceevent-datasets}

A próxima etapa do fluxo de trabalho requer a seleção de conjuntos de dados do ExperienceEvent . Essa tela é influenciada pelo método de mesclagem selecionado no [[!UICONTROL Selecionar conjuntos de dados do perfil]](#select-profile-datasets) tela.

### Carimbo de data e hora ordenado {#timestamp-ordered-experienceevent}

Se você selecionou **[!UICONTROL Carimbo de data e hora ordenado]** como método de mesclagem para conjuntos de dados de Perfil, os atributos dos conjuntos de dados ExperienceEvent atualizados mais recentemente também terão prioridade aqui.

>[!NOTE]
>
>O número entre colchetes ao lado de **[!UICONTROL Conjuntos de dados ExperienceEvent]** (por exemplo, `(20)` na imagem exibida) mostra o número total de conjuntos de dados do ExperienceEvent criados por sua organização que estão relacionados à classe de esquema selecionada na tela de configuração da política de mesclagem.

![](../images/merge-policies/timestamp-experienceevent.png)

### Precedência do conjunto de dados {#dataset-precedence-experienceevent}

Se você selecionou **[!UICONTROL Precedência do conjunto de dados]** como método de mesclagem para conjuntos de dados de Perfil, é necessário selecionar os conjuntos de dados do ExperienceEvent para incluir. Você pode selecionar até 50 conjuntos de dados do ExperienceEvent na lista de conjuntos de dados.

>[!NOTE]
>
>O número entre colchetes ao lado de **[!UICONTROL Conjuntos de dados ExperienceEvent]** (por exemplo, `(20)` na imagem exibida) mostra o número total de conjuntos de dados do ExperienceEvent criados por sua organização que estão relacionados à classe de esquema selecionada na tela de configuração da política de mesclagem.

À medida que os conjuntos de dados são selecionados, eles são exibidos na variável [!UICONTROL Selecionar conjuntos de dados] seção.

Os conjuntos de dados do ExperienceEvent não podem ser ordenados manualmente, em vez disso, os atributos nos conjuntos de dados do ExperienceEvent são anexados aos conjuntos de dados do Perfil se fizerem parte do mesmo fragmento de perfil.

Semelhante à seleção de conjuntos de dados de Perfil, selecionar um conjunto de dados ExperienceEvent também atualiza o **[!UICONTROL Schema da União]** , mostrando os campos no schema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre schemas de união, incluindo como interagir com as visualizações na interface do usuário, consulte o [guia da interface do usuário do schema de união](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Revisão] {#review}

A etapa final do fluxo de trabalho é revisar sua política de mesclagem. O **[!UICONTROL Revisão]** exibe informações sobre sua política de mesclagem, incluindo o método de compilação de ID selecionado, o método de mesclagem selecionado e os conjuntos de dados incluídos. (Para exibir todos os conjuntos de dados do Perfil ou ExperienceEvent incluídos, selecione o número de conjuntos de dados para expandir a lista suspensa.)

Também está incluído na tela de revisão o **[!UICONTROL Visualizar dados]** tabela que mostra exemplos de registros de perfil usando sua política de mesclagem. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar sua política de mesclagem.

Certifique-se de analisar a configuração da política de mesclagem e visualizar os dados cuidadosamente antes de selecionar **[!UICONTROL Concluir]** para concluir o workflow de criação.

### Carimbo de data e hora ordenado {#timestamp-ordered-review}

Se você selecionou **[!UICONTROL Carimbo de data e hora ordenado]** como método de mesclagem para sua política de mesclagem, a lista de conjuntos de dados de Perfil inclui todos os conjuntos de dados que foram criados por sua organização relacionados à classe de esquema, em ordem de carimbo de data e hora. A lista de conjuntos de dados do ExperienceEvent inclui todos os conjuntos de dados que sua organização criou para a classe de esquema escolhida e será anexada aos conjuntos de dados do Perfil.

O **[!UICONTROL Visualizar dados]** tabela mostra exemplos de registros de perfil com base em uma ordem de data e hora dos conjuntos de dados. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar sua política de mesclagem.

![](../images/merge-policies/timestamp-review.png)

### Precedência do conjunto de dados {#dataset-precedence-review}

Se você selecionou **[!UICONTROL Precedência do conjunto de dados]** como método de mesclagem para sua política de mesclagem, as listas de conjuntos de dados Perfil e ExperienceEvent incluem somente os conjuntos de dados Perfil e ExperienceEvent selecionados durante o fluxo de trabalho de criação, respectivamente. A ordem dos conjuntos de dados do Perfil deve corresponder à precedência especificada durante a criação. Caso contrário, use a variável [!UICONTROL Voltar] para retornar às etapas anteriores do fluxo de trabalho e ajustar a prioridade.

O **[!UICONTROL Visualizar dados]** mostra exemplos de registros de perfil usando os conjuntos de dados selecionados. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar sua política de mesclagem.

![](../images/merge-policies/dataset-precedence-review.png)

### Atualização da lista de políticas de mesclagem {#updated-list}

Após concluir o fluxo de trabalho para criar uma nova política de mesclagem, você volta para a **[!UICONTROL Políticas de Mesclagem]** guia . A lista de políticas de mesclagem para sua organização agora deve incluir a política de mesclagem que você acabou de criar.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar uma política de mesclagem

No [!UICONTROL Políticas de Mesclagem] você pode modificar uma política de mesclagem existente criada para a [!DNL XDM Individual Profile] selecionando a **[!UICONTROL Nome da política]** para a política de mesclagem que deseja editar.

![Página inicial de políticas de mesclagem](../images/merge-policies/select-edit.png)

Quando a variável **[!UICONTROL Editar política de mesclagem]** for exibida, você poderá fazer alterações no nome e [!UICONTROL Compilação de ID] , bem como alterar se essa política é ou não a política de mesclagem padrão da sua organização.

Selecionar **[!UICONTROL Próximo]** para continuar pelo fluxo de trabalho da política de mesclagem para atualizar o método de mesclagem e os conjuntos de dados incluídos na política de mesclagem.

![](../images/merge-policies/edit-screen.png)

Depois de fazer as alterações necessárias, revise a política de mesclagem e selecione **[!UICONTROL Concluir]** para salvar suas alterações e retornar ao [!UICONTROL Mesclar políticas] guia .

>[!WARNING]
>
>Alterar uma política de mesclagem pode afetar a segmentação e os resultados do perfil, pois alterará a maneira como os conflitos de dados são resolvidos. Certifique-se de revisar as alterações nas suas políticas de mesclagem cuidadosamente antes de salvá-las.

![](../images/merge-policies/edit-review.png)

## Violações da política de governança de dados

Ao criar ou atualizar uma política de mesclagem, é feita uma verificação para determinar se a política de mesclagem viola qualquer uma das políticas de uso de dados definidas pela organização. As políticas de uso de dados fazem parte do Adobe Experience Platform [!DNL Data Governance] e são regras que descrevem os tipos de ações de marketing das quais você tem permissão ou é restrito para executar em [!DNL Platform] dados. Por exemplo, se uma política de mesclagem foi usada para criar um segmento que foi ativado para um destino de terceiros e sua organização tinha uma política de uso de dados que impedia a exportação de dados específicos para terceiros, você receberia uma **[!UICONTROL Violação da política de controle de dados detectada]** ao tentar salvar sua política de mesclagem.

Esta notificação inclui uma lista de políticas de uso de dados que foram violadas e permite visualizar os detalhes da violação selecionando uma política na lista. Ao selecionar uma política violada, a variável **[!UICONTROL Linhagem de dados]** A guia fornece o motivo da violação e das ativações afetadas, cada uma fornecendo mais detalhes sobre como a política de uso de dados foi violada.

Para saber mais sobre como o controle de dados é executado no Adobe Experience Platform, comece lendo o [Visão geral da governança de dados](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Próximas etapas

Depois de criar e configurar políticas de mesclagem para sua organização, você pode usá-las para ajustar a exibição dos perfis do cliente no Platform e criar segmentos de público-alvo a partir dos dados do Perfil. Consulte a [visão geral da segmentação](../../segmentation/home.md) para obter mais informações sobre como criar e trabalhar com segmentos usando o [!DNL Experience Platform] Interface do usuário e APIs.
