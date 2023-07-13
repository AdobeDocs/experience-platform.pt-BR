---
keywords: Experience Platform;perfil;público;públicos;segmentação;interface do usuário;UI;personalização;painel;painel;;profile;audience;audiences;segmentation;user interface;UI;customization;audience dashboard;dashboard
title: Guia do Painel de públicos-alvo
description: A Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre os públicos-alvo criados por sua organização.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 5%

---

# [!UICONTROL Públicos-alvo] painel {#audiences-dashboard}

A interface do usuário (UI) do Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre seus públicos-alvo, conforme capturadas durante um instantâneo diário. Este guia descreve como acessar e trabalhar com a [!UICONTROL Públicos-alvo] painel na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Serviço de segmentação da Adobe Experience Platform na interface do usuário da Platform, visite o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).

## [!UICONTROL Públicos-alvo] dados do painel

A variável [!UICONTROL Públicos-alvo] O painel exibe um instantâneo dos dados do atributo (registro) que sua organização tem na área de armazenamento Perfil do Experience Platform. O instantâneo não inclui dados de evento (série temporal).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou uma amostra dos dados, e o [!UICONTROL Públicos-alvo] o painel não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o [!UICONTROL Públicos-alvo] painel {#explore}

Para navegar até o [!UICONTROL Públicos-alvo] no painel da interface do Platform, selecione **[!UICONTROL Públicos-alvo]** no painel à esquerda, selecione a variável **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados de Perfil ativos ou políticas de mesclagem criadas, a variável [!UICONTROL Públicos-alvo] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e a documentação para ajudar você a começar a segmentação.

![A variável [!UICONTROL Públicos-alvo] painel [!UICONTROL Visão geral] guia com [!UICONTROL Públicos-alvo] e [!UICONTROL Visão geral] destacado.](../images/audiences/dashboard-overview.png)

### Modifique o [!UICONTROL Públicos-alvo] painel {#modify}

Você pode modificar a aparência da variável [!UICONTROL Públicos-alvo] painel selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar o **[!UICONTROL Biblioteca de widgets]** para explorar widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) para saber mais.

### Adicionar widgets {#add-widget}

Selecionar **[!UICONTROL Adicionar widget]** para navegar até a biblioteca de widgets e ver uma lista dos widgets disponíveis para adicionar ao painel.

![A variável [!UICONTROL Públicos-alvo] visão geral do painel com [!UICONTROL Adicionar widget] destacado.](../images/audiences/audiences-overview-add-widget.png)

