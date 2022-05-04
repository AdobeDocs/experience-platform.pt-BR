---
keywords: Experience Platform, perfil, segmento, segmentos, segmentação, interface do usuário, interface do usuário, personalização, painel de segmentos, painel
title: Painel de segmentos
description: 'O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre segmentos criados por sua organização. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: b4cd7bc0d8c038346aacdda7c4c9def12864065c
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# Painel de segmentos {#segment-dashboard}

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmentos na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Serviço de segmentação da Adobe Experience Platform na interface do usuário da plataforma, visite o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).

## Segmentar dados do painel

O painel de segmentos exibe um instantâneo dos dados de atributo (registro) que sua organização tem no armazenamento de Perfil no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmentos não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de segmentos

Para navegar até o [!UICONTROL Segmentos] no painel da interface do usuário da plataforma, selecione **[!UICONTROL Segmentos]** no painel à esquerda, selecione o **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados ativos do Perfil ou políticas de mesclagem criadas, a variável [!UICONTROL Segmentos] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e documentação para ajudar você a começar a usar a segmentação.

![](../images/segments/dashboard-overview.png)

### Modificação do [!UICONTROL Segmentos] painel

Você pode modificar a aparência da variável [!UICONTROL Segmentos] painel selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar o **[!UICONTROL Biblioteca de widgets]** para explorar widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) documentação para saber mais.

## Selecionar um segmento

O painel seleciona automaticamente um segmento para exibição, no entanto, você pode alterar o segmento usando o menu suspenso ou o seletor de segmentos.

Para escolher um segmento diferente, selecione a lista suspensa ao lado do nome do segmento ou use o seletor de segmentos para abrir a caixa de diálogo de seleção de segmentos.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets e métricas

O painel de segmentos é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre o segmento selecionado.

A data e a hora da &quot;última atualização&quot; em um widget mostram quando o último instantâneo dos dados foi tirado. A data e a hora do instantâneo são fornecidas em UTC; não está no fuso horário do usuário individual ou da Organização IMS.

![](../images/segments/widget-timestamp.png)

## Widgets padrão

O Adobe fornece vários widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos seus segmentos. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre a criação de widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Tamanho do público-alvo]](#audience-size)
* [[!UICONTROL Sobreposição de identidade]](#identity-overlap)
* [[!UICONTROL Perfis por identidade]](#profiles-by-identity)
* [[!UICONTROL Ordem de ativação do público-alvo]](#audience-activation-order)
* [[!UICONTROL Tendência do tamanho do público-alvo]](#audience-size-trend)
* [[!UICONTROL Tendência de alteração do tamanho do público-alvo]](#audience-size-change-trend)
* [[!UICONTROL Tendência do tamanho do público-alvo por identidade]](#audience-size-trend-by-identity)

### [!UICONTROL Tamanho do público-alvo] {#audience-size}

O **[!UICONTROL Tamanho do público-alvo]** O widget exibe o número total de perfis mesclados no segmento selecionado no momento em que o instantâneo foi tirado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos seus dados de Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a variável [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

O **[!UICONTROL Sobreposição de identidade]** O widget exibe um diagrama Venn ou diagrama de conjunto, mostrando a sobreposição de perfis em seu segmento que contém várias identidades.

Depois de usar os menus suspensos no widget para selecionar as identidades que deseja comparar, os círculos aparecem exibindo o tamanho relativo de cada identidade, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de uma identidade.

Para saber mais sobre identidades, visite o [Documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

O **[!UICONTROL Perfis por identidade]** O widget exibe o detalhamento das identidades em todos os perfis mesclados no segmento selecionado. O número total de perfis por identidade pode ser maior que o número total de perfis no segmento, pois um perfil pode ter várias identidades associadas a ele. Em outras palavras, adicionar os valores mostrados para cada identidade pode totalizar mais do que o tamanho total do público no segmento, pois se um cliente interagir com sua marca em mais de um canal, várias identidades podem ser associadas a esse cliente individual.

Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas.

![A caixa de diálogo perfis por legendas de identidade.](../images/segments/profiles-by-identity.png)

Um modelo de aprendizado de máquina gera automaticamente insights de dados ao analisar a distribuição geral e as principais dimensões dos dados.

Para saber mais sobre identidades, visite o [Documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Ordem de ativação do público-alvo] {#audience-activation-order}

O [!UICONTROL Ordem de ativação do público-alvo] o widget fornece uma tabela de três colunas que lista a variável [!UICONTROL nome do destino], o [!UICONTROL plataforma]e a ativação [!UICONTROL data] do público-alvo. A lista é solicitada de alta para baixa de acordo com a recenticidade e pode acomodar até 10 linhas.

![O widget Ordem de ativação do público-alvo.](../images/segments/audience-activation-order.png)

### [!UICONTROL Tendência do tamanho do público-alvo] {#audience-size-trend}

O [!UICONTROL Tendência do tamanho do público-alvo] O widget fornece uma ilustração de gráfico de linhas para o número total de perfis que atendem aos critérios de **any** definição de segmento ao longo de um determinado período. A tendência do tamanho do público-alvo pode ser visualizada em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público-alvo é refletido no eixo y e no tempo no eixo x.

![O widget de tendência do tamanho do público-alvo.](../images/segments/audience-size-trend.png)

### [!UICONTROL Tendência de alteração do tamanho do público-alvo] {#audience-size-change-trend}

Este widget fornece um gráfico de linhas que ilustra a diferença no número total de perfis que se qualificaram para um determinado segmento entre os instantâneos diários mais recentes. O segmento escolhido para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. O tamanho do público-alvo é refletido no eixo y e no tempo no eixo x.

![O widget de tendência de alteração de tamanho de público-alvo.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Tendência do tamanho do público-alvo por identidade] {#audience-size-trend-by-identity}

Este widget ilustra a tendência do tamanho do público-alvo para um segmento específico com base no tipo de identidade escolhido no menu suspenso do widget. O segmento usado para análise é selecionado na lista suspensa de visão geral. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget.

![A tendência do tamanho do público-alvo por widget de identidade.](../images/segments/audience-size-trend-by-identity.png)

## Próximas etapas

Agora, ao seguir este documento, é possível localizar o painel de segmentos e selecionar um segmento a ser exibido. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).
