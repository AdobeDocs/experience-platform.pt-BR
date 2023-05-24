---
keywords: Experience Platform;perfil;segmento;segmentos;segmentação;interface do usuário;UI;personalização;painel;painel;;profile;segment;segments;segmentation;user interface;UI;customization;segment dashboard;dashboard
title: Guia do Painel de segmentos
description: A Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre os segmentos criados por sua organização.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 7%

---

# [!UICONTROL Segmentos] painel {#segment-dashboard}

A interface do usuário (UI) do Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre seus segmentos, conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmentos na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Serviço de segmentação da Adobe Experience Platform na interface do usuário da Platform, visite o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).

## [!UICONTROL Segmentos] dados do painel

O painel de segmentos exibe um instantâneo dos dados do atributo (registro) que sua organização tem na área de armazenamento Perfil do Experience Platform. O instantâneo não inclui dados de evento (série temporal).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmentos não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o [!UICONTROL Segmentos] painel {#explore}

Para navegar até o [!UICONTROL Segmentos] no painel da interface do Platform, selecione **[!UICONTROL Segmentos]** no painel à esquerda, selecione a variável **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados de Perfil ativos ou políticas de mesclagem criadas, a variável [!UICONTROL Segmentos] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e a documentação para ajudar você a começar a segmentação.

![A guia Visão geral do painel de Segmentos com os segmentos e a Visão geral destacados.](../images/segments/dashboard-overview.png)

### Modifique o [!UICONTROL Segmentos] painel {#modify}

Você pode modificar a aparência da variável [!UICONTROL Segmentos] painel selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar o **[!UICONTROL Biblioteca de widgets]** para explorar widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) para saber mais.

### Adicionar widgets {#add-widget}

Selecionar **[!UICONTROL Adicionar widget]** para navegar até a biblioteca de widgets e ver uma lista dos widgets disponíveis para adicionar ao painel.

![A visão geral do painel Segmentos com o widget Adicionar é destacada.](../images/segments/segments-overview-add-widget.png)

