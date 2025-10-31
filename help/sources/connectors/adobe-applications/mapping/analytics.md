---
title: Mapeamento de campos para o Adobe Analytics Source Connector
description: Mapeie campos do Adobe Analytics para campos XDM usando o Analytics Source Connector.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '3838'
ht-degree: 5%

---

# Mapeamentos de campo do Analytics

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio da fonte do Analytics. Alguns dados assimilados por meio do ADC podem ser mapeados diretamente dos campos do Analytics para os campos do Experience Data Model (XDM), enquanto outros dados exigem transformações e funções específicas para serem mapeados com êxito.

![Uma ilustração da jornada de dados do Adobe Analytics do Analytics para o Experience Platform.](../images/analytics-data-experience-platform.png)

## Parâmetros de mídia de transmissão

Leia a tabela a seguir para obter informações sobre parâmetros de mídia de transmissão.

| Feed de dados | Caminho do campo XDM | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | sequência de caracteres | O nome amigável (legível) do vídeo. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | sequência de caracteres | O nome do autor da mídia. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | sequência de caracteres | O nome do artista do álbum ou grupo que grava a música ou o vídeo. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | sequência de caracteres | O nome do álbum ao qual pertence a gravação de música ou vídeo. |
| `videolength` | `mediaReporting.sessionDetails.length` | inteiro | A duração ou o tempo de execução do vídeo. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | sequência de caracteres |  |
| `video` | `mediaReporting.sessionDetails.name` | sequência de caracteres | A ID do vídeo. |
| `videoshow` | `mediaReporting.sessionDetails.show` | sequência de caracteres | O nome do programa ou da série. O nome do programa/série só é necessário se o programa for parte de uma série. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | sequência de caracteres | O tipo de mídia de transmissão, como &quot;vídeo&quot; ou &quot;áudio&quot;. |
| `videoseason` | `mediaReporting.sessionDetails.season` | sequência de caracteres | O número da temporada do programa. Esse valor só será necessário se o programa for parte de uma série. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | sequência de caracteres | O número do episódio. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | cadeia de caracteres[] | O gênero do vídeo. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | sequência de caracteres | Um identificador para uma ocorrência de um fluxo de conteúdo exclusivo para uma reprodução individual. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName` | sequência de caracteres | O nome do reprodutor de vídeo. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | sequência de caracteres | O canal de distribuição de onde o conteúdo foi reproduzido. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | sequência de caracteres | O tipo de entrega de fluxo usado para o conteúdo. Isso é automaticamente definido como &quot;Vídeo&quot; para todas as visualizações de vídeo. Os valores recomendados incluem: VOD, Live, Linear, UGC, DVOD, Radio, Podcast, Audiobook e Song. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | sequência de caracteres | O nome da rede ou do canal. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | sequência de caracteres | O tipo de feed. Isso pode representar dados reais relacionados ao feed, como &quot;East HD&quot; ou &quot;SD&quot;, ou a fonte do feed, como um URL. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | sequência de caracteres |  |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | booleano | Um valor booleano que indica se o vídeo foi iniciado ou não. Isso ocorre depois que o usuário seleciona o botão Reproduzir e conta mesmo se houver anúncios antes da exibição, buffering, erros e assim por diante. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | booleano | Um valor booleano que indica se o primeiro quadro da mídia foi iniciado. Se o usuário ignorar o conteúdo durante qualquer anúncio ou período de buffer, o &quot;início do conteúdo&quot; não será qualificado. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | inteiro | A duração (em segundos) de todos os eventos de `type=PLAY` no conteúdo principal. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | booleano | Um valor booleano que indica se um ativo de mídia cronometrado foi observado até o fim. Esse valor não significa necessariamente que o visualizador assistiu ao vídeo inteiro, pois não considera o visualizador que pode pular adiante. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | inteiro | O tempo total gasto por um usuário em um ativo de mídia temporizado específico, incluindo o tempo gasto assistindo a anúncios. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | inteiro | A soma dos intervalos únicos vistos por um usuário em um ativo de mídia cronometrado. Em outras palavras, a duração dos intervalos de reprodução visualizados várias vezes é contada apenas uma vez. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | número | O tempo médio de conteúdo gasto para um item de mídia específico. Em outras palavras, o tempo total de conteúdo gasto dividido pela duração de todas as sessões de reprodução. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | booleano | Um valor booleano que indica se o indicador de reprodução de um determinado vídeo passou o marcador de 10% da duração total do vídeo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | booleano | Um valor booleano que indica se o indicador de reprodução de um determinado vídeo passou o marcador de 25% da duração total do vídeo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | booleano | Um valor booleano que indica se o indicador de reprodução de um determinado vídeo passou o marcador de 50% da duração total do vídeo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | booleano | Um valor booleano que indica se o indicador de reprodução de um determinado vídeo passou o marcador de 75% da duração total do vídeo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | booleano | Um valor booleano que indica se o indicador de reprodução de um determinado vídeo passou o marcador de 95% da duração total do vídeo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | booleano | Um valor booleano que indica se uma ou mais pausas ocorreram durante a reprodução de um único item de mídia. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | inteiro | O número de períodos de pausa que ocorreram durante a reprodução. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | inteiro | A duração total (em segundos) na qual a reprodução foi pausada por um usuário. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | sequência de caracteres | Um identificador MVPD fornecido pela autenticação Adobe. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | sequência de caracteres | Define se o usuário foi autorizado por meio da autenticação da Adobe. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | Define a hora do dia em que o conteúdo foi transmitido ou reproduzido. |  |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | booleano | Um valor booleano que marca cada reprodução que foi retomada após mais de 30 minutos de buffer, pausa ou um período de paralisação. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | booleano | Um valor booleano que indica que pelo menos um quadro foi visualizado. Este quadro não precisa ser o primeiro quadro. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | sequência de caracteres | O nome da gravadora. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | sequência de caracteres | A estação de rádio ou o nome no qual o áudio é reproduzido. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | sequência de caracteres | O nome do publicador do conteúdo de áudio. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | número | Indica o tempo (em segundos) decorrido entre a última interação conhecida de um usuário e o momento em que a sessão foi encerrada. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | sequência de caracteres | O tipo de anúncio carregado conforme definido pela sua própria representação interna. |

{style="table-layout:auto"}

## Parâmetros do Advertising

Leia a tabela a seguir para obter informações sobre parâmetros de publicidade.

| Feed de dados | Caminho do campo XDM | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | sequência de caracteres | O nome do anúncio. Nos relatórios, o &quot;Ad Name&quot; é a classificação e o &quot;Ad Name (variable)&quot; é a eVar. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | inteiro | O índice do anúncio dentro do início do anúncio principal. Por exemplo, o primeiro anúncio tem índice 0 e o segundo anúncio tem índice 1. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | inteiro | A duração do anúncio de vídeo, medida em segundos. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | sequência de caracteres | O nome do reprodutor usado para renderizar o anúncio. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | sequência de caracteres | A ID do ad break. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | sequência de caracteres | O nome amigável (legível) do ad break. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | sequência de caracteres | A empresa ou marca cujo produto é apresentado no anúncio. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | sequência de caracteres | A ID da campanha publicitária. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | booleano | Um valor booleano que indica se o anúncio foi iniciado ou não. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | booleano | Um valor booliano que indica se o foi concluído ou não. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | inteiro | A quantidade total de tempo, medida em segundos, gasta assistindo ao anúncio. |

{style="table-layout:auto"}

## Parâmetros de capítulo

Leia a tabela a seguir para obter informações sobre parâmetros de capítulo.

| Feed de dados | Caminho do campo XDM | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | sequência de caracteres | A ID gerada automaticamente do capítulo. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | booleano | Um valor booleano que indica se o capítulo foi iniciado ou não. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | booleano | Um valor booleano que indica se o capítulo foi ou não concluído. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | inteiro | O tempo, medido em segundos, gasto no capítulo. |

{style="table-layout:auto"}

## Parâmetros de estado do player

Leia a tabela a seguir para obter informações sobre os parâmetros do estado do player.

| Feed de dados | Caminho do campo XDM | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | booleano | Um valor booleano que indica se o estado do vídeo está ou não definido como tela cheia. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | inteiro | O número de vezes que um estado de vídeo foi definido como em tela cheia. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | inteiro | A duração total de quando o estado do vídeo foi definido como em tela cheia. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | booleano | Um valor booleano que indica se as legendas ocultas estão ou não ativadas. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | inteiro | O número de vezes que as legendas ocultas foram habilitadas. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | inteiro | A duração total de quando as legendas ocultas foram habilitadas. |
| `videostatemute` | `mediaReporting.states[].isSet` | booleano | Um valor booleano que indica se o estado do vídeo foi definido como mudo ou não. |
| `videostatemutecount` | `mediaReporting.states[].count` | inteiro | O número de vezes que um vídeo foi silenciado. |
| `videostatemutetime` | `mediaReporting.states[].time` | inteiro | A duração total do vídeo na função mudo. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | booleano | Um valor booleano que indica se o modo picture-in-picture está ativado ou não. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | inteiro | O número de vezes que o modo picture-in-picture é ativado. |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | inteiro | A duração total de quando o modo picture-in-picture foi habilitado. |
| `videostateinfocus` | `mediaReporting.states[].isSet` | booleano | Um valor booleano que indica se o modo em foco está ou não ativado |
| `videostateinfocuscount` | `mediaReporting.states[].count` | inteiro | O número de vezes que o modo em imagem foi habilitado. |
| `videostateinfocustime` | `mediaReporting.states[].time` | inteiro | A duração total de quando o modo em foco foi habilitado. |

{style="table-layout:auto"}

## Parâmetros de qualidade

Leia a tabela a seguir para obter informações sobre parâmetros de qualidade.

| Feed de dados | Caminho do campo XDM | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | número | A taxa média de bits (em kbps, número inteiro). Essa métrica é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | booleano | Um valor booliano que indica o número de fluxos nos quais ocorreram as alterações de taxa de bits. Essa métrica é definida como verdadeira somente se pelo menos um evento de alteração de taxa de bits ocorrer durante a sessão de reprodução. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | inteiro |  |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | sequência de caracteres | O número de alterações da taxa de bits. Esse valor é calculado como uma soma de todos os eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | inteiro | A duração, medida em segundos, entre o carregamento e o início do vídeo. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | booleano | Um valor booleano que indica o número de fluxos com quedas de quadros. Essa métrica é definida como verdadeira somente se pelo menos um quadro tiver sido descartado durante a sessão de reprodução. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | inteiro | O número de quadros ignorados durante a reprodução do conteúdo principal. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | inteiro | O número de eventos de buffer. Essa métrica é calculada como uma contagem dos estados de buffer diferentes ocorridos durante uma sessão de reprodução. Essa é uma contagem de quantas vezes o reprodutor entra em um estado de buffer a partir de outros estados, como reprodução ou pausa. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | inteiro | A quantidade total de tempo gasto com buffering, medida em segundos. Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | booleano | Um valor booleano que indica o número de fluxos afetados pelo buffer. Essa métrica é definida como verdadeira somente se pelo menos um evento de buffer ocorrer durante a sessão de reprodução. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | booleano | Um valor booliano que indica o número de fluxos nos quais ocorreram eventos de erro. Por exemplo, se um trackError foi chamado durante a sessão de reprodução e uma chamada de heartbeat type=error foi gerada. Essa métrica é definida como verdadeira somente se pelo menos um erro ocorrer durante a reprodução. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | inteiro | O número de erros que ocorreram. Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | matriz de sequência de caracteres | As IDs de erro exclusivas geradas pelo SDK do reprodutor. Você deve fornecer os códigos ou IDs de erro na implementação por meio das APIs de erro fornecidas. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | matriz de sequência de caracteres | As IDs de erro exclusivas de qualquer origem externa, como erros de CDN. Você deve fornecer os códigos ou IDs de erro na implementação por meio das APIs de erro fornecidas. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | booleano | As IDs de erro exclusivas geradas pelo Media SDK durante a reprodução. |

{style="table-layout:auto"}

## Campos obsoletos

Leia esta seção para obter informações sobre campos de mapeamento obsoletos do Analytics.

### Campos de mapeamento direto

+++Selecione para exibir uma tabela de campos de mapeamento direto obsoletos

| Feed de dados | Campo XDM | Tipo XDM | Descrição |
| --- | --- | --- | --- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | sequência de caracteres | eVars personalizadas do Analytics. Cada organização pode usar eVars de forma diferente. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | sequência de caracteres | Propriedades personalizadas do Analytics. Cada organização pode usar props de forma diferente. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | inteiro | A ID do número do navegador. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | inteiro | A altura do navegador, em pixels. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | inteiro | A largura do navegador, em pixels. |
| `m_campaign` | `marketing.trackingCode` | sequência de caracteres | A variável usada na dimensão Código de rastreamento. |
| `m_channel` | `web.webPageDetails.siteSection` | sequência de caracteres | A variável usada na dimensão Seções do site. |
| `m_domain` | `environment.domain` | sequência de caracteres | A variável usada na dimensão Domínio. Ele se baseia no provedor de serviços de Internet (ISP) do usuário. |
| `m_geo_city` | `placeContext.geo.city` | sequência de caracteres | O nome da cidade da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `m_geo_dma` | `placeContext.geo.dmaID` | inteiro | A ID numérica da área demográfica para a ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `m_geo_region` | `placeContext.geo.stateProvince` | sequência de caracteres | O nome do estado ou da região da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `m_geo_zip` | `placeContext.geo.postalCode` | sequência de caracteres | O CEP da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `m_keywords` | `search.keywords` | sequência de caracteres | A variável usada na dimensão Palavra-chave. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | inteiro | A ID numérica que representa o sistema operacional do visitante. Isso é baseado na coluna user_agent. |
| `m_page_url` | `web.webPageDetails.URL` | sequência de caracteres | O URL da ocorrência da página. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | sequência de caracteres | É igual a 1 nas ocorrências que têm um nome de página. É semelhante à métrica Exibições de página do Adobe Analytics. |
| `m_referrer` | `web.webReferrer.URL` | sequência de caracteres | O URL da página anterior. |
| `m_search_page_num` | `search.pageDepth` | inteiro | Usado pela dimensão Todas as classificações da página de pesquisa. Indica em qual página de resultados de pesquisa seu site foi exibido antes de o usuário clicar no site. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | sequência de caracteres | Variável de estado. |
| `m_user_server` | `web.webPageDetails.server` | sequência de caracteres | Uma variável usada na dimensão Servidor. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | sequência de caracteres | Uma variável usada para preencher a dimensão CEP. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | sequência de caracteres | Lista todas as linguagens aceitas, conforme indicado no cabeçalho HTTP Accept-Language. |
| `homepage` | `web.webPageDetails.isHomePage` | booleano | Não está mais em uso. Indicado se a URL atual é a página inicial do navegador. |
| `ipv6` | `environment.ipV6` | sequência de caracteres |  |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | sequência de caracteres | A versão do JavaScript compatível com o navegador. |
| `user_agent` | `environment.browserDetails.userAgent` | sequência de caracteres | A sequência de agente do usuário enviada no cabeçalho HTTP. |
| `mobileappid` | `application.name` | sequência de caracteres | A ID do aplicativo móvel, armazenada no seguinte formato: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | sequência de caracteres | O nome do dispositivo móvel. No iOS, ele é armazenado como uma cadeia de 2 dígitos separada por vírgulas. O primeiro número representa a geração do dispositivo e o segundo representa a família do dispositivo. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | sequência de caracteres | Usado pelos serviços móveis. Representa o ponto de interesse. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | número | Usado pelos serviços móveis. Representa a distância do ponto de interesse. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | número | Coletada da variável de dados de contexto a.loc.acc. Indica a precisão do GPS em metros no momento da coleta. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | sequência de caracteres | Coletada da variável de dados de contexto a.loc.category. Descreve a categoria de um local específico. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | sequência de caracteres | Coletada da variável de dados de contexto a.loc.id. Identificador para um determinado ponto de interesse. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | sequência de caracteres | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | número | Beacon principal do Mobile Services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | número | Beacon pequeno do Mobile Services. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | sequência de caracteres | UUID de sinal do Mobile Services. |
| `mobileinstalls` | `application.firstLaunches` | Objeto | Isso é disparado na primeira execução após a instalação ou reinstalação `{id (string), value (number)}` |
| `mobileupgrades` | `application.upgrades` | Objeto | Relata o número de atualizações do aplicativo. Aciona na primeira execução após a atualização ou sempre que o número da versão é alterado. `{id (string), value (number)}` |
| `mobilelaunches` | `application.launches` | Objeto | O número de vezes que o aplicativo foi iniciado.  `{id (string), value (number)}` |
| `mobilecrashes` | `application.crashes` | Objeto | `{id (string), value (number)}` |
| `mobilemessageclicks` | `directMarketing.clicks` | Objeto | `{id (string), value (number)}` |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objeto | `{id (string), value (number)}` |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objeto | `{id (string), value (number)}` |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objeto | O tempo para o início da qualidade do vídeo. `{id (string), value (number)}` |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objeto | `{id (string), value (number)}` |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objeto | Contagem de buffer de qualidade do vídeo `{id (string), value (number)}` |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objeto | Tempo de buffer de qualidade do vídeo `{id (string), value (number)}` |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objeto | Contagem de alterações de qualidade do vídeo `{id (string), value (number)}` |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objeto | Taxa média de bits de qualidade do vídeo `{id (string), value (number)}` |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objeto | Contagem de erros de qualidade do vídeo `{id (string), value (number)}` |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objeto | `{id (string), value (number)}` |

{style="table-layout:auto"}

+++

## Campos de mapeamento gerados

Selecionar campos provenientes do ADC devem ser transformados, exigindo que uma lógica além de uma cópia direta do Adobe Analytics seja gerada no XDM.

+++Selecione para exibir uma tabela de campos de mapeamento gerados obsoletos

| Feed de dados | Campo XDM | Tipo XDM | Descrição |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Props personalizadas do Analytics, configuradas para serem propriedades de lista. Ela contém uma lista delimitada de valores. `{}` |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Usado por variáveis de hierarquia. Ela contém uma lista delimitada de valores. `{values (array), delimiter (string)}` |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Variáveis personalizadas da lista do Analytics. Contém uma lista delimitada de valores.  `{value (string), key (string)}` |
| `m_color` | `device.colorDepth` | inteiro | A ID de intensidade de cor, que se baseia no valor da coluna c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Uma variável usada na dimensão Suporte a cookies. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comércio padrão acionados na ocorrência. `{id (string), value (number)}` |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados acionados na ocorrência. `{id (Object), value (Object)}` |
| `m_geo_country` | `placeContext.geo.countryCode` | sequência de caracteres | Abreviação do país no qual a ocorrência foi originada, com base no IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | número | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | número | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Um sinalizador que indica se o Java™ está ativado. |
| `m_latitude` | `placeContext.geo._schema.latitude` | número | |
| `m_longitude` | `placeContext.geo._schema.longitude` | número | |
| `m_page_event_var1` | `web.webInteraction.URL` | sequência de caracteres | Uma variável usada somente em solicitações de imagem de rastreamento de link. Essa variável contém o URL do link de download, link de saída, ou link personalizado clicado. |
| `m_page_event_var2` | `web.webInteraction.name` | sequência de caracteres | Uma variável usada somente em solicitações de imagem de rastreamento de link. Isso lista o nome personalizado do link, se for especificado. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | booleano | Uma variável usada para preencher a dimensão Páginas não encontradas. Essa variável deve estar vazia ou conter &quot;ErrorPage&quot;. |
| `m_pagename_no_url` | `web.webPageDetails.name` | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado vazio. |
| `m_paid_search` | `search.isPaid` | booleano | Um sinalizador que é definido se a ocorrência corresponder à detecção de pesquisa paga. |
| `m_product_list` | `productListItems[].items` | matriz | A lista de produtos, conforme enviado por meio da variável products. | {SKU (string), quantidade (inteiro), priceTotal (número)} |
| `m_ref_type` | `web.webReferrer.type` | sequência de caracteres | Uma ID numérica que representa o tipo de referência para a ocorrência.<br/>`1`: Dentro do site<br/>`2`: Outros sites<br/>`3`: Mecanismos de pesquisa<br/>`4`: Disco rígido<br/>`5`: USENET<br/>`6`: Digitado/Marcado (sem referenciador)<br/>`7`: email<br/>`8`: Sem JavaScript<br/>`9`: Redes sociais |
| `m_search_engine` | `search.searchEngine` | sequência de caracteres | A ID numérica que representa o mecanismo de pesquisa que direcionou o visitante ao seu site. |
| `post_currency` | `commerce.order.currencyCode` | sequência de caracteres | O código de moeda usado durante a transação. |
| `post_cust_hit_time_gmt` | `timestamp` | sequência de caracteres | Isso só é usado em conjuntos de dados habilitados para carimbo de data e hora. Esse é o carimbo de data e hora enviado com a ocorrência, com base no horário UNIX®. |
| `post_cust_visid` | `identityMap` | objeto | A ID de visitante do cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | booleano | A ID de visitante do cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | sequência de caracteres | A ID de visitante do cliente. |
| `post_visid_high` + `visid_low` | `identityMap` | objeto | Um identificador exclusivo para uma visita. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | sequência de caracteres | Um identificador exclusivo para uma visita. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | booleano | Usado com `visid_low` para identificar uma visita de maneira exclusiva. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | sequência de caracteres | Usado com `visid_low` para identificar uma visita de maneira exclusiva. |
| `post_visid_low` | `identityMap` | objeto | Usado com visid_high para identificar uma visita de maneira exclusiva. |
| `hit_time_gmt` | `receivedTimestamp` | sequência de caracteres | O carimbo de data e hora da ocorrência, com base no horário UNIX®. |
| `hitid_high` + `hitid_low` | `_id` | sequência de caracteres | Um identificador exclusivo para identificar uma ocorrência. |
| `hitid_low` | `_id` | sequência de caracteres | Usado com hitid_high para identificar uma ocorrência de maneira exclusiva. |
| `ip` | `environment.ipV4` | sequência de caracteres | O endereço IP, com base no cabeçalho HTTP da solicitação de imagem. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | booleano | A versão do JavaScript usada. |
| `mcvisid_high` + `mcvisid_low` | identityMap | objeto | A ID de visitante do Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | sequência de caracteres | A Experience Cloud ID (ECID) também é conhecida como MCID e às vezes é usada em namespaces. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | booleano | A Experience Cloud ID (ECID) também é conhecida como MCID e às vezes é usada em namespaces. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | sequência de caracteres | A Experience Cloud ID (ECID) também é conhecida como MCID e às vezes é usada em namespaces. |
| `mcvisid_low` | `identityMap` | objeto | A ID de visitante do Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | sequência de caracteres | ID de compilação da ocorrência. O campo de análise sdid_high e sdid_low é a ID de dados complementar usada para compilar duas (ou mais) ocorrências recebidas. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | sequência de caracteres | Proximidade de beacon do Mobile Services. |

{style="table-layout:auto"}

+++

## Campos de mapeamento dividido

Esses campos têm uma única origem, mas são mapeados para **vários** locais XDM.

+++Selecione para exibir uma tabela de campos de mapeamento dividido obsoletos

| Feed de dados | Campo XDM | Tipo XDM | Descrição |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | inteiro | ID numérica que representa a resolução do monitor. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | sequência de caracteres | Versão do sistema operacional do dispositivo móvel. |

{style="table-layout:auto"}

+++

## Campos de mapeamento avançado

Selecionar campos (conhecidos como &quot;valores de publicação&quot;) que contêm dados depois que o Adobe ajusta seus valores usando Regras de processamento, Regras VISTA e tabelas de pesquisa. A maioria dos valores de postagem tem uma contrapartida pré-processada.

O conector de origem do Analytics envia dados pré-processados em um conjunto de dados na Experience Platform. Você pode transformar esses dados em sua contraparte pós-processada usando transformações. Para saber mais sobre como executar essas transformações usando o Serviço de Consulta, consulte [funções definidas pela Adobe](/help/query-service/sql/adobe-defined-functions.md) no guia do usuário do Serviço de Consulta.

Para saber mais sobre como executar essas transformações usando o Serviço de Consulta, consulte [funções definidas pela Adobe](/help/query-service/sql/adobe-defined-functions.md) no guia do usuário do Serviço de Consulta.

+++Selecione para exibir uma tabela de campos de mapeamento avançado obsoletos

| Feed de dados | Campo XDM | Tipo XDM | Descrição |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | eVars personalizadas do Analytics. Cada organização pode usar eVars de forma diferente. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | string | Propriedades personalizadas do Analytics. Cada organização pode usar props de forma diferente. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | inteiro | A altura do navegador, em pixels. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | inteiro | A largura do navegador, em pixels. |
| `post_campaign` | `marketing.trackingCode` | string | A variável usada na dimensão Código de rastreamento. |
| `post_channel` | `web.webPageDetails.siteSection` | string | A variável usada na dimensão Seções do site. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | string | A ID de visitante personalizada, se definida. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | string | O URL da primeira página que o visitante acessa. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | string | Uma variável usada na dimensão Original da página de entrada. O nome da página de entrada do visitante. |
| `post_keywords` | `search.keywords` | string | As palavras-chave coletadas para a ocorrência. |
| `post_page_url` | `web.webPageDetails.URL` | string | O URL da ocorrência da página. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | string | É igual a 1 nas ocorrências que têm um nome de página. É semelhante à métrica Exibições de página do Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | string | Variável usada para identificar compras de maneira exclusiva. |
| `post_referrer` | `web.webReferrer.URL` | string | O URL da página anterior. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string |  Variável de estado. |
| `post_user_server` | `web.webPageDetails.server` | string | Uma variável usada na dimensão Servidor. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | string | Uma variável usada para preencher a dimensão CEP. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | inteiro | A ID numérica do navegador. |
| `domain` | `environment.domain` | string | A variável usada na dimensão Domínio. Ele se baseia no provedor de serviços de Internet (ISP) do usuário. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | string | O primeiro URL de referência do visitante. |
| `geo_city` | `placeContext.geo.city` | string | O nome da cidade da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `geo_dma` | `placeContext.geo.dmaID` | inteiro | A ID numérica da área demográfica para a ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `geo_region` | `placeContext.geo.stateProvince` | string | O nome do estado ou da região da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `geo_zip` | `placeContext.geo.postalCode` | string | O CEP da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | inteiro | A ID numérica que representa o sistema operacional do visitante. Isso é baseado na coluna user_agent. |
| `search_page_num` | `search.pageDepth` | inteiro | Essa variável é usada pela dimensão Todas as classificações da página de pesquisa e indica qual página de resultados de pesquisa seu site | apareceu em antes de o usuário clicar em seu site. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | string | Uma variável usada na dimensão Palavras-chave de pesquisa. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | inteiro | Uma variável usada na dimensão Número de visitas. Isso começa em 1, e incrementa a cada início de nova visita (por usuário). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | inteiro | Uma variável usada na dimensão Profundidade da ocorrência. Esse valor aumenta em uma unidade para cada ocorrência gerada pelo usuário e é redefinido após cada visita. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | string | O primeiro referenciador da visita. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | inteiro | O primeiro Nome da página da visita. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Props personalizadas do Analytics, configuradas para serem propriedades de lista. Ela contém uma lista delimitada de valores. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Usado por variáveis de hierarquia e contém uma lista delimitada de valores. | {values (matriz), delimitador (cadeia de caracteres)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Uma lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variável usada na dimensão Suporte a cookies. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comércio padrão acionados na ocorrência. | {id (string), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados acionados na ocorrência.| {id (Objeto), value (Objeto)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Um sinalizador que indica se o Java™ está ativado. |
| `post_latitude` | `placeContext.geo._schema.latitude` | número |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | número |   |
| `post_page_event` | `web.webInteraction.type` | string | O tipo de ocorrência enviado na solicitação da imagem (ocorrência padrão, link de download, link de saída ou link personalizado clicado). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | número | É igual a 1 se a ocorrência for um clique de link. É semelhante à métrica Eventos de página no Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | string | Essa variável é usada somente em solicitações de imagem de rastreamento de link. É o URL do link de download, link de saída, ou link personalizado clicado. |
| `post_page_event_var2` | `web.webInteraction.name` | string | Essa variável é usada somente em solicitações de imagem de rastreamento de link. É o nome personalizado do link. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | booleano | Isso é usado para preencher a dimensão Páginas não encontradas. Essa variável deve estar vazia ou conter &quot;ErrorPage&quot; |
| `post_pagename_no_url` | `web.webPageDetails.name` | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado vazio. |
| `post_product_list` | `productListItems[].items` | matriz | A lista de produtos, conforme enviado por meio da variável products. | {SKU (string), quantidade (inteiro), priceTotal (número)} |
| `post_search_engine` | `search.searchEngine` | string | A ID numérica que representa o mecanismo de pesquisa que direcionou o visitante ao seu site. |
| `mvvar1_instances` | `.list.items[]` | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| `mvvar2_instances` | `.list.items[]` | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| `mvvar3_instances` | `.list.items[]` | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| `color` | `device.colorDepth` | inteiro | ID de Intensidade de cor, com base no valor da coluna c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | string | A ID numérica, que representa o tipo do primeiro referenciador do visitante. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | inteiro | Carimbo de data e hora da primeira ocorrência do visitante no horário UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | string | Abreviação do país no qual a ocorrência foi originada, com base no IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | número |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | número |  |
| `paid_search` | `search.isPaid` | booleano | Um sinalizador que é definido se a ocorrência corresponder à detecção de pesquisa paga. |
| `ref_type` | `web.webReferrer.type` | string | Uma ID numérica que representa o tipo de referência para a ocorrência. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booleano | Um sinalizador (1=pago, 0=não pago) indicando se a primeira ocorrência da visita foi de uma ocorrência de pesquisa paga. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | string | ID numérica que representa o tipo do primeiro referenciador da visita. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | string | ID numérica do primeiro mecanismo de pesquisa da visita. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | inteiro | Carimbo de data e hora da primeira ocorrência da visita em horário UNIX®. |

+++
