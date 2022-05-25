---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, painel de perfil, painel
title: Painel Destinos
description: O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os destinos ativos da sua organização.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 2fdcd0748ccfe5b6b079bc21c8dbde491fbb2471
workflow-type: tm+mt
source-wordcount: '2671'
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

Consulte a [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) documentação para saber mais.

## Widgets padrão

O Adobe fornece vários widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos destinos e avaliar a integridade dos segmentos disponíveis para a análise de dados. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre a criação de widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Destinos mais usados]](#most-used-destinations)
* [[!UICONTROL Destinos criados recentemente]](#recently-created-destinations)
* [[!UICONTROL Segmentos ativados recentemente]](#recently-activated-segments)
* [[!UICONTROL Segmentos ativados recentemente por destino]](#recently-activated-segments-by-destination)
* [[!UICONTROL Tendência do tamanho do público-alvo]](#audience-size-trend)
* [[!UICONTROL Segmentos não mapeados por identidade]](#unmapped-segments-by-identity)
* [[!UICONTROL Segmentos mapeados por identidade]](#mapped-segments-by-identity)
* [[!UICONTROL Públicos-alvo comuns]](#common-audiences)
* [[!UICONTROL Estado de funcionamento do público-alvo mapeado]](#mapped-audience-health)
* [[!UICONTROL Contagem de destinos]](#destinations-count)
* [[!UICONTROL Status do destino]](#destination-status)
* [[!UICONTROL Destinos ativos por plataforma de destino]](#active-destinations-by-destination-platform)
* [[!UICONTROL Públicos-alvo ativados em todos os destinos]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Públicos-alvo ativados]](#activated-audiences)

### [!UICONTROL Destinos mais usados] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Destinos mais usados"
>abstract="Esse widget exibe os destinos mais ativos de sua organização pelo número de segmentos mapeados. Esses números são precisos no momento do último instantâneo. Essa classificação fornece informações sobre quais destinos são mais usados atualmente, destacando os que podem ser subutilizados."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#most-used-destinations" text="Saiba mais pela documentação"

O **[!UICONTROL Destinos mais usados]** O widget exibe os principais destinos de sua organização pelo número de segmentos mapeados a partir do último instantâneo. Essa classificação fornece informações sobre quais destinos estão sendo utilizados, além de mostrar potencialmente aqueles que podem ser subutilizados.

Por exemplo, se você configurou um destino ontem, mas não mapeou nenhum segmento para ele, seria possível ver que o destino está subutilizado no momento.

O número de segmentos mapeados mostrados na coluna de contagem de segmentos é preciso a partir do último instantâneo diário. Mapear um novo segmento para o destino não atualizará a contagem até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, conforme vinculado da **[!UICONTROL Procurar]** guia . Você também pode selecionar **[!UICONTROL Exibir todos]** para navegar até o **[!UICONTROL Procurar]** e selecione o nome de um destino para exibir seus detalhes.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos criados recentemente] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Destinos criados recentemente"
>abstract="Este widget exibe uma lista dos destinos configurados mais recentemente em sua organização."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#recently-created-destinations" text="Saiba mais pela documentação"

O **[!UICONTROL Destinos criados recentemente]** O widget permite que você veja uma lista dos destinos configurados mais recentemente de sua organização.

A data criada mostrada é precisa do último instantâneo diário. Em outras palavras, se você criar um novo destino, ele não aparecerá na lista até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, conforme vinculado da **[!UICONTROL Procurar]** guia . Você também pode selecionar **[!UICONTROL Exibir todos]** para navegar até o **[!UICONTROL Procurar]** e selecione o nome de um destino para exibir seus detalhes.

Para saber mais sobre como configurar tipos específicos de destinos, visite o [documentação de destinos](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmentos ativados recentemente] {#recently-activated-segments}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Segmentos ativados recentemente"
>abstract="Este widget fornece uma lista dos segmentos mapeados mais recentemente para um destino. Esta lista fornece um instantâneo dos segmentos e destinos que estão sendo usados ativamente no sistema e pode ajudar na solução de problemas de mapeamentos incorretos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#recently-activated-segments" text="Saiba mais pela documentação"

O **[!UICONTROL Segmentos ativados recentemente]** fornece uma lista dos segmentos mapeados mais recentemente para um destino. Esta lista fornece um instantâneo dos segmentos e destinos que estão sendo usados ativamente no sistema e pode ajudar na solução de problemas de mapeamentos incorretos.

A data atualizada mostrada exibe a última vez que o segmento foi ativado para o destino e é precisa do último instantâneo diário. Em outras palavras, se você ativar um segmento para o destino, a data atualizada não será alterada até que o próximo instantâneo seja tirado.

Selecionar o nome de um segmento na lista mostrada no widget leva você aos detalhes do segmento. Você também pode selecionar **[!UICONTROL Exibir todos]** para navegar até a guia navegador do segmento e, em seguida, selecionar o nome de um segmento para exibir seus detalhes.

Para obter mais informações sobre como trabalhar com segmentos no Experience Platform, comece lendo o [Visão geral do serviço de segmentação](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

### [!UICONTROL Segmentos ativados recentemente por destino] {#recently-activated-segments-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Segmentos ativados recentemente por destino"
>abstract="Esse widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente de acordo com o destino escolhido na lista suspensa de visão geral."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#recently-activated-segments-by-destination" text="Saiba mais pela documentação"

O **[!UICONTROL Segmentos ativados recentemente por destino]** O widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente de acordo com o destino escolhido na lista suspensa de visão geral. É semelhante ao [!UICONTROL Segmentos ativados recentemente] widget, mas os dados são exibidos **only** se aplica ao destino selecionado.

Este widget contém duas métricas: o nome do segmento e a data em que ele foi ativado pela última vez no destino. Os dados exibidos estão corretos a partir do último instantâneo diário.

Você pode visualizar os detalhes de um segmento selecionando o nome de um segmento na lista exibida.

![Segmentos ativados recentemente pelo widget de destino.](../images/destinations/recently-activated-segments-by-destination.png)

### [!UICONTROL Tendência do tamanho do público-alvo] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Tendência do tamanho do público-alvo"
>abstract="Este widget ilustra o número de perfis contidos no segmento, que está sendo enviado para a conta de destino diariamente. O primeiro menu suspenso ajusta o período de tempo da tendência do público-alvo. O segundo menu suspenso do widget seleciona o segmento para análise. O destino é escolhido na lista suspensa de visão geral."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#audience-size-trend" text="Saiba mais pela documentação"

O **[!UICONTROL Tendência do tamanho do público-alvo]** O widget descreve o relacionamento da contagem de perfis ao longo de um período de tempo para um segmento que foi mapeado para essa conta de destino. O widget usa um gráfico de linhas para ilustrar o número de perfis contidos no segmento, que estão sendo enviados para a conta de destino diariamente.

Um período para a tendência do público-alvo nos últimos 30 dias, 90 dias ou 12 meses pode ser ajustado usando o primeiro menu suspenso.

O segundo menu suspenso lista todos os segmentos disponíveis que podem ser enviados para a conta de destino escolhida na parte superior do painel.

![O widget de tendência do tamanho do público-alvo.](../images/destinations/audience-size-trend.png)

O **[!UICONTROL Tendência do tamanho do público-alvo]** o widget fornece um [!UICONTROL Legendas] na parte superior direita do widget. Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas. Um modelo de aprendizado de máquina gera automaticamente legendas para descrever as principais tendências e eventos importantes ao analisar o gráfico e os dados do segmento.

![A caixa de diálogo de legendas automáticas do widget de tendência do tamanho do público-alvo.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Segmentos não mapeados por identidade] {#unmapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Segmentos não mapeados por identidade"
>abstract="Este widget lista as cinco principais **não mapeado** segmentos classificados por contagem de identidade decrescente para um determinado destino e identidade. As IDs de filtro listadas na lista suspensa do widget mudam, dependendo da conta de destino selecionada na parte superior da página de visão geral."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#unmapped-segments-by-identity" text="Saiba mais pela documentação"

O **[!UICONTROL Segmentos não mapeados por identidade]** o widget lista os cinco principais **não mapeado** segmentos classificados por contagem de identidade decrescente para um determinado destino e identidade. Ele destaca os segmentos que são os mais benéficos para mapear para a conta de destino escolhida com base na ID escolhida.

A lista suspensa da ID de destino filtra os segmentos disponíveis. As IDs de filtro listadas na lista suspensa mudam, dependendo da conta de destino selecionada na parte superior da página de visão geral.

A coluna identidades conta o número de IDs de origem no segmento que podem ser mapeadas para a ID escolhida na lista suspensa ID de widget.

![Os segmentos não mapeados pelo widget de identidade.](../images/destinations/unmapped-segments-by-identity.png)

### [!UICONTROL Segmentos mapeados por identidade] {#mapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Segmentos mapeados por identidade"
>abstract="Este widget fornece uma lista das cinco principais **mapeado** segmentos. A lista é ordenada de alto a baixo de acordo com o número de IDs de origem contidas nos segmentos. A ID de destino a ser contada é selecionada no menu suspenso abaixo do título do widget. As IDs de destino disponíveis no menu suspenso do widget dependem do destino escolhido na parte superior do painel de visão geral."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#mapped-segments-by-identity" text="Saiba mais pela documentação"

Este widget fornece uma lista das cinco principais **mapeado** segmentos. A lista é ordenada de alto a baixo de acordo com o número de IDs de origem contidas nos segmentos. A ID de destino a ser contada é selecionada no menu suspenso abaixo do título do widget. As IDs de destino disponíveis no menu suspenso no widget serão alteradas de acordo com o filtro de conta de destino escolhido na parte superior do painel de visão geral.

![Os segmentos mapeados por widget de identidade.](../images/destinations/mapped-segments-by-identity.png)

O **[!UICONTROL Segmentos mapeados por identidade]** O widget destaca rapidamente a probabilidade de direcionar oportunidades de perfil com êxito para uma campanha dentro do destino escolhido. Uma campanha direcionada eficiente não depende do número de perfis enviados para o destino, mas sim do número de IDs de origem que provavelmente serão correspondidas com as IDs de destino para fornecer dados úteis e acionáveis.

### Públicos-alvo comuns {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Públicos-alvo comuns"
>abstract="Este widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget. A lista de segmentos é ordenada de acordo com a recentemente com que foram ativados. O segmento ativado mais recentemente é exibido na parte superior."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#common-audiences" text="Saiba mais pela documentação"

O **[!UICONTROL Públicos-alvo comuns]** O widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget. A lista de segmentos é ordenada de acordo com a recentemente com que foram ativados. O segmento ativado mais recentemente é exibido na parte superior.

O [!UICONTROL TAMANHO DO PÚBLICO-ALVO] fornece a contagem total de perfis de cada segmento listado.

![O widget Públicos-alvo comuns .](../images/destinations/common-audiences.png)

### Estado de funcionamento do público-alvo mapeado {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Estado de funcionamento do público-alvo mapeado"
>abstract="Este widget fornece uma lista de até 20 segmentos mapeados cujas contagens totais de perfil se desviam por um fator de pelo menos um desvio padrão do tamanho médio de público-alvo de 30 dias mapeado para esse destino. Ela fornece uma métrica calculada para a dispersão dos tamanhos do público-alvo da média nos últimos 30 dias. Os tamanhos do público são classificados de alto para baixo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#mapped-audience-health" text="Saiba mais pela documentação"

O widget fornece uma lista de até 20 segmentos mapeados cujo perfil total, a partir do último instantâneo diário, varia por um fator de pelo menos um desvio padrão do tamanho médio de público-alvo de 30 dias mapeado para esse destino.

Resumindo, ela fornece uma métrica calculada para a dispersão dos tamanhos do público-alvo da média nos últimos 30 dias. Ele compara se o tamanho do público-alvo atual está fora do desvio padrão histórico visto nos dados dos últimos 30 dias.

Todos os tamanhos de público-alvo no sistema são classificados de tamanho de público alto a baixo, conforme indicado na [!UICONTROL TAMANHO MAIS RECENTE] coluna.

Se a contagem de perfil mapeada do segmento estiver fora de um desvio padrão do tamanho médio do perfil mapeado nos últimos 30 dias, isso indica uma anomalia no sistema e deve ser investigado.

Se um segmento na [!UICONTROL Estado de funcionamento do público-alvo mapeado] Se o widget estiver se desviando por uma grande margem, você deve consultar o gráfico de tendência do tamanho do público-alvo e localizar o segmento anômalo. A tendência pode fornecer mais informações sobre a integridade do seu segmento.

![O widget de integridade do público-alvo mapeado.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Contagem de destinos] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Contagem de destinos"
>abstract="Este widget fornece o número total de endpoints disponíveis, onde um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#destinations-count" text="Saiba mais pela documentação"

O [!UICONTROL Contagem de destinos] O widget fornece o número total de endpoints disponíveis, onde um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos.

Abaixo da contagem total, selecione **[!UICONTROL Destinos]** para navegar até a guia destinos browse . Esta página lista todos os destinos com os quais você estabeleceu uma conexão até o momento.

![O widget Destinos conta.](../images/destinations/destinations-count.png)

### [!UICONTROL Status do destino] {#destination-status}

O [!UICONTROL Status do destino] O widget exibe o número total de destinos ativados como uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre destinos ativados e desativados.

As contagens individuais para destinos ativados ou desativados são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![O widget Status do Destino.](../images/destinations/destination-status.png)

### [!UICONTROL Destinos ativos por plataforma de destino] {#active-destinations-by-destination-platform}

O widget fornece uma tabela de duas colunas para mostrar uma lista de plataformas de destino ativas e o número total de destinos ativos para cada plataforma de destino. A lista de plataformas de destino é ordenada de cima para baixo.

![O widget Destinos ativos por plataforma de destino.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Públicos-alvo ativados em todos os destinos] {#activated-audiences-across-all-destinations}

O [!UICONTROL Públicos-alvo ativados em todos os destinos] O widget fornece o número total de públicos-alvo ativados em todos os destinos em uma única métrica. Esse número é preciso para o instantâneo mais recente.

![O widget Públicos-alvo ativados em todos os destinos.](../images/destinations/activated-audiences-across-all-destinations.png)

Selecionar **[!UICONTROL Públicos-alvo]** para navegar até os destinos [!UICONTROL Procurar] guia . Esta página fornece uma lista de todos os destinos ativados e uma variedade de métricas relevantes. Consulte a documentação para [mais informações sobre o [!UICONTROL Procurar] guia](../../destinations/ui/destinations-workspace.md#browse).

### [!UICONTROL Públicos-alvo ativados] {#activated-audiences}

Este widget fornece uma única métrica para o número total de públicos-alvo ativados em um destino.

![O widget Públicos-alvo ativados .](../images/destinations/activated-audiences.png)

Selecionar **[!UICONTROL Públicos-alvo]** para navegar até a página de detalhes do painel de destinos. O [!UICONTROL Dados de ativação] exibe uma lista de segmentos que foram mapeados para o destino, incluindo a data de início e a data de término (se aplicável) e outras informações relevantes para a exportação de dados, como tipo de exportação, programação e frequência. Para exibir os detalhes sobre um segmento específico, selecione o nome na lista.

![A página de detalhes do painel de destinos com a guia Ativation data realçada.](../images/destinations/activation-data-tab.png)

Este widget ajuda você a entender o valor dos destinos com base no número de públicos-alvo ativados imediatamente. Também fornece acesso fácil a informações mais detalhadas para análises mais detalhadas.

## Próximas etapas

Ao seguir este documento, você agora deve ser capaz de localizar o painel de destinos e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com destinos no Experience Platform, consulte o [documentação de destinos](../../destinations/home.md).
