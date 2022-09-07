---
keywords: Experience Platform, perfil, segmento, segmentos, segmentação, interface do usuário, interface do usuário, personalização, painel de segmentos, painel
title: Guia do painel Segmentos
description: O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre segmentos criados por sua organização.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 7f226a37996ab5e1fef432c6007d7d488f84ded6
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 0%

---

# [!UICONTROL Segmentos] painel {#segment-dashboard}

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmentos na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Serviço de segmentação da Adobe Experience Platform na interface do usuário da plataforma, visite o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).

## [!UICONTROL Segmentos] dados do painel

O painel de segmentos exibe um instantâneo dos dados de atributo (registro) que sua organização tem no armazenamento de Perfil no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmentos não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o [!UICONTROL Segmentos] painel {#explore}

Para navegar até o [!UICONTROL Segmentos] no painel da interface do usuário da plataforma, selecione **[!UICONTROL Segmentos]** no painel à esquerda, selecione o **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados ativos do Perfil ou políticas de mesclagem criadas, a variável [!UICONTROL Segmentos] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e documentação para ajudar você a começar a usar a segmentação.

![A guia Visão geral do painel Segmentos .](../images/segments/dashboard-overview.png)

### Modifique o [!UICONTROL Segmentos] painel {#modify}

Você pode modificar a aparência da variável [!UICONTROL Segmentos] painel selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar o **[!UICONTROL Biblioteca de widgets]** para explorar widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) documentação para saber mais.

### Adicionar widgets {#add-widget}

Selecionar **[!UICONTROL Adicionar widget]** para navegar até a biblioteca de widgets e ver uma lista dos widgets disponíveis para adicionar ao painel.

![A visão geral do painel Segmentos com Adicionar widget foi realçada.](../images/segments/segments-overview-add-widget.png)

