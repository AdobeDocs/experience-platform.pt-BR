---
keywords: plataforma; destinos; espaço de trabalho de destinos; espaço de trabalho; interface do usuário; destinos; interface do usuário; catálogo; catálogo de destinos;
title: Visão geral do espaço de trabalho Destinos
description: O espaço de trabalho Destinos consiste em quatro seções, Catálogo, Navegação, Contas e Visualização do sistema, descritas nas seções abaixo.
seo-description: No Adobe Experience Platform, selecione Destinos na barra de navegação esquerda para acessar o espaço de trabalho de destinos.
translation-type: tm+mt
source-git-commit: 95ff15b212e0d6f454f0319ac1ec5bbee9c07dac
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---


# Visão geral do espaço de trabalho Destinos {#destinations-workspace}

No Adobe Experience Platform, selecione **[!UICONTROL Destinations]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Destinations].

O espaço de trabalho [!UICONTROL Destinos] consiste em quatro seções, [!UICONTROL Catálogo], [!UICONTROL Procurar], [!UICONTROL Contas] e [!UICONTROL Vista do Sistema], que estão descritas nas seções abaixo.

![Visão geral dos destinos](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A guia **[!UICONTROL Catalog]** exibe uma lista de todos os destinos disponíveis na Plataforma, para os quais você pode enviar dados.

A interface do usuário da Plataforma fornece várias opções de pesquisa e filtro na página de catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtre destinos usando o controle [!UICONTROL Categorias].
* Alternar entre [!UICONTROL Todos os destinos] e [!UICONTROL Meus destinos]. Quando **[!UICONTROL All destination]** é selecionado, todos os destinos disponíveis da Plataforma são exibidos. Quando **[!UICONTROL Meus destinos]** é selecionado, você só pode ver os destinos com os quais estabeleceu uma conexão.
* Selecione para exibir **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]**. Para entender a diferença entre as duas categorias, consulte [Tipos e categorias de destino](../destination-types.md).

![filtragem de destinos e demonstração de pesquisa](../assets/ui/workspace/destinations-search-and-filter.gif)

Os cartões de destino contêm um controle **[!UICONTROL Configure]** ou **[!UICONTROL Ativate]** e um controle secundário que exibe mais opções. Todos eles estão descritos abaixo:

| Controle | Descrição |
---------|----------
| [!UICONTROL Configurar] | Permite criar uma conexão com o destino. |
| [!UICONTROL Ativar] | Depois de estabelecer uma conexão com o destino, é possível ativar segmentos. |
| [!UICONTROL Exibir conta] | Exiba as contas que você conectou para um destino. |
| [!UICONTROL Exibir fluxos de dados] | Visualize os fluxos de ativação de dados que existem para um destino. |
| [!UICONTROL Exibir documentação] | Abre um link para a página de documentação desse destino específico, para obter mais informações e para ajudar a configurá-lo. |

![Controles no cartão de destinos](../assets/ui/workspace/destination-card-options.png)

Selecione um cartão de destino no catálogo para abrir o painel direito.  Aqui, você pode ver uma descrição do destino. O painel direito fornece os mesmos controles descritos na tabela acima, bem como uma descrição do destino e uma indicação da categoria e do tipo de destino.

