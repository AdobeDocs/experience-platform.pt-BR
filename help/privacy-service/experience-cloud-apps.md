---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Aplicativos Privacy Service e Experience Cloud
topic: overview
description: Este documento fornece uma referência para como configurar diferentes aplicativos de Experience Cloud para operações relacionadas à privacidade.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 21%

---


# [!DNL Privacy Service] e  [!DNL Experience Cloud] aplicativos

O Adobe Experience Platform [!DNL Privacy Service] foi desenvolvido para suportar solicitações de privacidade para vários aplicativos Adobe Experience Cloud. Cada aplicativo oferece suporte a diferentes valores de produto e IDs para identificar os indivíduos de dados.

Este documento serve como uma referência para a documentação do aplicativo [!DNL Experience Cloud] que descreve como configurar esse aplicativo para operações relacionadas à privacidade. Isso inclui como formatar e rotular seus dados. São abrangidas duas categorias de aplicações:

* [Aplicativos integrados ao Privacy Service](#integrated): Aplicativos capazes de enviar solicitações de acesso, exclusão ou não participação para  [!DNL Privacy Service].
* [Aplicativos](#self-serve) autônomos: Aplicativos que devem gerenciar suas solicitações de privacidade internamente e com os quais não podem se comunicar  [!DNL Privacy Service] diretamente.

Consulte a documentação dos aplicativos [!DNL Experience Cloud] para saber como formatar suas solicitações de privacidade e quais valores são suportados para essas solicitações.

## Aplicativos integrados com [!DNL Privacy Service] {#integrated}

A seguir está uma lista de [!DNL Experience Cloud] aplicativos que estão integrados com [!DNL Privacy Service], incluindo os recursos [!DNL Privacy Service] com os quais eles são compatíveis e links para a documentação para obter mais informações.

| aplicação | Acesso/exclusão | Recusa de venda | Documentação e considerações |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | Satélite | Satélite | <ul><li>[Documentação de acesso/exclusão para RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Documentação de acesso/exclusão para CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentação de não venda para CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | Satélite | Satélite | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] lida com solicitações de recusa usando variáveis de relatórios de  [privacidade](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | Satélite | Satélite | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/pt-BR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentação de não participação](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | Satélite | Satélite | <ul><li>[Documentação de acesso/exclusão](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Documentação de não participação](../segmentation/honoring-opt-outs.md)</li></ul> |
| Atributos do cliente do Adobe (CRS) | Satélite | N/D | <ul><li>[Documentação de acesso/exclusão para RGPD](https://docs.adobe.com/content/help/pt-BR/core-services/interface/customer-attributes/gdpr.html)</li><li>[Documentação de acesso/exclusão para CCPA](https://docs.adobe.com/content/help/pt-BR/core-services/interface/customer-attributes/ccpa.html)</li><li>Os Atributos do cliente não têm a capacidade de transferir dados, portanto, as solicitações de não participação na venda não são aplicáveis.</li></ul> |
| Adobe Experience Platform | Satélite | Satélite | <ul><li>[Documentação de acesso/exclusão do Data Lake](../catalog/privacy.md)</li><li>[Documentação de acesso/exclusão para o Perfil do cliente em tempo real](../profile/privacy.md)</li><li>[!DNL Experience Platform] atende às solicitações de  [não participação para segmentos](../segmentation/honoring-opt-outs.md) de audiência.</li></ul> |
| Autenticação Adobe Primetime | Satélite | N/D | <ul><li>[Documentação de acesso/exclusão](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] não tem a capacidade de transferir dados, portanto os pedidos de opção de não venda não são aplicáveis.</li></ul> |
| Adobe Target | Satélite | N/D | <ul><li>[Documentação de acesso/exclusão](https://docs.adobe.com/content/help/pt-BR/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] não tem a capacidade de transferir dados, portanto os pedidos de opção de não venda não são aplicáveis.</li></ul> |


## Aplicativos autônomos {#self-serve}

A seguir está uma lista de [!DNL Experience Cloud] aplicativos que não estão integrados a [!DNL Privacy Service] e devem gerenciar suas preocupações de privacidade internamente. São fornecidos links para a documentação de cada aplicativo, juntamente com descrições do conteúdo da documentação.

| aplicação | Descrição da documentação |
| ------- | ----------- |
| [Adobe Campaign Classic](https://helpx.adobe.com/br/campaign/kb/campaign-privacy.html) | Uma visão geral das funcionalidades do RGPD para o Adobe Campaign Classic. |
| [Gerenciador dinâmico de tags do Adobe](https://docs.adobe.com/content/help/pt-BR/dtm/using/tools/opt-in.html) | Etapas para impedir o acionamento das tags Adobe até a aquisição do consentimento. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Uma visão geral de como um administrador de privacidade do cliente ou AEM administrador pode lidar com solicitações de RGPD. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Etapas para fazer com que o RGPD acesse e exclua solicitações usando o Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Como desenvolvedores podem usar extensões e o construtor de regras para definir soluções de opt-in/opt-out. |
