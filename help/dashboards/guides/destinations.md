---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, painel de perfil, painel
title: Painel Destinos
description: O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os destinos ativos da sua organização.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: a920e8aaccb4da6a3aa08f0d420cee0d1944ab9a
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# [!UICONTROL Destinos] painel

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre os destinos ativos de sua organização, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de destinos na interface do usuário e fornece mais informações sobre as métricas exibidas no painel.

Para obter uma visão geral dos destinos, bem como um catálogo de todos os destinos disponíveis no Experience Platform, visite o [documentação de destinos](../../destinations/home.md).

## [!UICONTROL Destinos] dados do painel {#destinations-dashboard-data}

O [!UICONTROL Destinos] O painel exibe um instantâneo dos destinos que sua organização habilitou no Experience Platform. Os dados no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de destinos não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de destinos

Para navegar até o painel de destinos na interface do usuário da plataforma, selecione **[!UICONTROL Destinos]** no painel à esquerda, selecione o **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver destinos ativos, a variável [!UICONTROL Destinos] painel e [!UICONTROL Visão geral] não estão visíveis. Em vez disso, selecione [!UICONTROL Destinos] no menu de navegação esquerdo, o [!UICONTROL Catálogo] guia . Para saber mais sobre o [!UICONTROL Catálogo] consulte a guia [[!UICONTROL Destinos] guia do workspace](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Modificação do painel de destinos

Você pode modificar a aparência do painel de destinos selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar o **[!UICONTROL Biblioteca de widgets]** para explorar widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [visão geral da biblioteca de widgets](../customize/widget-library.md) documentação para saber mais.

## Widgets padrão

O Adobe fornece vários widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos destinos. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre a criação de widgets personalizados, comece lendo o [visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Destinos mais usados]](#most-used-destinations)
* [[!UICONTROL Destinos criados recentemente]](#recently-created-destinations)
* [[!UICONTROL Segmentos ativados recentemente]](#recently-activated-segments)

### [!UICONTROL Destinos mais usados] {#most-used-destinations}

O **[!UICONTROL Destinos mais usados]** O widget exibe os principais destinos de sua organização por número de segmentos mapeados a partir do último instantâneo. Essa classificação fornece informações sobre quais destinos estão sendo utilizados, além de mostrar potencialmente aqueles que podem ser subutilizados.

Por exemplo, se você configurou um destino ontem, mas não mapeou nenhum segmento para ele, seria possível ver que o destino está subutilizado no momento.

O número de segmentos mapeados mostrados na coluna de contagem de segmentos é preciso a partir do último instantâneo diário. Mapear um novo segmento para o destino não atualizará a contagem até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, conforme vinculado da **[!UICONTROL Procurar]** guia . Você também pode selecionar **[!UICONTROL Exibir todos]** para navegar até o **[!UICONTROL Procurar]** e selecione o nome de um destino para exibir seus detalhes.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos criados recentemente] {#recently-created-destinations}

O **[!UICONTROL Destinos criados recentemente]** O widget permite que você veja uma lista dos destinos configurados mais recentemente de sua organização.

A data criada mostrada é precisa do último instantâneo diário. Em outras palavras, se você criar um novo destino, ele não aparecerá na lista até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, conforme vinculado da **[!UICONTROL Procurar]** guia . Você também pode selecionar **[!UICONTROL Exibir todos]** para navegar até o **[!UICONTROL Procurar]** e selecione o nome de um destino para exibir seus detalhes.

Para saber mais sobre como configurar tipos específicos de destinos, visite o [documentação de destinos](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmentos ativados recentemente] {#recently-activated-segments}

O **[!UICONTROL Segmentos ativados recentemente]** fornece uma lista dos segmentos mapeados mais recentemente para um destino. Esta lista fornece um instantâneo de quais segmentos e destinos estão sendo usados ativamente no sistema e pode ajudar na solução de problemas de mapeamentos incorretos.

A data atualizada mostrada exibe a última vez que o segmento foi ativado para o destino e é precisa do último instantâneo diário. Em outras palavras, se você ativar um segmento para o destino, a data atualizada não será alterada até que o próximo instantâneo seja tirado.

Selecionar o nome de um segmento na lista mostrada no widget leva você aos detalhes do segmento. Você também pode selecionar **[!UICONTROL Exibir todos]** para navegar até a guia navegador do segmento e, em seguida, selecionar o nome de um segmento para exibir seus detalhes.

Para obter mais informações sobre como trabalhar com segmentos no Experience Platform, comece lendo o [Visão geral do serviço de segmentação](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Próximas etapas

Ao seguir este documento, você agora deve ser capaz de localizar o painel de destinos e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com destinos no Experience Platform, consulte o [documentação de destinos](../../destinations/home.md).