![Opções de catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte o [Catálogo de Destino](../catalog/overview.md) e [Tipos e Categorias de Destino](../destination-types.md).

## [!UICONTROL Contas] {#accounts}

Na guia **[!UICONTROL Accounts]**, você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

>[!TIP]
>
>Use o botão ![Add data button](../assets/ui/workspace/add-data-symbol.png) na coluna **[!UICONTROL Platform]** para criar uma nova conexão de destino para essa conta.

![Guia Contas](../assets/ui/workspace/edit-account-destinations.png)

| Elemento | Descrição |
---------|----------
| [!UICONTROL Plataforma] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com seu bucket ou destino de armazenamento. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de anúncios em tempo real: Servidor para servidor</li><li>Para destinos de armazenamento em nuvem Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| [!UICONTROL Nome do usuário] | O nome de usuário selecionado no [assistente de destino de conexão](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinos] | Representa o número de fluxos de destino únicos bem-sucedidos conectados às informações básicas criadas para um destino. |
| [!UICONTROL Autorizado] | A data em que a conexão com esse destino foi autorizada. |

Além disso, você pode editar ou atualizar suas informações de conta. Selecione o ![Edit account button](../assets/ui/workspace/pencil-icon.png) na coluna **[!UICONTROL Platform]** para editar as informações da conta.

Para contas que usam um tipo de conexão `OAuth2`, você pode selecionar **[!UICONTROL Reconectar OAuth]** para renovar suas credenciais de conta.

![Imagem de Oauth](../assets/ui/workspace/reconnect-oauth.png)

Para contas que usam um tipo de conexão `Access Key` ou `ConnectionString`, é possível editar as informações de autenticação da conta, incluindo informações como ID de acesso, chaves secretas ou cadeias de conexão.

![Imagem de informações da conta](../assets/ui/workspace/edit-account-details.png)

Quando terminar de editar os detalhes da conta, selecione **[!UICONTROL Save]** para concluir a atualização.

## [!UICONTROL Procurar] {#browse}

A guia **[!UICONTROL Browse]** exibe os destinos com os quais você estabeleceu uma conexão. Destinos com a opção **[!UICONTROL Enabled]** ativada configuram o destino como ativo e vice-versa. Também é possível visualizar os destinos nos quais você tem dados fluindo selecionando **[!UICONTROL Segments]** > **[!UICONTROL Browse]** e selecionando um segmento a ser inspecionado. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

>[!TIP]
>
> * Use o botão ![Add segments](../assets/ui/workspace/add-data-symbol.png) na coluna **[!UICONTROL Name]** para ativar segmentos adicionais para esse destino.
> * Use o botão ![Delete destination](../assets/ui/workspace/delete-destination-symbol.png) na coluna **[!UICONTROL Name]** para excluir uma conexão existente a um destino.


![Guia Procurar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrição |
---------|----------
| Nome | O nome fornecido para o fluxo de ativação para este destino. A mesma coluna inclui dois controles: [!UICONTROL Ativar ] e [!UICONTROL Eliminar destino]. |
| Status da Execução do Último Fluxo | O status da última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| Data de Execução do Último Fluxo | Hora e data da última execução do fluxo de dados. Consulte [Exibir detalhes do destino](destination-details-page.md) para obter mais informações sobre execuções de fluxo de dados. |
| [!UICONTROL Destino] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com seu bucket ou destino de armazenamento. <ul><li>Para destinos de marketing por email: Pode ser S3, FTP ou [!DNL Azure Blob].</li><li>Para destinos de anúncios em tempo real: Servidor para servidor.</li><li>Para destinos de transmissão: Pode ser [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome do usuário] | As credenciais de conta que você selecionou para o fluxo de destino. |
| [!UICONTROL Dados de ativação] | Indica o número de segmentos que estão sendo ativados para esse destino. Selecione este controle para saber mais sobre os segmentos ativados. Consulte [Dados de ativação](/help/destinations/ui/destination-details-page.md#activation-data) na página de detalhes do destino para obter mais informações sobre os segmentos ativados. |
| [!UICONTROL Criado] | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. |
| [!UICONTROL Status] | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](./activate-destinations.md#disable-activation). |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](../assets/ui/workspace/click-destination-row.png)

Selecione o nome do destino para ver informações sobre os segmentos ativados para este destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos segmentos que estão sendo enviados para esse destino.

## [!UICONTROL Exibição do sistema] {#system-view}

A guia **[!UICONTROL Exibição do sistema]** exibe uma representação gráfica dos fluxos de ativação que você configurou no Adobe Experience Platform.

![Fluxos de dados1](../assets/ui/workspace/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione **[!UICONTROL View flows]** para ver informações sobre todas as conexões que você configurou para cada destino.

![Fluxos de dados2](../assets/ui/workspace/data-flows2.png)