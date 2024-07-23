---
audience: user
user-guide-title: Ajuda das tags
breadcrumb-title: Tags
user-guide-description: Saiba como implantar e gerenciar tags de análise, marketing e publicidade para potencializar as experiências dos clientes.
feature: Tags
solution: Data Collection
role: Developer
source-git-commit: 5cbc2f6809156bc1a554154527ff2c5e35d3a922
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 44%

---


# Tags {#tags}

* [Visão geral das tags](./home.md)
* Introdução {#get-started}
   * [Manual de início rápido](./quick-start/quick-start.md)
   * [Guias de implementação](./quick-start/implementation-guides.md)
* Guias de interface do usuário {#ui}
   * [Visão geral](./ui/managing-resources/overview.md)
   * Extensões {#extensions}
      * [Visão geral](./ui/managing-resources/extensions/overview.md)
      * [Atualizações de extensão](./ui/managing-resources/extensions/extension-upgrade.md)
   * [Elementos de dados](./ui/managing-resources/data-elements.md)
   * [Regras](./ui/managing-resources/rules.md)
   * [Notas](./ui/managing-resources/notes.md)
   * [Copiar recursos](./ui/managing-resources/copying-resources.md)
   * [Comparar revisões de recursos](./ui/managing-resources/compare-resource-revisions.md)
   * [Excluir recursos](./ui/managing-resources/delete-resources.md)
   * [Remover recursos de uma biblioteca](./ui/managing-resources/remove-resources-from-library.md)
* Publicação {#publish}
   * [Visão geral](./ui/publishing/overview.md)
   * [Fluxo de publicação](./ui/publishing/publishing-flow.md)
   * Hosts {#hosts}
      * [Visão geral](./ui/publishing/hosts/hosts-overview.md)
      * [Hosts gerenciados pela Adobe](./ui/publishing/hosts/managed-by-adobe-host.md)
      * [Hosts SFTP](./ui/publishing/hosts/sftp-host.md)
   * Ambientes {#environments}
      * [Visão geral](./ui/publishing/environments.md)
      * [Testar códigos incorporados usando o Adobe Experience Platform Debugger](./ui/publishing/embed-code-testing.md)
   * [Builds](./ui/publishing/builds.md)
   * [Bibliotecas](./ui/publishing/libraries.md)
   * [Bibliotecas de auto-hospedagem](./ui/publishing/hosts/self-hosting-libraries.md)
   * [Republicar uma biblioteca](./ui/publishing/republish.md)
   * [Tags do Experience Platform (China)](./ui/publishing/premium-cdn.md)
* Informações do lado do cliente {#client-side}
   * [Visão geral](./ui/client-side/overview.md)
   * [Implantação assíncrona](./ui/client-side/asynchronous-deployment.md)
   * [Referência a objeto do satélite](./ui/client-side/satellite-object.md)
   * [Implantar tags do JavaScript para gerenciar o consentimento do cliente](./ui/client-side/consent.md)
   * [Suporte à Política de segurança de conteúdo (CSP)](./ui/client-side/content-security-policy.md)
   * [Compatibilidade de Integridade de sub-recursos (SRI)](./ui/client-side/sri.md)
   * [Segurança da camada de transporte](./ui/client-side/transport-layer-security.md)
* Encaminhamento de eventos {#event-forwarding}
   * [Visão geral](./ui/event-forwarding/overview.md)
   * [Introdução](./ui/event-forwarding/getting-started.md)
   * [Configuração de segredos](./ui/event-forwarding/secrets.md)
   * [Monitoramento (Beta)](./ui/event-forwarding/monitoring.md)
* Administração {#admin}
   * [Visão geral](./ui/administration/overview.md)
   * [Empresas e propriedades](./ui/administration/companies-and-properties.md)
   * [Permissões de usuário](./ui/administration/user-permissions.md)
* Extensões {#extensions}
   * [Visão geral](./extensions/overview.md)
   * Extensões de marca (lado do cliente) {#client}
      * [Visão geral](./extensions/client/overview.md)
      * [Métricas de velocidade de site acessíveis](https://exchange.adobe.com/apps/ec/103053)
      * [Personalizador de Activity Map](https://exchange.adobe.com/apps/ec/101531)
      * [Atualização de Página de Ação](https://exchange.adobe.com/apps/ec/102848)
      * [Acompanhamento de Sites de Adform](https://exchange.adobe.com/apps/ec/103195)
      * [Adobe Advertising Cloud](https://exchange.adobe.com/apps/ec/100155)
      * Adobe Analytics {#analytics}
         * [Visão geral](./extensions/client/analytics/overview.md)
         * [Módulos compartilhados](./extensions/client/analytics/shared-modules.md)
         * [Notas de versão](./extensions/client/analytics/release-notes.md)
      * [Adobe Analytics E Adobe Target](https://exchange.adobe.com/apps/ec/105363/6sense-for-analytics-and-target)
      * [Adobe Analytics e Microsoft Dynamics](https://exchange.adobe.com/apps/ec/102966)
      * [Adobe Analytics e Salesforce](https://exchange.adobe.com/apps/ec/101530)
      * Cadeia de caracteres do produto Adobe Analytics {#product-string}
         * [Visão geral](./extensions/client/product-string/overview.md)
         * [Notas de versão](./extensions/client/product-string/release-notes.md)
      * [Construtor de cadeia de caracteres do produto Adobe Analytics](https://exchange.adobe.com/apps/ec/101461)
      * [Adobe Analytics via SDK da Web da Adobe Experience Platform](https://exchange.adobe.com/apps/ec/108985/search-discovery-for-adobe-analytics-via-aep-web-sdk)
      * Adobe Audience Manager {#audience-manager}
         * [Visão geral](./extensions/client/audience-manager/overview.md)
      * Camada de Dados de Clientes Adobe {#client-data-layer}
         * [Visão geral](./extensions/client/client-data-layer/overview.md)
         * [Notas de versão](./extensions/client/client-data-layer/release-notes.md)
      * Adobe ContextHub {#contexthub}
         * [Visão geral](./extensions/client/contexthub/overview.md)
      * [Adobe Experience Manager Forms](https://exchange.adobe.com/apps/ec/107493)
      * Serviço da Adobe Experience Cloud ID {#id-service}
         * [Visão geral](./extensions/client/id-service/overview.md)
         * [Notas de versão](./extensions/client/id-service/release-notes.md)
      * Demonstração do Adobe Experience Platform {#platform-demo}
         * [Visão geral](./extensions/client/platform-demo/overview.md)
      * SDK da Web da Adobe Experience Platform {#web-sdk}
         * [Visão geral](./extensions/client/web-sdk/overview.md)
         * [Configurar a extensão de tag do SDK da Web](./extensions/client/web-sdk/web-sdk-extension-configuration.md)
         * [Tipos de evento](./extensions/client/web-sdk/event-types.md)
         * [Tipos de ação](./extensions/client/web-sdk/action-types.md)
         * [Tipos de elementos de dados](./extensions/client/web-sdk/data-element-types.md)
         * [Acessar a ECID](./extensions/client/web-sdk/accessing-the-ecid.md)
         * [Plug-ins do SDK da Web](./extensions/client/web-sdk/web-sdk-plugins.md)
         * [Notas de versão da extensão SDK da Web](./extensions/client/web-sdk/web-sdk-ext-release-notes.md)
         * [Notas de versão dos plug-ins do SDK da Web](./extensions/client/web-sdk/web-sdk-plugins-release-notes.md)
      * Adobe Experience Manager Asset Insights {#asset-insights}
         * [Visão geral](./extensions/client/asset-insights/overview.md)
         * [Notas de versão](./extensions/client/asset-insights/release-notes.md)
      * [Adobe Fonts](https://exchange.adobe.com/apps/ec/101538)
      * Adobe Medium Analytics para áudio e vídeo {#media-analytics}
         * [Visão geral](./extensions/client/media-analytics/overview.md)
         * [Notas de versão](./extensions/client/media-analytics/release-notes.md)
      * Adobe Medium Analytics (SDK 3.x) {#media-analytics-3x}
         * [Visão geral](./extensions/client/media-analytics-3x/overview.md)
         * [Notas de versão](./extensions/client/media-analytics-3x/release-notes.md)
      * Privacidade Adobe {#privacy}
         * [Visão geral](./extensions/client/privacy/overview.md)
      * [Seletor do Conjunto de Relatórios de Adobe](https://exchange.adobe.com/apps/ec/100640)
      * Adobe Target {#target}
         * [Visão geral](./extensions/client/target/overview.md)
         * [Notas de versão](./extensions/client/target/release-notes.md)
      * Adobe Target v2 {#target-v2}
         * [Visão geral](./extensions/client/target-v2/overview.md)
         * [Notas de versão](./extensions/client/target-v2/release-notes.md)
      * [Kit de ferramentas do Adobe Target](https://exchange.adobe.com/apps/ec/100640)
      * [Advertising Cloud](https://exchange.adobe.com/apps/ec/100640)
      * [Insights de ativos do AEM](https://exchange.adobe.com/apps/ec/103406)
      * [Notificador JS de freio de ar](https://exchange.adobe.com/apps/ec/103342)
      * [Amplitude](https://exchange.adobe.com/apps/ec/108010)
      * [Apollo QAX](https://exchange.adobe.com/apps/ec/105068)
      * [Awin Advertiser MasterTag](https://exchange.adobe.com/apps/ec/103176)
      * [Marca De Conversão Awin](https://exchange.adobe.com/apps/ec/103240)
      * [Contexto Humano do Beemray](https://exchange.adobe.com/apps/ec/101063)
      * [Rastreamento de Evento Universal do Bing Ads](https://exchange.adobe.com/apps/ec/100154)
      * [Ramificação](https://exchange.adobe.com/apps/ec/101382)
      * [!DNL BrightCove] monitoramento de vídeo {#brightcove}
         * [Visão geral](./extensions/client/brightcove/overview.md)
         * [Notas de versão](./extensions/client/brightcove/release-notes.md)
      * [CallTrackingMetrics](https://exchange.adobe.com/apps/ec/107695)
      * [Identificador do Channel Source](https://exchange.adobe.com/apps/ec/101412)
      * [Experiências do Cheetah](https://exchange.adobe.com/apps/ec/102759)
      * [Clicktale](https://exchange.adobe.com/apps/ec/100082)
      * Plug-ins comuns do Analytics {#plugins}
         * [Visão geral](./extensions/client/plugins/overview.md)
         * [Notas de versão](./extensions/client/plugins/release-notes.md)
      * [Concat](https://exchange.adobe.com/apps/ec/104690)
      * [ContentSquare](https://exchange.adobe.com/apps/ec/100364)
      * [Gerenciamento de Consentimento de Cookies por Usercentrics CMP v2](https://exchange.adobe.com/apps/ec/107037)
      * Núcleo {#core}
         * [Visão geral](./extensions/client/core/overview.md)
         * [Notas de versão](./extensions/client/core/release-notes.md)
      * [Agente de Depuração Personalizado](https://exchange.adobe.com/apps/ec/104698)
      * [Reconhecimento de Cliente](https://exchange.adobe.com/apps/ec/100688)
      * [Assistente de Elemento de Dados (DEA)](https://exchange.adobe.com/apps/ec/101413)
      * [Gerenciador de Camada de Dados](https://exchange.adobe.com/apps/ec/101462)
      * [Decibel](https://exchange.adobe.com/apps/ec/100913)
      * [Demandbase](https://exchange.adobe.com/apps/ec/101605)
      * [Privacidade diferencial](https://exchange.adobe.com/apps/ec/104535)
      * [Visualizadores do Dynamic Media](https://exchange.adobe.com/apps/ec/103048)
      * [EDDL Helper](https://exchange.adobe.com/apps/ec/107691)
      * [OneTag de Falação Rápida](https://exchange.adobe.com/apps/ec/101392)
      * [ForeSee](https://exchange.adobe.com/apps/ec/100164)
      * [Gainsight PX](https://exchange.adobe.com/apps/ec/103343)
      * [Envolvimento preditivo da Genesys](https://exchange.adobe.com/apps/ec/106148)
      * Camada de dados do Google {#google-data-layer}
         * [Visão geral](./extensions/client/google-data-layer/overview.md)
         * [Notas de versão](./extensions/client/google-data-layer/release-notes.md)
      * [Marca de Site Global da Google (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)
      * [InMoment](https://exchange.adobe.com/apps/ec/100847)
      * [JSON Helper](https://exchange.adobe.com/apps/ec/106449)
      * [Análise do JW Player](https://exchange.adobe.com/apps/ec/101523)
      * [KickFire](https://exchange.adobe.com/apps/ec/101621)
      * [Tabela de Mapeamento](https://exchange.adobe.com/apps/ec/103136)
      * [!DNL Marketo Munchkin] {#marketo}
         * [Visão geral](./extensions/client/marketo/overview.md)
         * [Notas de versão](./extensions/client/marketo/release-notes.md)
      * [Gerenciador de Propriedades Mestre](https://exchange.adobe.com/apps/ec/102992)
      * [Marca do Merkury](https://exchange.adobe.com/apps/ec/600027/merkury-tag)
      * [!DNL Meta Pixel] {#meta}
         * [Visão geral](./extensions/client/meta/overview.md)
      * [Monita](https://exchange.adobe.com/apps/ec/106544)
      * [SDK digital Nielsen](https://exchange.adobe.com/apps/ec/101361)
      * [Gerenciamento de Consentimento do OneTrust para Cookies](https://exchange.adobe.com/apps/ec/100340)
      * [Pepperjam](https://exchange.adobe.com/apps/ec/103587)
      * [Conexão Persistente](https://exchange.adobe.com/apps/ec/103745)
      * [Acompanhamento de Conversão do Pinterest](https://exchange.adobe.com/apps/ec/100523)
      * [Carregador de pixels](https://exchange.adobe.com/apps/ec/100152)
      * [Comentários sobre o Site do Qualtrics](https://exchange.adobe.com/apps/ec/101569)
      * [Métrica Quantum](https://exchange.adobe.com/apps/ec/101535)
      * [Resolver Momentum](https://exchange.adobe.com/apps/ec/108352)
      * [Rokt](https://exchange.adobe.com/apps/ec/107591)
      * [Pesquisa de SDI](https://exchange.adobe.com/apps/ec/102991)
      * [Toolkit de SDI](https://exchange.adobe.com/apps/ec/101460)
      * [CamSessão](https://exchange.adobe.com/apps/ec/100517)
      * [Abrangente de Armazenamento](https://exchange.adobe.com/apps/ec/102990)
      * [TAGS por Horizonte de Loop](https://exchange.adobe.com/apps/ec/106092)
      * [Coleta de teálio](https://exchange.adobe.com/apps/ec/104217)
      * [Enriquecimento de Dados do Tealium](https://exchange.adobe.com/apps/ec/104217)
      * [Plataforma de Fundação TMMData](https://exchange.adobe.com/apps/ec/100148)
      * [Gerenciador de Consentimento de Cookie do TrustArc](https://exchange.adobe.com/apps/ec/107037)
      * [Reprodução do Vimeo](https://exchange.adobe.com/apps/ec/108937)
      * [Vitais da Web](https://exchange.adobe.com/apps/ec/106769)
      * [XDM Composer](https://exchange.adobe.com/apps/ec/106062)
      * [Ponto do Yahoo](https://exchange.adobe.com/apps/ec/106062)
      * [Rastreamento de Conversão de Texto](https://exchange.adobe.com/apps/ec/103174)
      * [[!DNL Youtube] Reprodução](https://exchange.adobe.com/apps/ec/103174)
      * [!DNL YouTube] monitoramento de vídeo {#youtube}
         * [Visão geral](./extensions/client/youtube/overview.md)
         * [Notas de versão](./extensions/client/youtube/release-notes.md)
   * Extensões de encaminhamento de eventos (lado do servidor) {#server}
      * [Visão geral](./extensions/server/overview.md)
      * Adobe Experience Platform Cloud Connector {#cloud-connector}
         * [Visão geral](./extensions/server/cloud-connector/overview.md)
         * [Notas de versão](./extensions/server/cloud-connector/release-notes.md)
      * [!DNL AWS] {#aws}
         * [Visão geral](./extensions/server/aws/overview.md)
      * [!DNL Braze] {#braze}
         * [Visão geral](./extensions/server/braze/overview.md)
      * [Conector de nuvem para Google Analytics](https://exchange.adobe.com/apps/ec/106542)
      * Núcleo {#core}
         * [Visão geral](./extensions/server/core/overview.md)
      * [API de Evento Epsilon](https://exchange.adobe.com/apps/ec/109127)
      * Conversões Aprimoradas do Google Ads {#google-ads-enhanced-conversions}
         * [Visão geral](./extensions/server/google-ads-enhanced-conversions/overview.md)
      * Plataforma de nuvem do Google {#google-cloud-platform}
         * [Visão geral](./extensions/server/google-cloud-platform/overview.md)
      * [!DNL LinkedIn Conversions API] {#linkedin}
         * [Visão geral](./extensions/server/linkedin/overview.md)
      * [!DNL Mailchimp] Edge {#mailchimp}
         * [Visão geral](./extensions/server/mailchimp/overview.md)
      * [!DNL Meta Conversions API] {#meta}
         * [Visão geral](./extensions/server/meta/overview.md)
      * [!DNL Microsoft Azure] {#azure}
         * [Visão geral](./extensions/server/azure/overview.md)
      * [!DNL Mixpanel] {#mixpanel}
         * [Visão geral](./extensions/server/mixpanel/overview.md)
      * [Hub de decisão do cliente Pega](https://exchange.adobe.com/apps/ec/107597)
      * [!DNL Pinterest] {#pinterest}
         * [Visão geral](./extensions/server/pinterest/overview.md)
      * [API de Conversões de Snap](https://exchange.adobe.com/apps/ec/108550)
      * [!DNL Snowflake] {#snowflake}
         * [Visão geral](./extensions/server/snowflake/overview.md)
      * [!DNL Splunk] {#splunk}
         * [Visão geral](./extensions/server/splunk/overview.md)
      * [!DNL Twitter] {#twitter}
         * [Visão geral](./extensions/server/twitter/overview.md)
      * [!DNL Tiktok] API de eventos da Web {#tiktok}
         * [Visão geral](./extensions/server/tiktok/overview.md)
      * [!DNL The Trade Desk] {#thetradedesk}
         * [Visão geral](./extensions/server/tradedesk/overview.md)
      * [!DNL Zendesk] API de eventos {#zendesk}
         * [Visão geral](./extensions/server/zendesk/overview.md)
* Desenvolvimento de extensão {#extension-dev}
   * [Visão geral](./extension-dev/overview.md)
   * [Introdução](./extension-dev/getting-started.md)
   * [Navegadores compatíveis](./extension-dev/browsers.md)
   * Processo de envio {#submit}
      * [Visão geral](./extension-dev/submit/overview.md)
      * [Configuração da empresa](./extension-dev/submit/setup.md)
      * [Conceder acesso ao usuário](./extension-dev/submit/access.md)
      * [Desenvolver uma extensão](./extension-dev/submit/develop.md)
      * [Criar uma lista de troca](./extension-dev/submit/create-listing.md)
      * [Fazer upload e implementar testes completos](./extension-dev/submit/upload-and-test.md)
      * [Lançar uma extensão](./extension-dev/submit/release.md)
   * [Configuração de extensão](./extension-dev/configuration.md)
   * [Manifesto de extensão](./extension-dev/manifest.md)
   * Extensões da Web {#web}
      * [Fluxo de extensão](./extension-dev/web/flow.md)
      * [Formato do módulo da biblioteca](./extension-dev/web/format.md)
      * [Exibições](./extension-dev/web/views.md)
      * [Tipos de evento](./extension-dev/web/event-types.md)
      * [Tipos de condição](./extension-dev/web/condition-types.md)
      * [Tipos de ação](./extension-dev/web/action-types.md)
      * [Tipos de elementos de dados](./extension-dev/web/data-element-types.md)
      * [Módulos principais](./extension-dev/web/core.md)
      * [Módulos compartilhados](./extension-dev/web/shared.md)
   * Extensões do Edge {#edge}
      * [Fluxo de extensão](./extension-dev/edge/flow.md)
      * [Formato do módulo da biblioteca](./extension-dev/edge/format.md)
      * [Tipos de condição](./extension-dev/edge/condition-types.md)
      * [Tipos de ação](./extension-dev/edge/action-types.md)
      * [Tipos de elementos de dados](./extension-dev/edge/data-element-types.md)
      * [Parâmetro de contexto](./extension-dev/edge/context.md)
   * [Hospedagem de bibliotecas de terceiros](./extension-dev/third-party-libraries.md)
   * [Variável sem turbina](./extension-dev/turbine.md)
   * [Padrão de compatibilidade com versões anteriores](./extension-dev/backwards-compatibility.md)
* API Reactor {#api}
   * [Visão geral](./api/overview.md)
   * [Autenticar e acessar a API do Reator](./api/getting-started.md)
   * Pontos de extremidade {#endpoints}
      * [Empresas](./api/endpoints/companies.md)
      * [Propriedades](./api/endpoints/properties.md)
      * [Elementos de dados](./api/endpoints/data-elements.md)
      * [Regras](./api/endpoints/rules.md)
      * [Componentes da regra](./api/endpoints/rule-components.md)
      * [Pacotes de extensão](./api/endpoints/extension-packages.md)
      * [Autorizações de uso de pacote de extensão](./api/endpoints/extension-package-usage-authorizations.md)
      * [Extensões](./api/endpoints/extensions.md)
      * [Bibliotecas](./api/endpoints/libraries.md)
      * [Builds](./api/endpoints/builds.md)
      * [Ambientes](./api/endpoints/environments.md)
      * [Hosts](./api/endpoints/hosts.md)
      * [Configurações do aplicativo](./api/endpoints/app-configurations.md)
      * [Eventos de auditoria](./api/endpoints/audit-events.md)
      * [Retornos de chamada](./api/endpoints/callbacks.md)
      * [Notas](./api/endpoints/notes.md)
      * [Perfil](./api/endpoints/profile.md)
      * [Pesquisa](./api/endpoints/search.md)
      * [Segredos](./api/endpoints/secrets.md)
   * Guias {#guides}
      * [Delegar IDs do descritor](./api/guides/delegate-descriptor-ids.md)
      * [Criptografar valores](./api/guides/encrypting-values.md)
      * [Tratamento de erros](./api/guides/error-handling.md)
      * [Compartilhamento de pacotes de extensão privados](./api/guides/extension-packages.md)
      * [Filtragem de respostas](./api/guides/filtering.md)
      * [Paginação de respostas](./api/guides/pagination.md)
      * [Classificação de respostas](./api/guides/sorting.md)
      * [Relações](./api/guides/relationships.md)
      * [Pesquisa de recursos](./api/guides/search.md)
      * [Segredos](./api/guides/secrets.md)
* [Perguntas frequentes](./faq.md)
* [Atualizações de terminologia](./term-updates.md)
* [Substituição do suporte para o Internet Explorer 10 e 11](./ie-deprecation.md)
* [Notas de versão da Platform](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest?lang=pt-BR)

