---
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: Na Plataforma de dados do cliente em tempo real da Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
seo-description: Na Plataforma de dados do cliente em tempo real da Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: e87ddff936da88b1b2b3cf71c2d6c24ed28b39ab

---


# Área de trabalho Destinos {#destinations-workspace}

Na Plataforma de dados do cliente em tempo real da Adobe, selecione **Destinos** na barra de navegação esquerda para acessar a área de trabalho Destinos.

A área de trabalho Destinos consiste em quatro seções, **Catálogo**, **Navegação**, **Contas** e Visualização **** do sistema, descritas nas seções abaixo.

![Destinos-visão geral](/help/rtcdp/destinations/assets/destinations-overview.png)

## Catálogo {#catalog}

A **[!UICONTROL Catalog]** guia exibe uma lista de todos os destinos oferecidos pela Adobe para os quais você pode enviar dados.

Use a funcionalidade de pesquisa na página para localizar um destino específico ou filtrar destinos usando o **[!UICONTROL Categories]** controle.

Selecione um destino no catálogo para abrir o painel direito. Aqui, você pode configurar uma conexão com o destino (destino **do** Connect), visualização as conexões de destino existentes (**Procurar destinos**) ou obter informações mais detalhadas sobre cada destino exibindo a documentação (documentação **de** Visualização).

![Opções de catálogo de destino](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destino.

## Procurar {#browse}

A **[!UICONTROL Browse]** guia exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a alternância **ativada** ativada definem o destino como ativo e vice-versa. Você também pode visualização os destinos onde os dados fluem selecionando **Segmentos > Procurar** e selecionando um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

![Guia Procurar](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descrição |
---------|----------
| Nome | O nome fornecido para o fluxo de ativação para este destino. |
| Destino | A plataforma de destino selecionada para o fluxo de ativação. |
| Tipo de conexão | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li></ul> |
| Nome do usuário | As credenciais de conta que você selecionou para o fluxo de destino. |
| Segmentos | O número de segmentos que estão sendo ativados para esse destino. |
| Criado | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. |
| Status | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](/help/rtcdp/destinations/assets/click-destination-row.png)

Selecione o nome de destino para ver informações sobre os segmentos ativados para este destino. Clique **[!UICONTROL Edit activation]** para modificar ou adicionar aos segmentos que estão sendo enviados para este destino.

## Contas {#accounts}

Na **[!UICONTROL Accounts]** guia, você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

![Guia Contas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descrição |
---------|----------
| Plataforma | O destino para o qual você configurou a conexão. |
| Tipo de conexão | Representa o tipo de conexão com o seu bucket ou destino de armazenamentos. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de publicidade em tempo real: Servidor para servidor</li><li>Para destinos de armazenamentos em nuvem do Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| Nome do usuário | O nome de usuário selecionado no assistente [de destino da](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexão. |
| Fluxos de dados | Representa o número de fluxos de destino exclusivos e bem-sucedidos ligados a informações básicas criadas para um destino. |
| Autorizado | A data em que a conexão com esse destino foi autorizada. |
| Status | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## Visualização do sistema {#system-view}

A **[!UICONTROL System View]** guia exibe uma representação gráfica dos fluxos de ativação que você configurou na Plataforma de dados do cliente em tempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione **[!UICONTROL View flows]** para ver informações sobre todas as conexões que você configurou para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)