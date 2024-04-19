---
keywords: Experience Platform;início;tópicos populares;habilitar conjunto de dados;conjunto de dados;conjunto de dados;;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guia da interface de conjuntos de dados
description: Saiba como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: b033f96002ed6da25cd6eb7012c397405dd85896
workflow-type: tm+mt
source-wordcount: '2943'
ht-degree: 3%

---

# Guia da interface do usuário de conjuntos de dados

Este guia do usuário fornece instruções sobre como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.

## Introdução

Este guia do usuário requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Conjuntos de dados](overview.md): a construção de armazenamento e gerenciamento para a persistência de dados no [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Editor de esquema](../../xdm/tutorials/create-schema-ui.md): saiba como criar seus próprios esquemas XDM personalizados usando o [!DNL Schema Editor] no prazo de [!DNL Platform] interface do usuário.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): garanta a conformidade com as regulamentações, as restrições e as políticas relacionadas ao uso dos dados do cliente.

## Visualizar conjuntos de dados {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Números negativos na atividade do conjunto de dados"
>abstract="Números negativos em registros assimilados significam que um usuário excluiu determinados lotes em um intervalo de tempo selecionado."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="Expiração do conjunto de dados"
>abstract="Esta coluna indica o número de dias que o conjunto de dados de destino tem antes de expirar automaticamente."

No [!DNL Experience Platform] Interface, selecione **[!UICONTROL Conjuntos de dados]** no painel de navegação esquerdo para abrir a **[!UICONTROL Conjuntos de dados]** painel. O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo seu nome, o esquema ao qual o conjunto de dados adere e o status da execução de ingestão mais recente.

![A interface do usuário da Platform com o item Conjuntos de dados realçado na barra de navegação à esquerda.](../images/datasets/user-guide/browse-datasets.png)

Selecione o nome de um conjunto de dados na [!UICONTROL Procurar] para acessar seu **[!UICONTROL Atividade do conjunto de dados]** e veja detalhes do conjunto de dados selecionado. A guia Atividade inclui um gráfico que visualiza a taxa de mensagens que estão sendo consumidas, bem como uma lista de lotes bem-sucedidos e com falha.

![As métricas e visualizações do conjunto de dados selecionado são destacadas.](../images/datasets/user-guide/dataset-activity-1.png)
![Os lotes de amostra relacionados ao conjunto de dados selecionado são destacados.](../images/datasets/user-guide/dataset-activity-2.png)

## Mais ações {#more-actions}

Você pode [!UICONTROL Excluir] ou [!UICONTROL Ativar um conjunto de dados para o Perfil] do [!UICONTROL Conjunto de dados] exibição de detalhes. Para ver as ações disponíveis, selecione **[!UICONTROL .. Mais]** na parte superior direita da interface do usuário. O menu suspenso é exibido.

![O espaço de trabalho dos conjuntos de dados com o [!UICONTROL .. Mais] menu suspenso realçado.](../images/datasets/user-guide/more-actions.png)

Se você selecionar **[!UICONTROL Ativar um conjunto de dados para o Perfil]**, uma caixa de diálogo de confirmação será exibida. Selecionar **[!UICONTROL Ativar]** para confirmar sua escolha.

