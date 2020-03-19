---
title: Área de trabalho Destinos
seo-title: Área de trabalho Destinos
description: Na Plataforma de dados do cliente em tempo real da Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
seo-description: Na Plataforma de dados do cliente em tempo real da Adobe, selecione Destinos na barra de navegação esquerda para acessar a área de trabalho de destinos.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# Área de trabalho Destinos {#destinations-workspace}

Na Plataforma de dados do cliente em tempo real da Adobe, selecione **Destinos** na barra de navegação esquerda para acessar a área de trabalho Destinos.

A área de trabalho Destinos consiste em quatro seções, **Catálogo**, **Navegação**, **Contas** e Fluxos **de** Dados, descritas nas seções abaixo.

![Destinos-visão geral](/help/rtcdp/destinations/assets/destinations-overview.png)

## Catálogo {#catalog}

A guia **[!UICONTROL Catálogo]** exibe uma lista de todos os destinos oferecidos pela Adobe para os quais você pode enviar dados. Selecione um destino no catálogo para abrir o painel direito. Aqui, você pode configurar uma conexão com o destino (destino **do** Connect) ou obter informações mais detalhadas sobre cada destino exibindo a documentação (**Exibir documentação**).

![Opções de catálogo de destino](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Para obter mais informações sobre categorias de destino e informações sobre cada destino, consulte Catálogo [](/help/rtcdp/destinations/destinations-catalog.md)de destino.

## Navegar {#browse}

A guia **[!UICONTROL Procurar]** exibe os destinos com os quais você estabeleceu uma conexão. Os destinos com a alternância ativada definem o destino como ativo e vice-versa. Você também pode exibir os destinos onde os dados fluem selecionando **Segmentos > Procurar** e selecionando um segmento para inspecionar. Consulte a tabela abaixo para obter todas as informações fornecidas para cada destino na guia Procurar:

![Guia Procurar](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descrição |
---------|----------
| Nome do destino | O nome fornecido para o fluxo de ativação para este destino. |
| Destino | A plataforma de destino selecionada para o fluxo de ativação. |
| Criado | A data e a hora UTC em que o fluxo de ativação para o destino foi criado. |
| Tipo de conexão | *Somente* para destinos de marketing por email. Representa o tipo de conexão com seu bucket de armazenamento. Pode ser S3 ou FTP. |
| Nome de usuário | As credenciais de conta que você selecionou para o fluxo de destino. |
| Segmentos | O número de segmentos que estão sendo ativados para esse destino. |
| Status | `Active` ou `Inactive`. Indica se os dados estão sendo ativados no momento para esse destino. Para editar o status, consulte [Desativar ativação](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Clique em uma linha de destino para exibir mais informações sobre o destino no painel direito.

![Clique na linha de destino](/help/rtcdp/destinations/assets/click-destination-row.png)

Selecione o nome de destino para ver informações sobre os segmentos ativados para este destino. Clique em **[!UICONTROL Editar ativação]** para modificar ou adicionar aos segmentos que estão sendo enviados para esse destino.

## Contas {#accounts}

Na guia **[!UICONTROL Contas]** , você pode saber mais sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

![Guia Contas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descrição |
---------|----------
| Plataforma | O destino para o qual você configurou a conexão. |
| Nome de usuário | O nome de usuário selecionado no assistente [de destino da](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexão. |
| Fluxos | Representa o número de fluxos de destino exclusivos e bem-sucedidos ligados a informações básicas criadas para um destino. |
| Autorizado | A data em que a conexão com esse destino foi autorizada. |

## Fluxos de dados {#data-flows}

A guia Fluxos **[!UICONTROL de]** dados exibe uma representação gráfica dos fluxos de ativação configurados na Plataforma de dados do cliente em tempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecione qualquer um dos destinos exibidos na página e pressione **[!UICONTROL Exibir fluxos]** para ver informações sobre todos os fluxos de dados que você configurou para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)