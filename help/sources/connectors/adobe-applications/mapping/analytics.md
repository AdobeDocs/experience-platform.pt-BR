---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Campos de mapeamento do Analytics
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '3328'
ht-degree: 11%

---


# Campos de mapeamento do Analytics

O Adobe Experience Platform permite que você ingira dados do Adobe Analytics por meio do Analytics Data Connector (ADC). Alguns dos dados ingeridos por meio do ADC podem ser mapeados diretamente dos campos Analytics para os campos do Modelo de dados de experiência (XDM), enquanto outros dados exigem transformações e funções específicas para serem mapeados com êxito.

![](../images/analytics-data-experience-platform.png)

## Campos de mapeamento direto

Os campos selecionados são mapeados diretamente do Adobe Analytics para o Experience Data Model (XDM).

A tabela a seguir inclui colunas que mostram o nome do campo Analytics (campo ** Analytics), o campo XDM correspondente (campo ** XDM) e seu tipo (tipo ** XDM), bem como uma descrição do campo (*Descrição*).

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Campo Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Uma variável personalizada, que pode variar de 1 a 250. Cada organização usará essas eVars personalizadas de forma diferente. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variáveis de tráfego personalizadas, que podem variar de 1 a 75. |
| m_browser | _experience.analytics.ambiente.browserID | integer | A ID do número do navegador. |
| m_browser_height | environment.browserDetails.viewportHeight | integer | A altura do navegador, em pixels. |
| m_browser_width | environment.browserDetails.viewportWidth | integer | A largura do navegador, em pixels. |
| m_campanha | marketing.trackingCode | string | A variável usada na dimensão Código de rastreamento. |
| m_canal | web.webPageDetails.siteSection | string | A variável usada na dimensão Seções do site. |
| m_domain | environment.domain | string | A variável usada na dimensão Domínio. Isso se baseará no provedor de serviço da Internet do usuário (ISP). |
| m_geo_city | placeContext.geo.city | string | O nome da cidade da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| m_geo_dma | placeContext.geo.dmaID | integer | A ID numérica da área demográfica para a ocorrência. Isso se baseia no endereço IP da ocorrência. |
| m_geo_region | placeContext.geo.stateProvince | string | O nome do estado ou região da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| m_geo_zip | placeContext.geo.postalCode | string | O código ZIP da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| m_keywords | search.keywords | string | A variável usada na dimensão Palavra-chave. |
| m_os | _experience.analytics.ambiente.operatingSystemID | integer | A ID numérica que representa o sistema operacional do visitante. Isso se baseia na coluna user_agent. |
| m_page_url | web.webPageDetails.URL | string | O URL da ocorrência da página. |
| m_pagename_no_url | web.webPageDetails.</span>name | string | Uma variável usada para preencher a dimensão Páginas. |
| m_quem indicou | web.webReferrer.URL | string | O URL da página anterior. |
| m_search_page_num | search.pageDepth | integer | Usada pela dimensão Toda classificação da página de pesquisa. Indica em qual página de resultados de pesquisa seu site foi exibido antes do usuário clicar no site. |
| m_state | _experience.analytics.customDimensions.stateProvince | string | Variável de estado. |
| m_user_server | web.webPageDetails.server | string | Uma variável usada na dimensão Servidor. |
| m_zip | _experience.analytics.customDimensions.postalCode | string | Uma variável usada para preencher a dimensão CEP. |
| accept_language | environment.browserDetails.acceptLanguage | string | Lista todos os idiomas aceitos, conforme indicado no cabeçalho HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booleano | Não está mais em uso. Indicado se o URL atual é a página inicial do navegador. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | A versão do JavaScript suportada pelo navegador. |
| user_agent | environment.browserDetails.userAgent | string | A string do agente do usuário enviada no cabeçalho HTTP. |
| mobileappid | application.</span>name | string | A ID do aplicativo móvel, armazenada no seguinte formato: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | string | O nome do dispositivo móvel. No iOS, ele é armazenado como uma sequência de 2 dígitos separada por vírgulas. O primeiro número representa a geração do dispositivo e o segundo número representa a família do dispositivo. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | string | Usada pelos serviços móveis. Representa o ponto de interesse. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | número | Usada pelos serviços móveis. Representa a distância do ponto de interesse. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | número | Coletada da variável de dados de contexto a.loc.acc. Indica a precisão do GPS em metros no momento da coleta. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | string | Coletada da variável de dados de contexto a.loc.category. Descreve a categoria de um local específico. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | string | Coletada da variável de dados de contexto a.loc.id. Identificador para um determinado ponto de interesse. |
| vídeo | media.mediaTimed.primaryAssetReference._id | string | O nome do vídeo. |
| videoad | advertising.adAssetReference._id | string | Identificador do ativo do anúncio. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | O Tipo De Conteúdo Do Vídeo. Isso é definido automaticamente como &quot;Vídeo&quot; para todas as visualizações de vídeo. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | O pod no qual o anúncio de vídeo está. |
| videoadinpod | advertising.adAssetViewDetails.index | integer | A posição do anúncio de vídeo no pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | O nome do player de vídeo. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | O canal Video. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | O nome do player do Anúncio de vídeo. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | O nome do capítulo Vídeo |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | string | O nome do Vídeo. |
| videoadname | advertising.adAssetReference._dc.title | string | O nome do anúncio de vídeo. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Exibição de vídeo. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Estação de vídeo. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episódio._iptc4xmpExt.Name | string | Episódio de vídeo. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Rede de vídeo. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Tipo de exibição de vídeo. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Cargas de vídeos e anúncios. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Tipo de feed do vídeo. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | número | Beacon do Mobile Services maior. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | número | Beacon do Mobile Services menor. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | UUID de beacon do Mobile Services. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID da sessão de vídeo. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | matriz | Gênero de vídeo. | {title (Object), descrição (Object), tipo (Object), meta:xdmType (Object), itens (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Objeto | Isso é acionado na primeira execução após a instalação ou reinstalação | {id (cadeia), valor (número)} |
| mobileupgrades | application.upgrades | Objeto | Relata o número de atualizações do aplicativo. Acionadores na primeira execução após a atualização ou a qualquer momento em que o número da versão for alterado. | {id (cadeia), valor (número)} |
| mobilelaunches | application.launches | Objeto | O número de vezes que o aplicativo foi iniciado. | {id (cadeia), valor (número)} |
| mobilecrashes | application.crashes | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| mobilemessageclicks | directMarketing.clicks | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videotime | media.mediaTimed.timePlayed | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videostart | media.mediaTimed.impressions | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videocomplete | media.mediaTimed.completes | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoadstart | advertising.impressions | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoadcomplete | advertising.completes | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoadtime | advertising.timePlayed | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoplay | media.mediaTimed.starts | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objeto | O tempo de start da qualidade do vídeo. | {id (cadeia), valor (número)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objeto | Contagem de buffer de qualidade do vídeo | {id (cadeia), valor (número)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objeto | Tempo de buffer de qualidade do vídeo | {id (cadeia), valor (número)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objeto | Contagem de alternância de qualidade do vídeo | {id (cadeia), valor (número)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objeto | Taxa média de bits de qualidade do vídeo | {id (cadeia), valor (número)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objeto | Contagem de erros de qualidade do vídeo | {id (cadeia), valor (número)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoprogress10 | media.mediaTimed.progress10 | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoprogress25 | media.mediaTimed.progress25 | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoprogress50 | media.mediaTimed.progress50 | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoprogress75 | media.mediaTimed.progress75 | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoprogress95 | media.mediaTimed.progress95 | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoresume | media.mediaTimed.resumes | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videopausecount | media.mediaTimed.pauses | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videopausetime | media.mediaTimed.pauseTime | Objeto | <!-- MISSING --> | {id (cadeia), valor (número)} |
| videoresincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | integer |

## Dividir campos de mapeamento

Esses campos têm uma única fonte, mas mapeiam para **várias** localizações XDM.

| Campo Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | integer | ID numérica que representa a resolução do monitor. |
| mobileosversion | ambiente.operatingSystem, ambiente.operatingSystemVersion | string | Versão do sistema operacional móvel. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | integer | Duração do anúncio de vídeo. |

## Campos de mapeamento gerados

Para serem gerados no XDM, é necessário transformar campos selecionados provenientes do ADC, exigindo lógica além de uma cópia direta da Adobe Analytics.

A tabela a seguir inclui colunas que mostram o nome do campo Analytics (campo ** Analytics), o campo XDM correspondente (campo ** XDM) e seu tipo (tipo ** XDM), bem como uma descrição do campo (*Descrição*).

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Campo Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variáveis de tráfego personalizadas, que variam de 1 a 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hieries.hier1 - _experience.analytics.customDimensions.hierarquias.hier5 | Objeto | Usada pelas variáveis de hierarquia. Contém um | lista de valores delimitada. | {values (array), delimitador (string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lista.lista1.lista[] - _experience.analytics.customDimensions.lista.lista3.lista[] | matriz | Lista de valores variáveis. Contém uma lista delimitada de valores personalizados, dependendo da implementação | {value (string), key (string)} |
| m_color | device.colorDepth | integer | A ID de profundidade de cor, que é baseada no valor da coluna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booleano | Uma variável usada na dimensão Suporte a cookies. |
| m_evento_lista | commerce.purch,, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemoments, commerce.productListViews | Objeto | eventos de comércio padrão acionados na ocorrência. | {id (cadeia), valor (número)} |
| m_evento_lista | _experience.analytics.evento1to100.evento1 - _experience.analytics.evento1to100.evento100, _experience.analytics.evento101to200.evento101 - _experience.analytics.evento101to20 0.evento200, _experience.analytics.evento201to300.evento201 - _experience.analytics.evento201to300.evento300, _experience.analytics.evento301to400.evento3 01 - _experience.analytics.evento301to400.evento400, _experience.analytics.evento401to500.evento401 - _experience.analytics.evento401to500.500, _experience .analytics.evento501to600.evento501 - _experience.analytics.evento501to600.evento600, _experience.analytics.evento601to700.evento601 - _experience.analytics.analytics.processors 601to700.evento700, _experience.analytics.evento701to800.evento701 - _experience.analytics.evento701to800.evento800, _experience.analytics.evento801to 900.evento801 - _experience.analytics.evento801 a900.evento900, _experience.analytics.evento901a1000.evento901 - _experience.analytics.evento901a100 10.evento | Objeto | eventos personalizados acionados na ocorrência. | {id (Objeto), valor (Objeto)} |
| m_geo_country | placeContext.geo.countryCode | string | Abreviação do país de onde veio a ocorrência, que é baseada fora do IP. |
| m_geo_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booleano | Um sinalizador que indica se o Java está ativado. |
| m_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| m_page_evento_var1 | web.webInteraction.URL | string | Uma variável que é usada somente em solicitações de imagem de rastreamento de link. Essa variável contém o URL do link de download, link de saída ou link personalizado clicado. |
| m_page_evento_var2 | web.webInteraction.name | string | Uma variável que é usada somente em solicitações de imagem de rastreamento de link. Isso lista o nome personalizado do link, se for especificado. |
| m_page_type | web.webPageDetails.isErrorPage | booleano | Uma variável usada para preencher a dimensão Páginas não encontradas. Essa variável deve estar vazia ou conter &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado em branco. |
| m_paid_search | search.isPaid | booleano | Um sinalizador que é definido se o hit corresponde à detecção de pesquisa paga. |
| m_product_lista | productListItems[].items | matriz | A lista do produto, como transmitida pela variável products. | {SKU (cadeia), quantidade (número inteiro), priceTotal (número)} |
| m_ref_type | web.webReferrer.type | string | Uma ID numérica que representa o tipo de referência para a ocorrência. 1 significa que dentro do site, 2 significa outros sites, 3 significa mecanismos de pesquisa, 4 significa disco rígido, 5 significa USENET, 6 significa Digitado/Marcado (sem quem indicou), 7 significa email, 8 significa Sem JavaScript e 9 significa Redes sociais. |
| m_search_engine | search.searchEngine | string | A ID numérica que representa o mecanismo de pesquisa que indicou o visitante para o site. |
| post_currency | commerce.order.currencyCode | string | O código de câmbio que foi usado durante a transação. |
| post_cust_hit_time_gmt | carimbo de data e hora | string | Isso é usado somente em conjuntos de dados com carimbo de data e hora. Este é o carimbo de data e hora enviado com ele, com base no horário Unix. |
| post_cust_visid | identityMap | objeto | A ID do visitante do cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.Primary | booleano | A ID do visitante do cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | string | A ID do visitante do cliente. |
| post_visid_high + visid_low | identityMap | objeto | Um identificador exclusivo para uma visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | string | Um identificador exclusivo para uma visita. |
| post_visid_high | endUserIDs._experience.aaid.Primary | booleano | Usado em conjunto com visid_low para identificar exclusivamente uma visita. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | string | Usado em conjunto com visid_low para identificar exclusivamente uma visita. |
| post_visid_low | identityMap | objeto | Usado em conjunto com visid_high para identificar exclusivamente uma visita. |
| hit_time_gmt | receiveTimestamp | string | O carimbo de data e hora da ocorrência, com base no horário Unix. |
| hitid_high + hitid_low | _id | string | Um identificador exclusivo para identificar uma ocorrência. |
| hitid_low | _id | string | Usado em conjunto com hitid_high para identificar exclusivamente uma ocorrência. |
| ip | environment.ipV4 | string | O Endereço IP, com base no cabeçalho HTTP da solicitação de imagem. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booleano | A versão do JavaScript usada. |
| mcvisid_high + mcvisid_low | identityMap | objeto | A ID do Visitante do Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | string | A ID do Visitante do Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.Primary | booleano | A ID do Visitante do Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | string | A ID do Visitante do Experience Cloud. |
| mcvisid_low | identityMap | objeto | A ID do Visitante do Experience Cloud. |
| sdid_high + sdid_low | _experience.público alvo.plementalDataID | string | ID de identificação de ocorrência. O campo sdid_high e sdid_low do Analytics é a ID de dados suplementar usada para unir duas (ou mais) ocorrências recebidas. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Proximidade de beacon do Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | integer | O nome do capítulo do vídeo. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | integer | A duração do vídeo. |

## Campos de mapeamento avançados

Os campos selecionados (conhecidos como &quot;pós-valores&quot;) exigem transformações mais avançadas antes de serem mapeados com êxito dos campos Adobe Analytics para o Experience Data Model (XDM). A execução dessas transformações avançadas envolve o uso do Serviço de Query do Adobe Experience Platfrom e funções pré-criadas (chamadas funções definidas pelo Adobe) para sessões, atribuições e desduplicação-duplicadas.

Para saber mais sobre como executar essas transformações usando o Serviço de Query, visite a documentação de funções [definidas pelo](../../../../query-service/sql/adobe-defined-functions.md) Adobe.

A tabela a seguir inclui colunas que mostram o nome do campo Analytics (campo ** Analytics), o campo XDM correspondente (campo ** XDM) e seu tipo (tipo ** XDM), bem como uma descrição do campo (*Descrição*).

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Campo Analytics | Campo XDM | Tipo XDM | Descrição |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Uma variável personalizada, que pode variar de 1 a 250. Cada organização usará essas eVars personalizadas de forma diferente. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variáveis de tráfego personalizadas, que podem variar de 1 a 75. |
| post_browser_height | environment.browserDetails.viewportHeight | integer | A altura do navegador, em pixels. |
| post_browser_width | environment.browserDetails.viewportWidth | integer | A largura do navegador, em pixels. |
| post_campanha | marketing.trackingCode | string | A variável usada na dimensão Código de rastreamento. |
| post_canal | web.webPageDetails.siteSection | string | A variável usada na dimensão Seções do site. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | string | A ID de visitante personalizada, se definida. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | O URL da primeira página que o visitante atinge. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | Uma variável usada na dimensão Original da página de entrada. O nome da página de entrada do visitante. |
| post_keywords | search.keywords | string | As palavras-chave que foram coletadas para a ocorrência. |
| post_page_url | web.webPageDetails.URL | string | O URL da ocorrência da página. |
| post_pagename_no_url | web.webPageDetails.name | string | Uma variável usada para preencher a dimensão Páginas. |
| post_purchaseid | commerce.order.purchaseID | string | Variável usada para identificar exclusivamente compras. |
| post_quem indicou | web.webReferrer.URL | string | O URL da página anterior. |
| post_state | _experience.analytics.customDimensions.stateProvince | string | Variável de estado. |
| post_user_server | web.webPageDetails.server | string | Uma variável usada na dimensão Servidor. |
| post_zip | _experience.analytics.customDimensions.postalCode | string | Uma variável usada para preencher a dimensão CEP. |
| navegador | _experience.analytics.ambiente.browserID | integer | A ID numérica do navegador. |
| domínio | environment.domain | string | A variável usada na dimensão Domínio. Isso se baseará no provedor de serviço da Internet do usuário (ISP). |
| first_hit_quem indicou | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | O primeiro URL de referência do visitante. |
| geo_city | placeContext.geo.city | string | O nome da cidade da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| geo_dma | placeContext.geo.dmaID | integer | A ID numérica da área demográfica para a ocorrência. Isso se baseia no endereço IP da ocorrência. |
| geo_region | placeContext.geo.stateProvince | string | O nome do estado ou região da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| geo_zip | placeContext.geo.postalCode | string | O código ZIP da ocorrência. Isso se baseia no endereço IP da ocorrência. |
| os | _experience.analytics.ambiente.operatingSystemID | integer | A ID numérica que representa o sistema operacional do visitante. Isso se baseia na coluna user_agent. |
| search_page_num | search.pageDepth | integer | Essa variável é usada pela dimensão Toda classificação da página de pesquisa e indica qual página de pesquisa resulta no site | apareceu antes do usuário clicar no site. |
| visit_keywords | _experience.analytics.session.search.keywords | string | Uma variável usada na dimensão Palavras-chave de pesquisa. |
| visit_num | _experience.analytics.session.num | integer | Uma variável usada na dimensão Número da visita. Isso start em 1 e aumenta cada vez que um novo start de visita (por usuário). |
| visit_page_num | _experience.analytics.session.deep | integer | Uma variável usada na dimensão Profundidade de ocorrência. Esse valor aumenta em 1 para cada ocorrência gerada pelo usuário e redefine após cada visita. |
| visit_quem indicou | _experience.analytics.session.web.web.referrer.URL | string | A primeira quem indicou da visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | integer | Nome da primeira página da visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variáveis de tráfego personalizadas 1-75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hieries.hier1 - _experience.analytics.customDimensions.hierarquias.hier5 | Objeto | Usada pelas variáveis de hierarquia e contém uma lista de valores delimitada. | {values (array), delimitador (string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lista.lista1.lista[] - _experience.analytics.customDimensions.lista.lista3.lista[] | matriz | Uma lista de valores variáveis. Contém uma lista delimitada de valores personalizados, dependendo da implementação. | {value (string), key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booleano | Variável usada na dimensão Suporte a cookies. |
| post_evento_lista | commerce.purch,, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemoments, commerce.productListViews | Objeto | eventos de comércio padrão acionados na ocorrência. | {id (cadeia), valor (número)} |
| post_evento_lista | _experience.analytics.evento1to100.evento1 - _experience.analytics.evento1to100.evento100, _experience.analytics.evento101to200.evento101 - _experience.analytics.evento101to20 0.evento200, _experience.analytics.evento201to300.evento201 - _experience.analytics.evento201to300.evento300, _experience.analytics.evento301to400.evento3 01 - _experience.analytics.evento301to400.evento400, _experience.analytics.evento401to500.evento401 - _experience.analytics.evento401to500.500, _experience .analytics.evento501to600.evento501 - _experience.analytics.evento501to600.evento600, _experience.analytics.evento601to700.evento601 - _experience.analytics.analytics.processors 601to700.evento700, _experience.analytics.evento701to800.evento701 - _experience.analytics.evento701to800.evento800, _experience.analytics.evento801to 900.evento801 - _experience.analytics.evento801 a900.evento900, _experience.analytics.evento901a1000.evento901 - _experience.analytics.evento901a100 10.evento | Objeto | eventos personalizados acionados na ocorrência. | {id (Objeto), valor (Objeto)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booleano | Um sinalizador que indica se o Java está ativado. |
| post_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| post_page_evento | web.webInteraction.type | string | O tipo de ocorrência que é enviado na solicitação de imagem (ocorrência padrão, link de download, link de saída ou link personalizado clicado). |
| post_page_evento | web.webInteraction.linkClicks.value | número | O tipo de ocorrência que é enviado na solicitação de imagem (ocorrência padrão, link de download, link de saída ou link personalizado clicado). |
| post_page_evento_var1 | web.webInteraction.URL | string | Essa variável é usada somente em solicitações de imagem de rastreamento de link. Este é o URL do link de download, link de saída ou link personalizado clicado. |
| post_page_evento_var2 | web.webInteraction.name | string | Essa variável é usada somente em solicitações de imagem de rastreamento de link. Esse será o nome personalizado do link. |
| post_page_type | web.webPageDetails.isErrorPage | booleano | Isso é usado para preencher a dimensão Páginas não encontradas. Essa variável deve estar vazia ou conter &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | número | O nome da página (se definido). Se nenhuma página for especificada, esse valor será deixado em branco. |
| post_product_lista | productListItems[].items | matriz | A lista do produto, como transmitida pela variável products. | {SKU (cadeia), quantidade (número inteiro), priceTotal (número)} |
| post_search_engine | search.searchEngine | string | A ID numérica que representa o mecanismo de pesquisa que indicou o visitante para o site. |
| mvvar1_instance | .lista.items[] | Objeto | Lista de valores variáveis. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| mvvar2_instance | .lista.items[] | Objeto | Lista de valores variáveis. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
|  | mvvar3_instance | .lista.items[] | Objeto | Lista de valores variáveis. Contém uma lista delimitada de valores personalizados, dependendo da implementação. |
| cor | device.colorDepth | integer | ID de profundidade de cor, com base no valor da coluna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | A ID numérica, que representa o tipo de quem indicou da primeira quem indicou do visitante. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | integer | Carimbo de data e hora, em horário Unix, da primeira ocorrência de um visitante. |
| geo_country | placeContext.geo.countryCode | string | Abreviação do país de onde o hit veio, com base no IP. |
| geo_latitude | placeContext.geo._schema.latitude | número | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | número | <!-- MISSING --> |
| paid_search | search.isPaid | booleano | Um sinalizador que é definido se o hit corresponde à detecção de pesquisa paga. |
| ref_type | web.webReferrer.type | string | Uma ID numérica que representa o tipo de referência para a ocorrência. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booleano | Um sinalizador (1=pago, 0=não pago) indicando se a primeira ocorrência da visita foi de uma ocorrência de pesquisa paga. |
| visit_ref_type | _experience.analytics.session.web.web.webReferrer.type | string | ID numérica que representa o tipo de quem indicou da primeira quem indicou da visita. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | string | ID numérica do primeiro mecanismo de pesquisa da visita. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | integer | Carimbo de data e hora da primeira ocorrência da visita no horário Unix. |
