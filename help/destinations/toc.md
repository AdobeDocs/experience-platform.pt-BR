---
product: experience-platform
audience: user
user-guide-title: Guia de destinos
user-guide-description: Ative seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.
description: Este documento lista o sumário para destinos do Adobe Experience Platform
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 11%

---


# Destinos {#destinations}

* [Visão geral dos destinos](./home.md)
* [Tipos de destino e categorias](./destination-types.md)
* Tutoriais de API {#api}
   * [Conecte-se a destinos de streaming e ative dados usando chamadas de API](./api/streaming-destinations.md)
   * [Conectar-se aos destinos de marketing de email e ativar dados usando chamadas de API](./api/email-marketing.md)
* Guias da interface {#ui}
   * [Visão geral da área de trabalho Destinos](./ui/destinations-workspace.md)
   * [Detalhes de destino da visualização](./ui/destination-details-page.md)
   * [Conectar-se a um destino](./ui/connect-destination.md)
   * [Ativar perfis e segmentos em um destino](./ui/activate-destinations.md)
* Catálogo de destinos {#catalog}
   * [Visão geral do catálogo de destinos](./catalog/overview.md)
   * [ (Alfa) Conexão HTTP](./catalog/http-destination.md)
   * destinos de Adobe{#adobe}
      * [Visão geral dos destinos de Adobe](./catalog/adobe/overview.md)
      * [compartilhamento de segmentos Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Destinos de publicidade{#advertising}
      * [Visão geral de destinos de publicidade](./catalog/advertising/overview.md)
      * [Extensão Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extensão da tag de conversão do anunciante Awin](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag extension](./catalog/advertising/awin-mastertag.md)
      * [Extensão UET (Rastreamento Universal de Eventos) do Bing Ads](./catalog/advertising/bing-ads.md)
      * [Extensão de ramificação](./catalog/advertising/branch.md)
      * [Extensão do DoubleClick Floodlight (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extensão de pixel do Facebook](./catalog/advertising/facebook-pixel.md)
      * [Extensão Flashspeak OneTag](./catalog/advertising/flashtalking.md)
      * [Conexão com o Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Extensão do Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Conexão com o Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [Conexão de correspondência de cliente do Google](./catalog/advertising/google-customer-match.md)
      * [Conexão com o Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
      * [Extensão do Google gtag](./catalog/advertising/gtag-advertising.md)
      * [Extensão da tag do LinkedIn Insight](./catalog/advertising/linkedin.md)
      * [Conexão do Microsoft Bing](./catalog/advertising/bing.md)
      * [Extensão de rastreamento de conversão do Pinterest](./catalog/advertising/pinterest.md)
      * [A conexão com o Trade Desk](./catalog/advertising/tradedesk.md)
      * [Extensão de tag do Twitter Universal Website](./catalog/advertising/twitter-uwt.md)
   * Destinos do Analytics {#analytics}
      * [Visão geral dos destinos do Analytics](./catalog/analytics/overview.md)
      * [Adicionar extensão de rastreamento de site](./catalog/analytics/adform.md)
      * [Extensão do Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Extensão Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Extensão Clicktale](./catalog/analytics/clicktale.md)
      * [Extensão Contentsquare](./catalog/analytics/contentsquare.md)
      * [Extensão decibel](./catalog/analytics/decibel.md)
      * [Extensão Demandbase](./catalog/analytics/demandbase.md)
      * [Extensão DialogTech](./catalog/analytics/dialogtech.md)
      * [Extensão da tag do site global do Google](./catalog/analytics/gtag-analytics.md)
      * [Extensão do Google Universal Analytics](./catalog/analytics/google-universal-analytics.md)
      * [Extensão do JW Player Analytics (Beta)](./catalog/analytics/jw-player-analytics.md)
      * [extensão Nielsen BSDK](./catalog/analytics/nielsen-bsdk.md)
      * [extensão Nielsen IMA Handler](./catalog/analytics/nielsen-ima.md)
      * [Extensão do manipulador Nielsen VideoJS Player](./catalog/analytics/nielsen-videojs.md)
      * [Extensão do Parse.ly Analytics](./catalog/analytics/parsely.md)
      * [Extensão da métrica quântica](./catalog/analytics/quantum-metric.md)
      * [Extensão SessionCam](./catalog/analytics/sessioncam.md)
      * [Extensão TMMData](./catalog/analytics/tmmdata.md)
      * [Extensão de rastreamento de conversão de texto](./catalog/analytics/yext.md)
   * Destinos do armazenamento na nuvem {#cloud-storage}
      * [Visão geral dos destinos de Armazenamentos na nuvem](./catalog/cloud-storage/overview.md)
      * [Criar um destino de armazenamento em nuvem](./catalog/cloud-storage/workflow.md)
      * [Conexão Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Conexão Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Conexão Blob do Azure](./catalog/cloud-storage/azure-blob.md)
      * [(Beta) Conexão de Hubs de Evento do Azure](./catalog/cloud-storage/azure-event-hubs.md)
      * [Conexão SFTP](./catalog/cloud-storage/sftp.md)
   * Destinos da plataforma de gestão de dados {#data-management}
      * [Visão geral dos destinos da Plataforma de gestão de dados (DMP)](./catalog/data-management/overview.md)
      * [extensão Audience Manager DIL](./catalog/data-management/aam-dil-extension.md)
   * Destinos de email {#email}
      * [Extensão bizível](./catalog/email/bizible.md)
      * [Extensão de marketing](./catalog/email/marketo.md)
      * [Extensão do Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [Extensão PebblePost](./catalog/email/pebblepost.md)
   * Destinos de marketing de email {#email-marketing}
      * [Visão geral dos destinos de marketing por email](./catalog/email-marketing/overview.md)
      * [Conexão Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Conexão oracle Eloqua](./catalog/email-marketing/oracle-eloqua.md)
      * [Conexão oracle Responsys](./catalog/email-marketing/oracle-responsys.md)
      * [Conexão de Marketing Cloud do Salesforce](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * extensões de Experience Platform Launch {#launch-extensions}
      * [Visão geral da extensão Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md)
   * Destinos de envolvimento móvel {#mobile-engagement}
      * [Visão geral dos destinos de envolvimento móvel](./catalog/mobile-engagement/overview.md)
      * [Ligação de atributos de dirigível](./catalog/mobile-engagement/airship-attributes.md)
      * [Ligação de Etiquetas de Avião](./catalog/mobile-engagement/airship-tags.md)
      * [Conexão com o Braze](./catalog/mobile-engagement/braze.md)
   * Destinos de personalização {#personalization}
      * [Visão geral dos destinos de personalização](./catalog/personalization/overview.md)
      * [Extensão do Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extensão do Adobe Target v2](./catalog/personalization/adobe-target-v2.md)
      * [Extensão de Beemray](./catalog/personalization/beemray.md)
      * [Extensão Inteligência do Visitante D&amp;B](./catalog/personalization/dnb.md)
      * [Extensão do Experience Cloud ID Service](./catalog/personalization/adobe-ecid.md)
      * [Extensão de gansight](./catalog/personalization/gainsight.md)
      * [Extensão KickFire](./catalog/personalization/kickfire.md)
      * [Extensão Marketo Web Personalization](./catalog/personalization/marketo-web-personalization.md)
   * Destinos de rede social{#social}
      * [Visão geral dos destinos de rede social](./catalog/social/overview.md)
      * [Criar um destino de rede social](./catalog/social/workflow.md)
      * [extensão Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Extensão do Facebook](./catalog/social/facebook.md)
   * Destinos de pesquisa {#survey}
      * [Visão geral dos destinos de pesquisa](./catalog/survey/overview.md)
      * [Destino da extensão anterior](./catalog/survey/foresee.md)
      * [Extensão InMoment](./catalog/survey/inmoment.md)
      * [Extensão de Comentários do Site Qualtrics](./catalog/survey/qualtrics.md)
      * [Extensão Pesquisas do Intercept do QuestionPro](./catalog/survey/web-intercept-surveys.md)
   * Voz dos destinos do cliente {#voice}
      * [Visão geral da voz dos destinos do Cliente](./catalog/voice/overview.md)
      * [Confirmar extensão de Comentários Digitais](./catalog/voice/confirmit-digital-feedback.md)
      * [Extensão Tags Invoca](./catalog/voice/invoca.md)
      * [Tensão de Medallia](./catalog/voice/medallia.md)
      * [Extensão da Caixa de Entrada do URL de Conversação](./catalog/voice/talkurl.md)
* [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)