---
audience: user
user-guide-title: Guia de destinos
user-guide-description: Ative seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.
description: Este documento lista o índice dos destinos do Adobe Experience Platform
feature: Destinations
source-git-commit: 9336545ce77406ca8b1a04d9b9c0ce7752aa9ce5
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 7%

---


# Destinos {#destinations}

* [Destinos visão geral](./home.md)
* [Tipos e categorias de destino](./destination-types.md)
* Tutoriais da API {#api}
   * [Conecte-se a destinos de fluxo e ative dados usando a API do Serviço de fluxo](./api/streaming-destinations.md)
   * [Conecte-se ao armazenamento em nuvem em lote e aos destinos de marketing por email e ative dados usando a API do Serviço de Fluxo](./api/connect-activate-batch-destinations.md)
   * [(Beta) Ativar segmentos de público-alvo para destinos em lote por meio da API de ativação ad-hoc](./api/ad-hoc-activation-api.md)
   * [Atualizar fluxos de dados de destino](./api/update-destination-dataflows.md)
   * [Excluir contas de destino](./api/delete-destination-account.md)
   * [Excluir fluxos de dados de destino](./api/delete-destination-dataflow.md)
* Guias da interface do usuário {#ui}
   * [Área de trabalho Destinos](./ui/destinations-workspace.md)
   * [Criar uma nova conexão de destino](./ui/connect-destination.md)
   * Ativar dados do público-alvo para destinos{#activate}
      * [Visão geral de Activation](./ui/activation-overview.md)
      * [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](./ui/activate-segment-streaming-destinations.md)
      * [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](./ui/activate-streaming-profile-destinations.md)
      * [Ativar dados do público-alvo para destinos de exportação de perfil em lote](./ui/activate-batch-profile-destinations.md)
      * [Ativar dados do público-alvo para destinos de solicitação de perfil](./ui/activate-profile-request-destinations.md)
      * [Configurar destinos de personalização para a personalização da mesma página e da próxima página](./ui/configure-personalization-destinations.md)
      * [(Beta) Exportar arquivos sob demanda para destinos em lote usando a interface do usuário do Experience Platform](./ui/export-file-now.md)
   * [Exibir detalhes do destino](./ui/destination-details-page.md)
   * [Atualizar contas de destino](./ui/update-accounts.md)
   * [Excluir contas de destino](./ui/delete-destination-account.md)
   * [Editar fluxos de dados de ativação](./ui/edit-activation.md)
   * [Excluir destinos](./ui/delete-destinations.md)
   * [Monitorar fluxos de dados](./ui/monitor-dataflows.md)
   * [Assinar alertas de destino no contexto](ui/alerts.md)
* Catálogo de destinos {#catalog}
   * [Visão geral do catálogo de destinos](./catalog/overview.md)
   * Destinos de Adobe{#adobe}
      * [Visão geral dos destinos Adobe](./catalog/adobe/overview.md)
      * [Marketo Engage connection](./catalog/adobe/marketo-engage.md)
      * [Compartilhamento de segmento Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Destinos de publicidade{#advertising}
      * [Visão geral de destinos de publicidade](./catalog/advertising/overview.md)
      * [Conexão Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Extensão do Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extensão de tag de conversão do Awin Advertiser](./catalog/advertising/awin-conversiontag.md)
      * [Extensão Awin Advertiser Mastertag](./catalog/advertising/awin-mastertag.md)
      * [Extensão Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Extensão de ramificação](./catalog/advertising/branch.md)
      * [(Beta) Conexão de critério](./catalog/advertising/criteo.md)
      * [Extensão DoubleClick Floodlight (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extensão facebook Pixel](./catalog/advertising/facebook-pixel.md)
      * [Extensão Flashtalk OneTag](./catalog/advertising/flashtalking.md)
      * [Conexão Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Extensão do Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Conexão com o Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Conexão com o Google Ad Manager 360](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Conexão Google Customer Match](./catalog/advertising/google-customer-match.md)
      * [Conexão Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
      * [Extensão de tag do Google](./catalog/advertising/gtag-advertising.md)
      * [Extensão de tag do linkedIn Insight](./catalog/advertising/linkedin.md)
      * [Conexão Microsoft Bing](./catalog/advertising/bing.md)
      * [Extensão de rastreamento de conversão do pinterest](./catalog/advertising/pinterest-extension.md)
      * [Conexão da Lista de clientes do pinterest](./catalog/advertising/pinterest.md)
      * [(Beta) Conexão de Anúncios em Snapchat](./catalog/advertising/snap-inc.md)
      * [A conexão com o Trade Desk](./catalog/advertising/tradedesk.md)
      * [(Beta) A conexão de CRM do Trade Desk](./catalog/advertising/tradedesk-emails.md)
      * [Extensão de tag do site universal do twitter](./catalog/advertising/twitter-uwt.md)
      * [Conexão de dados do Yahoo/Verizon](./catalog/advertising/datax.md)
   * Destinos do Analytics {#analytics}
      * [Visão geral dos destinos do Analytics](./catalog/analytics/overview.md)
      * [Adicionar extensão de rastreamento de site](./catalog/analytics/adform.md)
      * [Extensão do Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Extensão Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Extensão Clicktale](./catalog/analytics/clicktale.md)
      * [Extensão do Contentsquare](./catalog/analytics/contentsquare.md)
      * [Extensão Decibel](./catalog/analytics/decibel.md)
      * [Extensão do Demandbase](./catalog/analytics/demandbase.md)
      * [Extensão DialogTech](./catalog/analytics/dialogtech.md)
      * [Extensão de tag de site global do Google](./catalog/analytics/gtag-analytics.md)
      * [Extensão do Google Universal Analytics](./catalog/analytics/google-universal-analytics.md)
      * [Extensão JW Player Analytics (Beta)](./catalog/analytics/jw-player-analytics.md)
      * [Extensão BSDK da Nielsen](./catalog/analytics/nielsen-bsdk.md)
      * [Extensão Nielsen IMA Handler](./catalog/analytics/nielsen-ima.md)
      * [Extensão Nielsen VideoJS Player Handler](./catalog/analytics/nielsen-videojs.md)
      * [Extensão do Parse.ly Analytics](./catalog/analytics/parsely.md)
      * [Extensão de métrica quântica](./catalog/analytics/quantum-metric.md)
      * [Extensão SessionCam](./catalog/analytics/sessioncam.md)
      * [Extensão TMMData](./catalog/analytics/tmmdata.md)
      * [Extensão de rastreamento de conversão de texto](./catalog/analytics/yext.md)
   * Destinos de armazenamento na nuvem {#cloud-storage}
      * [Visão geral dos destinos de armazenamento na nuvem](./catalog/cloud-storage/overview.md)
      * [Conexão Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Conexão Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Conexão Blob do Azure](./catalog/cloud-storage/azure-blob.md)
      * [Conexão de Hubs de Eventos do Azure](./catalog/cloud-storage/azure-event-hubs.md)
      * [Conexão SFTP](./catalog/cloud-storage/sftp.md)
      * [Endereço IP lista de permissões para destinos de armazenamento em nuvem](./catalog/cloud-storage/ip-address-allow-list.md)
   * Destinos do Gerenciamento de Relacionamento com o Cliente (CRM) {#crm}
      * [Conexão Salesforce CRM](./catalog/crm/salesforce.md)
      * [Conexão de saída](catalog/crm/outreach.md)
   * Destinos da Plataforma de gerenciamento de dados {#data-management}
      * [Visão geral dos destinos da Plataforma de gerenciamento de dados (DMP)](./catalog/data-management/overview.md)
      * [Extensão Audience Manager DIL](./catalog/data-management/aam-dil-extension.md)
   * Destinos de email {#email}
      * [Extensão Bizible](./catalog/email/bizible.md)
      * [Extensão do Marketo](./catalog/email/marketo.md)
      * [Extensão do Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [Extensão PebblePost](./catalog/email/pebblepost.md)
   * Destinos de marketing por email {#email-marketing}
      * [Visão geral dos destinos de marketing por email](./catalog/email-marketing/overview.md)
      * [Conexão Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Conexão Adobe Campaign Managed Services](./catalog/email-marketing/adobe-campaign-managed-services.md)
      * [Conexão Eloqua do Oracle](./catalog/email-marketing/oracle-eloqua.md)
      * [Conexão Oracle Responsys](./catalog/email-marketing/oracle-responsys.md)
      * [(API) Conexão do Salesforce Marketing Cloud](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [(Arquivos) Conexão do Marketing Cloud Salesforce](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [Conexão SendGrid](./catalog/email-marketing/sendgrid.md)
   * Extensões de tag {#launch-extensions}
      * [Visão geral da extensão de tag](./catalog/launch-extensions/overview.md)
   * Destinos de envolvimento móvel {#mobile-engagement}
      * [Visão geral dos destinos de envolvimento móvel](./catalog/mobile-engagement/overview.md)
      * [Conexão de atributos de aeróstato](./catalog/mobile-engagement/airship-attributes.md)
      * [Ligação de Etiquetas de Avião](./catalog/mobile-engagement/airship-tags.md)
      * [Ligação de brasa](./catalog/mobile-engagement/braze.md)
   * Destinos de personalização {#personalization}
      * [Visão geral dos destinos de personalização](./catalog/personalization/overview.md)
      * [Conexão Adobe Target](./catalog/personalization/adobe-target-connection.md)
      * [Extensão do Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extensão do Adobe Target v2](./catalog/personalization/adobe-target-v2.md)
      * [Extensão do Beemray](./catalog/personalization/beemray.md)
      * [Conexão de personalização personalizada](./catalog/personalization/custom-personalization.md)
      * [Extensão Inteligência do visitante D&amp;B](./catalog/personalization/dnb.md)
      * [Extensão do Experience Cloud ID Service](./catalog/personalization/adobe-ecid.md)
      * [Extensão do Gainsight](./catalog/personalization/gainsight.md)
      * [Extensão KickFire](./catalog/personalization/kickfire.md)
      * [Extensão Marketo Web Personalization](./catalog/personalization/marketo-web-personalization.md)
      * [Conexão do Hub de decisão do cliente Pega](./catalog/personalization/pega.md)
   * Destinos sociais{#social}
      * [Visão geral dos destinos sociais](./catalog/social/overview.md)
      * [Extensão do Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Conexão facebook](./catalog/social/facebook.md)
      * [Conexão de públicos-alvo correspondentes ao linkedIn](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] conexão](./catalog/social/twitter.md)
   * Destinos de transmissão {#streaming}
      * [Conexão da API HTTP](./catalog/streaming/http-destination.md)
      * [Endereço IP lista de permissões para destinos de transmissão](./catalog/streaming/ip-address-allow-list.md)
   * Destinos da pesquisa {#survey}
      * [Visão geral dos destinos da pesquisa](./catalog/survey/overview.md)
      * [Destino da extensão da Foresee](./catalog/survey/foresee.md)
      * [Extensão InMoment](./catalog/survey/inmoment.md)
      * [Extensão de feedback do site do Qualtrics](./catalog/survey/qualtrics.md)
      * [Extensão Surveys do QuestionPro Intercept](./catalog/survey/web-intercept-surveys.md)
   * Voz dos destinos do cliente {#voice}
      * [Visão geral da voz dos destinos do cliente](./catalog/voice/overview.md)
      * [Confirmar extensão de Feedback digital](./catalog/voice/confirmit-digital-feedback.md)
      * [Extensão de Tags Invoca](./catalog/voice/invoca.md)
      * [Ligação Medallia](./catalog/voice/medallia-connector.md)
      * [Extensão Medallia](./catalog/voice/medallia.md)
      * [Extensão da Caixa de entrada do URL de conversa](./catalog/voice/talkurl.md)
* SDK de destino {#destination-sdk}
   * [Visão geral](./destination-sdk/overview.md)
   * [Pré-requisitos de integração](./destination-sdk/integration-prerequisites.md)
   * [Introdução](./destination-sdk/getting-started.md)
   * funcionalidade Destination SDK {#functionality}
      * [Opções de configuração](./destination-sdk/configuration-options.md)
      * [Configuração de destino de transmissão](./destination-sdk/destination-configuration.md)
      * [(Beta) Configuração de destino baseada em arquivo](./destination-sdk/file-based-destination-configuration.md)
      * [Especificações do servidor e do modelo de destinos de transmissão](./destination-sdk/server-and-template-configuration.md)
      * [(Beta) Destinos baseados em arquivo especificações do servidor e arquivo](./destination-sdk/server-and-file-configuration.md)
      * [Formato de mensagem](./destination-sdk/message-format.md)
      * [Gerenciamento de metadados do público-alvo](./destination-sdk/audience-metadata-management.md)
      * Autenticação {#authentication}
         * [Configuração de autenticação](./destination-sdk/authentication-configuration.md)
         * [Autenticação OAuth 2](./destination-sdk/oauth2-authentication.md)
      * Ferramentas do desenvolvedor {#developer-tools}
         * [Criar e testar um modelo de transformação de mensagem](./destination-sdk/create-template.md)
         * [Testar a configuração de destino](./destination-sdk/test-destination.md)
   * Operações de API {#api}
      * [Referência de API do Destination SDK (Destination Authoring)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [Operações de API do endpoint de destinos](./destination-sdk/destination-configuration-api.md)
      * [Operações da API de ponto de extremidade do servidor de destino](./destination-sdk/destination-server-api.md)
      * [Operações da API de ponto de extremidade de metadados de público-alvo](./destination-sdk/audience-metadata-api.md)
      * [Operações da API do endpoint de credenciais](./destination-sdk/credentials-configuration-api.md)
      * [Publicar operações da API de ponto de extremidade](./destination-sdk/destination-publish-api.md)
      * Referência de ferramentas do desenvolvedor {#developer-tools-reference}
         * API de teste de destino de transmissão {#streaming-destination-testing-api}
            * [Obter exemplos de operações da API de modelo](./destination-sdk/sample-template-api.md)
            * [Renderizar operações da API do modelo](./destination-sdk/render-template-api.md)
            * [Operações da API de teste de destino](./destination-sdk/destination-testing-api.md)
            * [Exemplos de operações da API de geração de perfil](./destination-sdk/sample-profile-generation-api.md)
         * API de teste de destino baseada em arquivo {#file-based-destination-testing-api}
            * [Visão geral da API de teste de destino baseada em arquivo](./destination-sdk/file-based-destination-testing-overview.md)
            * [Gerar perfis de amostra com base em um schema de origem](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [Teste seu destino baseado em arquivo com perfis de amostra](./destination-sdk/file-based-destination-testing-api.md)
            * [Exibir resultados detalhados da ativação](./destination-sdk/file-based-destination-results-api.md)
            * [Validar campos de clientes modelos](./destination-sdk/file-based-render-template-api.md)
   * Guias {#guides}
      * [Use o Destination SDK para configurar um destino de transmissão](./destination-sdk/configure-destination-instructions.md)
      * [(Beta) Use o Destination SDK para configurar um destino baseado em arquivo](./destination-sdk/configure-file-based-destination-instructions.md)
      * [Enviar para revisão de um destino criado no Destination SDK](./destination-sdk/submit-destination.md)
      * Configurar destinos com base em arquivo {#configure-file-based-destinations}
         * [(Beta) Configure um destino Amazon S3 com opções predefinidas de formatação de arquivo e configuração personalizada de nome de arquivo](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md)
         * [(Beta) Configure um destino do Amazon S3 com opções personalizadas de nome de arquivo e formatação](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-custom-file-formatting.md)
         * [(Beta) Configure um destino do Armazenamento Azure Blob com opções personalizadas de formatação de arquivos e configuração personalizada de nome de arquivo](../destinations/destination-sdk/guides/batch/configure-blob-destination-with-custom-file-formatting.md)
         * [(Beta) Configure um destino do Armazenamento do Azure Data Lake com opções personalizadas de formatação de arquivos e configuração personalizada de nome de arquivo](../destinations/destination-sdk/guides/batch/configure-adls-destination-with-custom-file-formatting.md)
         * [(Beta) Configure um destino de DLZ (Data Landing Zone) com opções personalizadas de formatação de arquivo e configuração personalizada de nome de arquivo](../destinations/destination-sdk/guides/batch/configure-dlz-destination-with-custom-file-formatting.md)
         * [(Beta) Configure um destino SFTP com opções predefinidas de formatação de arquivo e configuração personalizada de nome de arquivo](../destinations/destination-sdk/guides/batch/configure-sftp-destination-with-predefined-file-formatting.md)
   * Referência {#reference}
      * [Taxa de limitação e política de nova tentativa para destinos de transmissão](./destination-sdk/rate-limiting-retry-policy.md)
      * [Funções de transformação suportadas](./destination-sdk/supported-functions.md)
   * Documente seu destino {#document-destination}
      * [Documente seu destino no Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Usar a interface da Web do GitHub para criar uma página de documentação de destino](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Usar um editor de texto no ambiente local para criar uma página de documentação de destino](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Modelo de autoatendimento da documentação](./destination-sdk/docs-framework/self-service-template.md)
      * [Práticas recomendadas de criação](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Perguntas frequentes](./destinations-faq.md)
* [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)
