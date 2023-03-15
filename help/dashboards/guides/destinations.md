---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;interface do usuário;UI;personalização;painel de perfis;painel;profile;profile dashboard
title: Guia do Painel de destinos
description: A Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre os destinos ativos da sua organização.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: d9e10271db52f61cdc3e4adc546fe05adadb5a46
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 0%

---

# [!UICONTROL Destinos] painel

A interface do usuário (UI) do Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre os destinos ativos da sua organização, conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de destinos na interface do usuário e fornece mais informações sobre as métricas exibidas no painel.

Para obter uma visão geral dos destinos, bem como um catálogo de todos os destinos disponíveis no Experience Platform, visite o [documentação de destinos](../../destinations/home.md).

## [!UICONTROL Destinos] dados do painel {#destinations-dashboard-data}

O painel Destinos exibe um instantâneo dos destinos que sua organização ativou no Experience Platform. Os dados no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de destinos não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o [!UICONTROL Destinos] painel {#explore}

Para navegar até o painel de destinos na interface do Platform, selecione **[!UICONTROL Destinos]** no painel à esquerda, selecione a variável **[!UICONTROL Visão geral]** para exibir o painel.

A data e a hora do snapshot mais recente são exibidas na parte superior do [!UICONTROL Visão geral] ao lado da lista suspensa de destino. Todos os dados do widget são precisos a partir dessa data e hora. O carimbo de data e hora do instantâneo é fornecido em UTC; ele não está no fuso horário do usuário ou organização individual.

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver destinos ativos, o painel Destinos e [!UICONTROL Visão geral] não estão visíveis. Em vez disso, selecione [!UICONTROL Destinos] no painel de navegação esquerdo, exibe a [!UICONTROL Catálogo] guia. Para saber mais sobre o [!UICONTROL Catálogo] consulte a guia [[!UICONTROL Destinos] guia do espaço de trabalho](../../destinations/ui/destinations-workspace.md).

![A Visão geral dos destinos da interface do usuário do Platform com o instantâneo mais recente realçado.](../images/destinations/snapshot-timestamp.png)

### Modifique o [!UICONTROL Destinos] painel {#modify}

Selecionar **[!UICONTROL Modificar painel]** para alterar a aparência do painel de destinos. Isso permite mover, adicionar e remover widgets do painel, bem como acessar a biblioteca de widgets. Na biblioteca de widgets, você pode explorar os widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [visão geral da biblioteca de widgets](../customize/widget-library.md) para saber mais.

### Adicionar widgets {#add-widget}

Selecionar **[!UICONTROL Adicionar widget]** para navegar até a biblioteca de widgets e ver uma lista dos widgets disponíveis para adicionar ao painel.

![A visão geral do painel Destinos com o widget Adicionar é realçada.](../images/destinations/destinations-overview-add-widget.png)

Na biblioteca de widgets, você pode navegar pela seleção de widgets de segmentos padrão e personalizados. Para obter informações sobre como adicionar widgets, consulte a documentação da biblioteca de widgets sobre como [adicionar um widget](../customize/widget-library.md#add-widgets).

## Widgets padrão {#standard-widgets}

O Adobe fornece vários widgets padrão que você pode usar para visualizar métricas diferentes relacionadas aos seus destinos e avaliar a integridade dos segmentos disponíveis para sua análise de dados. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre como criar widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

### Pré-requisitos {#prerequisites}

Antes de continuar com as descrições dos widgets padrão, verifique se você está familiarizado com as definições dos seguintes termos principais usados na documentação:

* **Segmento:** Um segmento é **o conjunto de regras** que incluem atributos e dados de evento que qualificam vários perfis como um público-alvo.
* **Público**: um público-alvo é **o conjunto de perfis** que atendem aos critérios de uma definição de segmento.
* **Mapeado/Mapeamento**: o mapeamento de dados é o processo de mapear campos de dados de origem para campos de destino relacionados em um destino.
* **Identidade**: uma identidade é um identificador que representa exclusivamente um cliente individual, como uma ID de cookie, ID de dispositivo ou ID de email.
* **Ativar**: Ativar é a ação realizada por um usuário para mapear um segmento ou perfis para um destino, como o Oracle Eloqua, Google ou Marketing Cloud do Salesforce.

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na lista a seguir:

* [[!UICONTROL Destinos mais usados]](#most-used-destinations)
* [[!UICONTROL Destinos criados recentemente]](#recently-created-destinations)
* [[!UICONTROL Segmentos ativados recentemente]](#recently-activated-segments)
* [[!UICONTROL Segmentos ativados recentemente por destino]](#recently-activated-segments-by-destination)
* [[!UICONTROL Tendência de tamanho do público]](#audience-size-trend)
* [[!UICONTROL Segmentos não mapeados por identidade]](#unmapped-segments-by-identity)
* [[!UICONTROL Segmentos mapeados por identidade]](#mapped-segments-by-identity)
* [[!UICONTROL Públicos comuns]](#common-audiences)
* [[!UICONTROL Públicos mapeados]](#mapped-audiences)
* [[!UICONTROL Integridade do público mapeado]](#mapped-audience-health)
* [[!UICONTROL Contagem de destinos]](#destinations-count)
* [[!UICONTROL Status do destino]](#destination-status)
* [[!UICONTROL Destinos ativos por plataforma de destino]](#active-destinations-by-destination-platform)
* [[!UICONTROL Públicos ativados em todos os destinos]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Públicos ativados]](#activated-audiences)

### [!UICONTROL Destinos mais usados] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Destinos mais usados"
>abstract="Este widget exibe os destinos mais ativos da sua organização pelo número de segmentos mapeados. Esses números são precisos no momento do último instantâneo. Essa classificação fornece informações sobre quais destinos são mais usados no momento, destacando os que podem ser subutilizados."

A variável **[!UICONTROL Destinos mais usados]** O widget exibe os principais destinos da sua organização pelo número de segmentos mapeados, a partir do último instantâneo. Essa classificação fornece insight sobre quais destinos estão sendo utilizados, além de mostrar os que podem estar subutilizados.

Por exemplo, se você configurou um destino ontem, mas não mapeou nenhum segmento para ele, é possível ver que o destino está subutilizado no momento.

O número de segmentos mapeados exibido na coluna de contagem de segmentos é preciso desde o último instantâneo diário. Mapear um novo segmento para o destino não atualizará a contagem até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, como vinculado a partir do **[!UICONTROL Procurar]** guia. Também é possível selecionar **[!UICONTROL Exibir todos]** para navegar até o **[!UICONTROL Procurar]** e selecione o nome de um destino para exibir seus detalhes.

![A guia Visão geral do painel Destinos com o widget Destinos mais usados é realçada.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos criados recentemente] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Destinos criados recentemente"
>abstract="Esse widget exibe uma lista dos destinos configurados mais recentemente na sua organização."

A variável **[!UICONTROL Destinos criados recentemente]** O widget permite visualizar uma lista dos destinos configurados mais recentemente pela sua organização.

A data de criação mostrada é precisa para o último instantâneo diário. Em outras palavras, se você criar um novo destino, ele não aparecerá na lista até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget levará você aos detalhes do destino, como vinculado a partir do **[!UICONTROL Procurar]** guia. Também é possível selecionar **[!UICONTROL Exibir todos]** para navegar até o **[!UICONTROL Procurar]** e selecione o nome de um destino para exibir seus detalhes.

Para saber mais sobre como configurar tipos específicos de destinos, visite o [documentação de destinos](../../destinations/home.md).

![A guia Visão geral do painel Destinos com o widget Destinos criados recentemente destacado.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmentos ativados recentemente] {#recently-activated-segments}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Segmentos ativados recentemente"
>abstract="Este widget fornece uma lista dos segmentos mapeados mais recentemente para um destino. Esta lista fornece um instantâneo dos segmentos e destinos que estão ativamente em uso no sistema e pode ajudar a solucionar problemas de mapeamentos incorretos."

A variável **[!UICONTROL Segmentos ativados recentemente]** O widget fornece uma lista dos segmentos mapeados mais recentemente para um destino. Esta lista fornece um instantâneo dos segmentos e destinos que estão ativamente em uso no sistema e pode ajudar a solucionar problemas de mapeamentos incorretos.

A data atualizada mostrada exibe a última vez que o segmento foi ativado para o destino e é precisa para o último instantâneo diário. Em outras palavras, se você ativar um segmento para o destino, a data atualizada não será alterada até que o próximo instantâneo seja tirado.

Selecionar o nome de um segmento na lista mostrada no widget levará você aos detalhes do segmento. Também é possível selecionar **[!UICONTROL Exibir todos]** para navegar até a guia navegação de segmento e, em seguida, selecione o nome de um segmento para exibir seus detalhes.

Para obter mais informações sobre como trabalhar com segmentos no Experience Platform, consulte o [Visão geral do serviço de segmentação](../../segmentation/home.md).

![A guia Visão geral do painel Destinos com o widget Segmentos ativados recentemente realçado.](../images/destinations/recently-activated-segments.png)

### [!UICONTROL Segmentos ativados recentemente por destino] {#recently-activated-segments-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Segmentos ativados recentemente por destino"
>abstract="Este widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente, de acordo com o destino escolhido na lista suspensa visão geral."

A variável **[!UICONTROL Segmentos ativados recentemente por destino]** O widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente de acordo com o destino escolhido na lista suspensa visão geral. É semelhante ao [!UICONTROL Segmentos ativados recentemente] mas os dados exibidos **somente** se aplica ao destino selecionado.

Este widget contém duas métricas: o nome do segmento e a data em que o segmento foi ativado pela última vez no destino. Os dados exibidos estão corretos desde o último instantâneo diário.

Você pode visualizar os detalhes de um segmento selecionando o nome de um segmento na lista mostrada.

![O widget Segmentos ativados recentemente por destino.](../images/destinations/recently-activated-segments-by-destination.png)

Consulte a seção de pré-requisitos para [definições de termos usados](#prerequisites) nesta descrição.

### [!UICONTROL Tendência de tamanho do público] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Tendência de tamanho do público"
>abstract="Este widget ilustra o número de perfis contidos no segmento, que está sendo enviado para a conta de destino diariamente. O primeiro menu suspenso ajusta o período da tendência de público-alvo. O segundo menu suspenso do widget seleciona o segmento para análise. O destino é escolhido na lista suspensa de visão geral."

A variável **[!UICONTROL Tendência de tamanho do público]** O widget representa a relação da contagem de perfis durante um período de tempo para um segmento que foi mapeado para essa conta de destino. O widget usa um gráfico de linhas para ilustrar o número de perfis contidos no segmento, que estão sendo enviados para a conta de destino diariamente.

Um período para a tendência do público-alvo nos últimos 30 dias, 90 dias ou 12 meses pode ser ajustado usando o primeiro menu suspenso.

O segundo menu suspenso lista cada segmento disponível que pode ser enviado para a conta de destino escolhida na parte superior do painel.

![O widget Tendência de tamanho do público-alvo.](../images/destinations/audience-size-trend.png)

A variável **[!UICONTROL Tendência de tamanho do público]** o widget fornece um [!UICONTROL Legendas] no canto superior direito do widget. Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo legendas automáticas. Um modelo de aprendizado de máquina gera legendas automaticamente para descrever as principais tendências e eventos importantes, analisando o gráfico e os dados de segmento.

![A caixa de diálogo de legendas automáticas do widget de tendência de tamanho de Público-alvo.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Segmentos não mapeados por identidade] {#unmapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Segmentos não mapeados por identidade"
>abstract="Este widget lista os cinco principais **não mapeado** segmentos classificados por contagem decrescente de identidades para um determinado destino e identidade. As IDs de filtro listadas na lista suspensa do widget mudam, dependendo da conta de destino selecionada na parte superior da página de visão geral."

A variável **[!UICONTROL Segmentos não mapeados por identidade]** o widget lista os cinco principais **não mapeado** segmentos classificados por contagem decrescente de identidades para um determinado destino e identidade. Ele destaca os segmentos que são os mais benéficos a serem mapeados para a conta de destino escolhida com base na ID escolhida.

A lista suspensa ID de destino filtra os segmentos disponíveis. As IDs de filtro listadas na lista suspensa mudam, dependendo da conta de destino selecionada na parte superior da página de visão geral.

A coluna de identidades conta o número de IDs de origem no segmento que podem mapear para a ID escolhida na lista suspensa de ID do widget.

![O widget Segmentos não mapeados por identidade.](../images/destinations/unmapped-segments-by-identity.png)

Consulte a seção de pré-requisitos para [definições de termos usados](#prerequisites) nesta descrição.

### [!UICONTROL Segmentos mapeados por identidade] {#mapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Segmentos mapeados por identidade"
>abstract="Este widget fornece uma lista dos cinco principais **mapeado** segmentos. A lista é ordenada de cima para baixo de acordo com o número de IDs de origem contidas nos segmentos. A ID de destino a ser contada é selecionada no menu suspenso abaixo do título do widget. As IDs de destino disponíveis no menu suspenso do widget dependem do destino escolhido na parte superior do painel de visão geral."

Este widget fornece uma lista dos cinco principais **mapeado** segmentos. A lista é ordenada de cima para baixo de acordo com o número de IDs de origem contidas nos segmentos. A ID de destino a ser contada é selecionada no menu suspenso abaixo do título do widget. As IDs de destino disponíveis no menu suspenso do widget serão alteradas de acordo com o filtro de conta de destino escolhido na parte superior do painel de visão geral.

![O widget Segmentos mapeados por identidade.](../images/destinations/mapped-segments-by-identity.png)

A variável **[!UICONTROL Segmentos mapeados por identidade]** principais características do widget, a probabilidade de direcionar com sucesso as oportunidades de perfil para uma campanha no destino escolhido. Uma campanha direcionada eficiente não depende do número de perfis enviados para o destino, mas sim do número de IDs de origem que provavelmente serão correspondidas às IDs de destino para fornecer dados úteis e acionáveis.

### Públicos comuns {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Públicos comuns"
>abstract="Este widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget. A lista de segmentos é ordenada de acordo com a recente ativação. O segmento ativado mais recentemente é exibido na parte superior."

A variável **[!UICONTROL Públicos comuns]** O widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa widget. A lista de segmentos é ordenada de acordo com a recente ativação. O segmento ativado mais recentemente é exibido na parte superior.

A variável [!UICONTROL TAMANHO DO PÚBLICO] fornece a contagem total de perfis de cada segmento listado.

![O widget Públicos-alvo comuns.](../images/destinations/common-audiences.png)

### Públicos mapeados {#mapped-audiences}

A variável [!UICONTROL Públicos mapeados] O widget exibe o número total de públicos mapeados que podem ser ativados para o destino selecionado na parte superior da página.

Selecionar **[!UICONTROL Segmentos]** para navegar até o painel Segmentos [!UICONTROL Procurar] guia. Este espaço de trabalho exibe uma lista de todas as definições de segmento para sua organização.

![O widget Públicos mapeados.](../images/destinations/mapped-audiences.png)

### Integridade do público mapeado {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Integridade do público mapeado"
>abstract="Este widget fornece uma lista de até 20 segmentos mapeados cujas contagens totais de perfis se desviam por um fator de pelo menos um desvio padrão do tamanho médio do público-alvo de 30 dias mapeado para esse destino. Ela fornece uma métrica calculada para a dispersão dos tamanhos de público-alvo em relação à média nos últimos 30 dias. Os tamanhos dos públicos-alvo são classificados de alto a baixo."

O widget fornece uma lista de até 20 segmentos mapeados cujas contagens totais de perfil, desde o último instantâneo diário, desviam-se por um fator de pelo menos um desvio padrão do tamanho médio do público-alvo de 30 dias mapeado para esse destino.

Em resumo, fornece uma métrica calculada para a dispersão dos tamanhos de público-alvo da média nos últimos 30 dias. Ela compara se o tamanho do público-alvo de hoje está fora do desvio padrão histórico visto nos dados nos últimos 30 dias.

Todos os tamanhos de público no sistema são classificados de alto a baixo, conforme indicado na [!UICONTROL TAMANHO MAIS RECENTE] coluna.

Se a contagem de perfis mapeados do segmento estiver fora de um desvio padrão do tamanho médio do perfil mapeado nos últimos 30 dias, isso indica uma anomalia no sistema e deve ser investigado.

Se um segmento dentro do [!UICONTROL Integridade do público mapeado] O widget está se desviando por uma grande margem. Você deve consultar o gráfico de tendência de tamanho de público e localizar o segmento anômalo. A tendência pode fornecer mais informações sobre a saúde do seu segmento.

>[!NOTE]
>
>O tamanho padrão do widget de integridade Público-alvo mapeado pode obstruir as informações da tabela. Modifique o tamanho do widget para melhorar a legibilidade dos nomes de segmento e títulos de coluna mapeados. Consulte a documentação de modificação de painéis para obter orientação sobre [como redimensionar um widget](../customize/modify.md).

![O widget de integridade Público-alvo mapeado.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Contagem de destinos] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Contagem de destinos"
>abstract="Este widget fornece o número total de endpoints disponíveis nos quais um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos."

A variável [!UICONTROL Contagem de destinos] O widget fornece o número total de endpoints disponíveis nos quais um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos.

Abaixo da contagem total, selecione **[!UICONTROL Destinos]** para navegar até a guia navegação de destinos. Esta página lista todos os destinos com os quais você estabeleceu uma conexão até o momento.

![O widget Contagem de destinos.](../images/destinations/destinations-count.png)

### [!UICONTROL Status do destino] {#destination-status}

A variável [!UICONTROL Status do destino] O widget exibe o número total de destinos ativados como uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre destinos ativados e desativados.

As contagens individuais para destinos habilitados ou desabilitados são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![O widget Status de destino.](../images/destinations/destination-status.png)

### [!UICONTROL Destinos ativos por plataforma de destino] {#active-destinations-by-destination-platform}

O widget fornece uma tabela de duas colunas para mostrar uma lista de plataformas de destino ativas e o número total de destinos ativos para cada plataforma de destino. A lista de plataformas de destino é ordenada de cima para baixo.

![O widget Plataforma Ativa de destinos por destino.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Públicos ativados em todos os destinos] {#activated-audiences-across-all-destinations}

A variável [!UICONTROL Públicos ativados em todos os destinos] O widget fornece o número total de públicos ativados em todos os destinos em uma única métrica.

>[!NOTE]
>
>Este widget mostra a contagem de públicos-alvo, e não a contagem de segmentos.

Esse número é preciso para o instantâneo mais recente.

![O widget Públicos ativados em todos os destinos.](../images/destinations/activated-audiences-across-all-destinations.png)

Selecionar **[!UICONTROL Públicos-alvo]** para navegar até os destinos [!UICONTROL Procurar] guia. Esta página fornece uma lista de todos os destinos ativados e diversas métricas relevantes. Consulte a documentação para obter mais informações sobre o [[!UICONTROL Procurar] guia](../../destinations/ui/destinations-workspace.md#browse).

Consulte a seção de pré-requisitos para [definições de termos usados](#prerequisites) nesta descrição.

### [!UICONTROL Públicos ativados] {#activated-audiences}

Esse widget fornece uma única métrica para o número total de públicos-alvo ativados para um destino.

![O widget Públicos ativados.](../images/destinations/activated-audiences.png)

Selecionar **[!UICONTROL Públicos-alvo]** para navegar até a página de detalhes do painel de destinos. A variável [!UICONTROL Dados de ativação] A guia exibe uma lista de segmentos que foram mapeados para o destino, incluindo a data inicial e a data final (se aplicável) e outras informações relevantes para a exportação de dados, como tipo de exportação, programação e frequência. Para exibir os detalhes sobre um segmento específico, selecione o nome dele na lista.

![A página de detalhes do painel de destinos com a guia de dados Ativação destacada.](../images/destinations/activation-data-tab.png)

Este widget ajuda você a entender o valor dos seus destinos com base no número de públicos-alvo ativados rapidamente. Ele também fornece acesso fácil a informações mais detalhadas para análise adicional.

Consulte a seção de pré-requisitos para [definições de termos usados](#prerequisites) nesta descrição.

## Próximas etapas

Ao seguir este documento, agora é possível localizar o painel de destinos e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com destinos no Experience Platform, consulte o [documentação de destinos](../../destinations/home.md).
