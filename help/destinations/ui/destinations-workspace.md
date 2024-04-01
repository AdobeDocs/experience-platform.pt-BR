---
keywords: plataforma;destinos;destinos espaço de trabalho;espaço de trabalho;ui;destinos ui;catálogo;destinos catálogo;
title: Espaço de trabalho Destinos
description: 'O espaço de trabalho Destinos consiste em cinco seções: Visão geral, Catálogo, Procurar, Contas e Exibição de sistema. Eles são descritos nas seções abaixo.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: dad07add8c5f9cc98a187c2e2222a51611dbd1a2
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 1%

---

# Espaço de trabalho Destinos {#destinations-workspace}

No Adobe Experience Platform, selecione **[!UICONTROL Destinos]** na barra de navegação esquerda, para acessar a [!UICONTROL Destinos] espaço de trabalho.

A variável [!UICONTROL Destinos] o espaço de trabalho consiste em cinco seções, [!UICONTROL Visão geral], [!UICONTROL Catálogo], [!UICONTROL Procurar], [!UICONTROL Contas], e [!UICONTROL Exibição do sistema], descrito nas seções abaixo.

![Painel de visão geral Destinos mostrando três widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Visão geral] {#overview}

A variável **[!UICONTROL Visão geral]** exibe a variável [!UICONTROL Destinos] painel, fornecendo as métricas principais relacionadas aos dados de destino de sua organização. Para saber mais, visite o [[!UICONTROL Destinos] guia do painel](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver destinos ativos, a variável [!UICONTROL Destinos] painel e [!UICONTROL Visão geral] não estão visíveis. Em vez disso, selecione [!UICONTROL Destinos] no painel de navegação esquerdo, exibe a [[!UICONTROL Catálogo] guia](#catalog).

![A guia Visão geral do painel de Destinos.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A variável **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos disponíveis no [!DNL Platform], para o qual você pode enviar dados.

A variável [!DNL Platform] A interface do usuário do fornece várias opções de pesquisa e filtro na página catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtrar destinos usando o [!UICONTROL Categorias] controle.
* Alternar entre [!UICONTROL Todos os destinos] e [!UICONTROL Meus destinos]. Ao selecionar **[!UICONTROL Todos os destinos]**, todos os disponíveis [!DNL Platform] os destinos serão exibidos. Ao selecionar **[!UICONTROL Meus destinos]**, você só poderá ver os destinos com os quais estabeleceu uma conexão.
* Selecione para exibir o **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]** tipos. Para entender a diferença entre as duas categorias, leia [Tipos e categorias de destino](../destination-types.md).

![Catálogo de destinos que mostra alguns destinos de anúncios e armazenamento em nuvem.](../assets/ui/workspace/catalog.png)

Os cartões de destino contêm opções de controle primário e secundário. Os controles primários incluem [!UICONTROL Configurar], [!UICONTROL Ativar], [!UICONTROL Ativar públicos]ou [!UICONTROL Exportar conjuntos de dados]. Os controles secundários permitem opções de exibição. Esses controles estão descritos abaixo:

| Controle | Descrição |
|---------|----------|
| [!UICONTROL Configurar] | Permite criar uma conexão com o destino. |
| [!UICONTROL Ativar] | Depois de estabelecer uma conexão com o destino, você pode ativar públicos ou exportar conjuntos de dados para esse destino. |
| [!UICONTROL Ativar públicos] | Depois de estabelecer uma conexão com o destino, você poderá ativar os públicos para esse destino. |
| [!UICONTROL Exportar conjuntos de dados] | Depois de estabelecer uma conexão com o destino, você poderá exportar conjuntos de dados para esse destino. |
| [!UICONTROL Exibir conta] | Exibir as contas conectadas a um destino. |
| [!UICONTROL Exibir fluxos de dados] | Exibir os fluxos de ativação de dados existentes para um destino. |
| [!UICONTROL Exibir documentação] | Abre um link para a página de documentação do destino específico. Para obter mais informações e ajudar a configurar. |

{style="table-layout:auto"}

![Controles no cartão de destinos](../assets/ui/workspace/destination-card-options.png)

Selecione um cartão de destino no catálogo para abrir o painel direito. Aqui, você pode ver uma descrição do destino. O painel direito fornece os mesmos controles descritos na tabela acima, incluindo uma descrição do destino e uma indicação da categoria e do tipo de destino.

![Opções do catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte a [Catálogo de destino](../catalog/overview.md) e [Tipos e categorias de destino](../destination-types.md).

## [!UICONTROL Contas] {#accounts}

A variável **[!UICONTROL Contas]** A guia mostra detalhes sobre as conexões estabelecidas com vários destinos e permite atualizar ou excluir detalhes da conta existente. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada conta de destino.

>[!TIP]
>
> * Selecione as reticências (`...`) no [!UICONTROL Platform] e use o ![Ativar controle](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Ativar ]**/**[!UICONTROL  Ativar públicos ]**/**[!UICONTROL  Exportar conjuntos de dados ]**para exportar públicos ou conjuntos de dados para esse destino.
> * Selecione as reticências (`...`) no [!UICONTROL Platform] e use o ![Editar controle de detalhes](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Editar detalhes ]**controle para [atualizar](update-accounts.md) os detalhes de uma conta de destino existente.
> * Selecione as reticências (`...`) no [!UICONTROL Platform] e use o ![Excluir controle](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Excluir ]**controle para [excluir](delete-destination-account.md) uma conta de destino existente.

![Guia Contas](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descrição |
|---|---|
| [!UICONTROL Platform] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão de conta para seu bucket de armazenamento ou destino. Dependendo do destino, as opções de autenticação são: <ul><li>Para destinos de marketing por email: pode ser S3, FTP ou Blob do Azure.</li><li>Para destinos de anúncios em tempo real: de servidor para servidor</li><li>Para destinos de armazenamento na nuvem do Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento na nuvem SFTP: autenticação básica para SFTP</li><li>Autenticação OAuth 1 ou OAuth 2</li><li>Autenticação de token do portador</li></ul> |
| [!UICONTROL Nome de usuário] | O nome de usuário selecionado na variável [assistente de conexão de destino](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinos] | Representa o número de fluxos de dados de destino exclusivos bem-sucedidos conectados às informações básicas criadas para um destino. |
| [!UICONTROL Autorizado] | A data em que a conexão com esse destino foi autorizada. |

{style="table-layout:auto"}

## [!UICONTROL Navegar] {#browse}

A variável **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Destinos com o **[!UICONTROL Ativado/Desativado]** alternância ativada: definir o destino como ativo ou inativo, respectivamente. Você também pode exibir os destinos nos quais há dados fluindo selecionando **[!UICONTROL Públicos-alvo]** > **[!UICONTROL Procurar]** e selecionar um público-alvo a ser inspecionado. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na [!UICONTROL Procurar] guia:

>[!TIP]
>
> * Selecione as reticências (`...`) no [!UICONTROL Nome] e use o ![Ativar controle de públicos](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Ativar ]**para exportar públicos ou conjuntos de dados para esse destino.
> * Selecione as reticências (`...`) no [!UICONTROL Nome] e use o ![Excluir controle](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Excluir ]**controle para [remover](delete-destinations.md) uma conexão existente com um destino.
> * Selecione as reticências (`...`) no [!UICONTROL Nome] e use o ![Exibir no controle de monitoramento](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL Exibir no monitoramento ]**controle para exibir informações de ativação para este destino no [painel de monitoramento](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Selecione as reticências (`...`) no [!UICONTROL Nome] e use o ![Assinar alertas ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Assinar alertas ]**controle para assinar alertas de fluxo de dados de destino. Você pode assinar alertas para receber mensagens sobre o status, o sucesso ou a falha da execução do fluxo. Consulte [Assinar alertas de destino em contexto](alerts.md) para obter informações detalhadas sobre alertas de fluxo de dados de destino.

![Guia Procurar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrição |
|---------|----------|
| Nome | O nome fornecido para o fluxo de ativação para esse destino. A mesma coluna inclui dois controles: [!UICONTROL Ativar] e [!UICONTROL Excluir destino]. |
| [!UICONTROL Status da Última Execução de Fluxo] | O status da última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Data da Última Execução do Fluxo] | Hora e data em que ocorreu a última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Destino] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão para seu bucket de armazenamento ou destino. <ul><li>Para destinos de marketing por email: pode ser S3, FTP ou [!DNL Azure Blob].</li><li>Para destinos de anúncios em tempo real: de servidor para servidor.</li><li>Para destinos de transmissão: pode ser [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome de usuário] | As credenciais de conta selecionadas para o fluxo de destino. |
| [!UICONTROL Dados de ativação] | Indica o número de públicos-alvo que estão sendo ativados para esse destino. Selecione este controle para saber mais sobre os públicos ativados. Consulte [Dados de ativação](/help/destinations/ui/destination-details-page.md#activation-data) na página de detalhes do destino para obter mais informações sobre os públicos ativados. |
| [!UICONTROL Criado] | A data e hora UTC quando o fluxo de ativação para o destino foi criado. Selecione o símbolo de seta para cima/para baixo para classificar os fluxos de ativação pelo mais recente primeiro ou pelo mais antigo primeiro. |
| [!UICONTROL Status] | `Enabled` ou `Disabled`. Indica se os dados estão sendo ativados para este destino. |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito, como ID de destino, descrição, o número de públicos ativados e muito mais.

![Clique na linha de destino](../assets/ui/workspace/click-destination-row.png)

Selecione o nome do destino para ver informações sobre os públicos ativados para esse destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos públicos-alvo que estão sendo enviados a este destino.

## [!UICONTROL Exibição do sistema] {#system-view}

A variável **[!UICONTROL Exibição do sistema]** exibe uma representação gráfica dos fluxos de ativação configurados no Adobe Experience Platform.

![Fluxos de dados1](../assets/ui/workspace/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e clique em **[!UICONTROL Exibir fluxos de dados]** para ver informações sobre todas as conexões configuradas para cada destino.

![Fluxos de dados2](../assets/ui/workspace/data-flows2.png)
