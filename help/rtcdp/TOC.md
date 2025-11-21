---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Manual da Real-time Customer Data Platform
user-guide-description: Reúna dados conhecidos e anônimos de diversas fontes empresariais para criar perfis de clientes, criar públicos-alvo a partir desses perfis e ativar esses públicos-alvo para destinos de terceiros.
role: Admin
source-git-commit: 74a73b568c850f8e749afea039afd2821858bd69
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 60%

---


# Ajuda da Real-time Customer Data Platform {#rtcdp}

* [Documentação do Real-Time CDP](home.md)
* Introdução {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Visão geral da Real-Time CDP](overview.md)
      * [Introdução à Real-Time CDP](get-started.md)
      * [Página inicial](home-page-dashboards.md)
   * Real-Time CDP B2B Edition {#rtcdpb2b-intro}
      * [Visão geral da Real-Time CDP B2B Edition](b2b-overview.md)
      * [Exemplo de caso de uso](./b2b-use-case.md)
      * [Tutorial completo](./b2b-tutorial.md)
      * [Medidas de proteção da Real-Time CDP B2B Edition](b2b-guardrails.md)
      * [Atualizações da arquitetura do Real-Time CDP B2B edition](b2b-architecture-upgrade.md)
* AUDIENCE MANAGER e REAL-TIME CDP {#evolution}
   * [Evolução do Audience Manager](aam-to-rtcdp.md)
* Perfis de conta {#account}
   * [Visão geral do perfil da conta](accounts/account-profile-overview.md)
   * [Guia da interface do perfil da conta](accounts/account-profile-ui-guide.md)
* Administração {#admin}
   * [Visão geral da administração](administration/admin-overview.md)
* Públicos-alvo e segmentação {#segmentation}
   * [Visão geral da segmentação](segmentation/segmentation-overview.md)
   * [Guia do Audience Builder](segmentation/audience-builder.md)
   * [Segmentação na Real-Time CDP B2B Edition](segmentation/b2b.md)
   * [IA do cliente](segmentation/customer-ai.md)
* Conjuntos de dados {#datasets}
   * [Conjuntos de dados](datasets/dataset.md)
   * [Qualidade dos dados no Experience Platform](datasets/data-quality.md)
* Destinos {#destinations}
   * [Visão geral dos destinos](destinations/overview.md)
   * [Destinos na Real-Time CDP B2B Edition](destinations/b2b.md)
* Medidas de proteção {#guardrails}
   * [Visão geral das medidas de proteção do Real-Time CDP](guardrails/overview.md)
   * [Medidas de proteção para assimilação de dados](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=pt-BR){target="_blank"}
   * [Medidas de proteção para [!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/){target="_blank"}
   * [Medidas de proteção para [!DNL Real-Time Customer Profile] dados e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR){target="_blank"}
   * [Medidas de proteção para [!DNL Identity Service] dados](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=pt-BR){target="_blank"}
   * [Medidas de proteção para [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=pt-BR){target="_blank"}
   * [Medidas de proteção para ativação de dados por meio de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=pt-BR){target="_blank"}
* Identidades {#identity}
   * [Identidades e namespaces de identidade](profile/identities-overview.md)
* Mesclar políticas {#merge-policies}
   * [Visão geral das políticas de mesclagem](profile/merge-policies.md)
* Privacidade e governança de dados {#privacy}
   * [Visão geral de privacidade](privacy/privacy-overview.md)
   * [Visão geral da governança de dados](privacy/data-governance-overview.md)
* Perfis {#profile}
   * [Visão geral do perfil](profile/profile-overview.md)
   * [Procurar perfil](profile/profile-browse.md)
* Serviços Real-Time CDP B2B edition AI/ML {#b2b-cdp-ai-ml}
   * [Contas relacionadas](b2b-ai-ml-services/related-accounts.md)
   * [Correspondência de conta para lead](b2b-ai-ml-services/lead-to-account-matching.md)
   * Pontuação preditiva de leads e contas {#predictive-lead-and-account-scoring-intro}
      * [Visão geral de pontuação preditiva de conta e lead](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [Gerenciar pontuação preditiva de conta e leads](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* Esquemas {#schemas}
   * [Visão geral dos esquemas](schemas/overview.md)
   * [Esquemas no Real-Time CDP B2B Edition](schemas/b2b.md)
* Origens {#sources}
   * [Visão geral das fontes](sources/sources-overview.md)
   * [Fontes na Real-Time CDP B2B Edition](sources/b2b.md)
* Casos de uso {#use-cases}
   * [Visão geral de casos de uso de exemplo](/help/rtcdp/use-case-guides/overview.md)
   * Aquisição de clientes {#customer-acquisition}
      * [Envolva e adquira novos clientes sem dependência de cookies de terceiros](/help/rtcdp/partner-data/prospecting.md)
      * [Personalizar experiências no site para visitantes desconhecidos usando o reconhecimento de visitantes auxiliados por parceiros](/help/rtcdp/partner-data/onsite-personalization.md)
      * [Redirecionamento externo de usuários não autenticados](./partner-data/offsite-retargeting.md)
      * [Redirecionamento não autenticado do lado do servidor](./partner-data/unauthenticated-retargeting.md)
   * Enriquecimento de perfil {#profile-enrichment}
      * [Suplementar perfis próprios com atributos fornecidos por parceiros](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * Insights e engajamento personalizados {#personalization-insights-engagement}
      * [Evoluir valor único do cliente para valor vitalício](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [Reenvolva seus clientes de forma inteligente](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [Reenvolva seus clientes de forma inteligente: exemplos da Luma](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Notas de versão da Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/release-notes/latest)
* [Glossário da Experience Platform](https://www.adobe.com/go/platform-glossary-en)