Na biblioteca de widgets, você pode navegar pela seleção de widgets de segmento padrão e personalizado.Para obter informações sobre como adicionar widgets, consulte a documentação da biblioteca de widgets sobre como [adicionar um widget](../customize/widget-library.md#add-widgets).

## Selecionar um segmento

O painel seleciona automaticamente um segmento para exibição, no entanto, você pode alterar o segmento usando o menu suspenso ou o seletor de segmentos.

Para escolher um segmento diferente, selecione a lista suspensa ao lado do nome do segmento ou use o seletor de segmentos para abrir a caixa de diálogo de seleção de segmentos.

>[!IMPORTANT]
>
>Somente os segmentos com uma contagem de perfil acima de zero são exibidos na lista de segmentos selecionáveis.

![A visão geral do painel Segmentos com o menu suspenso de segmentos globais foi realçada.](../images/segments/change-segment.png)

![A caixa de diálogo Selecionar segmento que exibe todos os segmentos disponíveis.](../images/segments/select-segment-dialog.png)

## Widgets e métricas

O painel de segmentos é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre o segmento selecionado.

A data e a hora do instantâneo mais recente são exibidas na parte superior do [!UICONTROL Visão geral] ao lado da lista suspensa do segmento. Todos os dados do widget são precisos a partir dessa data e hora. O carimbo de data e hora do instantâneo é fornecido em UTC; não está no fuso horário do usuário ou da organização individual.

![A guia Visão geral dos segmentos com um carimbo de data e hora de widget destacado.](../images/segments/widget-timestamp.png)

## Widgets padrão {#standard-widgets}

O Adobe fornece vários widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos seus segmentos. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre a criação de widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Tamanho do público-alvo]](#audience-size)
* [[!UICONTROL Ordem de ativação do público-alvo]](#audience-activation-order)
* [[!UICONTROL Tendência do tamanho do público-alvo]](#audience-size-trend)
* [[!UICONTROL Tendência de alteração do tamanho do público-alvo]](#audience-size-change-trend)
* [[!UICONTROL Tendência do tamanho do público-alvo por identidade]](#audience-size-trend-by-identity)
* [[!UICONTROL Sobreposição de público]](#audience-overlap)
* [[!UICONTROL Sobreposição de identidade]](#identity-overlap)
* [[!UICONTROL Perfis por identidade]](#profiles-by-identity)
* [[!UICONTROL Ativações programadas]](#scheduled-activations)

### [!UICONTROL Tamanho do público-alvo] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Tamanho do público-alvo"
>abstract="Este widget exibe o número total de perfis mesclados no segmento selecionado. Esse número depende da política de mesclagem aplicada aos seus dados e está correto no momento do instantâneo mais recente."

O **[!UICONTROL Tamanho do público-alvo]** O widget exibe o número total de perfis mesclados no segmento selecionado no momento em que o instantâneo foi tirado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos seus dados de Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a variável [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

![A visão geral do painel Segmentos com o widget Audience size é realçada.](../images/segments/audience-size.png)

### [!UICONTROL Tendência do tamanho do público-alvo] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendência do tamanho do público-alvo"
>abstract="Este widget fornece informações sobre o número total de perfis que atendem aos critérios de **any** definição de segmento, conforme capturado durante o instantâneo diário, nos últimos 30 dias, 90 dias ou 12 meses."

O **[!UICONTROL Tendência do tamanho do público-alvo]** O widget fornece uma ilustração de gráfico de linhas para o número total de perfis que atendem aos critérios de **any** definição de segmento ao longo de um determinado período. A tendência do tamanho do público-alvo pode ser visualizada em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público-alvo é refletido no eixo y e no tempo no eixo x.

Este widget também inclui o [!UICONTROL Legendas] recurso em que um modelo de aprendizado de máquina analisa o gráfico e os dados do segmento e gera automaticamente legendas para descrever as principais tendências e eventos importantes. Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas.

![A visão geral de Segmentos exibe o widget de tendência do tamanho do público-alvo.](../images/segments/audience-size-trend-captions.png)

A caixa de diálogo de legendas automáticas é aberta, fornecendo insights sobre seus dados.

![A caixa de diálogo de legendas automáticas do widget de tendência do tamanho do público-alvo.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Para saber mais sobre a avaliação de segmentos e como os perfis se qualificam e saem dos segmentos, consulte [Documentação do Serviço de segmentação](../../segmentation/home.md).

### [!UICONTROL Tendência de alteração do tamanho do público-alvo] {#audience-size-change-trend}

Este widget fornece um gráfico de linhas que ilustra a diferença no número total de perfis que se qualificaram para um determinado segmento entre os instantâneos diários mais recentes. O segmento escolhido para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público-alvo é refletido no eixo y e no tempo no eixo x.

![O widget de tendência de alteração de tamanho de público-alvo.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Tendência do tamanho do público-alvo por identidade] {#audience-size-trend-by-identity}

Este widget ilustra a tendência do tamanho do público-alvo para um segmento específico com base no tipo de identidade escolhido no menu suspenso do widget. O segmento usado para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget.

![A tendência do tamanho do público-alvo por widget de identidade.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Ordem de ativação do público-alvo] {#audience-activation-order}

O [!UICONTROL Ordem de ativação do público-alvo] o widget fornece uma tabela de três colunas que lista a variável [!UICONTROL nome do destino], o [!UICONTROL plataforma]e a ativação [!UICONTROL data] do público-alvo. A lista é solicitada de alta para baixa de acordo com a recenticidade e pode acomodar até 10 linhas.

![O widget Ordem de ativação do público-alvo.](../images/segments/audience-activation-order.png)

### [!UICONTROL Sobreposição de público] {#audience-overlap}

Este widget representa o número de perfis de dois segmentos que atendem aos critérios de ambas as definições de segmento. Os segmentos usados para comparação são selecionados nos menus suspensos do widget. O número total de perfis contidos na definição de segmento relevante pode ser visualizado ao passar o cursor do mouse sobre um círculo ou na interseção do diagrama Venn.

Esse widget permite otimizar sua estratégia de segmentação ao visualizar as semelhanças nos resultados das definições de segmento.

![O widget de sobreposição de público-alvo.](../images/segments/audience-overlap.png)

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Sobreposição de identidade"
>abstract="Este widget mostra a sobreposição de perfis em seu segmento que contém ambas as identidades escolhidas. Os círculos exibem o tamanho relativo de cada identidade. O número de perfis que contém ambos os namespaces é representado pela sobreposição entre os círculos."

O **[!UICONTROL Sobreposição de identidade]** O widget exibe um diagrama Venn ou diagrama de conjunto, mostrando a sobreposição de perfis em seu segmento que contém várias identidades.

Use os menus suspensos do widget para selecionar as identidades que deseja comparar. Os círculos exibem o tamanho relativo de cada identidade escolhida, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de uma identidade.

Para saber mais sobre identidades, visite o [Documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![A visão geral do painel Segmentos com o widget Sobreposição de identidade foi realçada.](../images/segments/identity-overlap.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Perfis por identidade"
>abstract="Este widget exibe o detalhamento das identidades em cada perfil mesclado no segmento selecionado."

O **[!UICONTROL Perfis por identidade]** o widget exibe o detalhamento das identidades em cada perfil mesclado no segmento selecionado. O número total de perfis por identidade pode ser maior que o número total de perfis no segmento, pois um perfil pode ter várias identidades associadas a ele. Em outras palavras, adicionar os valores mostrados para cada identidade pode totalizar mais do que o tamanho total do público no segmento, pois se um cliente interagir com sua marca em mais de um canal, várias identidades podem ser associadas a esse cliente individual.

Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas.

![A caixa de diálogo Perfis por legendas de identidade.](../images/segments/profiles-by-identity.png)

Um modelo de aprendizado de máquina gera automaticamente insights de dados ao analisar a distribuição geral e as principais dimensões dos dados.

Para saber mais sobre identidades, visite o [Documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

### Ativações programadas {#scheduled-activations}

O [!UICONTROL Ativações programadas] O widget fornece uma exibição em tabela dos destinos ativados mais recentemente. A tabela inclui a plataforma de destino, o nome do fluxo de ativação para esse destino e a data de início e de término da ativação para o segmento selecionado. Se não houver uma data final fornecida para a ativação, ela será exibida como [!UICONTROL Em curso]. O segmento para análise é selecionado na lista suspensa na parte superior da página.

O widget permite descobrir rapidamente onde e quando o público-alvo está sendo ativado e torna as ativações duplicadas ou desnecessárias mais transparentes. Essas informações acumuladas também destacam onde quaisquer ativações foram deixadas de fora.

![O widget de Ativações programadas.](../images/segments/scheduled-activations.png)

## Próximas etapas

Agora, ao seguir este documento, é possível localizar o painel de segmentos e selecionar um segmento a ser exibido. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).
