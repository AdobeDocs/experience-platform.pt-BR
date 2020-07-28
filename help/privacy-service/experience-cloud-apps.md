---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aplicativos Privacy Service e Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 22%

---


# [!DNL Privacy Service] e [!DNL Experience Cloud] aplicativos

O Adobe Experience Platform [!DNL Privacy Service] foi desenvolvido para suportar solicitações de privacidade para vários aplicativos Adobe Experience Cloud. Cada aplicativo oferece suporte a diferentes valores de produto e IDs para identificar os indivíduos de dados.

Este documento serve como uma referência para a documentação do [!DNL Experience Cloud] aplicativo que descreve como configurar esse aplicativo para operações relacionadas à privacidade. Isso inclui como formatar e rotular seus dados. São abrangidas duas categorias de aplicações:

* [Aplicativos integrados ao Privacy Service](#integrated): Aplicativos capazes de enviar solicitações de acesso, exclusão ou não participação para [!DNL Privacy Service].
* [Aplicativos](#self-serve)autônomos: Aplicativos que devem gerenciar suas solicitações de privacidade internamente e com os quais não podem se comunicar [!DNL Privacy Service] diretamente.

Consulte a documentação de seus [!DNL Experience Cloud] aplicativos para saber como formatar suas solicitações de privacidade e quais valores são suportados para essas solicitações.

## Aplicativos integrados com [!DNL Privacy Service] {#integrated}

Veja a seguir uma lista de [!DNL Experience Cloud] aplicativos integrados com [!DNL Privacy Service], incluindo os [!DNL Privacy Service] recursos compatíveis e links para a documentação para obter mais informações.

| aplicação | Acesso/exclusão | Recusa de venda | Documentação e considerações |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>[!DNL Advertising Cloud] aproveita os recursos globais de opção de não participação existentes fornecidos pelo Centro de privacidade do Adobe. Consulte o guia sobre como [fazer solicitações](https://docs.adobe.com/content/help/pt-BR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) de privacidade de dados para obter mais informações.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] lida com solicitações de recusa usando variáveis de relatórios de [privacidade](https://docs.adobe.com/content/help/pt-BR/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/pt-BR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentação de não participação](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Documentação de não participação](../segmentation/honoring-opt-outs.md)</li></ul> |
| Atributos do cliente do Adobe (CRS) | ✓ | N/D | <ul><li>[Documentação de acesso/exclusão para RGPD](https://docs.adobe.com/content/help/pt-BR/core-services/interface/customer-attributes/gdpr.html)</li><li>[Documentação de acesso/exclusão para CCPA](https://docs.adobe.com/content/help/pt-BR/core-services/interface/customer-attributes/ccpa.html)</li><li>Os Atributos do cliente não têm a capacidade de transferir dados, portanto, as solicitações de não participação na venda não são aplicáveis.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Documentação de acesso/exclusão do Data Lake](../catalog/privacy.md)</li><li>[Documentação de acesso/exclusão para o Perfil do cliente em tempo real](../profile/privacy.md)</li><li>[!DNL Experience Platform] atende às solicitações de [não participação para segmentos](../segmentation/honoring-opt-outs.md)de audiência.</li></ul> |
| Autenticação Adobe Primetime | ✓ | N/D | <ul><li>[Documentação de acesso/exclusão](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] não tem a capacidade de transferir dados, portanto os pedidos de opção de não venda não são aplicáveis.</li></ul> |
| Adobe Target | ✓ | N/D | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/pt-BR/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] não tem a capacidade de transferir dados, portanto os pedidos de opção de não venda não são aplicáveis.</li></ul> |


## Aplicativos autônomos {#self-serve}

Veja a seguir uma lista de [!DNL Experience Cloud] aplicativos que não estão integrados com [!DNL Privacy Service] e devem gerenciar suas preocupações de privacidade internamente. São fornecidos links para a documentação de cada aplicativo, juntamente com descrições do conteúdo da documentação.

| aplicação | Descrição da documentação |
| ------- | ----------- |
| [Adobe Campaign Classic](https://helpx.adobe.com/br/campaign/kb/campaign-privacy.html) | Uma visão geral das funcionalidades do RGPD para o Adobe Campaign Classic. |
| [Gerenciador dinâmico de tags do Adobe](https://docs.adobe.com/content/help/pt-BR/dtm/using/tools/opt-in.html) | Etapas para impedir o acionamento das tags Adobe até a aquisição do consentimento. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Uma visão geral de como um administrador de privacidade do cliente ou AEM administrador pode lidar com solicitações de RGPD. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Etapas para fazer com que o RGPD acesse e exclua solicitações usando o Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Como desenvolvedores podem usar extensões e o construtor de regras para definir soluções de opt-in/opt-out. |
