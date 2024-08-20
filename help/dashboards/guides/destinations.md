---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;interface do usuário;UI;personalização;painel de perfis;painel;profile;profile dashboard
title: Painel de destinos
description: A Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre os destinos ativos da sua organização.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: a8b5ed09e8e28075a3a4f37ad30f01c1cc389b9c
workflow-type: tm+mt
source-wordcount: '3243'
ht-degree: 19%

---

# Painel [!UICONTROL Destinos]

A interface do usuário (UI) do Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre os destinos ativos da sua organização, conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de destinos na interface do usuário e fornece mais informações sobre as métricas exibidas no painel.

Para obter uma visão geral dos destinos, bem como um catálogo de todos os destinos disponíveis no Experience Platform, visite a [documentação sobre destinos](../../destinations/home.md).

## Dados do painel [!UICONTROL Destinos] {#destinations-dashboard-data}

O painel Destinos exibe um instantâneo dos destinos que sua organização ativou no Experience Platform. Os dados no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de destinos não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o painel [!UICONTROL Destinos] {#explore}

Para navegar até o painel de destinos na interface do usuário da Platform, selecione **[!UICONTROL Destinos]** no painel à esquerda e clique na guia **[!UICONTROL Visão geral]** para exibir o painel.

A data e a hora do instantâneo mais recente são exibidas na parte superior da [!UICONTROL Visão geral], ao lado da lista suspensa de destino. Todos os dados do widget são precisos a partir dessa data e hora. O carimbo de data e hora do instantâneo é fornecido em UTC; ele não está no fuso horário do usuário ou organização individual.

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver destinos ativos, o Painel de destinos e a guia [!UICONTROL Visão geral] não estarão visíveis. Em vez disso, selecionar [!UICONTROL Destinos] na navegação à esquerda exibe a guia [!UICONTROL Catálogo]. Para saber mais sobre a guia [!UICONTROL Catálogo], consulte o [[!UICONTROL guia do espaço de trabalho] de Destinos](../../destinations/ui/destinations-workspace.md).

![A Visão Geral dos Destinos da Interface do Usuário da Plataforma com o instantâneo mais recente realçado.](../images/destinations/snapshot-timestamp.png)

### Modificar o painel [!UICONTROL Destinos] {#modify}

Selecione **[!UICONTROL Modificar painel]** para alterar a aparência do painel de destinos. As alterações no painel são por usuário e não por toda a organização. Você pode mover, adicionar, redimensionar e remover widgets do painel e acessar a biblioteca de widgets para personalizar seu painel. Na biblioteca de widgets, você pode explorar os widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a documentação [modificando painéis](../customize/modify.md) e [visão geral da biblioteca de widgets](../customize/widget-library.md) para saber mais.

### Adicionar widgets {#add-widget}

Selecione **[!UICONTROL Adicionar widget]** para navegar até a biblioteca de widgets e ver uma lista dos widgets disponíveis para adicionar ao seu painel.

![A visão geral do painel Destinos com o widget Adicionar foi realçada.](../images/destinations/destinations-overview-add-widget.png)

Na biblioteca de widgets, você pode navegar pela seleção de widgets de público-alvo padrão e personalizados. Para obter informações sobre como adicionar widgets, consulte a documentação da biblioteca de widgets sobre como [adicionar um widget](../customize/widget-library.md#add-widgets).

### Exibir SQL {#view-sql}

Você pode exibir o SQL que gera os insights visualizados no painel com um alternador no espaço de trabalho [!UICONTROL Visão geral]. Você pode se inspirar no SQL de seus insights existentes para criar novas consultas que obtenham insights exclusivos dos dados da plataforma com base nas necessidades comerciais. Para saber mais sobre este recurso, consulte o [Exibir Guia da Interface do Usuário do SQL](../view-sql.md).

## Widgets padrão {#default-widgets}

Uma transferência de widget padrão é fornecida para todas as novas instâncias do Adobe Experience Platform que destacam os insights mais recentes disponíveis de seus dados. Os widgets a seguir são pré-configurados na visualização de segmentos desde o início. Veja abaixo detalhes completos sobre a finalidade e a função dos dispositivos.

* [[!UICONTROL Destinos mais usados]](#most-used-destinations)
* [[!UICONTROL Destinos criados recentemente]](#recently-created-destinations)
* [[!UICONTROL Segmentos ativados recentemente]](#recently-activated-segments)

>[!NOTE]
>
>A partir de 26 de julho de 2023, os painéis de Visão geral do [!UICONTROL Perfis], [!UICONTROL Públicos-alvo] e [!UICONTROL Destinos] foram redefinidos como uma nova carga de widget padrão para todos os usuários que não modificaram suas visualizações nos seis meses anteriores.
>Consulte a documentação nas seções de widget padrão [Perfis](./profiles.md#default-widgets) e [Públicos-alvo](./audiences.md#default-widgets) para obter detalhes sobre quais widgets são incluídos como parte dos carregamentos de widget padrão. Você pode continuar personalizando seus widgets de painel como antes.

## Widgets padrão {#standard-widgets}

O Adobe fornece vários widgets padrão que você pode usar para visualizar métricas diferentes relacionadas aos seus destinos e avaliar a integridade dos públicos-alvo disponíveis para sua análise de dados. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando a [!UICONTROL Biblioteca de widgets]. Para saber mais sobre como criar widgets personalizados, comece lendo a [Visão geral da biblioteca de widgets](../customize/widget-library.md).

### Pré-requisitos {#prerequisites}

Antes de continuar com as descrições dos widgets padrão, verifique se você está familiarizado com as definições dos seguintes termos principais usados na documentação:

* **Definição de segmento:** uma definição de segmento é um **conjunto de regras** usado para descrever as principais características ou comportamento de um público-alvo. Essas regras incluem dados de atributo e evento que qualificam os perfis como parte de um público-alvo.
* **Público-alvo**: um conjunto de pessoas, contas, famílias ou outras entidades que compartilham características e comportamentos comuns.
* **Mapeamento/Mapeamento**: o mapeamento de dados é o processo de mapear campos de dados de origem para campos de destino relacionados em um destino.
* **Identidade**: uma identidade é um identificador que representa exclusivamente um cliente individual, como uma ID de cookie, ID de dispositivo ou ID de email.
* **Ativar**: Ativar é a ação realizada por um usuário para mapear um público ou perfis para um destino, como o Oracle Eloqua, Google ou Marketing Cloud Salesforce.

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na lista a seguir:

* [[!UICONTROL Destinos mais usados]](#most-used-destinations)
* [[!UICONTROL Destinos criados recentemente]](#recently-created-destinations)
* [[!UICONTROL Públicos-alvo ativados recentemente]](#recently-activated-audiences)
* [[!UICONTROL Públicos-alvo ativados recentemente por destino]](#recently-activated-audiences-by-destination)
* [[!UICONTROL Tendência de tamanho do público-alvo]](#audience-size-trend)
* [[!UICONTROL Públicos-alvo não mapeados por identidade]](#unmapped-audiences-by-identity)
* [[!UICONTROL Públicos-alvo mapeados por identidade]](#mapped-audiences-by-identity)
* [[!UICONTROL Públicos-alvo comuns]](#common-audiences)
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
>abstract="Esse dispositivo exibe os destinos mais ativos da sua organização de acordo com o número de públicos-alvo mapeados. Esses números são precisos no momento do último instantâneo. Essa classificação fornece informações sobre quais destinos são mais usados atualmente, destacando os que podem ser subutilizados."

O widget **[!UICONTROL Destinos mais usados]** exibe os principais destinos de sua organização pelo número de públicos mapeados, a partir do último instantâneo. Essa classificação fornece insight sobre quais destinos estão sendo utilizados, além de mostrar os que podem estar subutilizados.

Por exemplo, se você configurou um destino ontem, mas não mapeou nenhum público para ele, é possível ver que o destino está subutilizado no momento.

A quantidade de públicos mapeados mostrada na coluna [!UICONTROL Contagem de público] é precisa a partir do último instantâneo diário. Mapear um novo público para o destino não atualiza a contagem até que o próximo instantâneo seja tirado.

Selecione o nome de um destino na lista mostrada no widget para navegar até os detalhes do destino para esse destino em particular. Você também pode selecionar **[!UICONTROL Exibir tudo]** para navegar até a guia **[!UICONTROL Procurar]** e selecionar o nome de um destino para exibir seus detalhes.

![A guia Visão Geral do painel Destinos com o widget de Destinos mais usado realçado.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos criados recentemente] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Destinos criados recentemente"
>abstract="Esse widget exibe uma lista dos destinos configurados mais recentemente em sua organização."

O widget **[!UICONTROL Destinos criados recentemente]** permite visualizar uma lista dos destinos configurados mais recentemente pela sua organização.

A data de criação mostrada é precisa para o último instantâneo diário. Em outras palavras, se você criar um novo destino, ele não aparecerá na lista até que o próximo instantâneo seja tirado.

Selecionar o nome de um destino na lista mostrada no widget o levará aos detalhes do destino, conforme vinculado na guia **[!UICONTROL Procurar]**. Você também pode selecionar **[!UICONTROL Exibir tudo]** para navegar até a guia **[!UICONTROL Procurar]** e selecionar o nome de um destino para exibir seus detalhes.

Para saber mais sobre como configurar tipos específicos de destinos, visite a [documentação sobre destinos](../../destinations/home.md).

![A guia Visão Geral do painel Destinos com o widget Destinos criado recentemente destacado.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Públicos-alvo ativados recentemente] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Públicos-alvo ativados recentemente"
>abstract="Esse dispositivo fornece uma lista dos públicos-alvo mapeados mais recentemente para um destino. Essa lista fornece um instantâneo dos públicos-alvo e destinos que estão sendo usados ativamente no sistema e pode ajudar na solução de problemas de mapeamentos incorretos."

O widget **[!UICONTROL Públicos-alvo recentemente ativados]** fornece uma lista dos públicos-alvo mapeados mais recentemente para um destino. Essa lista fornece um instantâneo dos públicos-alvo e destinos que estão sendo usados ativamente no sistema e pode ajudar na solução de problemas de mapeamentos incorretos.

A data [!UICONTROL Atualizada] mostrada exibe a última vez que o público-alvo foi ativado para o destino e é precisa para o último instantâneo diário. Em outras palavras, se você ativar um público-alvo para o destino, a data atualizada não será alterada até que o próximo instantâneo seja tirado.

Selecionar o nome de um público-alvo na lista mostrada no widget direciona você aos detalhes do público-alvo. Você também pode selecionar **[!UICONTROL Exibir tudo]** para navegar até a guia [!UICONTROL Públicos-alvo] [!UICONTROL Procurar] e selecionar o nome de um público-alvo para exibir seus detalhes.

Para obter mais informações sobre como trabalhar com públicos no Experience Platform, consulte a [visão geral do Serviço de segmentação](../../segmentation/home.md).

![A guia Visão geral do painel Destinos com o widget de Públicos ativados recentemente realçado.](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL Públicos-alvo ativados recentemente por destino] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Públicos-alvo ativados recentemente por destino"
>abstract="Esse dispositivo exibe os cinco principais públicos-alvo que foram ativados mais recentemente, em ordem decrescente e de acordo com o destino escolhido na lista suspensa de visão geral."

O widget **[!UICONTROL Públicos-alvo ativados recentemente por destino]** exibe os cinco principais públicos-alvo ativados mais recentemente em ordem decrescente de acordo com o destino escolhido na lista suspensa visão geral. É semelhante ao widget [!UICONTROL Públicos-alvo recentemente ativados], mas os dados exibidos **somente** se aplicam ao destino selecionado.

Esse widget contém duas métricas: o nome dos públicos-alvo e a data em que eles foram ativados pela última vez no destino. Os dados exibidos estão corretos desde o último instantâneo diário.

Para exibir os detalhes de um público-alvo, selecione o nome dele na lista exibida.

![Widget de Públicos recentemente ativados por destino.](../images/destinations/recently-activated-audiences-by-destination.png)

Consulte a seção de pré-requisitos para as [definições de termos usados](#prerequisites) nesta descrição.

### [!UICONTROL Tendência de tamanho do público-alvo] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Tendência de tamanho do público"
>abstract="Esse dispositivo ilustra o número de perfis contidos no público-alvo que estão sendo enviados para a conta de destino diariamente. O primeiro menu suspenso ajusta o período da tendência do público-alvo. O segundo menu suspenso do dispositivo seleciona o público-alvo para análise. O destino é escolhido na lista suspensa de visão geral."

O widget **[!UICONTROL Tendência de tamanho do público-alvo]** ilustra a relação da contagem de perfis durante um período para um público-alvo que foi mapeado para essa conta de destino. O widget usa um gráfico de linhas para ilustrar o número de perfis contidos no público-alvo, que estão sendo enviados para a conta de destino diariamente.

Um período para a tendência do público-alvo nos últimos 30 dias, 90 dias ou 12 meses pode ser ajustado usando o primeiro menu suspenso.

O segundo menu suspenso lista cada público-alvo disponível que pode ser enviado para a conta de destino escolhida na parte superior do painel.

![Widget de tendência de tamanho do público-alvo.](../images/destinations/audience-size-trend.png)

O widget **[!UICONTROL Tendência de tamanho do público-alvo]** fornece um botão [!UICONTROL Legendas] na parte superior direita do widget. Selecione **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas. Um modelo de aprendizado de máquina gera legendas automaticamente para descrever as principais tendências e eventos importantes, analisando o gráfico e os dados do público-alvo.

![A caixa de diálogo de legendas automáticas do widget de tendência de tamanho de Público-alvo.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Públicos-alvo não mapeados por identidade] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Públicos-alvo não mapeados por identidade"
>abstract="Esse dispositivo lista os cinco principais públicos-alvo **não mapeados**, classificados em ordem decrescente pela contagem de identidade de um determinado destino e identidade. As IDs de filtro listadas na lista suspensa do dispositivo mudam dependendo da conta de destino selecionada na parte superior da página de visão geral."

O widget **[!UICONTROL Públicos não mapeados por identidade]** lista os cinco principais públicos-alvo **não mapeados** classificados por contagem decrescente de identidades para um determinado destino e identidade. Ele destaca os públicos-alvo que são os mais benéficos a serem mapeados para a conta de destino escolhida com base na ID escolhida.

A lista suspensa ID de destino filtra os públicos-alvo disponíveis. As IDs de filtro listadas na lista suspensa mudam, dependendo da conta de destino selecionada na parte superior da página de visão geral.

A coluna Identidades conta o número de IDs de origem no público-alvo que podem ser mapeadas para a ID escolhida na lista suspensa de ID do widget.

![O widget Públicos não mapeados por identidade.](../images/destinations/unmapped-audiences-by-identity.png)

Consulte a seção de pré-requisitos para as [definições de termos usados](#prerequisites) nesta descrição.

### [!UICONTROL Públicos-alvo mapeados por identidade] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Públicos-alvo mapeados por identidade"
>abstract="Esse dispositivo fornece uma lista dos cinco principais públicos-alvo **mapeados**. A lista é ordenada do mais alto ao mais baixo de acordo com o número de IDs de origem contidas nos públicos-alvo. A ID de destino a ser contada é selecionada no menu suspenso abaixo do título do widget. As IDs de destino disponíveis no menu suspenso do widget dependem do destino escolhido na parte superior do painel de visão geral."

Esse dispositivo fornece uma lista dos cinco principais públicos-alvo **mapeados**. A lista é ordenada do mais alto ao mais baixo de acordo com o número de IDs de origem contidas nos públicos-alvo. A ID de destino a ser contada é selecionada no menu suspenso abaixo do título do widget. As IDs de destino disponíveis no menu suspenso do widget serão alteradas de acordo com o filtro de conta de destino escolhido na parte superior do painel de visão geral.

![O widget Públicos mapeados por identidade.](../images/destinations/mapped-audiences-by-identity.png)

O widget **[!UICONTROL Públicos mapeados por identidade]** destaca rapidamente a probabilidade de direcionar com êxito as oportunidades de perfil para uma campanha no destino escolhido. Uma campanha direcionada eficiente não depende do número de perfis enviados para o destino, mas sim do número de IDs de origem que provavelmente serão correspondidas às IDs de destino para fornecer dados úteis e acionáveis.

### Públicos comuns {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Públicos comuns"
>abstract="Esse dispositivo fornece uma lista dos cinco principais públicos-alvo ativados na conta de destino escolhida na parte superior da página e o destino selecionado na lista suspensa do dispositivo. A lista de públicos-alvo é ordenada de acordo com a data mais recente de ativação. O público-alvo ativado mais recentemente é exibido na parte superior."

O widget **[!UICONTROL Públicos-alvo comuns]** fornece uma lista dos cinco principais públicos-alvo ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget. A lista de públicos-alvo é ordenada de acordo com a data mais recente de ativação. O público-alvo ativado mais recentemente é exibido na parte superior.

A coluna [!UICONTROL AUDIENCE SIZE] fornece a contagem total de perfis de cada público listado.

![O widget Públicos-alvo Comuns.](../images/destinations/common-audiences.png)

### Públicos-alvo mapeados {#mapped-audiences}

O widget [!UICONTROL Públicos mapeados] exibe o número total de públicos mapeados que podem ser ativados para o destino selecionado na parte superior da página.

Selecione **[!UICONTROL Públicos-alvo]** para navegar até a guia [!UICONTROL Procurar] do painel Públicos-alvo. Este espaço de trabalho exibe uma lista de todas as definições de segmento para sua organização.

![O widget Públicos mapeados.](../images/destinations/mapped-audiences.png)

### Integridade do público mapeado {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Integridade do público mapeado"
>abstract="Esse dispositivo fornece uma lista de até 20 públicos-alvo mapeados cujas contagens totais de perfil apresentam pelo menos um desvio padrão do tamanho médio de públicos-alvo (em um período de 30 dias) mapeados para esse destino. Ele fornece uma métrica calculada para a dispersão dos tamanhos do público da média nos últimos 30 dias. Os tamanhos do público são classificados do maior ao menor."

O widget fornece uma lista de até 20 públicos-alvo mapeados cujo total de perfis conta, a partir do último instantâneo diário, desvio por um fator de pelo menos um desvio padrão do tamanho médio do público-alvo de 30 dias mapeado para esse destino.

Em resumo, fornece uma métrica calculada para a dispersão dos tamanhos de público-alvo da média nos últimos 30 dias. Ela compara se o tamanho do público-alvo de hoje está fora do desvio padrão histórico visto nos dados nos últimos 30 dias.

Todos os tamanhos de público no sistema são classificados de alto a baixo, conforme indicado na coluna [!UICONTROL LATEST SIZE].

Se a contagem de perfis de público-alvo mapeada estiver fora de um desvio padrão do tamanho médio do perfil mapeado nos últimos 30 dias, isso indica uma anomalia no sistema e deve ser investigado.

Se um público do widget [!UICONTROL Integridade do público-alvo mapeado] estiver se desviando por uma grande margem, consulte o gráfico de tendência de tamanho do público-alvo e localize o público anômalo. A tendência pode fornecer mais informações sobre a saúde do seu público-alvo.

>[!NOTE]
>
>O tamanho padrão do widget de integridade Público-alvo mapeado pode obstruir as informações da tabela. Modifique o tamanho do widget para melhorar a legibilidade dos nomes dos públicos-alvo e títulos de coluna mapeados. Consulte a documentação de modificação de painéis para obter orientação sobre [como redimensionar um widget](../customize/modify.md).

![Widget de integridade do público mapeado.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Contagem de destinos] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Contagem de destinos"
>abstract="Esse widget fornece o número total de pontos de acesso disponíveis, onde um público pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos."

O widget [!UICONTROL Contagem de destinos] fornece o número total de pontos de extremidade disponíveis nos quais um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos.

Abaixo da contagem total, selecione **[!UICONTROL Destinos]** para navegar até a guia de navegação de destinos. Esta página lista todos os destinos com os quais você estabeleceu uma conexão até o momento.

![Widget de contagem de Destinos.](../images/destinations/destinations-count.png)

### [!UICONTROL Status do destino] {#destination-status}

O widget [!UICONTROL Status do destino] exibe o número total de destinos habilitados como uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre destinos habilitados e desabilitados.

As contagens individuais para destinos habilitados ou desabilitados são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![Widget de status de Destino.](../images/destinations/destination-status.png)

### [!UICONTROL Destinos ativos por plataforma de destino] {#active-destinations-by-destination-platform}

O widget fornece uma tabela de duas colunas para mostrar uma lista de plataformas de destino ativas e o número total de destinos ativos para cada plataforma de destino. A lista de plataformas de destino é ordenada de cima para baixo.

![O widget Destinos ativos por plataforma de destino.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Públicos ativados em todos os destinos] {#activated-audiences-across-all-destinations}

O widget [!UICONTROL Públicos-alvo ativados em todos os destinos] fornece o número total de públicos-alvo ativados em todos os destinos em uma única métrica. Esse número é preciso para o instantâneo mais recente.

![Widget de Públicos ativados em todos os destinos.](../images/destinations/activated-audiences-across-all-destinations.png)

Selecione **[!UICONTROL Públicos]** para navegar até a guia de destinos [!UICONTROL Procurar]. Esta página fornece uma lista de todos os destinos ativados e diversas métricas relevantes. Consulte a documentação para obter mais informações sobre a [[!UICONTROL guia Procurar]](../../destinations/ui/destinations-workspace.md#browse).

Consulte a seção de pré-requisitos para as [definições de termos usados](#prerequisites) nesta descrição.

### [!UICONTROL Públicos ativados] {#activated-audiences}

Esse widget fornece uma única métrica para o número total de públicos-alvo ativados para um destino.

![Widget de Públicos-alvo ativados.](../images/destinations/activated-audiences.png)

Selecione **[!UICONTROL Públicos-alvo]** para navegar até a página de detalhes do painel de destinos. A guia [!UICONTROL Dados de ativação] exibe uma lista de públicos que foram mapeados para o destino, incluindo sua data inicial e data final (se aplicável), e outras informações relevantes para a exportação de dados, como tipo de exportação, agendamento e frequência. Para exibir os detalhes sobre um público-alvo específico, selecione o nome na coluna [!UICONTROL Nome do público-alvo].

![A página de detalhes do painel de destinos com a guia de dados Ativação realçada.](../images/destinations/activation-data-tab.png)

Este widget ajuda você a entender o valor dos seus destinos com base no número de públicos-alvo ativados rapidamente. Ele também fornece acesso fácil a informações mais detalhadas para análise adicional.

Consulte a seção de pré-requisitos para as [definições de termos usados](#prerequisites) nesta descrição.

## Próximas etapas

Ao seguir este documento, agora é possível localizar o painel de destinos e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com destinos no Experience Platform, consulte a [documentação sobre destinos](../../destinations/home.md).
