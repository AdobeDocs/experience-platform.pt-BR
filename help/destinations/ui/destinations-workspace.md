---
keywords: plataforma; destinos; espaço de trabalho de destinos; espaço de trabalho; interface do usuário; destinos; interface do usuário; catálogo; catálogo de destinos;
title: Área de trabalho Destinos
description: 'O espaço de trabalho Destinos consiste em cinco seções: Visão geral, Catálogo, Navegação, Contas e Visualização do sistema. Elas estão descritas nas seções abaixo.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 69e1f065cb3b302c4b144f39c84179075379f648
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 2%

---

# Área de trabalho Destinos {#destinations-workspace}

No Adobe Experience Platform, selecione **[!UICONTROL Destinos]** na barra de navegação esquerda para acessar o [!UICONTROL Destinos] espaço de trabalho.

O [!UICONTROL Destinos] o workspace consiste em cinco seções, [!UICONTROL Visão geral], [!UICONTROL Catálogo], [!UICONTROL Procurar], [!UICONTROL Contas]e [!UICONTROL Exibição do sistema], descritas nas seções abaixo.

![Painel de visão geral de Destinos que mostra três widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Visão geral] {#overview}

O **[!UICONTROL Visão geral]** exibe a guia [!UICONTROL Destinos] , fornecendo métricas principais relacionadas aos dados de destino de sua organização. Para saber mais, visite o [[!UICONTROL Destinos] guia do painel](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver destinos ativos, a variável [!UICONTROL Destinos] painel e [!UICONTROL Visão geral] não estão visíveis. Em vez disso, selecione [!UICONTROL Destinos] no menu de navegação esquerdo, o [[!UICONTROL Catálogo] guia](#catalog).

![A guia Visão geral do painel Destinos .](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catálogo] {#catalog}

O **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos disponíveis em [!DNL Platform], para a qual você pode enviar dados.

O [!DNL Platform] a interface do usuário fornece várias opções de pesquisa e filtro na página de catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtrar destinos usando o [!UICONTROL Categorias] controlo.
* Alternar entre [!UICONTROL Todos os destinos] e [!UICONTROL Meus destinos]. Ao selecionar **[!UICONTROL Todos os destinos]**, todos disponíveis [!DNL Platform] os destinos são exibidos. Ao selecionar **[!UICONTROL Meus destinos]**, você só poderá ver os destinos com os quais estabeleceu uma conexão.
* Selecione para exibir o **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]** tipos. Para entender a diferença entre as duas categorias, leia [Tipos e categorias de destino](../destination-types.md).

![Catálogo de destinos que mostra alguns destinos de publicidade e armazenamento em nuvem.](../assets/ui/workspace/catalog.png)

As placas de destino contêm opções de controle primário e secundário. Os controles principais incluem [!UICONTROL Configurar], [!UICONTROL Ativar], [!UICONTROL Ativar segmentos]ou [!UICONTROL Exportar conjuntos de dados]. Os controles secundários permitem opções de visualização. Esses controles estão descritos abaixo:

| Controle | Descrição |
|---------|----------|
| [!UICONTROL Configurar] | Permite criar uma conexão com o destino. |
| [!UICONTROL Ativar] | Depois de estabelecer uma conexão com o destino, é possível ativar segmentos ou exportar conjuntos de dados para esse destino. |
| [!UICONTROL Ativar segmentos] | Depois de estabelecer uma conexão com o destino, é possível ativar segmentos para esse destino. |
| [!UICONTROL Exportar conjuntos de dados] | Depois de estabelecer uma conexão com o destino, é possível exportar conjuntos de dados para esse destino. |
| [!UICONTROL Exibir conta] | Exiba as contas que você conectou para um destino. |
| [!UICONTROL Exibir fluxos de dados] | Visualize os fluxos de ativação de dados que existem para um destino. |
| [!UICONTROL Exibir documentação] | Abre um link para a página de documentação desse destino específico, para obter mais informações e para ajudar a configurá-lo. |

{style=&quot;table-layout:auto&quot;}

![Controles no cartão de destinos](../assets/ui/workspace/destination-card-options.png)

Selecione um cartão de destino no catálogo para abrir o painel direito. Aqui, você pode ver uma descrição do destino. O painel direito fornece os mesmos controles descritos no quadro acima, incluindo uma descrição do destino e uma indicação da categoria e do tipo de destino.

![Opções de catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte o [Catálogo de destino](../catalog/overview.md) e [Tipos e categorias de destino](../destination-types.md).

## [!UICONTROL Contas] {#accounts}

O **[!UICONTROL Contas]** A guia mostra detalhes sobre as conexões estabelecidas com vários destinos e permite atualizar ou excluir detalhes da conta existente. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada conta de destino.

>[!TIP]
>
> * Selecione as reticências (`...`) na [!UICONTROL Plataforma] e use a ![Ativar controle](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Ativar ]**/**[!UICONTROL  Ativar segmentos ]**/**[!UICONTROL  Exportar conjuntos de dados ]**controle para exportar segmentos ou conjuntos de dados para esse destino.
> * Selecione as reticências (`...`) na [!UICONTROL Plataforma] e use a ![Editar controle de detalhes](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Editar detalhes ]**controle para [atualizar](update-accounts.md) os detalhes de uma conta de destino existente.
> * Selecione as reticências (`...`) na [!UICONTROL Plataforma] e use a ![Excluir controle](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Excluir ]**controle para [excluir](delete-destination-account.md) uma conta de destino existente.


![Guia Contas](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descrição |
|---|---|
| [!UICONTROL Plataforma] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão da conta para o seu bucket ou destino de armazenamento. Dependendo do destino, as opções de autenticação são: <ul><li>Para destinos de marketing por email: Pode ser S3, FTP ou Azure Blob.</li><li>Para destinos de anúncios em tempo real: Servidor para servidor</li><li>Para destinos de armazenamento em nuvem Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li><li>Autenticação OAuth 1 ou OAuth 2</li><li>Autenticação de token portador</li></ul> |
| [!UICONTROL Nome de usuário] | O nome de usuário selecionado no [assistente de destino de conexão](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinos] | Representa o número de fluxos de dados de destino exclusivos bem-sucedidos conectados às informações básicas criadas para um destino. |
| [!UICONTROL Autorizado] | A data em que a conexão com esse destino foi autorizada. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Navegar] {#browse}

O **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Destinos com o **[!UICONTROL Ativado/Desativado]** Ativar ou ativar definir o destino como ativo ou inativo, respectivamente. Também é possível visualizar os destinos nos quais você tem dados fluindo selecionando **[!UICONTROL Segmentos]** > **[!UICONTROL Procurar]** e selecionar um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino no [!UICONTROL Procurar] guia :

>[!TIP]
>
> * Selecione as reticências (`...`) na [!UICONTROL Nome] e use a ![Ativar controle de segmentos](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Ativar ]**controle para exportar segmentos ou conjuntos de dados para esse destino.
> * Selecione as reticências (`...`) na [!UICONTROL Nome] e use a ![Excluir controle](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Excluir ]**controle para [remove](delete-destinations.md) uma conexão existente com um destino.
> * Selecione as reticências (`...`) na [!UICONTROL Nome] e use a ![Exibir no controle de monitoramento](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL Exibir no monitoramento ]**controle para exibir informações de ativação para esse destino no [painel de monitoramento](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Selecione as reticências (`...`) na [!UICONTROL Nome] e use a ![Inscrever-se em alertas ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Inscrever-se em alertas ]**controle para assinar alertas de fluxo de dados de destino. Você pode assinar alertas para receber mensagens relacionadas ao status, sucesso ou falha da execução do fluxo. Consulte [Assinar alertas de destino no contexto](alerts.md) para obter informações detalhadas sobre alertas de fluxo de dados de destino.


![Guia Procurar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrição |
|---------|----------|
| Nome | O nome fornecido para o fluxo de ativação para este destino. A mesma coluna inclui dois controles: [!UICONTROL Ativar ] e [!UICONTROL Excluir destino]. |
| [!UICONTROL Status da Execução do Último Fluxo] | O status da última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Data de Execução do Último Fluxo] | Hora e data em que ocorreu a última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Destino] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com seu bucket ou destino de armazenamento. <ul><li>Para destinos de marketing por email: Pode ser S3, FTP ou [!DNL Azure Blob].</li><li>Para destinos de anúncios em tempo real: Servidor para servidor.</li><li>Para destinos de transmissão: Pode ser [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome de usuário] | As credenciais de conta que você selecionou para o fluxo de destino. |
| [!UICONTROL Dados de ativação] | Indica o número de segmentos que estão sendo ativados para esse destino. Selecione este controle para saber mais sobre os segmentos ativados. Consulte [Dados de ativação](/help/destinations/ui/destination-details-page.md#activation-data) na página de detalhes do destino para obter mais informações sobre os segmentos ativados. |
| [!UICONTROL Criado] | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. Selecione o símbolo de seta para cima/para baixo para classificar os fluxos de ativação primeiro ou mais antigos. |
| [!UICONTROL Status] | `Enabled` ou `Disabled`. Indica se os dados estão sendo ativados para esse destino. |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](../assets/ui/workspace/click-destination-row.png)

Selecione o nome do destino para ver informações sobre os segmentos ativados para este destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos segmentos que estão sendo enviados para esse destino.

## [!UICONTROL Exibição do sistema] {#system-view}

O **[!UICONTROL Exibição do sistema]** exibe uma representação gráfica dos fluxos de ativação configurados na Adobe Experience Platform.

![Fluxos de dados1](../assets/ui/workspace/data-flows1.png)

Selecione qualquer destino exibido na página e clique em **[!UICONTROL Exibir fluxos de dados]** para ver informações sobre todas as conexões configuradas para cada destino.

![Fluxos de dados2](../assets/ui/workspace/data-flows2.png)
