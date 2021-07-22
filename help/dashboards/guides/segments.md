---
keywords: Experience Platform, perfil, segmento, segmentos, segmentação, interface do usuário, interface do usuário, personalização, painel de segmentos, painel
title: Painel de segmentos
description: 'O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre segmentos criados por sua organização. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# Painel de segmentos {#segment-dashboard}

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmentos na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Serviço de segmentação da Adobe Experience Platform na interface do usuário da plataforma, visite o [Guia da interface do usuário do Serviço de segmentação](../../segmentation/ui/overview.md).

## Segmentar dados do painel

O painel de segmentos exibe um instantâneo dos dados de atributo (registro) que sua organização tem no armazenamento de Perfil no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmentos não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de segmentos

Para navegar até o painel [!UICONTROL Segmentos] na interface do usuário da plataforma, selecione **[!UICONTROL Segmentos]** no painel esquerdo e selecione a guia **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados ativos do Perfil ou políticas de mesclagem criadas, o painel [!UICONTROL Segmentos] não estará visível. Em vez disso, a guia [!UICONTROL Visão geral] exibe links e documentação para ajudá-lo a começar a usar a segmentação.

![](../images/segments/dashboard-overview.png)

### Modificar o painel [!UICONTROL Segmentos]

Você pode modificar a aparência do painel [!UICONTROL Segmentos] selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar a **[!UICONTROL biblioteca de widgets]** para explorar os widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a documentação [modificando painéis](../customize/modify.md) e [visão geral da biblioteca de widgets](../customize/widget-library.md) para saber mais.

## Selecionar um segmento

O painel seleciona automaticamente um segmento para exibição, no entanto, você pode alterar o segmento usando o menu suspenso ou o seletor de segmentos.

Para escolher um segmento diferente, selecione o menu suspenso ao lado do nome do segmento ou use o seletor de segmentos para abrir a caixa de diálogo de seleção de segmentos.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets e métricas

O painel de segmentos é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre o segmento selecionado.

A data e a hora da &quot;última atualização&quot; em um widget mostram quando o último instantâneo dos dados foi tirado. A data e a hora do instantâneo são fornecidas em UTC; não está no fuso horário do usuário individual ou da Organização IMS.

![](../images/segments/widget-timestamp.png)

## Widgets padrão

O Adobe fornece vários widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos seus segmentos. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando a [!UICONTROL biblioteca de widgets]. Para saber mais sobre como criar widgets personalizados, comece lendo a [visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Tamanho do público-alvo]](#audience-size)
* [[!UICONTROL Tendência do tamanho do público-alvo]](#audience-size-trend)
* [[!UICONTROL Sobreposição de identidade]](#identity-overlap)
* [[!UICONTROL Perfis por identidade]](#profiles-by-identity)

### [!UICONTROL Tamanho do público-alvo] {#audience-size}

O widget **[!UICONTROL Audience size]** exibe o número total de perfis mesclados no segmento selecionado no momento em que o instantâneo foi tirado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos seus dados de Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Tendência do tamanho do público-alvo] {#audience-size-trend}

O widget **[!UICONTROL Audience size tend]** fornece informações sobre o número total de perfis no segmento conforme capturados durante o instantâneo diário, nos últimos 30 dias, 90 dias ou 12 meses. Este widget exibe como o tamanho do segmento pode ter mudado ao longo do tempo, à medida que novos perfis se qualificam para ou saem do segmento.

Para saber mais sobre a avaliação de segmentos e como os perfis se qualificam e saem dos segmentos, consulte a [documentação do Serviço de segmentação](../../segmentation/home.md).

![](../images/segments/audience-size-trend.png)

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

O widget **[!UICONTROL Sobreposição de identidade]** exibe um diagrama Venn ou um diagrama de conjunto, mostrando a sobreposição de perfis em seu segmento que contém várias identidades.

Depois de usar os menus suspensos no widget para selecionar as identidades que deseja comparar, os círculos aparecem exibindo o tamanho relativo de cada identidade, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de uma identidade.

Para saber mais sobre identidades, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

O widget **[!UICONTROL Perfis por identidade]** exibe o detalhamento das identidades em todos os perfis mesclados no segmento selecionado. O número total de perfis por identidade pode ser maior que o número total de perfis no segmento, pois um perfil pode ter várias identidades associadas a ele. Em outras palavras, adicionar os valores mostrados para cada identidade pode totalizar mais do que o tamanho total do público no segmento, pois se um cliente interagir com sua marca em mais de um canal, várias identidades podem ser associadas a esse cliente individual.

Para saber mais sobre identidades, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/profiles-by-identity.png)

## Próximas etapas

Agora, ao seguir este documento, é possível localizar o painel de segmentos e selecionar um segmento a ser exibido. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md).
