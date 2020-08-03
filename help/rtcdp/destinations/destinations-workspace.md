---
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: No Adobe Real-time Customer Data Platform, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
seo-description: No Adobe Real-time Customer Data Platform, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 3%

---


# Área de trabalho Destinos {#destinations-workspace}

No Adobe Real-time Customer Data Platform, selecione **[!UICONTROL Destinos]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Destinos] .

A área de trabalho [!UICONTROL Destinos] consiste em quatro seções, **[!UICONTROL Catálogo]**, **[!UICONTROL Navegação]**, **[!UICONTROL Contas]** e Visualização **[!UICONTROL do]** sistema, descritas nas seções abaixo.

![Destinos-visão geral](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

A guia **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos oferecidos pelo Adobe para os quais você pode enviar dados.

Use a funcionalidade de pesquisa na página para localizar um destino específico ou filtrar destinos usando o controle **[!UICONTROL Categoria]** .

Selecione um destino no catálogo para abrir o painel direito. Aqui, você pode configurar uma conexão com o destino (destino **[!UICONTROL do]** Connect), visualização as conexões de destino existentes (**[!UICONTROL Procurar destinos]**) ou obter informações mais detalhadas sobre cada destino exibindo a documentação (documentação **[!UICONTROL de]** Visualização).

![Opções de catálogo de destino](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destino.

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

A guia Visualização **[!UICONTROL do]** sistema exibe uma representação gráfica dos fluxos de ativação configurados no Platform de dados do cliente em tempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione os fluxos **[!UICONTROL de]** Visualização para ver informações sobre todas as conexões que você configurou para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)