---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Serviços de privacidade e aplicativos da Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Serviços de privacidade e aplicativos da Experience Cloud

O Adobe Experience Platform Privacy Service foi criado para suportar solicitações de privacidade de vários aplicativos da Adobe Experience Cloud. Cada aplicativo oferece suporte a diferentes valores de produto e IDs para identificar os indivíduos de dados.

Esse documento serve como uma referência para a documentação do aplicativo da Experience Cloud que descreve como configurar esse aplicativo para operações relacionadas à privacidade. Isso inclui como formatar e rotular seus dados. São abrangidas duas categorias de aplicações:

* [Aplicativos integrados ao Privacy Service](#integrated): Aplicativos capazes de enviar solicitações de acesso, exclusão ou cancelamento ao Privacy Service.
* [Aplicativos](#self-serve)autônomos: Aplicativos que devem gerenciar suas solicitações de privacidade internamente e não podem se comunicar diretamente com o Privacy Service.

Consulte a documentação dos aplicativos da Experience Cloud para saber como formatar suas solicitações de privacidade e quais valores são suportados para essas solicitações.

## Aplicativos integrados ao Privacy Service {#integrated}

Veja a seguir uma lista de aplicativos da Experience Cloud que são integrados ao Privacy Service, incluindo os recursos do Privacy Service com os quais são compatíveis, e links para a documentação para obter mais informações.

| aplicação | Acesso/exclusão | Recusa de venda | Documentação e considerações |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>A Advertising Cloud aproveita os recursos globais de opção de não participação existentes fornecidos pelo Adobe Privacy Center. Consulte o guia sobre como [fazer solicitações](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) de privacidade de dados para obter mais informações.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/index.html)</li><li>O Analytics lida com solicitações de recusa usando variáveis de relatórios de [privacidade](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://marketing.adobe.com/resources/help/en_US/aam/aam-gdpr.html)</li><li>[Documentação de não participação](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Documentação de não participação](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão do Data Lake](../catalog/privacy.md)</li><li>[Documentação de acesso/exclusão para o Perfil do cliente em tempo real](../profile/privacy.md)</li><li>A plataforma de experiência aceita solicitações de [cancelamento para segmentos](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/honoring-opt-outs.md)de audiência.</li></ul> |
| Autenticação do Adobe Primetime | ✓ | N/D | <ul><li>[Documentação de acesso/exclusão](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>O Primetime não tem a capacidade de transferir dados, portanto, as solicitações de não participação na venda não são aplicáveis.</li></ul> |
| Adobe Target | ✓ | N/D | <ul><li>[Documentação de acesso/exclusão](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)</li><li>O Público alvo não tem a capacidade de transferir dados, portanto, as solicitações de não participação na venda não são aplicáveis.</li></ul> |

<!-- (To include once access/delete documentation is available)
Adobe Customer Attributes (CRS) | ✓ | N/A | <ul><li>Customer Attributes does not have the capability to transfer data, therefore opt-out-of-sale requests are not applicable.</li></ul>
-->

## Aplicativos autônomos {#self-serve}

Veja a seguir uma lista de aplicativos da Experience Cloud que não estão integrados ao Privacy Service e devem gerenciar suas preocupações de privacidade internamente. São fornecidos links para a documentação de cada aplicativo, juntamente com descrições do conteúdo da documentação.

| aplicação | Descrição da documentação |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Uma visão geral das funcionalidades do RGPD para o Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://marketing.adobe.com/resources/help/en_US/dtm/opt-in.html) | Etapas para impedir que as tags da Adobe sejam acionadas até que o consentimento seja adquirido. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Uma visão geral de como um administrador de privacidade do cliente ou um administrador de AEM pode lidar com solicitações de RGPD. |
| [Adobe Experience Manager Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/c_gdpr_compliance.html) | Etapas para fazer com que o RGPD acesse e exclua solicitações usando o Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Como desenvolvedores podem usar extensões e o construtor de regras para definir soluções de opt-in/opt-out. |
| [Adobe Social](https://marketing.adobe.com/resources/help/en_US/social/c_gdpr-request.html) | Etapas para usar o formulário de solicitação do RGPD para acessar ou excluir dados coletados pelo Social. |