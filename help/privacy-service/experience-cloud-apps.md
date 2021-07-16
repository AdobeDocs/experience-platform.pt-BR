---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Aplicativos Privacy Service e Experience Cloud
topic-legacy: overview
description: Este documento fornece uma referência para como configurar diferentes aplicativos Experience Cloud para operações relacionadas à privacidade.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 892bb4fa5302d63923c1a2e4759f0253955576e2
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 13%

---

# [!DNL Privacy Service] e  [!DNL Experience Cloud] aplicativos

O Adobe Experience Platform [!DNL Privacy Service] foi criado para oferecer suporte a solicitações de privacidade para vários aplicativos Adobe Experience Cloud. Cada aplicativo oferece suporte a diferentes valores de produto e IDs para identificação de titulares de dados.

Este documento serve como uma referência para a documentação do aplicativo [!DNL Experience Cloud] que descreve como configurar esse aplicativo para operações relacionadas à privacidade. Isso inclui como formatar e rotular os dados. São abrangidas duas categorias de pedidos:

* [Aplicativos integrados com o Privacy Service](#integrated): Aplicativos que podem enviar solicitações de acesso, exclusão ou recusa para o  [!DNL Privacy Service].
* [Aplicativos](#self-serve) autônomos: Aplicativos que devem gerenciar suas solicitações de privacidade internamente e não podem se comunicar  [!DNL Privacy Service] diretamente.

Revise a documentação de seus aplicativos [!DNL Experience Cloud] para saber como formatar suas solicitações de privacidade e quais valores são compatíveis com essas solicitações.

## Aplicativos integrados com [!DNL Privacy Service] {#integrated}

Veja a seguir uma lista de [!DNL Experience Cloud] aplicativos integrados com [!DNL Privacy Service], incluindo os recursos [!DNL Privacy Service] com os quais são compatíveis, e links para a documentação para obter mais informações.

| aplicação | Acessar/excluir | Recusa de venda | Documentação e considerações |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | Instantâneo | Instantâneo | <ul><li>[Documentação de acesso/exclusão do GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Documentação de acesso/exclusão para CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentação de cancelamento de venda da CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | Instantâneo | Instantâneo | <ul><li>[Documentação de acesso/exclusão](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=pt-BR)</li><li>[!DNL Analytics] lida com solicitações de recusa usando variáveis de relatório de  [privacidade](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | Instantâneo | Instantâneo | <ul><li>[Documentação de acesso/exclusão](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentação de rejeição](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | Instantâneo | Instantâneo | <ul><li>[Documentação de acesso/exclusão](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=pt-BR)</li><li>[Documentação de rejeição](../segmentation/consents.md)</li></ul> |
| Atributos do cliente do Adobe (CRS) | Instantâneo | N/D | <ul><li>[Documentação de acesso/exclusão do GDPR](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Documentação de acesso/exclusão para CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Os Atributos do cliente não têm a capacidade de transferir dados, portanto, as solicitações de recusa de venda não são aplicáveis.</li></ul> |
| Adobe Experience Platform | Instantâneo | Instantâneo | <ul><li>[Documentação de acesso/exclusão para o Data Lake](../catalog/privacy.md)</li><li>[Documentação de acesso/exclusão para o Perfil do cliente em tempo real](../profile/privacy.md)</li><li>[!DNL Experience Platform] atende às solicitações de  [recusa para segmentos de público-alvo](../segmentation/consents.md).</li></ul> |
| Autenticação Adobe Primetime | Instantâneo | N/D | <ul><li>[Documentação de acesso/exclusão](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] não tem a capacidade de transferir dados, portanto, as solicitações de recusa de venda não são aplicáveis.</li></ul> |
| Adobe Target | Instantâneo | N/D | <ul><li>[Documentação de acesso/exclusão](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=pt-BR)</li><li>[!DNL Target] não tem a capacidade de transferir dados, portanto, as solicitações de recusa de venda não são aplicáveis.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Aplicativos autônomos {#self-serve}

Veja a seguir uma lista de [!DNL Experience Cloud] aplicativos que não estão integrados com [!DNL Privacy Service] e devem gerenciar suas preocupações de privacidade internamente. São fornecidos links para a documentação de cada aplicativo, juntamente com descrições do conteúdo da documentação.

| aplicação | Descrição da documentação |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html) | Uma visão geral das funcionalidades do GDPR para o Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Uma visão geral de como um administrador de privacidade do cliente ou AEM administrador pode lidar com solicitações do GDPR. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Etapas para fazer com que o GDPR acesse e exclua solicitações usando o Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Certifique-se de que as instalações do Magento Commerce estejam em conformidade com os requisitos de legislações específicas de privacidade. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Saiba como as regras de privacidade se aplicam ao Marketo. |
| [Tags no Adobe Experience Platform](../tags/ui/client-side/consent.md) | Como desenvolvedores podem usar extensões e o construtor de regras para definir soluções de opt-in/opt-out. |
| [Workfront](https://www.workfront.com/privacy-notice) | Saiba como o Workfront coleta dados pessoais e como um titular de dados pode enviar uma solicitação de privacidade por meio de um formulário. |

{style=&quot;table-layout:auto&quot;}