Na biblioteca de widgets, você pode navegar pela seleção de widgets de público-alvo padrão e personalizados. Para obter informações sobre como adicionar widgets, consulte a documentação da biblioteca de widgets sobre como [adicionar um widget](../customize/widget-library.md#add-widgets).

## Selecionar um público {#select-audience}

O painel seleciona automaticamente um público-alvo a ser exibido. No entanto, é possível alterar o público-alvo usando o menu suspenso ou o seletor de público-alvo.

Para escolher um público-alvo diferente, selecione a lista suspensa ao lado do nome do público-alvo ou use o seletor de público-alvo para abrir a caixa de diálogo de seleção de público-alvo.

>[!IMPORTANT]
>
>Somente os públicos-alvo com uma contagem de perfis acima de zero são exibidos na lista de públicos-alvo selecionáveis.

![A visão geral do painel Públicos-alvo com o menu suspenso Público-alvo global é destacada.](../images/audiences/change-audience.png)

![A variável [!UICONTROL Selecionar público] que exibe todos os públicos disponíveis.](../images/audiences/select-audience-dialog.png)

## Widgets e métricas {#widgets-and-metrics}

A variável [!UICONTROL Públicos-alvo] o painel é composto por widgets, que são métricas somente leitura que fornecem informações importantes sobre o público-alvo selecionado.

A data e a hora do snapshot mais recente são exibidas na parte superior do [!UICONTROL Visão geral] ao lado da lista suspensa público-alvo. Todos os dados do widget são precisos a partir dessa data e hora. O carimbo de data e hora do instantâneo é fornecido em UTC; ele não está no fuso horário do usuário ou organização individual.

![A guia Visão geral de públicos-alvo com um carimbo de data e hora de widget realçado.](../images/audiences/widget-timestamp.png)

## Widgets padrão {#standard-widgets}

O Adobe fornece vários widgets padrão que você pode usar para visualizar métricas diferentes relacionadas aos seus públicos. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre como criar widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na lista a seguir:

* [[!UICONTROL Tamanho do público]](#audience-size)
* [[!UICONTROL Ordem de ativação de público]](#audience-activation-order)
* [[!UICONTROL Tendência de tamanho do público]](#audience-size-trend)
* [[!UICONTROL Tendência de alteração de tamanho do público]](#audience-size-change-trend)
* [[!UICONTROL Tendência de tamanho do público por identidade]](#audience-size-trend-by-identity)
* [[!UICONTROL Sobreposição de público]](#audience-overlap)
* [[!UICONTROL Relatório de sobreposição de público]](#audience-overlap-report)
* [[!UICONTROL Sobreposição de identidade]](#identity-overlap)
* [[!UICONTROL Perfis por identidade]](#profiles-by-identity)
* [[!UICONTROL Ativações programadas]](#scheduled-activations)

### [!UICONTROL Tamanho do público] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Tamanho do público"
>abstract="Este widget exibe o número total de perfis mesclados dentro do público-alvo selecionado. Esse número depende da política de mesclagem aplicada aos seus dados e é correto no momento do instantâneo mais recente."

A variável **[!UICONTROL Tamanho do público]** O widget exibe o número total de perfis mesclados no público selecionado no momento em que o instantâneo foi tirado. Esse número é o resultado da aplicação da política de mesclagem de público-alvo aos dados do seu Perfil para mesclar fragmentos de perfil e formar um único perfil para cada indivíduo no público-alvo.

Para obter mais informações sobre fragmentos e perfis mesclados, consulte [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

![A variável [!UICONTROL Públicos-alvo] visão geral do painel com o [!UICONTROL Tamanho do público] widget realçado.](../images/audiences/audience-size.png)

### [!UICONTROL Tendência de tamanho do público] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendência de tamanho do público"
>abstract="Esse widget fornece informações sobre o número total de perfis que atendem aos critérios de **qualquer** definição de segmento, conforme capturado durante o instantâneo diário, nos últimos 30 dias, 90 dias ou 12 meses."

A variável **[!UICONTROL Tendência de tamanho do público]** O widget fornece uma ilustração de gráfico de linhas para o número total de perfis qualificados para **qualquer** público-alvo durante um determinado período. A tendência de tamanho do público pode ser visualizada em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público é refletido no eixo y e a hora no eixo x.

Esse widget também inclui o [!UICONTROL Legendas] recurso em que um modelo de aprendizado de máquina analisa o gráfico e os dados do público-alvo e gera automaticamente legendas para descrever as principais tendências e eventos importantes. Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo legendas automáticas.

![A variável [!UICONTROL Públicos-alvo] visão geral exibe o widget tendência de tamanho do público-alvo.](../images/audiences/audience-size-trend-captions.png)

A caixa de diálogo de legendas automáticas é aberta, fornecendo insights sobre seus dados.

![A caixa de diálogo de legendas automáticas do widget de tendência de tamanho de Público-alvo.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Para saber mais sobre a avaliação de públicos e como os perfis se qualificam e saem dos públicos, consulte a [Documentação do Serviço de segmentação](../../segmentation/home.md).

### [!UICONTROL Tendência de alteração de tamanho do público] {#audience-size-change-trend}

Este widget fornece uma ilustração de gráfico de linhas da diferença no número total de perfis qualificados para um determinado público-alvo entre os instantâneos diários mais recentes. O público-alvo escolhido para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público é refletido no eixo y e a hora no eixo x.

![O widget de tendência de alteração de tamanho do público-alvo.](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Tendência de tamanho do público por identidade] {#audience-size-trend-by-identity}

Este widget ilustra a tendência de tamanho do público-alvo para um público-alvo específico com base no tipo de identidade escolhido no menu suspenso widget. O público-alvo usado para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget.

![O widget tendência de tamanho do público por identidade.](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Ordem de ativação de público] {#audience-activation-order}

A variável [!UICONTROL Ordem de ativação de público] O widget fornece uma tabela de três colunas que lista o nome do destino, a plataforma e a data de ativação do público-alvo. A lista é ordenada de cima para baixo de acordo com a recenticidade e pode acomodar até 10 linhas.

![O widget Ordem de ativação de público-alvo.](../images/audiences/audience-activation-order.png)

### [!UICONTROL Sobreposição de público] {#audience-overlap}

Este widget usa um diagrama de Venn para visualizar o número de pessoas que correspondem aos critérios para ambos os públicos-alvo. Os públicos-alvo usados para comparação são selecionados nos menus suspensos do widget. O número total de perfis contidos na definição de segmento relevante pode ser visto ao passar o mouse sobre um círculo ou sobre a interseção do diagrama de Venn.

Esse widget permite otimizar sua estratégia de segmentação ao visualizar as semelhanças nos resultados das suas definições de segmento.

![O widget Sobreposição de público-alvo.](../images/audiences/audience-overlap.png)

### [!UICONTROL Relatório de sobreposição de público] {#audience-overlap-report}

Esse widget tabula os dados de sobreposição de perfil para um público-alvo específico. Uma lista de cinco públicos-alvo classificados da maior para a menor porcentagem de sobreposição é fornecida para o público-alvo escolhido no menu suspenso na parte superior da tela. Para maior clareza, o público-alvo escolhido está listado na [!UICONTROL NOME DO PÚBLICO-ALVO] coluna. A análise de sobreposição de público é fornecida para o segundo público listado na [!UICONTROL AUDIENCE B NAME] coluna. A percentagem de sobreposição é indicada na terceira coluna, com uma precisão de doze casas decimais.

O relatório de sobreposição de público-alvo ajuda você a criar públicos-alvo novos e de alto desempenho. A observação de sobreposições de alta porcentagem permite suprimir públicos-alvo e impedir o envio do mesmo público-alvo para destinos diferentes. Elas também ajudam a identificar insights ocultos que podem ajudar com uma melhor segmentação. A baixa porcentagem de sobreposição ajuda a localizar perfis únicos a serem perseguidos.

Selecionar **[!UICONTROL Exibir mais]** para abrir uma caixa de diálogo em tela cheia que contém mais dados de sobreposição de público-alvo.

![O widget Relatório de sobreposição de público-alvo com a opção Exibir mais realçada .](../images/audiences/audience-overlap-report.png)

A variável [!UICONTROL Relatório de sobreposição de público] será exibida. Essa caixa de diálogo pode conter até 50 linhas de análises de sobreposição de público-alvo divididas em seis colunas. Selecione o ícone de configurações (![O ícone de configurações.](../images/audiences/settings-icon.png)) para remover ou adicionar colunas da tabela.

![A caixa de diálogo Relatório de sobreposição de público-alvo.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Selecione o **[!UICONTROL Sobreposição]** cabeçalho da coluna para alterar a classificação dos resultados entre o mais alto e o mais baixo ou do mais baixo para o mais alto.

Para baixar o relatório inteiro no formato PDF, selecione o menu de opções (**`...`**) seguido por **[!UICONTROL Baixar]**.

![A caixa de diálogo Relatório de sobreposição de público-alvo com as reticências e a opção Download destacadas.](../images/audiences/audience-overlap-report-dialog-download.png)

Selecione uma linha do relatório para abrir um diagrama Venn da análise de sobreposição. Passe o mouse sobre uma seção do diagrama de Venn para ver a contagem de perfis em uma caixa de diálogo.

![A caixa de diálogo Relatório de sobreposição de público-alvo com um diagrama Venn e uma linha realçada.](../images/audiences/audience-overlap-report-dialog-venn.png)

Selecionar **[!UICONTROL Fechar]** para retornar ao [!UICONTROL Públicos-alvo] painel.

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Sobreposição de identidade"
>abstract="Este widget mostra a sobreposição de perfis no seu público-alvo contendo as identidades escolhidas. Os círculos exibem o tamanho relativo de cada identidade. O número de perfis que contém ambos os namespaces é representado pela sobreposição entre os círculos."

A variável **[!UICONTROL Sobreposição de identidade]** O widget exibe um diagrama de Venn ou um diagrama de conjunto, mostrando a sobreposição de perfis no seu público-alvo contendo várias identidades.

Use os menus suspensos no widget para selecionar as identidades que deseja comparar. Os círculos exibem o tamanho relativo de cada identidade escolhida, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual. Essa situação faz com que seja provável que sua organização tenha vários perfis contendo fragmentos de mais de uma identidade.

Para saber mais sobre identidades, visite o [Documentação do Serviço de identidade](../../identity-service/home.md).

![A variável [!UICONTROL Públicos-alvo] visão geral do painel com o widget Sobreposição de identidade destacado.](../images/audiences/identity-overlap.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Perfis por identidade"
>abstract="Este widget exibe o detalhamento das identidades em cada perfil mesclado no público-alvo selecionado."

A variável **[!UICONTROL Perfis por identidade]** O widget exibe o detalhamento das identidades em cada perfil mesclado no público-alvo selecionado. O número total de perfis por identidade pode ser maior que o número total de perfis no público-alvo, pois um perfil pode ter várias identidades associadas a ele. Em outras palavras, a adição dos valores mostrados para cada identidade pode totalizar mais do que o tamanho total do público-alvo. Isso ocorre porque se um cliente interagir com sua marca em mais de um canal, várias identidades podem ser associadas a esse cliente individual.

Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo legendas automáticas.

![A variável [!UICONTROL Públicos-alvo] visão geral do painel com o widget Perfis por identidade e a opção Legendas destacadas.](../images/audiences/profiles-by-identity.png)

Um modelo de aprendizado de máquina gera insights de dados automaticamente ao analisar a distribuição geral e as dimensões principais dos dados.

Para saber mais sobre identidades, visite o [Documentação do Serviço de identidade](../../identity-service/home.md).

### Ativações programadas {#scheduled-activations}

A variável [!UICONTROL Ativações programadas] O widget fornece uma exibição tabulada dos destinos ativados mais recentemente. A tabela inclui a plataforma de destino, o nome do fluxo de ativação para esse destino e as datas de início e término da ativação para o público-alvo selecionado. Se não houver uma data final fornecida para a ativação, ela será exibida como [!UICONTROL Em andamento]. O público-alvo da análise é selecionado na lista suspensa na parte superior da página.

O widget permite descobrir onde e quando o público-alvo está sendo ativado e torna mais transparentes as ativações duplicadas ou desnecessárias. Essas informações acumuladas também destacam onde as ativações foram deixadas de fora.

![O widget de Ativações programadas.](../images/audiences/scheduled-activations.png)

## Próximas etapas

Ao seguir este documento, você poderá localizar o [!UICONTROL Públicos-alvo] e selecione um público-alvo a ser exibido. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com públicos-alvo na interface do Experience Platform, consulte a [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).
