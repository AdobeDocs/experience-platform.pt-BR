---
keywords: plataforma;destinos;destinos espaço de trabalho;espaço de trabalho;ui;destinos ui;catálogo;destinos catálogo;
title: Espaço de trabalho Destinos
description: 'O espaço de trabalho Destinos consiste em cinco seções: Visão geral, Catálogo, Procurar, Contas e Exibição de sistema. Eles são descritos nas seções abaixo.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# Espaço de trabalho Destinos {#destinations-workspace}

No Adobe Experience Platform, selecione **[!UICONTROL Destinos]** na barra de navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Destinos].

O espaço de trabalho [!UICONTROL Destinos] consiste em cinco seções, [!UICONTROL Visão Geral], [!UICONTROL Catálogo], [!UICONTROL Procurar], [!UICONTROL Contas] e [!UICONTROL Exibição de Sistema], descritas nas seções abaixo.

![Painel de visão geral de destinos mostrando três widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Visão geral] {#overview}

A guia **[!UICONTROL Visão geral]** exibe o painel [!UICONTROL Destinos], fornecendo as métricas principais relacionadas aos dados de destino de sua organização. Para saber mais, visite o [[!UICONTROL guia do painel] de Destinos](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver destinos ativos, o painel [!UICONTROL Destinos] e a guia [!UICONTROL Visão geral] não estarão visíveis. Em vez disso, selecionar [!UICONTROL Destinos] na navegação à esquerda exibe a guia [[!UICONTROL Catálogo]](#catalog).

![A guia Visão geral do painel Destinos.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A guia **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos disponíveis em [!DNL Experience Platform] para os quais você pode enviar dados.

A interface de usuário do [!DNL Experience Platform] fornece várias opções de pesquisa e filtro na página de catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtrar destinos usando o controle [!UICONTROL Categorias].
* Alternar entre [!UICONTROL Todos os destinos] e [!UICONTROL Meus destinos]. Quando você seleciona **[!UICONTROL Todos os destinos]**, todos os destinos [!DNL Experience Platform] disponíveis são exibidos. Ao selecionar **[!UICONTROL Meus destinos]**, você só poderá ver os destinos com os quais tiver estabelecido uma conexão.
* Selecione para exibir os tipos de **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]**. Para entender a diferença entre as duas categorias, leia [Tipos de Destino e Categorias](../destination-types.md).

![Catálogo de destinos que mostra alguns destinos de anúncios e de armazenamento na nuvem.](../assets/ui/workspace/catalog.png)

Os cartões de destino contêm opções de controle primário e secundário. Os controles primários incluem [!UICONTROL Configurar], [!UICONTROL Ativar], [!UICONTROL Ativar públicos] ou [!UICONTROL Exportar conjuntos de dados]. Os controles secundários permitem opções de exibição. Esses controles estão descritos abaixo:

| Controle | Descrição |
|---------|----------|
| [!UICONTROL Configurar] | Permite criar uma conexão com o destino. |
| [!UICONTROL Ativar] | Depois de estabelecer uma conexão com o destino, você pode ativar públicos ou exportar conjuntos de dados para esse destino. |
| [!UICONTROL Ativar públicos-alvo] | Depois de estabelecer uma conexão com o destino, você poderá ativar os públicos para esse destino. |
| [!UICONTROL Exportar conjuntos de dados] | Depois de estabelecer uma conexão com o destino, você poderá exportar conjuntos de dados para esse destino. |
| [!UICONTROL Exibir conta] | Exibir as contas conectadas a um destino. |
| [!UICONTROL Exibir fluxos de dados] | Exibir os fluxos de ativação de dados existentes para um destino. |
| [!UICONTROL Exibir documentação] | Abre um link para a página de documentação do destino específico. Para obter mais informações e ajudar a configurar. |

{style="table-layout:auto"}

![Controles no cartão de destinos](../assets/ui/workspace/destination-card-options.png)

Selecione um cartão de destino no catálogo para abrir o painel direito. Aqui, você pode ver uma descrição do destino. O painel direito fornece os mesmos controles descritos na tabela acima, incluindo uma descrição do destino e uma indicação da categoria e do tipo de destino.

![Opções do catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte o [Catálogo de destinos](../catalog/overview.md) e [Tipos e categorias de destino](../destination-types.md).

## [!UICONTROL Contas] {#accounts}

A guia **[!UICONTROL Contas]** mostra detalhes sobre as conexões estabelecidas com vários destinos e permite atualizar ou excluir detalhes de contas existentes. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada conta de destino.

>[!TIP]
>
> * Selecione as reticências (`...`) na coluna [!UICONTROL Platform] e use o controle ![Ativate](/help/images/icons/data-add.png)**[!UICONTROL Ativate &#x200B;]**/**[!UICONTROL &#x200B; Ativate audiences &#x200B;]**/**[!UICONTROL &#x200B; Export datasets &#x200B;]**&#x200B;para exportar audiences ou conjuntos de dados para esse destino.
> * Selecione as reticências (`...`) na coluna [!UICONTROL Plataforma] e use o controle ![Editar detalhes](/help/images/icons/edit.png)**[!UICONTROL Editar detalhes &#x200B;]**&#x200B;para [atualizar](update-accounts.md) os detalhes de uma conta de destino existente.
> * Selecione as reticências (`...`) na coluna [!UICONTROL Plataforma] e use o controle ![Excluir](/help/images/icons/delete.png)**[!UICONTROL Excluir &#x200B;]**&#x200B;para [excluir](delete-destination-account.md) uma conta de destino existente.

![Guia Contas](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descrição |
|---|---|
| [!UICONTROL Destino] | O conector de destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão de conta para seu bucket de armazenamento ou destino. Dependendo do destino, as opções de autenticação são: <ul><li>Para destinos de marketing por email: pode ser S3, FTP ou Blob do Azure.</li><li>Para destinos de anúncios em tempo real: de servidor para servidor</li><li>Para destinos de armazenamento na nuvem do Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento na nuvem SFTP: autenticação básica para SFTP</li><li>Autenticação OAuth 1 ou OAuth 2</li><li>Autenticação de token do portador</li></ul> |
| [!UICONTROL Nome de usuário] | O nome de usuário selecionado no [fluxo de trabalho de destino de conexão](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Conexões] | Representa o número de fluxos de dados de destino exclusivos bem-sucedidos conectados às informações básicas criadas para um destino. |
| [!UICONTROL Data de autorização] | A data em que a conexão com esse destino foi autorizada. |

{style="table-layout:auto"}

## [!UICONTROL Procurar] {#browse}

A guia **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a opção **[!UICONTROL Habilitada/Desabilitada]** ativada definem o destino como ativo ou inativo, respectivamente. Você também pode exibir os destinos nos quais há dados fluindo selecionando **[!UICONTROL Públicos-alvo]** > **[!UICONTROL Procurar]** e selecionando um público a ser inspecionado. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia [!UICONTROL Procurar]:

>[!TIP]
>
> * Selecione as reticências (`...`) na coluna [!UICONTROL Nome] e use o controle ![Ativar públicos-alvo](/help/images/icons/data-add.png)**[!UICONTROL Ativar &#x200B;]**&#x200B;para exportar públicos-alvo ou conjuntos de dados para esse destino.
> * Selecione as reticências (`...`) na coluna [!UICONTROL Nome] e use o controle ![Excluir](/help/images/icons/delete.png)**[!UICONTROL Excluir &#x200B;]**&#x200B;para [remover](delete-destinations.md) uma conexão existente com um destino.
> * Selecione as reticências (`...`) na coluna [!UICONTROL Nome] e use a ![Exibição no controle de monitoramento](/help/images/icons/monitoring.png)**[!UICONTROL Exibição no monitoramento &#x200B;]**&#x200B;para exibir informações de ativação para este destino no [painel de monitoramento](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Selecione as reticências (`...`) na coluna [!UICONTROL Nome] e use o controle ![Assinar alertas ](/help/images/icons/alert-add.png)**[!UICONTROL Assinar alertas &#x200B;]**&#x200B;para assinar alertas de fluxo de dados de destino. Você pode assinar alertas para receber mensagens sobre o status, o sucesso ou a falha da execução do fluxo. Consulte [Assinar alertas de destino em contexto](alerts.md) para obter informações detalhadas sobre alertas de fluxo de dados de destino.

![Guia Procurar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrição |
|---------|----------|
| Nome | O nome fornecido para o fluxo de ativação para esse destino. A mesma coluna inclui dois controles: [!UICONTROL Ativar] e [!UICONTROL Excluir destino]. |
| [!UICONTROL Status da Última Execução de Fluxo] | O status da última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Data da Última Execução do Fluxo] | Hora e data em que ocorreu a última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Destino] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão para seu bucket de armazenamento ou destino. <ul><li>Para destinos de marketing por email: pode ser S3, FTP ou [!DNL Azure Blob].</li><li>Para destinos de anúncios em tempo real: de servidor para servidor.</li><li>Para destinos de streaming: pode ser [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome de usuário] | As credenciais de conta selecionadas para o fluxo de destino. |
| [!UICONTROL Dados de ativação] | Indica o número de públicos-alvo que estão sendo ativados para esse destino. Selecione este controle para saber mais sobre os públicos ativados. Consulte [Dados de ativação](/help/destinations/ui/destination-details-page.md#activation-data) na página de detalhes do destino para obter mais informações sobre os públicos ativados. |
| [!UICONTROL Criado] | A data e hora UTC quando o fluxo de ativação para o destino foi criado. Selecione o símbolo de seta para cima/para baixo para classificar os fluxos de ativação pelo mais recente primeiro ou pelo mais antigo primeiro. |
| [!UICONTROL Status] | `Enabled` ou `Disabled`. Indica se os dados estão sendo ativados para este destino. |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito, como ID de destino, descrição, o número de públicos ativados e muito mais.

![Clique na linha de destino](../assets/ui/workspace/click-destination-row.png)

Selecione o nome do destino para ver informações sobre os públicos ativados para esse destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos públicos-alvo que estão sendo enviados a este destino.

## [!UICONTROL Exibição do Sistema] {#system-view}

A guia **[!UICONTROL Exibição de Sistema]** exibe uma representação gráfica dos fluxos de ativação configurados no Adobe Experience Platform.

![Fluxos de dados1](../assets/ui/workspace/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e clique em **[!UICONTROL Exibir fluxos de dados]** para ver informações sobre todas as conexões configuradas para cada destino.

![Fluxos de dados2](../assets/ui/workspace/data-flows2.png)
