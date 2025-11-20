---
title: Guia da interface de políticas de mesclagem
type: Documentation
description: Saiba como trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 2%

---


# Guia da interface de políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Experience Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar a exibição unificada.

Usando APIs RESTful ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform.

Para saber mais sobre as políticas de mesclagem e a função que elas desempenham no Experience Platform, comece lendo a [visão geral das políticas de mesclagem](overview.md).

## Introdução

Este guia requer uma compreensão funcional de vários recursos importantes do [!DNL Experience Platform]. Antes de seguir este guia, consulte a documentação dos seguintes serviços:

* [Perfil de cliente em tempo real](../home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): habilita o Perfil de Cliente em Tempo Real unindo identidades de diferentes fontes de dados que estão sendo assimiladas em [!DNL Experience Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.

## Exibir políticas de mesclagem {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="Política de mesclagem não encontrada"
>abstract="Isso significa que a Experience Platform não encontrou a política de mesclagem solicitada. Para resolver esse erro, tente uma das seguintes soluções:<ul><li>Verifique se a ID da política de mesclagem correta está listada no URL.</li><li>Verifique se você tem a combinação correta de organização e sandbox para a política de mesclagem que está tentando acessar.</li></ul>"

Na interface do usuário do [!DNL Experience Platform], você pode começar a trabalhar com políticas de mesclagem selecionando **[!UICONTROL Profiles]** na navegação à esquerda e depois selecionando a guia **[!UICONTROL Merge Policies]**.

Essa guia inclui uma lista de todas as políticas de mesclagem existentes para sua organização, bem como detalhes para cada política de mesclagem, incluindo o nome da política, se a política de mesclagem é ou não a política de mesclagem padrão e a classe de esquema à qual a política de mesclagem está relacionada.

![A página de navegação das políticas de mesclagem é exibida.](../images/merge-policies/landing.png)

Para selecionar quais detalhes estão visíveis ou adicionar outras colunas à exibição, selecione ![o ícone de configurações de coluna](../../images/icons/column-settings.png) e selecione um nome de coluna para adicioná-lo ou removê-lo da exibição.

![As opções disponíveis para personalizar a página de navegação da política de mesclagem são exibidas.](../images/merge-policies/adjust-view.png)

## Criar uma política de mesclagem {#create-a-merge-policy}

Para criar uma nova política de mesclagem, selecione **[!UICONTROL Create merge policy]** na guia políticas de mesclagem para inserir o novo fluxo de trabalho da política de mesclagem.

![Página de aterrissagem das políticas de mesclagem com o botão criar realçado.](../images/merge-policies/create-new.png)

O fluxo de trabalho **[!UICONTROL New merge policy]** exige que você forneça informações importantes para sua nova política de mesclagem por meio de uma série de etapas guiadas. Essas etapas são descritas nas seções a seguir.

![O novo fluxo de trabalho da política de mesclagem.](../images/merge-policies/create.png)

## [!UICONTROL Configure] {#configure}

A primeira etapa do fluxo de trabalho permite configurar a política de mesclagem fornecendo informações básicas. Essas informações incluem:

* **[!UICONTROL Name]**: o nome da sua política de mesclagem deve ser descritivo, mas conciso.
* **[!UICONTROL Schema class]**: a classe de esquema XDM associada à política de mesclagem. Especifica a classe de esquema para a qual essa política de mesclagem é criada. As organizações podem criar várias políticas de mesclagem por classe de esquema. Atualmente, apenas a classe [!UICONTROL XDM Individual Profile] está disponível na interface do usuário. Você pode visualizar o esquema de união para a classe de esquema selecionando **[!UICONTROL View Union Schema]**. Para obter mais informações, consulte a seção sobre [exibição do esquema de união](#view-union-schema) a seguir.
* **[!UICONTROL ID stitching]**: este campo define como determinar as identidades relacionadas de um cliente. Há dois valores possíveis para a compilação de identidade, e é importante entender como o tipo de compilação de identidade que você seleciona afetará seus dados. Para saber mais, consulte a [visão geral das políticas de mesclagem](overview.md).
   * **[!UICONTROL None]**: Não executar nenhuma identificação de identidade.
   * **[!UICONTROL Private Graph]**: Execute a compilação de identidade com base em seu gráfico de identidade privado.
* **[!UICONTROL Default merge policy]**: um botão de alternância que permite selecionar se essa política de mesclagem será ou não o padrão para sua organização. Se o seletor estiver ativado, um aviso será exibido solicitando que você confirme se deseja alterar a política de mesclagem padrão da organização. Consulte a [visão geral das políticas de mesclagem](overview.md) para saber mais sobre políticas de mesclagem padrão.
  ![Um popover que explica o que acontece quando a política de mesclagem é definida como uma política de mesclagem padrão.](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge Merge Policy]**: Um botão de alternância que permite selecionar se essa política de mesclagem estará ou não ativa na borda. Para garantir que todos os consumidores de perfil estejam trabalhando com a mesma exibição nas bordas, as políticas de mesclagem podem ser marcadas como ativas na borda. Para que um público-alvo seja ativado na borda (marcado como um público-alvo de borda), ele deve estar vinculado a uma política de mesclagem marcada como ativo na borda. Se um público-alvo estiver **não** vinculado a uma política de mesclagem marcada como ativo na borda, o público-alvo não será marcado como ativo na borda e será marcado como um público de streaming. Além disso, cada sandbox em uma Organização só pode ter **uma** política de mesclagem ativa na borda.

Depois que os campos obrigatórios forem preenchidos, você poderá selecionar **[!UICONTROL Next]** para continuar com o fluxo de trabalho.

![Uma tela Configurar concluída com o botão Avançar realçado.](../images/merge-policies/create-complete.png)

## [!UICONTROL View Union Schema] {#view-union-schema}

Ao criar ou editar uma política de mesclagem, você pode visualizar o esquema de união para a classe de esquema escolhida selecionando **[!UICONTROL View Union Schema]**.

![O botão &quot;Exibir Esquema de União&quot; está realçado no fluxo de trabalho Nova política de mesclagem.](../images/merge-policies/view-union-schema.png)

Isso abre a caixa de diálogo [!UICONTROL View Union Schema], mostrando todos os esquemas, identidades e relações de contribuição associados ao esquema de união. Você pode usar a caixa de diálogo para explorar o esquema de união da mesma forma que faria ao acessar a guia [!UICONTROL Union Schema] na seção [!UICONTROL Profiles] da interface do usuário do Experience Platform.

Para obter informações detalhadas sobre esquemas de união, incluindo como interagir com eles na guia [!UICONTROL Union Schema] ou na caixa de diálogo [!UICONTROL View Union Schema] mostrada no fluxo de trabalho políticas de mesclagem, visite o [guia da interface do esquema de união](../ui/union-schema.md).

![A caixa de diálogo Exibir esquema de união.](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Select Profile datasets] {#select-profile-datasets}

Na tela **[!UICONTROL Select Profile datasets]**, selecione o **[!UICONTROL Merge method]** que deseja usar para a política de mesclagem. Também exibido na tela é o número total de [!UICONTROL Profile datasets] em sua organização relacionados à classe de esquema selecionada na tela anterior.

Dependendo do método de mesclagem escolhido, todos os conjuntos de dados do Perfil serão mesclados pela ordem em que foram atualizados pela última vez (carimbo de data e hora ordenado) ou você precisará selecionar quais conjuntos de dados do Perfil incluir na política de mesclagem e a ordem em que eles serão mesclados (precedência do conjunto de dados).

Para obter mais informações sobre métodos de mesclagem, consulte a [visão geral das políticas de mesclagem](overview.md).

>[!BEGINTABS]

>[!TAB Carimbo de data/hora ordenado]

Selecionar **[!UICONTROL Timestamp ordered]** como método de mesclagem significa que os atributos dos conjuntos de dados atualizados mais recentemente terão prioridade. Isso se aplica a todos os conjuntos de dados do Perfil.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL Profile datasets]** (por exemplo, `(37)` na imagem mostrada) mostra o número total de conjuntos de dados de perfil que serão incluídos.

![Uma imagem que exibe o método de mesclagem ordenada por carimbo de data/hora que está sendo selecionado.](../images/merge-policies/timestamp-ordered.png)

>[!TAB Prioridade de conjunto de dados]

Selecionar **[!UICONTROL Dataset precedence]** como método de mesclagem exige que você selecione conjuntos de dados de perfil e os priorize manualmente. Cada conjunto de dados listado também inclui o status do último lote assimilado ou exibe um aviso de que nenhum lote foi assimilado nesse conjunto de dados.

É possível selecionar até 50 conjuntos de dados na lista de conjuntos de dados para incluir na política de mesclagem.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL Profile datasets]** (por exemplo, `(37)` na imagem mostrada) mostra o número total de conjuntos de dados de perfil disponíveis para seleção.

À medida que os conjuntos de dados são selecionados, eles são adicionados à seção **[!UICONTROL Select datasets]**, permitindo arrastar e soltar os conjuntos de dados e ordená-los de acordo com a precedência desejada. À medida que os conjuntos de dados são ajustados na lista, o ordinal (1, 2, 3 etc.) ao lado do conjunto de dados será atualizado, exibindo a prioridade (1 tendo a prioridade mais alta, depois 2 e adiante).

Selecionar um conjunto de dados também atualiza a seção **[!UICONTROL Union schema]**, mostrando os campos no esquema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre esquemas de união, incluindo como interagir com as visualizações na interface, consulte o [guia da interface do esquema de união](../ui/union-schema.md)

![Uma imagem que exibe a precedência do conjunto de dados que está sendo selecionado, juntamente com as configurações correspondentes que você precisa escolher se essa opção está selecionada.](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

A próxima etapa do fluxo de trabalho requer que você selecione conjuntos de dados ExperienceEvent. Esta tela é influenciada pelo método de mesclagem selecionado na tela [[!UICONTROL Select Profile datasets]](#select-profile-datasets).

>[!BEGINTABS]

>[!TAB Carimbo de data/hora ordenado]

Se você selecionou **[!UICONTROL Timestamp ordered]** como o método de mesclagem para conjuntos de dados de Perfil, os atributos dos conjuntos de dados ExperienceEvent atualizados mais recentemente também terão prioridade aqui.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL ExperienceEvent datasets]** (por exemplo, `(1)` na imagem mostrada) mostra o número total de conjuntos de dados ExperienceEvent criados por sua organização que estão relacionados à classe de esquema selecionada na tela de configuração da política de mesclagem.

![The total number of ExperienceEvent datasets that can relate to the schema class is displayed.](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB Prioridade de conjunto de dados]

If you selected **[!UICONTROL Dataset precedence]** as the merge method for Profile datasets, you will need to select ExperienceEvent datasets to include. You can select up to 50 ExperienceEvent datasets from the dataset list.

>[!NOTE]
>
>O número entre parênteses ao lado de **[!UICONTROL ExperienceEvent datasets]** (por exemplo, `(1)` na imagem mostrada) mostra o número total de conjuntos de dados ExperienceEvent criados por sua organização que estão relacionados à classe de esquema selecionada na tela de configuração da política de mesclagem.

À medida que os conjuntos de dados são selecionados, eles aparecem na seção [!UICONTROL Select datasets].

Os conjuntos de dados ExperienceEvent não podem ser ordenados manualmente, em vez disso, os atributos nos conjuntos de dados ExperienceEvent são anexados aos conjuntos de dados do Perfil se fizerem parte do mesmo fragmento de perfil.

Semelhante à seleção de conjuntos de dados de Perfil, a seleção de um conjunto de dados ExperienceEvent também atualiza a seção **[!UICONTROL Union schema]**, mostrando os campos no esquema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre esquemas de união, incluindo como interagir com as visualizações na interface, consulte o [guia da interface do esquema de união](../ui/union-schema.md).

![Os conjuntos de dados ExperienceEvent selecionáveis são exibidos.](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Review] {#review}

A etapa final do fluxo de trabalho é revisar a política de mesclagem. A tela **[!UICONTROL Review]** exibe informações sobre sua política de mesclagem, incluindo o método de compilação de ID selecionado, o método de mesclagem selecionado e os conjuntos de dados incluídos. (Para exibir todos os conjuntos de dados de Perfil ou ExperienceEvent incluídos, selecione o número de conjuntos de dados para expandir a lista suspensa.)

Também incluída na tela de revisão é a tabela **[!UICONTROL Preview data]**, que mostra exemplos de registros de perfil usando sua política de mesclagem. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar a política de mesclagem.

Revise a configuração da política de mesclagem e visualize os dados cuidadosamente antes de selecionar **[!UICONTROL Finish]** para concluir o fluxo de trabalho de criação.

>[!BEGINTABS]

>[!TAB Carimbo de data/hora ordenado]

Se você selecionou **[!UICONTROL Timestamp ordered]** como método de mesclagem para sua política de mesclagem, a lista de conjuntos de dados de Perfil incluirá todos os conjuntos de dados que foram criados por sua organização relacionados à classe de esquema, em ordem de carimbo de data e hora. A lista de conjuntos de dados ExperienceEvent inclui todos os conjuntos de dados que sua organização criou para a classe de esquema escolhida e serão anexados aos conjuntos de dados do Perfil.

A tabela **[!UICONTROL Preview data]** mostra registros de perfil de exemplo com base em uma ordenação de carimbo de data/hora dos conjuntos de dados. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar a política de mesclagem.

Selecione **[!UICONTROL Finish]** para criar sua nova política de mesclagem.

![A página Revisar é exibida. Esta página permite examinar os detalhes da política de mesclagem recém-criada.](../images/merge-policies/timestamp-review.png)

>[!TAB Prioridade de conjunto de dados]

Se você selecionou **[!UICONTROL Dataset precedence]** como método de mesclagem para sua política de mesclagem, as listas de conjuntos de dados Profile e ExperienceEvent incluirão apenas os conjuntos de dados Profile e ExperienceEvent selecionados durante o fluxo de trabalho de criação, respectivamente. A ordem dos conjuntos de dados do Perfil deve corresponder à precedência especificada durante a criação. Caso contrário, use o botão [!UICONTROL Back] para retornar às etapas anteriores do fluxo de trabalho e ajustar a prioridade.

A tabela **[!UICONTROL Preview data]** mostra registros de perfil de exemplo usando os conjuntos de dados selecionados. Isso permite que você visualize a aparência de um perfil de cliente antes de salvar a política de mesclagem.

Selecione **[!UICONTROL Finish]** para criar sua nova política de mesclagem.

![A página Revisar é exibida. Esta página permite examinar os detalhes da política de mesclagem recém-criada.](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## Editar uma política de mesclagem {#edit}

Na guia [!UICONTROL Merge Policies], você pode modificar uma política de mesclagem existente criada para a classe [!DNL XDM Individual Profile] selecionando o **[!UICONTROL Policy name]** da política de mesclagem que deseja editar.

Quando a tela **[!UICONTROL Edit merge policy]** for exibida, você poderá fazer alterações no nome e no método [!UICONTROL ID stitching], bem como alterar se essa política é ou não a política de mesclagem padrão para sua organização.

Selecione **[!UICONTROL Next]** para continuar pelo fluxo de trabalho da política de mesclagem para atualizar o método de mesclagem e os conjuntos de dados incluídos na política de mesclagem.

![O fluxo de trabalho de edição de política de mesclagem é exibido.](../images/merge-policies/edit-screen.png)

Depois de fazer as alterações necessárias, revise sua política de mesclagem e selecione **[!UICONTROL Finish]** para salvar suas alterações e retornar à guia [!UICONTROL Merge policies].

>[!WARNING]
>
>Alterar uma política de mesclagem pode afetar a segmentação e os resultados do perfil, pois alterará a maneira como os conflitos de dados são resolvidos. Certifique-se de revisar cuidadosamente as alterações em suas políticas de mesclagem antes de salvá-las.

![A página de revisão do fluxo de trabalho de edição de política é exibida.](../images/merge-policies/edit-review.png)

## Violações da política de governança de dados

Ao criar ou atualizar uma política de mesclagem, uma verificação é executada para determinar se a política de mesclagem viola qualquer uma das políticas de uso de dados definidas pela organização. As políticas de uso de dados fazem parte da Governança de dados da Adobe Experience Platform e são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados específicos do [!DNL Experience Platform].

Por exemplo, se uma política de mesclagem fosse usada para criar um público-alvo que fosse ativado para um destino de terceiros, e sua organização tivesse uma política de uso de dados que impedia a exportação de dados específicos para terceiros, você receberia uma notificação do **[!UICONTROL Data governance policy violation detected]** ao tentar salvar sua política de mesclagem.

Esta notificação inclui uma lista de políticas de uso de dados que foram violadas e permite exibir os detalhes da violação selecionando uma política na lista. Ao selecionar uma política violada, a guia **[!UICONTROL Data lineage]** fornece o motivo da violação e as ativações afetadas, cada uma fornecendo mais detalhes sobre como a política de uso de dados foi violada.

Para saber mais sobre como a governança de dados é realizada no Adobe Experience Platform, comece lendo a [visão geral da Governança de dados](../../data-governance/home.md).

## Próximas etapas

Agora que você criou e configurou políticas de mesclagem para sua organização, é possível usá-las para ajustar a visualização de perfis de clientes no Experience Platform e para criar públicos-alvo a partir dos dados do perfil. Consulte a [visão geral da segmentação](../../segmentation/home.md) para obter mais informações sobre como criar e trabalhar com públicos usando a interface e as APIs do [!DNL Experience Platform].
