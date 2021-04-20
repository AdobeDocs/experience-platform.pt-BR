---
keywords: Experience Platform, home, tópicos populares, campos de mapeamento do Analytics, mapeamento do analytics
solution: Experience Platform
title: Mapeamento de campos para o conector de origem do Adobe Analytics
topic-legacy: overview
description: O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do ADC (Conector de dados do Analytics). Alguns dos dados assimilados por meio do ADC podem ser mapeados diretamente dos campos do Analytics para campos do Experience Data Model (XDM), enquanto outros dados exigem transformações e funções específicas para serem mapeados com êxito.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '3405'
ht-degree: 13%

---

# Mapeamentos de campo do Analytics

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do ADC (Conector de dados do Analytics). Alguns dos dados assimilados por meio do ADC podem ser mapeados diretamente dos campos do Analytics para campos do Experience Data Model (XDM), enquanto outros dados exigem transformações e funções específicas para serem mapeados com êxito.

![](../images/analytics-data-experience-platform.png)

## Campos de mapeamento direto

Os campos selecionados são mapeados diretamente do Adobe Analytics para o Experience Data Model (XDM).

A tabela a seguir inclui colunas que mostram o nome do campo do Analytics (*campo do Analytics*), o campo XDM correspondente (*campo XDM*) e seu tipo (*XDM type*), bem como uma descrição do campo (*Descrição*).

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Uma variável personalizada, que pode variar de 1 a 250. Cada organização usará essas eVars personalizadas de forma diferente. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variáveis de tráfego personalizadas, que podem variar de 1 a 75. |
| m_browser | _experience.analytics.environment.browserID | integer | A ID do número do navegador. |
| m_browser_height | environment.browserDetails.viewportHeight | integer | A altura do navegador, em pixels. |
| m_browser_width | environment.browserDetails.viewportWidth | integer | A largura do navegador, em pixels. |
| m_campaign | marketing.trackingCode | string | A variável usada na dimensão Código de rastreamento. |
| m_channel | web.webPageDetails.siteSection | string | A variável usada na dimensão Seções do site. |
| m_domain | environment.domain | string | A variável usada na dimensão Domínio . Isso será baseado no provedor de serviço de Internet (ISP) do usuário. |
| m_geo_city | placeContext.geo.city | string | O nome da cidade da ocorrência. Isso é baseado no endereço IP da ocorrência. |
| m_geo_dma | placeContext.geo.dmaID | integer | A ID numérica da área demográfica para a ocorrência. Isso é baseado no endereço IP da ocorrência. |
| m_geo_region | placeContext.geo.stateProvince | string | O nome do estado ou região da ocorrência. Isso é baseado no endereço IP da ocorrência. |
| m_geo_zip | placeContext.geo.postalCode | string | O CEP da ocorrência. Isso é baseado no endereço IP da ocorrência. |
| m_keywords | search.keywords | string | A variável usada na dimensão Palavra-chave. |
| m_os | _experience.analytics.environment.operationSystemID | integer | A ID numérica que representa o sistema operacional do visitante. Isso é baseado na coluna user_agent. |
| m_page_url | web.webPageDetails.URL | string | O URL da ocorrência da página. |
| m_pagename_no_url | web.webPageDetails.</span>name | string | Uma variável usada para preencher a dimensão Páginas. |
| m_referrer | web.webReferrer.URL | string | O URL da página anterior. |
| m_search_page_num | search.pageDepth | integer | Usado pela dimensão Todas as classificações da página de pesquisa. Indica em qual página de resultados de pesquisa seu site foi exibido antes de o visitante clicar no seu site. |
| m_state | _experience.analytics.customDimensions.stateProvincia | string | Variável de estado. |
| m_user_server | web.webPageDetails.server | string | Uma variável usada na dimensão Servidor . |
| m_zip | _experience.analytics.customDimensions.postalCode | string | Uma variável usada para preencher a dimensão CEP. |
| accept_language | environment.browserDetails.acceptLanguage | string | Lista todos os idiomas aceitos, conforme indicado no cabeçalho HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booleano | Não está mais em uso. Indicado se o URL atual é a página inicial do navegador. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | A versão do JavaScript suportada pelo navegador. |
| user_agent | environment.browserDetails.userAgent | string | A sequência de agente do usuário enviada no cabeçalho HTTP. |
| mobileappid | application.</span>name | string | A ID do aplicativo móvel, armazenada no seguinte formato: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | string | O nome do dispositivo móvel. No iOS, ele é armazenado como uma sequência de 2 dígitos separada por vírgulas. O primeiro número representa a geração do dispositivo e o segundo representa a família do dispositivo. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | string | Usada pelos serviços móveis. Representa o ponto de interesse. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | número | Usada pelos serviços móveis. Representa a distância do ponto de interesse. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | número | Coletada da variável de dados de contexto a.loc.acc. Indica a precisão do GPS em metros no momento da coleta. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | string | Coletada da variável de dados de contexto a.loc.category. Descreve a categoria de um local específico. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | string | Coletada da variável de dados de contexto a.loc.id. Identificador para um determinado ponto de interesse. |
| vídeo | media.mediaTimed.primaryAssetReference._id | string | O nome do vídeo. |
| videoad | advertising.adAssetReference._id | string | Identificador do ativo de anúncio. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | O Tipo De Conteúdo Do Vídeo. Isso é automaticamente definido como &quot;Vídeo&quot; para todas as visualizações de vídeo. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | O pod no qual o anúncio de vídeo está. |
| videoadinpod | advertising.adAssetViewDetails.index | integer | A posição do anúncio de vídeo no pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | O nome do reprodutor de vídeo. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | O Canal de vídeo. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | O nome do reprodutor do anúncio de vídeo. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | O nome do capítulo Vídeo |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | string | O nome do Vídeo. |
| videoadname | advertising.adAssetReference._dc.title | string | O nome do anúncio de vídeo. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Exibição de vídeo. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Temporada de vídeo. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episódio._iptc4xmpExt.Name | string | Episódio de vídeo. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Rede de vídeo. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Tipo de exibição de vídeo. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Cargas de vídeos e anúncios. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Tipo de feed do vídeo. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | número | Beacon do Mobile Services maior. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | número | Beacon do Mobile Services menor. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | UUID de beacon do Mobile Services. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID da sessão de vídeo. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Gênero | array | Gênero de vídeo. | {title (Object), descrição (Object), tipo (Object), meta:xdmType (Object), itens (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Objeto | Isso é acionado na primeira execução após a instalação ou reinstalação | {id (cadeia de caracteres), valor (número)} |
| mobileupgrades | application.upgrades | Objeto | Relata a quantidade de atualizações do aplicativo. Acionadores na primeira execução após a atualização ou quando o número da versão mudar. | {id (cadeia de caracteres), valor (número)} |
| mobilelaunches | application.launches | Objeto | O número de vezes que o aplicativo foi iniciado. | {id (cadeia de caracteres), valor (número)} |
| mobilecrashes | application.crashes | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| mobilemessageclicks | directMarketing.clicks | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videotime | media.mediaTimed.timePlayed | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videostart | media.mediaTimed.impressions | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videocomplete | media.mediaTimed.completes | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoadstart | advertising.impressions | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoadcomplete | advertising.completes | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoadtime | advertising.timePlayed | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoplay | media.mediaTimed.starts | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objeto | O tempo de início da qualidade do vídeo. | {id (cadeia de caracteres), valor (número)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objeto | Contagem de buffer de qualidade do vídeo | {id (cadeia de caracteres), valor (número)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objeto | Tempo de buffer de qualidade do vídeo | {id (cadeia de caracteres), valor (número)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objeto | Contagem de alternância de qualidade do vídeo | {id (cadeia de caracteres), valor (número)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objeto | Taxa média de bits de qualidade do vídeo | {id (cadeia de caracteres), valor (número)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objeto | Contagem de erros de qualidade do vídeo | {id (cadeia de caracteres), valor (número)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoprogress10 | media.mediaTimed.progress10 | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoprogress25 | media.mediaTimed.progress25 | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoprogress50 | media.mediaTimed.progress50 | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoprogress75 | media.mediaTimed.progress75 | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoprogress95 | media.mediaTimed.progress95 | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videoresume | media.mediaTimed.resumes | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videopausecount | media.mediaTimed.pauses | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videopausetime | media.mediaTimed.pauseTime | Objeto | <!-- MISSING --> | {id (cadeia de caracteres), valor (número)} |
| videosessincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | integer |

{style=&quot;table-layout:auto&quot;}

## Dividir campos de mapeamento

Esses campos têm uma única fonte, mas mapeiam para **vários** locais XDM.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | integer | ID numérica que representa a resolução do monitor. |
| mobileosversion | environment.operationSystem, environment.operationSystemVersion | string | Versão do sistema operacional móvel. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | integer | Duração do anúncio de vídeo. |

{style=&quot;table-layout:auto&quot;}

## Campos de mapeamento gerados

Selecionar campos provenientes do ADC precisam ser transformados, exigindo lógica além de uma cópia direta do Adobe Analytics para serem gerados no XDM.

A tabela a seguir inclui colunas que mostram o nome do campo do Analytics (*campo do Analytics*), o campo XDM correspondente (*campo XDM*) e seu tipo (*XDM type*), bem como uma descrição do campo (*Descrição*).

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variáveis de tráfego personalizadas, variando de 1 a 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hieries.hier1 - _experience.analytics.customDimensions.hierarquias.hier5 | Objeto | Usado por variáveis de hierarquia. Ele contém um | lista de valores delimitada. | {values (matriz), delimitador (cadeia de caracteres)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.list3.list[] | array | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação | {value (cadeia de caracteres), key (cadeia de caracteres)} |
| m_color | device.colorDepth | integer | A ID da profundidade de cor, que se baseia no valor da coluna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booleano | Uma variável usada na dimensão Suporte a cookies. |
| m_event_list | commerce.compras, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemoments, commerce.productListViews, commerce.productListViews | Objeto | Eventos de comércio padrão acionados na ocorrência. | {id (cadeia de caracteres), valor (número)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event20 _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objeto | Eventos personalizados acionados na ocorrência. | {id (Objeto), valor (Objeto)} |
| m_geo_country | placeContext.geo.countryCode | string | Abreviação do país de onde a ocorrência veio, que é baseada fora do IP. |
| m_geo_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booleano | Um sinalizador que indica se o Java está ativado. |
| m_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | string | Uma variável que é usada somente em solicitações de imagem de rastreamento de link. Essa variável contém o URL do link de download, do link de saída ou do link personalizado clicado. |
| m_page_event_var2 | web.webInteraction.name | string | Uma variável que é usada somente em solicitações de imagem de rastreamento de link. Isso lista o nome personalizado do link, se ele for especificado. |
| m_page_type | web.webPageDetails.isErrorPage | booleano | Uma variável usada para preencher a dimensão Páginas não encontradas . Essa variável deve estar vazia ou conter &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado em branco. |
| m_paid_search | search.isPaid | booleano | Um sinalizador que é definido se a ocorrência corresponder à detecção de pesquisa paga. |
| m_product_list | productListItems[].items | array | A lista de produtos, conforme passada pela variável de produtos. | {SKU (cadeia de caracteres), quantidade (número inteiro), priceTotal (número)} |
| m_ref_type | web.webReferrer.type | string | Uma ID numérica que representa o tipo de referência para a ocorrência. 1 significa que, dentro do site, 2 significa outros sites, 3 significa mecanismos de pesquisa, 4 significa disco rígido, 5 significa USENET, 6 significa Digitado/Marcado (sem referenciador), 7 significa email, 8 significa Sem JavaScript e 9 significa Redes sociais. |
| m_search_engine | search.searchEngine | string | A ID numérica que representa o mecanismo de pesquisa que enviou o visitante para o site. |
| post_currency | commerce.order.currencyCode | string | O código de câmbio que foi usado durante a transação. |
| post_cust_hit_time_gmt | carimbo de data e hora | string | Isso é usado somente em conjuntos de dados com carimbo de data e hora ativado. Este é o carimbo de data e hora enviado com ele, com base no horário Unix. |
| post_cust_visid | identityMap | objeto | A ID de visitante do cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | booleano | A ID de visitante do cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | string | A ID de visitante do cliente. |
| post_visid_high + visid_low | identityMap | objeto | Um identificador exclusivo para uma visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | string | Um identificador exclusivo para uma visita. |
| post_visid_high | endUserIDs._experience.aaid.primary | booleano | Usado em conjunto com visid_low para identificar uma visita de maneira exclusiva. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | string | Usado em conjunto com visid_low para identificar uma visita de maneira exclusiva. |
| post_visid_low | identityMap | objeto | Usado em conjunto com visid_high para identificar uma visita de maneira exclusiva. |
| hit_time_gmt | receiveTimestamp | string | O carimbo de data e hora da ocorrência, com base em horário Unix. |
| hitid_high + hitid_low | _id | string | Um identificador exclusivo para identificar uma ocorrência. |
| hitid_low | _id | string | Usado em conjunto com hitid_high para identificar uma ocorrência de maneira exclusiva. |
| ip | environment.ipV4 | string | O Endereço IP, com base no cabeçalho HTTP da solicitação de imagem. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booleano | A versão do JavaScript usada. |
| mcvisid_high + mcvisid_low | identityMap | objeto | A ID de visitante do Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | string | A ID de visitante do Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.primary | booleano | A ID de visitante do Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | string | A ID de visitante do Experience Cloud. |
| mcvisid_low | identityMap | objeto | A ID de visitante do Experience Cloud. |
| sdid_high + sdid_low | _experience.target.plementalDataID | string | ID de identificação de ocorrência. O campo de análise sdid_high e sdid_low é a ID de dados complementares usada para unir duas (ou mais) ocorrências recebidas. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Proximidade de beacon do Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | integer | O nome do capítulo do vídeo. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | integer | A duração do vídeo. |

{style=&quot;table-layout:auto&quot;}

## Campos de mapeamento avançados

Selecione os campos (conhecidos como &quot;postvalues&quot;) que exigem transformações mais avançadas antes de serem mapeados com êxito dos campos do Adobe Analytics para o Experience Data Model (XDM). A execução dessas transformações avançadas envolve o uso do Serviço de query da Adobe Experience Platform e funções pré-criadas (chamadas de funções definidas pelo Adobe) para sessão, atribuição e desduplicação.

Para saber mais sobre como executar essas transformações usando o Serviço de query, visite a documentação [Adobe-defined functions](../../../../query-service/sql/adobe-defined-functions.md).

A tabela a seguir inclui colunas que mostram o nome do campo do Analytics (*campo do Analytics*), o campo XDM correspondente (*campo XDM*) e seu tipo (*XDM type*), bem como uma descrição do campo (*Descrição*).

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Campo do Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Uma variável personalizada, que pode variar de 1 a 250. Cada organização usará essas eVars personalizadas de forma diferente. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variáveis de tráfego personalizadas, que podem variar de 1 a 75. |
| post_browser_height | environment.browserDetails.viewportHeight | integer | A altura do navegador, em pixels. |
| post_browser_width | environment.browserDetails.viewportWidth | integer | A largura do navegador, em pixels. |
| post_campaign | marketing.trackingCode | string | A variável usada na dimensão Código de rastreamento. |
| post_channel | web.webPageDetails.siteSection | string | A variável usada na dimensão Seções do site. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | string | A ID de visitante personalizada, se configurada. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | O URL da primeira página que o visitante chega. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | Uma variável usada na dimensão Página de entrada original . O nome da página da página de entrada do visitante. |
| post_keywords | search.keywords | string | As palavras-chave que foram coletadas para a ocorrência. |
| post_page_url | web.webPageDetails.URL | string | O URL da ocorrência da página. |
| post_pagename_no_url | web.webPageDetails.name | string | Uma variável usada para preencher a dimensão Páginas. |
| post_purchaseid | commerce.order.purchaseID | string | Variável usada para identificar compras de maneira exclusiva. |
| post_referrer | web.webReferrer.URL | string | O URL da página anterior. |
| post_state | _experience.analytics.customDimensions.stateProvincia | string | Variável de estado. |
| post_user_server | web.webPageDetails.server | string | Uma variável usada na dimensão Servidor . |
| post_zip | _experience.analytics.customDimensions.postalCode | string | Uma variável usada para preencher a dimensão CEP. |
| navegador | _experience.analytics.environment.browserID | integer | A ID numérica do navegador. |
| domínio | environment.domain | string | A variável usada na dimensão Domínio . Isso será baseado no provedor de serviço de Internet (ISP) do usuário. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | O primeiro URL de referência do visitante. |
| geo_city | placeContext.geo.city | string | O nome da cidade da ocorrência. Isso é baseado no endereço IP da ocorrência. |
| geo_dma | placeContext.geo.dmaID | integer | A ID numérica da área demográfica para a ocorrência. Isso é baseado no endereço IP da ocorrência. |
| geo_region | placeContext.geo.stateProvince | string | O nome do estado ou região da ocorrência. Isso é baseado no endereço IP da ocorrência. |
| geo_zip | placeContext.geo.postalCode | string | O CEP da ocorrência. Isso é baseado no endereço IP da ocorrência. |
| os | _experience.analytics.environment.operationSystemID | integer | A ID numérica que representa o sistema operacional do visitante. Isso é baseado na coluna user_agent. |
| search_page_num | search.pageDepth | integer | Essa variável é usada pela dimensão Toda classificação da página de pesquisa e indica qual página de resultados de pesquisa site | apareceu em antes do usuário clicar para acessar seu site. |
| visit_keywords | _experience.analytics.session.search.keywords | string | Uma variável usada na dimensão Palavras-chave de pesquisa. |
| visit_num | _experience.analytics.session.num | integer | Uma variável usada na dimensão Número de visitas. Isso começa em 1 e é incrementado sempre que uma nova visita é iniciada (por usuário). |
| visit_page_num | _experience.analytics.session.depth | integer | Uma variável usada na dimensão Profundidade da ocorrência. Esse valor aumenta em uma unidade para cada ocorrência gerada pelo usuário e é redefinido após cada visita. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | string | O primeiro referenciador da visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | integer | Nome da primeira página da visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variáveis de tráfego personalizadas 1 - 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hieries.hier1 - _experience.analytics.customDimensions.hierarquias.hier5 | Objeto | Usado por variáveis de hierarquia e contém uma lista delimitada de valores. | {values (matriz), delimitador (cadeia de caracteres)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.list3.list[] | array | Uma lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. | {value (cadeia de caracteres), key (cadeia de caracteres)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booleano | Variável usada na dimensão Suporte a cookies. |
| post_event_list | commerce.compras, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemoments, commerce.productListViews, commerce.productListViews | Objeto | Eventos de comércio padrão acionados na ocorrência. | {id (cadeia de caracteres), valor (número)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event20 _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objeto | Eventos personalizados acionados na ocorrência. | {id (Objeto), valor (Objeto)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booleano | Um sinalizador que indica se o Java está ativado. |
| post_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | string | O tipo de ocorrência que é enviado na solicitação da imagem (ocorrência padrão, link de download, link de saída ou link personalizado clicado). |
| post_page_event | web.webInteraction.linkClicks.value | número | O tipo de ocorrência que é enviado na solicitação da imagem (ocorrência padrão, link de download, link de saída ou link personalizado clicado). |
| post_page_event_var1 | web.webInteraction.URL | string | Essa variável é usada somente nas solicitações de imagem de rastreamento de link. Este é o URL do link de download, link de saída ou link personalizado clicado. |
| post_page_event_var2 | web.webInteraction.name | string | Essa variável é usada somente nas solicitações de imagem de rastreamento de link. Esse será o nome personalizado do link. |
| post_page_type | web.webPageDetails.isErrorPage | booleano | Isso é usado para preencher a dimensão Páginas não encontradas . Essa variável deve estar vazia ou conter &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado em branco. |
| post_product_list | productListItems[].items | array | A lista de produtos, conforme passada pela variável de produtos. | {SKU (cadeia de caracteres), quantidade (número inteiro), priceTotal (número)} |
| post_search_engine | search.searchEngine | string | A ID numérica que representa o mecanismo de pesquisa que enviou o visitante para o site. |
| mvvar1_instances | .list.items[] | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| mvvar2_instances | .list.items[] | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
|  | mvvar3_instances | .list.items[] | Objeto | Lista de valores de variável. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| color | device.colorDepth | integer | ID da profundidade de cor, com base no valor da coluna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | A ID numérica, que representa o tipo do referenciador do primeiro referenciador do visitante. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | integer | Carimbo de data e hora, em horário Unix, da primeira ocorrência de um visitante. |
| geo_country | placeContext.geo.countryCode | string | Abreviação do país no qual a ocorrência foi originada, com base no IP. |
| geo_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| paid_search | search.isPaid | booleano | Um sinalizador que é definido se a ocorrência corresponder à detecção de pesquisa paga. |
| ref_type | web.webReferrer.type | string | Uma ID numérica que representa o tipo de referência para a ocorrência. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booleano | Um sinalizador (1=pago, 0=não pago) indicando se a primeira ocorrência da visita foi de uma ocorrência de pesquisa paga. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | string | ID numérica que representa o tipo do primeiro referenciador da visita. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | string | ID numérica do primeiro mecanismo de pesquisa da ocorrência. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | integer | Carimbo de data e hora da primeira ocorrência da visita em horário Unix. |

{style=&quot;table-layout:auto&quot;}