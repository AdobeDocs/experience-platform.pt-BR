---
keywords: plataforma;destinos;área de trabalho de destinos;área de trabalho;ui;destinos ui;catálogo;catálogo de destinos;
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: A área de trabalho Destinos consiste em quatro seções, Catálogo, Procurar, Contas e Visualização do sistema, descritas nas seções abaixo.
seo-description: No Adobe Experience Platform, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---


# Área de trabalho de destinos {#destinations-workspace}

No Adobe Experience Platform, selecione **[!UICONTROL Destinos]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Destinos].

A área de trabalho [!UICONTROL Destinos] consiste em quatro seções, [!UICONTROL Catálogo], [!UICONTROL Procurar], [!UICONTROL Contas] e [!UICONTROL Visualização do sistema], que estão descritas nas seções abaixo.

![Destinos-visão geral](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A guia **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos disponíveis na Plataforma para os quais você pode enviar dados.

A interface do usuário da Plataforma fornece várias opções de pesquisa e filtro na página de catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtre destinos usando o controle [!UICONTROL Categoria].
* Alterne entre [!UICONTROL Todos os destinos] e [!UICONTROL Os meus destinos]. Quando **[!UICONTROL Todos os destinos]** são selecionados, todos os destinos disponíveis da Plataforma são exibidos. Quando **[!UICONTROL Os meus destinos]** são selecionados, só é possível ver os destinos com os quais estabeleceu uma ligação.
* Selecione para visualização **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]**. Para entender a diferença entre as duas categorias, consulte [Tipos de destino e Categoria](../destination-types.md).

![filtragem de destinos e demonstração de pesquisa](../assets/ui/workspace/destinations-search-and-filter.gif)

As placas de destino contêm um **[!UICONTROL Configure]** ou um **[!UICONTROL controle Ativate]** e um controle secundário que apresenta mais opções. Todos eles estão descritos abaixo:

| Controle | Descrição |
---------|----------
| [!UICONTROL Configurar] | Permite criar uma conexão com o destino. |
| [!UICONTROL Ativar] | Depois de estabelecer uma conexão com o destino, é possível ativar os segmentos. |
| [!UICONTROL conta de visualização] | Visualização as contas que você conectou para um destino. |
| [!UICONTROL Fluxos de dados de visualização] | Visualização dos fluxos de ativação de dados que existem para um destino. |
| [!UICONTROL Documentação de visualização] | Abre um link para a página de documentação referente ao destino específico, para obter mais informações e para ajudá-lo a configurá-lo. |

![Controles no cartão de destinos](../assets/ui/workspace/destination-card-options.png)

Selecione um cartão de destino no catálogo para abrir o painel direito.  Aqui, você pode ver uma descrição do destino. O painel direito fornece os mesmos controles descritos na tabela acima, bem como uma descrição do destino e uma indicação da categoria de destino e do tipo.

![Opções de catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte [Catálogo de destino](../catalog/overview.md) e [Tipos de destino e Categorias](../destination-types.md).

## [!UICONTROL Contas] {#accounts}

Na guia **[!UICONTROL Accounts]**, você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

>[!TIP]
>
>Use o botão ![Adicionar dados](../assets/ui/workspace/add-data-symbol.png) na coluna **[!UICONTROL Plataforma]** para criar uma nova conexão de destino para essa conta.

![Guia Contas](../assets/ui/workspace/edit-account-destinations.png)

| Elemento | Descrição |
---------|----------
| [!UICONTROL Plataforma] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li><li>Para destinos de armazenamentos em nuvem Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| [!UICONTROL Nome do usuário] | O nome de usuário selecionado no [assistente de destino de conexão](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinos] | Representa o número de fluxos de destino exclusivos e bem-sucedidos ligados a informações básicas criadas para um destino. |
| [!UICONTROL Autorizado] | A data em que a conexão com esse destino foi autorizada. |

Além disso, você pode editar ou atualizar suas informações de conta. Selecione o botão ![Editar conta](../assets/ui/workspace/pencil-icon.png) na coluna **[!UICONTROL Plataforma]** para editar as informações da conta.

Para contas que usam um tipo de conexão `OAuth2`, você pode selecionar **[!UICONTROL Reconectar OAuth]** para renovar suas credenciais de conta.

![Imagem de Oauth](../assets/ui/workspace/reconnect-oauth.png)

Para contas que usam um tipo de conexão `Access Key` ou `ConnectionString`, você pode editar as informações de autenticação da conta, incluindo informações como ID de acesso, chaves secretas ou strings de conexão.

![Imagem de informações da conta](../assets/ui/workspace/edit-account-details.png)

Quando terminar de editar os detalhes de sua conta, selecione **[!UICONTROL Salvar]** para concluir a atualização.

## [!UICONTROL Procurar] {#browse}

A guia **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a alternância **[!UICONTROL Enabled]** ativada definem o destino como ativo e vice-versa. Você também pode visualização os destinos onde os dados fluem selecionando **[!UICONTROL Segmentos]** > **[!UICONTROL Procurar]** e selecionando um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

>[!TIP]
>
>Use o botão ![Adicionar dados](../assets/ui/workspace/add-data-symbol.png) na coluna **[!UICONTROL Nome]** para ativar segmentos adicionais para esse destino.

![Guia Procurar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrição |
---------|----------
| Nome | O nome fornecido para o fluxo de ativação para este destino. |
| [!UICONTROL Destino] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li></ul> |
| [!UICONTROL Nome do usuário] | As credenciais de conta que você selecionou para o fluxo de destino. |
| [!UICONTROL Segmentos] | O número de segmentos que estão sendo ativados para esse destino. |
| [!UICONTROL Criado] | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. |
| [!UICONTROL Status] | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](./activate-destinations.md#disable-activation). |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](../assets/ui/workspace/click-destination-row.png)

Selecione o nome de destino para ver informações sobre os segmentos ativados para este destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos segmentos que estão sendo enviados para esse destino.

## [!UICONTROL Visualização do sistema] {#system-view}

A guia **[!UICONTROL Visualização do sistema]** exibe uma representação gráfica dos fluxos de ativação configurados no Adobe Experience Platform.

![Fluxos de dados1](../assets/ui/workspace/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione **[!UICONTROL fluxos de Visualização]** para ver informações sobre todas as conexões que você configurou para cada destino.

![Fluxos de dados2](../assets/ui/workspace/data-flows2.png)