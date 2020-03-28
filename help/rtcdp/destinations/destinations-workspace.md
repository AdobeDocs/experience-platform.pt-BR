---
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: Na Plataforma de dados do cliente em tempo real da Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
seo-description: Na Plataforma de dados do cliente em tempo real da Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Área de trabalho Destinos {#destinations-workspace}

Na Plataforma de dados do cliente em tempo real da Adobe, selecione **[!UICONTROL Destinations]** na barra de navegação esquerda para acessar a área de [!UICONTROL Destinations] trabalho.

O [!UICONTROL Destinations] espaço de trabalho consiste em quatro seções, **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]** e **[!UICONTROL System View]**, descritas nas seções abaixo.

![Destinos-visão geral](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

A **[!UICONTROL Catalog]** guia exibe uma lista de todos os destinos oferecidos pela Adobe para os quais você pode enviar dados.

Use a funcionalidade de pesquisa na página para localizar um destino específico ou filtrar destinos usando o **[!UICONTROL Categories]** controle.

Selecione um destino no catálogo para abrir o painel direito. Aqui, você pode configurar uma conexão com o destino (**[!UICONTROL Connect destination]**), visualização as conexões de destino existentes (**[!UICONTROL Browse destinations]**) ou obter informações mais detalhadas sobre cada destino ao exibir a documentação (**[!UICONTROL View documentation]**).

![Opções de catálogo de destino](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destino.

## [!UICONTROL Browse] {#browse}

A **[!UICONTROL Browse]** guia exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a **[!UICONTROL enabled]** alternância ativada definem o destino como ativo e vice-versa. Você também pode visualização os destinos onde os dados fluem selecionando **[!UICONTROL Segments > Browse]** e selecionando um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

![Guia Procurar](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descrição |
---------|----------
| Nome | O nome fornecido para o fluxo de ativação para este destino. |
| [!UICONTROL Destination] | A plataforma de destino selecionada para o fluxo de ativação. |
| [!UICONTROL Connection Type] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li></ul> |
| [!UICONTROL Username] | As credenciais de conta que você selecionou para o fluxo de destino. |
| [!UICONTROL Segments] | O número de segmentos que estão sendo ativados para esse destino. |
| [!UICONTROL Created] | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. |
| [!UICONTROL Status] | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](/help/rtcdp/destinations/assets/click-destination-row.png)

Selecione o nome de destino para ver informações sobre os segmentos ativados para este destino. Clique **[!UICONTROL Edit activation]** para modificar ou adicionar aos segmentos que estão sendo enviados para este destino.

## [!UICONTROL Accounts] {#accounts}

Na **[!UICONTROL Accounts]** guia, você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

![Guia Contas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descrição |
---------|----------
| [!UICONTROL Platform] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Connection Type] | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li><li>Para destinos de armazenamentos em nuvem do Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| [!UICONTROL Username] | O nome de usuário selecionado no assistente [de destino da](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexão. |
| [!UICONTROL Data Flows] | Representa o número de fluxos de destino exclusivos e bem-sucedidos ligados a informações básicas criadas para um destino. |
| [!UICONTROL Authorized] | A data em que a conexão com esse destino foi autorizada. |
| [!UICONTROL Status] | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL System View] {#system-view}

A **[!UICONTROL System View]** guia exibe uma representação gráfica dos fluxos de ativação que você configurou na Plataforma de dados do cliente em tempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione **[!UICONTROL View flows]** para ver informações sobre todas as conexões que você configurou para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)