>[!NOTE]
>
>Para habilitar um conjunto de dados para o Perfil, o esquema que o conjunto de dados segue deve ser compatível para uso no Perfil do cliente em tempo real. Consulte a [Ativar um conjunto de dados para o perfil](#enable-profile) para obter mais informações.

![A caixa de diálogo de confirmação Habilitar conjunto de dados.](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

Se você selecionar **[!UICONTROL Excluir]**, o [!UICONTROL Excluir conjunto de dados] confirmação será exibida. Selecionar **[!UICONTROL Excluir]** para confirmar sua escolha.

>[!NOTE]
>
>Não é possível excluir conjuntos de dados do sistema.

Você também pode excluir um conjunto de dados ou adicionar um conjunto de dados para uso com o Perfil de cliente em tempo real a partir das ações embutidas encontradas no [!UICONTROL Procurar] guia. Consulte a [seção ações embutidas](#inline-actions) para obter mais informações.

![O diálogo de confirmação Excluir conjunto de dados.](../images/datasets/user-guide/delete-confirmation-dialog.png)

## Ações embutidas do conjunto de dados {#inline-actions}

A interface dos conjuntos de dados agora oferece uma coleção de ações em linha para cada conjunto de dados disponível. Selecione as reticências (...) de um conjunto de dados que você deseja gerenciar para ver as opções disponíveis em um menu pop-up. As ações disponíveis incluem: [[!UICONTROL Visualizar conjunto de dados]](#preview), [[!UICONTROL Gerenciar dados e acessar rótulos]](#manage-and-enforce-data-governance), [[!UICONTROL Ativar perfil unificado]](#enable-profile), [[!UICONTROL Gerenciar tags]](#add-tags), [[!UICONTROL Mover para pastas]](#move-to-folders), e [[!UICONTROL Excluir]](#delete). Mais informações sobre essas ações disponíveis podem ser encontradas nas respectivas seções.

### Adicionar tags de conjunto de dados {#add-tags}

Adicione tags criadas personalizadas para organizar conjuntos de dados e melhorar os recursos de pesquisa, filtragem e classificação. No [!UICONTROL Procurar] guia do [!UICONTROL Conjuntos de dados] selecione as reticências de um conjunto de dados que deseja gerenciar, seguidas por **[!UICONTROL Gerenciar tags]** no menu suspenso.

![A guia Procurar do espaço de trabalho Conjuntos de dados com a opção de reticências e Gerenciar tags foi destacada para o conjunto de dados escolhido.](../images/datasets/user-guide/manage-tags.png)

A variável [!UICONTROL Gerenciar tags] será exibida. Insira uma breve descrição para criar uma tag personalizada ou escolha em uma tag pré-existente para rotular seu conjunto de dados. Selecionar **[!UICONTROL Salvar]** para confirmar as configurações.

![A caixa de diálogo Gerenciar tags com tags personalizadas destacadas.](../images/datasets/user-guide/manage-tags-dialog.png)

A variável [!UICONTROL Gerenciar tags] A caixa de diálogo também pode remover tags existentes de um conjunto de dados. Basta selecionar o &quot;x&quot; ao lado da tag que deseja remover e selecionar **[!UICONTROL Salvar]**.

Depois que uma tag é adicionada a um conjunto de dados, os conjuntos de dados podem ser filtrados com base na tag correspondente. Consulte a seção sobre como [filtrar conjuntos de dados por tags](#enable-profile) para obter mais informações.

Para obter mais informações sobre como classificar objetos comerciais para facilitar a descoberta e a categorização, consulte o manual sobre [gerenciamento de taxonomias de metadados](../../administrative-tags/ui/managing-tags.md). Este guia detalha como um usuário com permissões apropriadas pode criar tags predefinidas, atribuir categorias a tags e executar todas as operações CRUD relacionadas em tags e categorias de tags na interface do usuário da Platform.

## Pesquisar e filtrar conjuntos de dados {#search-and-filter}

Para pesquisar ou filtrar a lista de conjuntos de dados disponíveis, selecione o ícone de filtro (![O ícone de filtro.](../images/datasets/user-guide/icon.png)) na parte superior esquerda do espaço de trabalho. Um conjunto de opções de filtro no painel esquerdo é exibido. Há vários métodos para filtrar seus conjuntos de dados disponíveis. Isso inclui: [[!UICONTROL Mostrar conjuntos de dados do sistema]](#show-system-datasets), [[!UICONTROL Incluído no perfil]](#filter-profile-enabled-datasets), [[!UICONTROL Tags]](#filter-by-tag), [[!UICONTROL Data de criação]](#filter-by-creation-date), [[!UICONTROL Data de modificação], [!UICONTROL Criado por]](#filter-by-creation-date), e [[!UICONTROL Esquema]](#filter-by-schema).

A lista de filtros aplicados é exibida acima dos resultados filtrados.

![A guia Procurar do espaço de trabalho Conjuntos de dados com a lista de filtros aplicados destacada.](../images/datasets/user-guide/applied-filters.png)

### Mostrar conjuntos de dados do sistema {#show-system-datasets}

Por padrão, somente os conjuntos de dados que você assimilou no são mostrados. Se quiser ver os conjuntos de dados gerados pelo sistema, selecione a variável **[!UICONTROL Sim]** caixa de seleção na caixa [!UICONTROL Mostrar conjuntos de dados do sistema] seção. Os conjuntos de dados gerados pelo sistema são usados apenas para processar outros componentes. Por exemplo, o conjunto de dados de exportação de perfil gerado pelo sistema é usado para processar o painel de perfis.

![As opções de filtro do espaço de trabalho Conjuntos de dados com a variável [!UICONTROL Mostrar conjuntos de dados do sistema] seção realçada.](../images/datasets/user-guide/show-system-datasets.png)

### Filtrar conjuntos de dados habilitados para o perfil {#filter-profile-enabled-datasets}

Os conjuntos de dados que foram habilitados para dados de Perfil são usados para preencher perfis de clientes após a assimilação de dados. Consulte a seção sobre [ativar conjuntos de dados para o Perfil](#enable-profile) para saber mais.

Para filtrar seu conjunto de dados com base no fato de terem sido habilitados para o Perfil, selecione a [!UICONTROL Sim] nas opções de filtro.

![As opções de filtro do espaço de trabalho Conjuntos de dados com a variável [!UICONTROL Incluído no perfil] seção realçada.](../images/datasets/user-guide/included-in-profile.png)

### Filtrar conjuntos de dados por tag {#filter-by-tag}

Insira o nome da sua tag personalizada na [!UICONTROL Tags] e selecione a tag na lista de opções disponíveis para pesquisar e filtrar conjuntos de dados que correspondem a essa tag.

![As opções de filtro do espaço de trabalho Conjuntos de dados com a variável [!UICONTROL Tags] ícone de entrada e filtro realçado.](../images/datasets/user-guide/filter-tags.png)

### Filtrar conjuntos de dados por data de criação {#filter-by-creation-date}

Os conjuntos de dados podem ser filtrados pela data de criação em um período personalizado. Isso pode ser usado para excluir dados históricos ou gerar insights de dados cronológicos e relatórios específicos. Escolha um [!UICONTROL Data inicial] e uma [!UICONTROL Data final] selecionando o ícone de calendário de cada campo. Depois disso, somente os conjuntos de dados que estão em conformidade com esses critérios aparecerão na guia Procurar.

### Filtrar conjuntos de dados por data de modificação {#filter-by-modified-date}

Semelhante ao filtro para data de criação, é possível filtrar seus conjuntos de dados com base na data em que foram modificados pela última vez. No [!UICONTROL Data de modificação] , Escolha uma [!UICONTROL Data inicial] e uma [!UICONTROL Data final] selecionando o ícone de calendário de cada campo. Depois disso, somente os conjuntos de dados modificados durante esse período aparecerão na guia Procurar.

### Filtrar por esquema {#filter-by-schema}

Você pode filtrar conjuntos de dados com base no esquema que define sua estrutura. Selecione o ícone suspenso ou insira o nome do schema no campo de texto. Uma lista de correspondências em potencial é exibida. Selecione o schema apropriado na lista.

## Classificar conjuntos de dados por data de criação {#sort}

Conjuntos de dados na [!UICONTROL Procurar] pode ser classificada por datas crescentes ou decrescentes. Selecione o [!UICONTROL Criado em] ou [!UICONTROL Última atualização] cabeçalhos de coluna para alternar entre crescente e decrescente. Depois de selecionada, a coluna indica isso com uma seta para cima ou para baixo ao lado do cabeçalho da coluna.

![A guia Procurar do espaço de trabalho Conjuntos de dados com a coluna Criado e Última atualização realçada.](../images/datasets/user-guide/ascending-descending-columns.png)

## Visualizar um conjunto de dados {#preview}

Você pode visualizar dados de amostra do conjunto de dados a partir das opções em linha do [!UICONTROL Procurar] e também a guia [!UICONTROL Atividade do conjunto de dados] exibição. No [!UICONTROL Procurar] selecione as reticências (...) ao lado do nome do conjunto de dados que deseja visualizar. Uma lista de opções de menu é exibida. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** na lista de opções disponíveis. Se o conjunto de dados estiver vazio, o link de visualização será desativado e indicará que a visualização não está disponível.

![A guia Procurar do espaço de trabalho Conjuntos de dados com a opção de conjunto de dados reticências e Visualização realçada para o conjunto de dados escolhido.](../images/datasets/user-guide/preview-dataset-option.png)

Isso abre a janela de pré-visualização, onde a visualização hierárquica do esquema do conjunto de dados é mostrada à direita.

![A caixa de diálogo de visualização do conjunto de dados com informações sobre a estrutura, bem como valores de amostra para o conjunto de dados, são mostradas.](../images/datasets/user-guide/preview-dataset.png)

Alternativamente, a partir do **[!UICONTROL Atividade do conjunto de dados]** , selecione **[!UICONTROL Visualizar conjunto de dados]** próximo ao canto superior direito da tela para visualizar até 100 linhas de dados.

![O botão Visualizar conjunto de dados é realçado.](../images/datasets/user-guide/select-preview.png)

Para obter métodos mais robustos para acessar seus dados, [!DNL Experience Platform] O fornece serviços downstream, como [!DNL Query Service] e [!DNL JupyterLab] para explorar e analisar dados. Consulte os seguintes documentos para obter mais informações:

* [Visão geral do Serviço de consulta](../../query-service/home.md)
* [Guia do usuário do JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Criar um conjunto de dados {#create}

Para criar um novo conjunto de dados, comece selecionando **[!UICONTROL Criar conjunto de dados]** no **[!UICONTROL Conjuntos de dados]** painel.

![O botão Criar conjunto de dados é realçado.](../images/datasets/user-guide/select-create.png)

Na próxima tela, você verá as duas opções a seguir para criar um novo conjunto de dados:

* [Criar conjunto de dados a partir do esquema](#schema)
* [Criar conjunto de dados a partir de arquivo CSV](#csv)

### Criar um conjunto de dados com um esquema existente {#schema}

No **[!UICONTROL Criar conjunto de dados]** , selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]** para criar um novo conjunto de dados vazio.

![O botão Criar conjunto de dados a partir do esquema é realçado.](../images/datasets/user-guide/create-dataset-schema.png)

A variável **[!UICONTROL Selecionar esquema]** é exibida. Navegue pela listagem de esquemas e selecione o esquema ao qual o conjunto de dados seguirá antes de selecionar **[!UICONTROL Próxima]**.

![Uma lista de schemas é exibida. O esquema que será usado para criar o conjunto de dados é realçado.](../images/datasets/user-guide/select-schema.png)

A variável **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados e selecione **[!UICONTROL Concluir]** para criar o conjunto de dados.

![Os detalhes de configuração do conjunto de dados são inseridos. Isso inclui detalhes como o nome e a descrição do conjunto de dados.](../images/datasets/user-guide/configure-dataset-schema.png)

Os conjuntos de dados podem ser filtrados da lista de conjuntos de dados disponíveis na interface do usuário com o filtro de esquema. Consulte a seção sobre como [filtrar conjuntos de dados por esquema](#filter-by-schema) para obter mais informações.

### Criar um conjunto de dados com um arquivo CSV {#csv}

Quando um conjunto de dados é criado usando um arquivo CSV, um esquema ad hoc é criado para fornecer ao conjunto de dados uma estrutura que corresponde ao arquivo CSV fornecido. No **[!UICONTROL Criar conjunto de dados]** , selecione **[!UICONTROL Criar conjunto de dados a partir de arquivo CSV]**.

![O botão Criar conjunto de dados a partir de arquivo CSV é realçado.](../images/datasets/user-guide/create-dataset-csv.png)

A variável **[!UICONTROL Configurar]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados e selecione **[!UICONTROL Próxima]**.

![Os detalhes de configuração do conjunto de dados são inseridos. Isso inclui detalhes como o nome e a descrição do conjunto de dados.](../images/datasets/user-guide/configure-dataset-csv.png)

A variável **[!UICONTROL Adicionar dados]** é exibida. Carregue o arquivo CSV arrastando-o e soltando-o no centro da tela ou selecione **[!UICONTROL Procurar]** para explorar o diretório de arquivos. O arquivo pode ter até dez gigabytes. Depois que o arquivo CSV for carregado, selecione **[!UICONTROL Salvar]** para criar o conjunto de dados.

>[!NOTE]
>
>Os nomes das colunas CSV devem começar com caracteres alfanuméricos e podem conter apenas letras, números e sublinhados.

![A tela Adicionar dados é exibida. O local onde você pode fazer upload do arquivo CSV para o conjunto de dados é destacado.](../images/datasets/user-guide/add-csv-data.png)

## Ativar um conjunto de dados para o Perfil do cliente em tempo real {#enable-profile}

Cada conjunto de dados tem a capacidade de enriquecer os perfis do cliente com seus dados assimilados. Para fazer isso, o esquema que o conjunto de dados segue deve ser compatível para uso no [!DNL Real-Time Customer Profile]. Um esquema compatível satisfaz os seguintes requisitos:

* O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
* O esquema tem uma propriedade de identidade definida como a identidade principal.

Para obter mais informações sobre como ativar um esquema para [!DNL Profile], consulte o [Guia do usuário do Editor de esquema](../../xdm/tutorials/create-schema-ui.md).

Você pode ativar um conjunto de dados para o Perfil nas opções em linha do [!UICONTROL Procurar] e também a guia [!UICONTROL Atividade do conjunto de dados] exibição. No [!UICONTROL Procurar] guia do [!UICONTROL Conjuntos de dados] selecione as reticências de um conjunto de dados que deseja ativar para o Perfil. Uma lista de opções de menu é exibida. Em seguida, selecione **[!UICONTROL Ativar perfil unificado]** na lista de opções disponíveis.

![A guia Procurar do espaço de trabalho Conjuntos de dados com as reticências e Ativar perfil unificado foi realçada.](../images/datasets/user-guide/enable-for-profile.png)

Como alternativa, a partir da variável **[!UICONTROL Atividade do conjunto de dados]** , selecione a **[!UICONTROL Perfil]** alternar dentro do **[!UICONTROL Propriedades]** coluna. Depois de ativados, os dados assimilados no conjunto de dados também serão usados para preencher perfis de clientes.

>[!NOTE]
>
>Se um conjunto de dados já contiver dados e estiver ativado para [!DNL Profile], os dados existentes não são consumidos automaticamente pelo [!DNL Profile]. Depois que um conjunto de dados é ativado para [!DNL Profile], é recomendável assimilar novamente todos os dados existentes para que eles contribuam com os perfis do cliente.

![A opção de Perfil é realçada na página de detalhes do conjunto de dados.](../images/datasets/user-guide/enable-dataset-profiles.png)

Os conjuntos de dados que foram ativados para o Perfil também podem ser filtrados com esse critério. Consulte a seção sobre como [Filtrar conjuntos de dados habilitados para o perfil](#filter-profile-enabled-datasets) para obter mais informações.

## Gerenciar e aplicar a governança de dados em um conjunto de dados {#manage-and-enforce-data-governance}

Você pode gerenciar os rótulos de governança de dados para um conjunto de dados selecionando as opções em linha do [!UICONTROL Procurar] guia. Selecione as reticências (...) ao lado do nome do conjunto de dados que você deseja gerenciar, seguido por **[!UICONTROL Gerenciar dados e acessar rótulos]** no menu suspenso.

Os rótulos de uso de dados, aplicados no nível do esquema, permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para saber mais sobre rótulos ou consulte o [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para obter instruções sobre como aplicar rótulos a esquemas para propagação em conjuntos de dados.

## Mover para pastas {#move-to-folders}

Você pode colocar conjuntos de dados em pastas para melhorar o gerenciamento do conjunto de dados. Para mover um conjunto de dados para uma pasta, selecione as reticências (...) ao lado do nome do conjunto de dados que você deseja gerenciar, seguido por **[!UICONTROL Mover para a pasta]** no menu suspenso.

![A variável [!UICONTROL Conjuntos de dados] painel com as reticências e [!UICONTROL Mover para a pasta] destacado.](../images/datasets/user-guide/move-to-folder.png)

A variável [!UICONTROL Mover] conjunto de dados para pasta é exibida. Selecione a pasta para a qual deseja mover o público-alvo e selecione **[!UICONTROL Mover]**. Uma notificação pop-up informa que a movimentação do conjunto de dados foi bem-sucedida.

![A variável [!UICONTROL Mover] caixa de diálogo do conjunto de dados com [!UICONTROL Mover] destacado.](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>Você também pode criar pastas diretamente na caixa de diálogo Mover conjunto de dados. Para criar uma pasta, selecione o ícone criar pasta (![O ícone criar pasta.](../images/datasets/user-guide/create-folder-icon.png)) na parte superior direita da caixa de diálogo.
>
>![A variável [!UICONTROL Mover] caixa de diálogo conjunto de dados com o ícone criar pasta realçado.](/help/catalog/images/datasets/user-guide/create-folder.png)

Quando o conjunto de dados estiver em uma pasta, você poderá optar por exibir somente os conjuntos de dados que pertencem a uma pasta específica. Para abrir a estrutura de pastas, selecione o ícone mostrar pastas (![O ícone show folders](../images/datasets/user-guide/show-folders-icon.png)). Em seguida, selecione a pasta escolhida para ver todos os conjuntos de dados associados.

![A variável [!UICONTROL Conjuntos de dados] painéis com a estrutura de pastas dos conjuntos de dados exibida, o ícone mostrar pastas e uma pasta selecionada realçada.](../images/datasets/user-guide/folder-structure.png)

## Excluir um conjunto de dados {#delete}

É possível excluir um conjunto de dados das ações em linha do conjunto de dados na [!UICONTROL Procurar] ou na parte superior direita do [!UICONTROL Atividade do conjunto de dados] exibição. No [!UICONTROL Procurar] selecione as reticências (...) ao lado do nome do conjunto de dados que deseja excluir. Uma lista de opções de menu é exibida. Em seguida, selecione **[!UICONTROL Excluir]** no menu suspenso.

![A guia Procurar do espaço de trabalho Conjuntos de dados com as reticências e a opção Excluir realçada para o conjunto de dados escolhido.](../images/datasets/user-guide/inline-delete-dataset.png)

Uma caixa de diálogo de confirmação é exibida. Selecione **[!UICONTROL Excluir]** para confirmar.

Como alternativa, selecione **[!UICONTROL Excluir conjunto de dados]** do **[!UICONTROL Atividade do conjunto de dados]** tela.

>[!NOTE]
>
>Conjuntos de dados criados e utilizados por aplicativos e serviços Adobe (como Adobe Analytics, Adobe Audience Manager ou [!DNL Offer Decisioning]) não pode ser excluída.

![O botão Excluir conjunto de dados é realçado na página de detalhes do conjunto de dados.](../images/datasets/user-guide/delete-dataset.png)

Uma caixa de confirmação é exibida. Selecionar **[!UICONTROL Excluir]** para confirmar a exclusão do conjunto de dados.

![A modal de confirmação para exclusão é exibida, com o botão Excluir realçado.](../images/datasets/user-guide/confirm-delete.png)

## Excluir um conjunto de dados habilitado para perfil

Se um conjunto de dados estiver ativado para o Perfil, a exclusão desse conjunto de dados por meio da interface do usuário o excluirá do data lake, do Serviço de identidade e também de quaisquer dados de perfil associados a esse conjunto de dados no Armazenamento de perfis.

É possível excluir dados de perfil associados a um conjunto de dados da [!DNL Profile] armazenar (deixando os dados no data lake) usando a API de perfil do cliente em tempo real. Para obter mais informações, consulte [guia de ponto de extremidade da API de trabalhos do sistema de perfil](../../profile/api/profile-system-jobs.md).

## Monitorar assimilação de dados

No [!DNL Experience Platform] Interface, selecione **[!UICONTROL Monitoramento]** no painel de navegação esquerdo. A variável **[!UICONTROL Monitoramento]** O painel permite visualizar os status dos dados de entrada da assimilação em lote ou por transmissão. Para exibir os status de lotes individuais, selecione **[!UICONTROL Lote de ponta a ponta]** ou **[!UICONTROL Transmissão de ponta a ponta]**. Os painéis listam todas as execuções de assimilação em lote ou por transmissão, incluindo as que foram bem-sucedidas, falharam ou ainda estão em andamento. Cada lista fornece detalhes do lote, incluindo a ID do lote, o nome do conjunto de dados de destino e o número de registros assimilados. Se o conjunto de dados de destino estiver habilitado para [!DNL Profile], o número de registros de identidade e perfil assimilados também é exibido.

![A tela de monitoramento completa do lote é exibida. O monitoramento e a análise de lote a lote são destacados.](../images/datasets/user-guide/batch-listing.png)

Você pode selecionar um indivíduo **[!UICONTROL ID do lote]** para acessar o **[!UICONTROL Visão geral de lotes]** e consulte os detalhes do lote, incluindo logs de erros, caso o lote não seja assimilado.

![Os detalhes do lote selecionado são exibidos. Isso inclui o número de registros assimilados, o número de registros com falha, o status do lote, o tamanho do arquivo, as horas de início e término da assimilação, o conjunto de dados e as IDs do lote, a ID da organização, o nome do conjunto de dados e as informações de acesso.](../images/datasets/user-guide/batch-overview.png)

Se desejar excluir o lote, selecione **[!UICONTROL Excluir lote]** próximo à parte superior direita do painel. A exclusão de um lote também remove seus registros do conjunto de dados ao qual o lote foi originalmente assimilado.

>[!NOTE]
>
>Se os dados assimilados tiverem sido ativados para Perfil e processados, a exclusão de um lote não excluirá esses dados da Loja de perfis.

![O botão Excluir lote é realçado na página de detalhes do conjunto de dados.](../images/datasets/user-guide/delete-batch.png)

## Próximas etapas

Este guia do usuário forneceu instruções para executar ações comuns ao trabalhar com conjuntos de dados na [!DNL Experience Platform] interface do usuário. Para obter as etapas sobre como executar tarefas [!DNL Platform] fluxos de trabalho envolvendo conjuntos de dados, consulte os seguintes tutoriais:

* [Criar um conjunto de dados usando APIs](create.md)
* [Consultar dados do conjunto de dados usando a API de acesso a dados](../../data-access/home.md)
* [Configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../../profile/tutorials/dataset-configuration.md)
