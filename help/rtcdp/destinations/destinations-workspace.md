---
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: Na Plataforma de dados do cliente em tempo real do Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
seo-description: Na Plataforma de dados do cliente em tempo real do Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: f3e489416a9bc80cfb0502d3973a86748123a687
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 2%

---


# Área de trabalho Destinos {#destinations-workspace}

Na Plataforma de dados do cliente em tempo real do Adobe, selecione **[!UICONTROL Destinos]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Destinos] .

A área de trabalho [!UICONTROL Destinos] consiste em quatro seções, **[!UICONTROL Catálogo]**, **[!UICONTROL Navegação]**, **[!UICONTROL Contas]** e Visualização **[!UICONTROL do]** sistema, descritas nas seções abaixo.

![Destinos-visão geral](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A guia **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos disponíveis no Adobe Real-time CDP, para os quais você pode enviar dados.

A interface de usuário CDP em tempo real do Adobe fornece várias opções de pesquisa e filtro na página de catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtre destinos usando o controle **[!UICONTROL Categoria]** .
* Alternar entre **[!UICONTROL Todos os destinos]** e **[!UICONTROL Meus destinos]**. Quando **[!UICONTROL Todos os destinos]** são selecionados, todos os destinos CDP em tempo real disponíveis do Adobe são exibidos. Quando a opção **[!UICONTROL Meus destinos]** estiver selecionada, você só poderá ver os destinos com os quais estabeleceu uma conexão.
* Selecione para visualização de **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]**. Para entender a diferença entre as duas categorias, consulte Tipos de [destino e Categorias](/help/rtcdp/destinations/destination-types.md).

![filtragem de destinos e demonstração de pesquisa](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

As placas de destino contêm um controle **[!UICONTROL Configure]** ou **[!UICONTROL Ativate]** e um controle secundário que exibe mais opções. Todos eles estão descritos abaixo:

| Controle | Descrição |
---------|----------
| [!UICONTROL Configurar ] | Permite criar uma conexão com o destino. |
| [!UICONTROL Ativar] | Depois de estabelecer uma conexão com o destino, é possível ativar os segmentos. |
| [!UICONTROL conta de visualização] | Visualização as contas que você conectou para um destino. |
| [!UICONTROL Fluxos de dados de visualização] | Visualização dos fluxos de ativação de dados existentes para um destino |
| [!UICONTROL Documentação de visualização] | Abre um link para a página de documentação referente ao destino específico, para obter mais informações e para ajudá-lo a configurá-lo. |

![Controles no cartão de destinos](/help/rtcdp/destinations/assets/destination-card-options.png)

Selecione um cartão de destino no catálogo para abrir o painel direito.  Aqui, você pode ver uma descrição do destino. O painel direito fornece os mesmos controles descritos na tabela acima, bem como uma descrição do destino e uma indicação da categoria de destino e do tipo.

![Opções de catálogo de destino](/help/rtcdp/destinations/assets/destination-right-rail.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte o Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) destino e Tipos de [destino e Categorias](/help/rtcdp/destinations/destination-types.md).

## [!UICONTROL Procurar] {#browse}

A guia **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a alternância **[!UICONTROL ativada]** ativada definem o destino como ativo e vice-versa. Você também pode visualização os destinos onde os dados fluem selecionando **[!UICONTROL Segmentos]** > **[!UICONTROL Navegar]** e selecionando um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

![Guia Procurar](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descrição |
---------|----------
| Nome | O nome fornecido para o fluxo de ativação para este destino. |
| [!UICONTROL Destino] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li></ul> |
| [!UICONTROL Nome do usuário] | As credenciais de conta que você selecionou para o fluxo de destino. |
| [!UICONTROL Segmentos] | O número de segmentos que estão sendo ativados para esse destino. |
| [!UICONTROL Criado] | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. |
| [!UICONTROL Status] | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](/help/rtcdp/destinations/assets/click-destination-row.png)

Selecione o nome de destino para ver informações sobre os segmentos ativados para este destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos segmentos que estão sendo enviados para esse destino.

## [!UICONTROL Contas] {#accounts}

Na guia **[!UICONTROL Contas]** , você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

![Guia Contas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descrição |
---------|----------
| [!UICONTROL Plataforma] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li><li>Para destinos de armazenamentos em nuvem Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| [!UICONTROL Nome do usuário] | O nome de usuário selecionado no assistente [de destino da](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexão. |
| [!UICONTROL Fluxos de dados] | Representa o número de fluxos de destino exclusivos e bem-sucedidos ligados a informações básicas criadas para um destino. |
| [!UICONTROL Autorizado] | A data em que a conexão com esse destino foi autorizada. |
| [!UICONTROL Status] | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL Visualização do sistema] {#system-view}

A guia Visualização **[!UICONTROL do]** sistema exibe uma representação gráfica dos fluxos de ativação configurados na Plataforma de dados do cliente em tempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione os fluxos **[!UICONTROL de]** Visualização para ver informações sobre todas as conexões que você configurou para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)