---
keywords: RTCDP;rtcdp
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: A área de trabalho Destinos consiste em quatro seções, Catálogo, Procurar, Contas e Visualização do sistema, descritas nas seções abaixo.
seo-description: Na Plataforma de dados do cliente em tempo real, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 2%

---


# Área de trabalho Destinos {#destinations-workspace}

Na Plataforma de dados do cliente em tempo real, selecione **[!UICONTROL Destinos]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Destinos] .

A área de trabalho [!UICONTROL Destinos] consiste em quatro seções, [!UICONTROL Catálogo], [!UICONTROL Navegação], [!UICONTROL Contas]e Visualização [!UICONTROL do]sistema, descritas nas seções abaixo.

![Destinos-visão geral](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A guia **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos disponíveis em CDP em tempo real para os quais você pode enviar dados.

A interface de usuário CDP em tempo real fornece várias opções de pesquisa e filtro na página de catálogo de destinos:

* Use a funcionalidade de pesquisa na página para localizar um destino específico.
* Filtre destinos usando o controle [!UICONTROL Categoria] .
* Alternar entre [!UICONTROL Todos os destinos] e [!UICONTROL Meus destinos]. Quando **[!UICONTROL Todos os destinos]** são selecionados, todos os destinos CDP em tempo real disponíveis são exibidos. Quando a opção **[!UICONTROL Meus destinos]** estiver selecionada, você só poderá ver os destinos com os quais estabeleceu uma conexão.
* Selecione para visualização de **[!UICONTROL Conexões]** e/ou **[!UICONTROL Extensões]**. Para entender a diferença entre as duas categorias, consulte Tipos de [destino e Categorias](../destination-types.md).

![filtragem de destinos e demonstração de pesquisa](../assets/ui/workspace/destinations-search-and-filter.gif)

As placas de destino contêm um controle **[!UICONTROL Configure]** ou **[!UICONTROL Ativate]** e um controle secundário que exibe mais opções. Todos eles estão descritos abaixo:

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

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte o Catálogo [de](../catalog/overview.md) destino e Tipos de [destino e Categorias](../destination-types.md).

## [!UICONTROL Contas] {#accounts}

Na guia **[!UICONTROL Contas]** , você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

>[!TIP]
>
>Use o botão ![](../assets/ui/workspace/add-data-symbol.png) Adicionar dados na coluna **[!UICONTROL Plataforma]** para criar uma nova conexão de destino para essa conta.

![Guia Contas](../assets/ui/workspace/edit-account-destinations.png)

| Elemento | Descrição |
---------|----------
| [!UICONTROL Plataforma] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Tipo de conexão] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li><li>Para destinos de armazenamentos em nuvem Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| [!UICONTROL Nome do usuário] | O nome de usuário selecionado no assistente [de destino da](../catalog/email-marketing/overview.md#connect-destination)conexão. |
| [!UICONTROL Destinos] | Representa o número de fluxos de destino exclusivos e bem-sucedidos ligados a informações básicas criadas para um destino. |
| [!UICONTROL Autorizado] | A data em que a conexão com esse destino foi autorizada. |

Além disso, você pode editar ou atualizar suas informações de conta. Selecione o botão ![](../assets/ui/workspace/pencil-icon.png) Editar conta na coluna **[!UICONTROL Plataforma]** para editar as informações da conta.

Para contas que usam um tipo de `OAuth2` conexão, você pode selecionar **[!UICONTROL Reconectar OAuth]** para renovar suas credenciais de conta.

![Imagem de Oauth](../assets/ui/workspace/reconnect-oauth.png)

Para contas que usam um tipo `Access Key` ou `ConnectionString` conexão, é possível editar as informações de autenticação da conta, incluindo informações como ID de acesso, chaves secretas ou strings de conexão.

![Imagem de informações da conta](../assets/ui/workspace/edit-account-details.png)

Quando terminar de editar os detalhes de sua conta, selecione **[!UICONTROL Salvar]** para concluir a atualização.

## [!UICONTROL Procurar] {#browse}

A guia **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a opção **[!UICONTROL Ativado]** ativada definem o destino como ativo e vice-versa. Você também pode visualização os destinos onde os dados fluem selecionando **[!UICONTROL Segmentos]** > **[!UICONTROL Navegar]** e selecionando um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

>[!TIP]
>
>Use o botão ![](../assets/ui/workspace/add-data-symbol.png) Adicionar dados na coluna **[!UICONTROL Nome]** para ativar segmentos adicionais para esse destino.

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

A guia Visualização **[!UICONTROL do]** sistema exibe uma representação gráfica dos fluxos de ativação configurados na Plataforma de dados do cliente em tempo real.

![Data-flows1](../assets/ui/workspace/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione os fluxos **[!UICONTROL de]** Visualização para ver informações sobre todas as conexões que você configurou para cada destino.

![Data-flows2](../assets/ui/workspace/data-flows2.png)