Na biblioteca de widgets, você pode navegar pela seleção de widgets de segmentos padrão e personalizados.Para obter informações sobre como adicionar widgets, consulte a documentação da biblioteca de widgets sobre como [adicionar um widget](../customize/widget-library.md#add-widgets).

## Selecionar um segmento

O painel seleciona automaticamente um segmento para exibição, no entanto, você pode alterar o segmento usando o menu suspenso ou o seletor de segmentos.

Para escolher um segmento diferente, selecione a lista suspensa ao lado do nome do segmento ou use o seletor de segmentos para abrir a caixa de diálogo de seleção de segmentos.

>[!IMPORTANT]
>
>Somente os segmentos com uma contagem de perfis acima de zero são exibidos na lista de segmentos selecionáveis.

![A visão geral do painel Segmentos com o menu suspenso de segmentos global é realçada.](../images/segments/change-segment.png)

![A caixa de diálogo Selecionar segmento que exibe todos os segmentos disponíveis.](../images/segments/select-segment-dialog.png)

## Widgets e métricas

O painel de segmentos é composto por widgets, que são métricas somente leitura que fornecem informações importantes sobre o segmento selecionado.

A data e a hora do snapshot mais recente são exibidas na parte superior do [!UICONTROL Visão geral] ao lado da lista suspensa de segmentos. Todos os dados do widget são precisos a partir dessa data e hora. O carimbo de data e hora do instantâneo é fornecido em UTC; ele não está no fuso horário do usuário ou organização individual.

![A guia Visão geral de segmentos com um carimbo de data e hora de widget realçado.](../images/segments/widget-timestamp.png)

## Widgets padrão {#standard-widgets}

O Adobe fornece vários widgets padrão que você pode usar para visualizar métricas diferentes relacionadas aos seus segmentos. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre como criar widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

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
>abstract="Esse widget exibe o número total de perfis mesclados no segmento selecionado. Esse número depende da política de mesclagem aplicada aos seus dados e é correto no momento do instantâneo mais recente."

A variável **[!UICONTROL Tamanho do público]** O widget exibe o número total de perfis mesclados no segmento selecionado no momento em que o instantâneo foi tirado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos dados do seu Perfil para mesclar fragmentos de perfil e formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, consulte [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

![A visão geral do painel Segmentos com o widget de tamanho Público-alvo destacado.](../images/segments/audience-size.png)

### [!UICONTROL Tendência de tamanho do público] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendência de tamanho do público"
>abstract="Esse widget fornece informações sobre o número total de perfis que atendem aos critérios de **qualquer** definição de segmento, conforme capturado durante o instantâneo diário, nos últimos 30 dias, 90 dias ou 12 meses."

A variável **[!UICONTROL Tendência de tamanho do público]** O widget fornece uma ilustração de gráfico de linhas para o número total de perfis que atendem aos critérios de **qualquer** definição de segmento em um determinado período. A tendência de tamanho do público pode ser visualizada em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público é refletido no eixo y e a hora no eixo x.

Esse widget também inclui o [!UICONTROL Legendas] recurso em que um modelo de aprendizado de máquina analisa o gráfico e os dados de segmento e gera automaticamente legendas para descrever as principais tendências e eventos importantes. Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo legendas automáticas.

![A visão geral de Segmentos exibe o widget de tendência de tamanho do Público-alvo.](../images/segments/audience-size-trend-captions.png)

A caixa de diálogo de legendas automáticas é aberta, fornecendo insights sobre seus dados.

![A caixa de diálogo de legendas automáticas do widget de tendência de tamanho de Público-alvo.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Para saber mais sobre a avaliação de segmentos e como os perfis se qualificam e saem dos segmentos, consulte o [Documentação do Serviço de segmentação](../../segmentation/home.md).

### [!UICONTROL Tendência de alteração de tamanho do público] {#audience-size-change-trend}

Este widget fornece uma ilustração de gráfico de linhas da diferença no número total de perfis qualificados para um determinado segmento entre os instantâneos diários mais recentes. O segmento escolhido para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público é refletido no eixo y e a hora no eixo x.

![O widget de tendência de alteração de tamanho do público-alvo.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Tendência de tamanho do público por identidade] {#audience-size-trend-by-identity}

Este widget ilustra a tendência do tamanho do público-alvo para um segmento específico com base no tipo de identidade escolhido no menu suspenso widget. O segmento usado para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget.

![O widget tendência de tamanho do público por identidade.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Ordem de ativação de público] {#audience-activation-order}

A variável [!UICONTROL Ordem de ativação de público] O widget fornece uma tabela de três colunas que lista as [!UICONTROL nome do destino], o [!UICONTROL platform]e a ativação [!UICONTROL data] do público. A lista é ordenada de cima para baixo de acordo com a recenticidade e pode acomodar até 10 linhas.

![O widget Ordem de ativação de público-alvo.](../images/segments/audience-activation-order.png)

### [!UICONTROL Sobreposição de público] {#audience-overlap}

Este widget representa o número de perfis de dois segmentos que atendem aos critérios para ambas as definições de segmento. Os segmentos usados para comparação são selecionados nos menus suspensos do widget. O número total de perfis contidos na definição de segmento relevante pode ser visto ao passar o mouse sobre um círculo ou sobre a interseção do diagrama de Venn.

Esse widget permite otimizar sua estratégia de segmentação ao visualizar as semelhanças nos resultados das suas definições de segmento.

![O widget Sobreposição de público-alvo.](../images/segments/audience-overlap.png)

### [!UICONTROL Relatório de sobreposição de público] {#audience-overlap-report}

Esse widget tabula os dados de sobreposição de público-alvo para um segmento específico. Uma lista de cinco públicos-alvo classificados do maior para o menor percentual de sobreposição é fornecida para o segmento escolhido no menu suspenso na parte superior da tela. Para maior clareza, o segmento escolhido está listado no [!UICONTROL NOME DO SEGMENTO A] coluna. A análise de sobreposição de público-alvo é fornecida para o segundo segmento listado no [!UICONTROL NOME DO SEGMENTO B] coluna. A percentagem de sobreposição é indicada na terceira coluna, com uma precisão de doze casas decimais.

O relatório de sobreposição de público-alvo ajuda você a criar segmentos novos e de alto desempenho. A observação de sobreposições de alta porcentagem permite suprimir públicos-alvo e impedir o envio do mesmo público-alvo para destinos diferentes. Elas também ajudam a identificar insights ocultos que podem ajudar com uma melhor segmentação. A baixa porcentagem de sobreposição ajuda a localizar perfis únicos a serem perseguidos.

Selecionar **[!UICONTROL Exibir mais]** para abrir uma caixa de diálogo de tela cheia que contém mais dados de sobreposição de segmento.

![O widget Relatório de sobreposição de público-alvo com a opção Exibir mais realçada .](../images/segments/audience-overlap-report.png)

A variável [!UICONTROL Relatório de sobreposição de público] será exibida. Essa caixa de diálogo pode conter até 50 linhas de análises de sobreposição de público-alvo divididas em seis colunas. Selecione o ícone de configurações (![O ícone de configurações.](../images/segments/settings-icon.png)) para remover ou adicionar colunas da tabela.

![A caixa de diálogo Relatório de sobreposição de público-alvo.](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Selecione o **[!UICONTROL Sobreposição]** cabeçalho da coluna para alterar a classificação dos resultados entre o mais alto e o mais baixo ou do mais baixo para o mais alto.

Para baixar o relatório inteiro no formato PDF, selecione o menu de opções (**`...`**) seguido por **[!UICONTROL Baixar]**.

![A caixa de diálogo Relatório de sobreposição de público-alvo com as reticências e a opção Download destacadas.](../images/segments/segments-audience-overlap-report-dialog-download.png)

Selecione uma linha do relatório para abrir um diagrama Venn da análise de sobreposição. Passe o mouse sobre uma seção do diagrama de Venn para ver a contagem de perfis em uma caixa de diálogo.

![A caixa de diálogo Relatório de sobreposição de público-alvo com um diagrama Venn e uma linha realçada.](../images/segments/audience-overlap-report-dialog-venn.png)

Selecionar **[!UICONTROL Fechar]** para retornar ao [!UICONTROL Segmentos] painel.

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Sobreposição de identidade"
>abstract="Esse widget mostra a sobreposição de perfis em seu segmento que contém ambas as identidades escolhidas. Os círculos exibem o tamanho relativo de cada identidade. O número de perfis que contém ambos os namespaces é representado pela sobreposição entre os círculos."

A variável **[!UICONTROL Sobreposição de identidade]** O widget exibe um diagrama de Venn ou um diagrama de conjunto, mostrando a sobreposição de perfis no seu segmento que contém várias identidades.

Use os menus suspensos no widget para selecionar as identidades que deseja comparar. Os círculos exibem o tamanho relativo de cada identidade escolhida, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis que contenham fragmentos de mais de uma identidade.

Para saber mais sobre identidades, visite o [Documentação do serviço de identidade da Adobe Experience Platform](../../identity-service/home.md).

![A visão geral do painel Segmentos com o widget Sobreposição de identidade é realçada.](../images/segments/identity-overlap.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Perfis por identidade"
>abstract="Esse widget exibe o detalhamento das identidades em cada perfil mesclado no segmento selecionado."

A variável **[!UICONTROL Perfis por identidade]** O widget exibe o detalhamento das identidades em cada perfil mesclado no segmento selecionado. O número total de perfis por identidade pode ser maior que o número total de perfis no segmento, pois um perfil pode ter várias identidades associadas a ele. Em outras palavras, adicionar os valores mostrados para cada identidade pode totalizar mais do que o tamanho total do público-alvo no segmento, pois se um cliente interagir com sua marca em mais de um canal, várias identidades podem ser associadas a esse cliente individual.

Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo legendas automáticas.

![A visão geral do painel Segmentos com o widget Perfis por identidade e a opção Legendas destacadas.](../images/segments/profiles-by-identity.png)

Um modelo de aprendizado de máquina gera insights de dados automaticamente ao analisar a distribuição geral e as dimensões principais dos dados.

Para saber mais sobre identidades, visite o [Documentação do serviço de identidade da Adobe Experience Platform](../../identity-service/home.md).

### Ativações programadas {#scheduled-activations}

A variável [!UICONTROL Ativações programadas] O widget fornece uma exibição tabulada dos destinos ativados mais recentemente. A tabela inclui a plataforma de destino, o nome do fluxo de ativação para esse destino e as datas inicial e final de ativação do segmento selecionado. Se não houver uma data final fornecida para a ativação, ela será exibida como [!UICONTROL Em andamento]. O segmento para análise é selecionado na lista suspensa na parte superior da página.

O widget permite descobrir onde e quando o público-alvo está sendo ativado e torna mais transparentes as ativações duplicadas ou desnecessárias. Essas informações acumuladas também destacam onde as ativações foram deixadas de fora.

![O widget de Ativações programadas.](../images/segments/scheduled-activations.png)

## Próximas etapas

Ao seguir esse documento, agora é possível localizar o painel de segmentos e selecionar um segmento a ser exibido. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).
