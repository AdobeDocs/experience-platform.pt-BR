---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Aplicativos Privacy Service e Experience Cloud
description: Este documento fornece uma referência sobre como configurar diferentes aplicativos do Experience Cloud para operações relacionadas à privacidade.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: b8b862a2134d4901e45f5dce82ac4de457ed6db6
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 7%

---

# [!DNL Privacy Service] e [!DNL Experience Cloud] aplicativos

O Adobe Experience Platform [!DNL Privacy Service] foi criado para dar suporte a solicitações de privacidade para vários aplicativos Adobe Experience Cloud. Cada aplicativo suporta diferentes valores de produto e IDs para identificar titulares de dados.

Este documento serve como uma referência para a documentação do aplicativo [!DNL Experience Cloud], que descreve como configurar esse aplicativo para operações relacionadas à privacidade. Isso inclui como formatar e rotular os dados. São abrangidas duas categorias de pedidos:

* [Aplicativos integrados ao Privacy Service](#integrated): aplicativos que podem enviar solicitações de acesso, exclusão ou recusa para [!DNL Privacy Service].
* [Aplicativos de autoatendimento](#self-serve): aplicativos que devem gerenciar suas solicitações de privacidade internamente e não podem se comunicar diretamente com [!DNL Privacy Service].

Revise a documentação dos aplicativos do [!DNL Experience Cloud] para saber como formatar suas solicitações de privacidade e quais valores são suportados para essas solicitações.

## Aplicativos integrados com o [!DNL Privacy Service] {#integrated}

Esta é uma lista de aplicativos do [!DNL Experience Cloud] que estão integrados ao [!DNL Privacy Service], incluindo os recursos do [!DNL Privacy Service] com os quais são compatíveis, seus protocolos para processamento de solicitações de exclusão e links para a documentação para mais informações.

>[!NOTE]
>
>Todos os produtos integrados respondem às solicitações de privacidade em 30 dias ou menos.

| Aplicativo | Acessar/excluir | Recusar a venda | Excluir comportamento | Documentação e outras considerações |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising | ✓ | ✓ | A ID do cookie ou a ID do dispositivo do titular dos dados é excluída do sistema, juntamente com todos os dados de custo, clique e receita associados ao cookie. | <ul><li>[Acessar/excluir a documentação do GDPR](https://experienceleague.adobe.com/en/docs/advertising/privacy/gdpr)</li><li>[Acessar/excluir a documentação da CCPA](https://experienceleague.adobe.com/en/docs/advertising/privacy/ccpa/ccpa-access-delete)</li><li>[Documentação de cancelamento da venda para a CCPA](https://experienceleague.adobe.com/en/docs/advertising/privacy/ccpa/ccpa-opt-out-of-sale)</li></ul> |
| Adobe Analytics | ✓ | ✓ | O Adobe Analytics fornece ferramentas para rotular dados de acordo com sua sensibilidade e restrições contratuais. Os rótulos são uma etapa importante para:<ol><li>Identificação de titulares de dados.</li><li>Determinar quais dados retornar como parte de uma solicitação de acesso.</li><li>Identificação de campos de dados que devem ser excluídos como parte de uma solicitação de exclusão.</li></ol> | <ul><li>[Fluxo de Trabalho de Privacidade](https://experienceleague.adobe.com/en/docs/analytics/technotes/privacy/gdpr)</li><li>[Rotulação do Analytics](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/privacy-labeling/labels)</li><li>[Opção de não participação do Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/cm-opt-out)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Todas as características e segmentos associados ao identificador do Audience Manager incluído na solicitação são excluídos. Além disso, os respectivos identificadores do indivíduo são recusados na coleta de dados e os respectivos mapeamentos de ID são removidos. | <ul><li>Documentação do [Access](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#access-data) / [delete](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#delete-data)</li><li>[Documentação de recusa](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/declared-ids#opt-out-calls)</li><li>[Solicitações de recusa](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Gerenciamento de privacidade](https://experienceleague.adobe.com/en/docs/campaign-classic/using/getting-started/privacy/privacy-management)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir a documentação](https://experienceleague.adobe.com/en/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[Documentação de recusa](https://experienceleague.adobe.com/en/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Atributos do cliente da Adobe (CRS) | ✓ | N/D | Os atributos do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir a documentação do GDPR](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/gdpr)</li><li>[Acessar/excluir a documentação da CCPA](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/ccpa)</li><li>Os atributos do cliente não têm a capacidade de transferir dados, portanto, as solicitações de cancelamento de venda não são aplicáveis.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Quando o Experience Platform recebe uma solicitação de exclusão do Privacy Service Experience Platform, ele envia uma confirmação para a Privacy Service de que a solicitação foi recebida e de que os dados afetados foram marcados para exclusão. Os registros são removidos do Data Lake ou do Armazenamento de perfis após a conclusão do trabalho de privacidade. Antes que o trabalho seja concluído, os dados são excluídos por software e, portanto, não podem ser acessados por nenhum serviço da Experience Platform. | <ul><li>[Acessar/excluir a documentação do Data Lake](../catalog/privacy.md)</li><li>[Acessar/excluir a documentação do Serviço de Identidade](../identity-service/privacy.md)</li><li>[Acessar/excluir a documentação do Perfil de Cliente em Tempo Real](../profile/privacy.md)</li><li>[!DNL Experience Platform] atende a [solicitações de recusa para segmentos de público-alvo](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/D | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir a documentação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass Authentication | ✓ | N/D | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir a documentação](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>O Pass não tem a capacidade de transferir dados, portanto, as solicitações de recusa de venda não são aplicáveis.</li></ul> |
| Adobe Target | ✓ | N/D | Todos os dados associados à ID do titular dos dados são excluídos do Perfil do visitante. Dados agregados ou anônimos que não identificam o indivíduo ou que não estão relacionados (como dados de conteúdo) não se aplicam a solicitações de exclusão. | <ul><li>[Acessar/excluir a documentação](https://experienceleague.adobe.com/en/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation)</li><li>[!DNL Target] não tem a capacidade de transferir dados, portanto, as solicitações de recusa de venda não são aplicáveis.</li></ul> |
| Commerce (Personalization) | ✓ | N/D | A Privacy Service exclui [!DNL Commerce] dados armazenados nos serviços SaaS da Commerce para fins de marketing, o que significa que perfis e pedidos de titulares de dados não são mais enviados para aplicativos de marketing da Adobe para uso em campanhas e jornadas de clientes. No entanto, a Privacy Service não exclui dados no aplicativo [!DNL Commerce], pois eles ainda podem ser necessários para necessidades transacionais de comerciante. Os comerciantes são responsáveis por qualquer solicitação de exclusão/acesso de dados no aplicativo [!DNL Commerce]. | <ul><li>[Acessar/excluir a documentação do Commerce](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | N/D | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir a documentação](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests)</li><li>[!DNL Marketo] não tem a capacidade de transferir dados, portanto, as solicitações de recusa de venda não são aplicáveis.</li></ul> |

## Aplicativos de autoatendimento {#self-serve}

Esta é uma lista de aplicativos do [!DNL Experience Cloud] que não estão integrados ao [!DNL Privacy Service] e devem gerenciar internamente suas preocupações com privacidade. São fornecidos links para a documentação de cada aplicativo, juntamente com descrições do conteúdo da documentação.

| Aplicativo | Descrição da documentação |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy) | Uma visão geral de como um administrador de privacidade do cliente ou administrador do AEM pode lidar com solicitações do GDPR. |
| [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/overview) | Certifique-se de que suas instalações do Adobe Commerce estejam em conformidade com os requisitos de legislações de privacidade específicas. |
| [Marcas no Adobe Experience Platform](../tags/ui/client-side/consent.md) | Como desenvolvedores podem usar extensões e o construtor de regras para definir soluções de opt-in/opt-out. |
| [Workfront](https://www.workfront.com/privacy-notice) | Saiba como a Workfront coleta dados pessoais e como um titular de dados pode enviar uma solicitação de privacidade por meio de um formulário. |
