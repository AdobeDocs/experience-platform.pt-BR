---
keywords: campos de mapeamento do Analytics;mapeamento do Analytics
solution: Experience Platform
title: Mapeamento de campos para o Adobe Analytics Source Connector
description: Mapeie campos do Adobe Analytics para campos XDM usando o Analytics Source Connector.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 6cbd902c6a1159d062fb38bf124a09bb18ad1ba8
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 8%

---

# Mapeamentos de campo do Analytics

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio da fonte do Analytics. Alguns dados assimilados por meio do ADC podem ser mapeados diretamente dos campos do Analytics para os campos do Experience Data Model (XDM), enquanto outros dados exigem transformações e funções específicas para serem mapeados com êxito.

![](../images/analytics-data-experience-platform.png)

## Campos de mapeamento direto

Os campos selecionados são mapeados diretamente do Adobe Analytics para o Experience Data Model (XDM).

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
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
| `ipv6` | `environment.ipV6` | sequência de caracteres |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | sequência de caracteres | A versão do JavaScript compatível com o navegador. |
| `user_agent` | `environment.browserDetails.userAgent` | sequência de caracteres | A sequência de agente do usuário enviada no cabeçalho HTTP. |
| `mobileappid` | `application.name` | sequência de caracteres | A ID do aplicativo móvel, armazenada no seguinte formato: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | sequência de caracteres | O nome do dispositivo móvel. No iOS, ele é armazenado como uma cadeia de 2 dígitos separada por vírgulas. O primeiro número representa a geração do dispositivo e o segundo representa a família do dispositivo. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | sequência de caracteres | Usado pelos serviços móveis. Representa o ponto de interesse. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | número | Usado pelos serviços móveis. Representa a distância do ponto de interesse. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | número | Coletada da variável de dados de contexto a.loc.acc. Indica a precisão do GPS em metros no momento da coleta. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | sequência de caracteres | Coletada da variável de dados de contexto a.loc.category. Descreve a categoria de um local específico. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | sequência de caracteres | Coletada da variável de dados de contexto a.loc.id. Identificador para um determinado ponto de interesse. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | sequência de caracteres | O nome do vídeo. |
| `videoad` | `advertising.adAssetReference._id` | sequência de caracteres | Identificador do ativo do anúncio. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | sequência de caracteres | O Conteúdo-Tipo Do Vídeo. Isso é automaticamente definido como &quot;Vídeo&quot; para todas as visualizações de vídeo. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | sequência de caracteres | O pod no qual o anúncio de vídeo está. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | inteiro | A posição do anúncio de vídeo no pod. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | sequência de caracteres | O nome do reprodutor de vídeo. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | sequência de caracteres | O canal de vídeo. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | sequência de caracteres | O nome do reprodutor do anúncio de vídeo. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | sequência de caracteres | O nome do capítulo do Vídeo |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | sequência de caracteres | O nome do vídeo. |
| `videoadname` | `advertising.adAssetReference._dc.title` | sequência de caracteres | O nome do anúncio de vídeo. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | sequência de caracteres | Programa de vídeo. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | sequência de caracteres | Temporada de vídeos. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | sequência de caracteres | Episódio em vídeo. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | sequência de caracteres | Rede de vídeo. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | sequência de caracteres | Tipo de apresentação de vídeo. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | sequência de caracteres | Carregamentos de vídeos e anúncios. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | sequência de caracteres | Tipo de feed de vídeo. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | número | Beacon principal do Mobile Services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | número | Beacon pequeno do Mobile Services. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | sequência de caracteres | UUID de sinal do Mobile Services. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | sequência de caracteres | ID da sessão de vídeo. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | matriz | Gênero de vídeo. | {title (Objeto), description (Objeto), type (Objeto), meta:xdmType (Objeto), items (string), meta:xdmField (Objeto)} |
| `mobileinstalls` | `application.firstLaunches` | Objeto | Isso é acionado na primeira execução após a instalação ou reinstalação | {id (string), value (number)} |
| `mobileupgrades` | `application.upgrades` | Objeto | Relata o número de atualizações do aplicativo. Aciona na primeira execução após a atualização ou sempre que o número da versão é alterado. | {id (string), value (number)} |
| `mobilelaunches` | `application.launches` | Objeto | O número de vezes que o aplicativo foi iniciado. | {id (string), value (number)} |
| `mobilecrashes` | `application.crashes` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videotime` | `media.mediaTimed.timePlayed` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videostart` | `media.mediaTimed.impressions` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videocomplete` | `media.mediaTimed.completes` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoadstart` | `advertising.impressions` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoadcomplete` | `advertising.completes` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoadtime` | `advertising.timePlayed` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoplay` | `media.mediaTimed.starts` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objeto | O tempo para o início da qualidade do vídeo. | {id (string), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objeto | Contagem de buffer de qualidade do vídeo | {id (string), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objeto | Tempo de buffer de qualidade do vídeo | {id (string), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objeto | Contagem de alterações de qualidade do vídeo | {id (string), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objeto | Taxa média de bits de qualidade do vídeo | {id (string), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objeto | Contagem de erros de qualidade do vídeo | {id (string), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress10` | `media.mediaTimed.progress10` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress25` | `media.mediaTimed.progress25` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress50` | `media.mediaTimed.progress50` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress75` | `media.mediaTimed.progress75` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress95` | `media.mediaTimed.progress95` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videoresume` | `media.mediaTimed.resumes` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videopausecount` | `media.mediaTimed.pauses` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | Objeto | <!-- MISSING --> | {id (string), value (number)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | inteiro |

{style="table-layout:auto"}

## Campos de mapeamento dividido

Esses campos têm uma única origem, mas são mapeados para **vários** locais XDM.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | inteiro | ID numérica que representa a resolução do monitor. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | sequência de caracteres | Versão do sistema operacional do dispositivo móvel. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | inteiro | Duração do anúncio de vídeo. |

{style="table-layout:auto"}

## Campos de mapeamento gerados

Selecionar campos provenientes do ADC devem ser transformados, exigindo que uma lógica além de uma cópia direta do Adobe Analytics seja gerada no XDM.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Props personalizadas do Analytics, configuradas para serem propriedades de lista. Ela contém uma lista delimitada de valores. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Usado por variáveis de hierarquia. Ela contém uma lista delimitada de valores. | {values (matriz), delimitador (cadeia de caracteres)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Variáveis personalizadas da lista do Analytics. Contém uma lista delimitada de valores. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | inteiro | A ID de intensidade de cor, que se baseia no valor da coluna c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Uma variável usada na dimensão Suporte a cookies. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comércio padrão acionados na ocorrência. | {id (string), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados acionados na ocorrência. | {id (Objeto), value (Objeto)} |
| `m_geo_country` | `placeContext.geo.countryCode` | sequência de caracteres | Abreviação do país no qual a ocorrência foi originada, com base no IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Um sinalizador que indica se o Java™ está ativado. |
| `m_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
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
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | sequência de caracteres | A ID de Experience Cloud (ECID) também é conhecida como MCID e, às vezes, é usada em namespaces. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | booleano | A ID de Experience Cloud (ECID) também é conhecida como MCID e, às vezes, é usada em namespaces. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | sequência de caracteres | A ID de Experience Cloud (ECID) também é conhecida como MCID e, às vezes, é usada em namespaces. |
| `mcvisid_low` | `identityMap` | objeto | A ID de visitante do Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | sequência de caracteres | ID de compilação da ocorrência. O campo de análise sdid_high e sdid_low é a ID de dados complementar usada para compilar duas (ou mais) ocorrências recebidas. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | sequência de caracteres | Proximidade de beacon do Mobile Services. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | inteiro | O nome do capítulo do vídeo. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | inteiro | A duração do vídeo. |

{style="table-layout:auto"}

## Campos de mapeamento avançado

Selecionar campos (conhecidos como &quot;valores de publicação&quot;) contêm dados depois que o Adobe ajusta seus valores usando Regras de processamento, regras VISTA e tabelas de pesquisa. A maioria dos valores de postagem tem uma contrapartida pré-processada. Sua organização pode decidir se deseja usar o campo pré-processado, o campo pós-processado ou ambos.

Para saber mais sobre como executar essas transformações usando o Serviço de Consulta, consulte [funções definidas por Adobe](/help/query-service/sql/adobe-defined-functions.md) no guia do usuário do Serviço de Consulta.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | sequência de caracteres | eVars personalizadas do Analytics. Cada organização pode usar eVars de forma diferente. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | sequência de caracteres | Propriedades personalizadas do Analytics. Cada organização pode usar props de forma diferente. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | inteiro | A altura do navegador, em pixels. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | inteiro | A largura do navegador, em pixels. |
| `post_campaign` | `marketing.trackingCode` | sequência de caracteres | A variável usada na dimensão Código de rastreamento. |
| `post_channel` | `web.webPageDetails.siteSection` | sequência de caracteres | A variável usada na dimensão Seções do site. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | sequência de caracteres | A ID de visitante personalizada, se definida. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | sequência de caracteres | O URL da primeira página que o visitante acessa. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | sequência de caracteres | Uma variável usada na dimensão Original da página de entrada. O nome da página de entrada do visitante. |
| `post_keywords` | `search.keywords` | sequência de caracteres | As palavras-chave coletadas para a ocorrência. |
| `post_page_url` | `web.webPageDetails.URL` | sequência de caracteres | O URL da ocorrência da página. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | sequência de caracteres | É igual a 1 nas ocorrências que têm um nome de página. É semelhante à métrica Exibições de página do Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | sequência de caracteres | Variável usada para identificar compras de maneira exclusiva. |
| `post_referrer` | `web.webReferrer.URL` | sequência de caracteres | O URL da página anterior. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | sequência de caracteres | Variável de estado. |
| `post_user_server` | `web.webPageDetails.server` | sequência de caracteres | Uma variável usada na dimensão Servidor. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | sequência de caracteres | Uma variável usada para preencher a dimensão CEP. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | inteiro | A ID numérica do navegador. |
| `domain` | `environment.domain` | sequência de caracteres | A variável usada na dimensão Domínio. Ele se baseia no provedor de serviços de Internet (ISP) do usuário. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | sequência de caracteres | O primeiro URL de referência do visitante. |
| `geo_city` | `placeContext.geo.city` | sequência de caracteres | O nome da cidade da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `geo_dma` | `placeContext.geo.dmaID` | inteiro | A ID numérica da área demográfica para a ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `geo_region` | `placeContext.geo.stateProvince` | sequência de caracteres | O nome do estado ou da região da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `geo_zip` | `placeContext.geo.postalCode` | sequência de caracteres | O CEP da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | inteiro | A ID numérica que representa o sistema operacional do visitante. Isso é baseado na coluna user_agent. |
| `search_page_num` | `search.pageDepth` | inteiro | Essa variável é usada pela dimensão Todas as classificações da página de pesquisa e indica qual página de resultados de pesquisa seu site | apareceu em antes de o usuário clicar em seu site. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | sequência de caracteres | Uma variável usada na dimensão Palavras-chave de pesquisa. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | inteiro | Uma variável usada na dimensão Número de visitas. Isso começa em 1, e incrementa a cada início de nova visita (por usuário). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | inteiro | Uma variável usada na dimensão Profundidade da ocorrência. Esse valor aumenta em uma unidade para cada ocorrência gerada pelo usuário e é redefinido após cada visita. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | sequência de caracteres | O primeiro referenciador da visita. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | inteiro | O primeiro Nome da página da visita. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Props personalizadas do Analytics, configuradas para serem propriedades de lista. Ela contém uma lista delimitada de valores. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Usado por variáveis de hierarquia e contém uma lista delimitada de valores. | {values (matriz), delimitador (cadeia de caracteres)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Uma lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variável usada na dimensão Suporte a cookies. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comércio padrão acionados na ocorrência. | {id (string), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados acionados na ocorrência. | {id (Objeto), value (Objeto)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Um sinalizador que indica se o Java™ está ativado. |
| `post_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | sequência de caracteres | O tipo de ocorrência enviado na solicitação da imagem (ocorrência padrão, link de download, link de saída ou link personalizado clicado). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | número | É igual a 1 se a ocorrência for um clique de link. É semelhante à métrica Eventos de página no Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | sequência de caracteres | Essa variável é usada somente em solicitações de imagem de rastreamento de link. É o URL do link de download, link de saída, ou link personalizado clicado. |
| `post_page_event_var2` | `web.webInteraction.name` | sequência de caracteres | Essa variável é usada somente em solicitações de imagem de rastreamento de link. É o nome personalizado do link. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | booleano | Isso é usado para preencher a dimensão Páginas não encontradas. Essa variável deve estar vazia ou conter &quot;ErrorPage&quot; |
| `post_pagename_no_url` | `web.webPageDetails.name` | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado vazio. |
| `post_product_list` | `productListItems[].items` | matriz | A lista de produtos, conforme enviado por meio da variável products. | {SKU (string), quantidade (inteiro), priceTotal (número)} |
| `post_search_engine` | `search.searchEngine` | sequência de caracteres | A ID numérica que representa o mecanismo de pesquisa que direcionou o visitante ao seu site. |
| `mvvar1_instances` | `.list.items[]` | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| `mvvar2_instances` | `.list.items[]` | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| `mvvar3_instances` | `.list.items[]` | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| `color` | `device.colorDepth` | inteiro | ID de Intensidade de cor, com base no valor da coluna c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | sequência de caracteres | A ID numérica, que representa o tipo do primeiro referenciador do visitante. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | inteiro | Carimbo de data e hora da primeira ocorrência do visitante no horário UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | sequência de caracteres | Abreviação do país no qual a ocorrência foi originada, com base no IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | booleano | Um sinalizador que é definido se a ocorrência corresponder à detecção de pesquisa paga. |
| `ref_type` | `web.webReferrer.type` | sequência de caracteres | Uma ID numérica que representa o tipo de referência para a ocorrência. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booleano | Um sinalizador (1=pago, 0=não pago) indicando se a primeira ocorrência da visita foi de uma ocorrência de pesquisa paga. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | sequência de caracteres | ID numérica que representa o tipo do primeiro referenciador da visita. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | sequência de caracteres | ID numérica do primeiro mecanismo de pesquisa da visita. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | inteiro | Carimbo de data e hora da primeira ocorrência da visita em horário UNIX®. |

{style="table-layout:auto"}