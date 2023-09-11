---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Aplicativos de Privacy Service e Experience Cloud
description: Este documento fornece uma referência sobre como configurar diferentes aplicativos Experience Cloud para operações relacionadas à privacidade.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: ed3089a86d6ef25f23e4d69eee7da800d7242545
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 12%

---

# [!DNL Privacy Service] e [!DNL Experience Cloud] aplicativos

Adobe Experience Platform [!DNL Privacy Service] O foi criado para atender a solicitações de privacidade de vários aplicativos da Adobe Experience Cloud. Cada aplicativo suporta diferentes valores de produto e IDs para identificar titulares de dados.

Este documento serve como referência para [!DNL Experience Cloud] documentação do aplicativo que descreve como configurar esse aplicativo para operações relacionadas à privacidade. Isso inclui como formatar e rotular os dados. São abrangidas duas categorias de pedidos:

* [Aplicativos integrados com o Privacy Service](#integrated): aplicativos que podem enviar solicitações de acesso, exclusão ou recusa para o [!DNL Privacy Service].
* [Aplicativos de autoatendimento](#self-serve): aplicativos que devem gerenciar suas solicitações de privacidade internamente e não podem se comunicar com o [!DNL Privacy Service] diretamente.

Revise a documentação de seu [!DNL Experience Cloud] aplicativos para saber como formatar suas solicitações de privacidade e quais valores são compatíveis com essas solicitações.

## Aplicativos integrados com [!DNL Privacy Service] {#integrated}

Veja a seguir uma lista de [!DNL Experience Cloud] aplicativos integrados com [!DNL Privacy Service], incluindo a [!DNL Privacy Service] recursos com os quais são compatíveis, seus protocolos para processar solicitações de exclusão e links para a documentação para obter mais informações.

>[!NOTE]
>
>Todos os produtos integrados respondem às solicitações de privacidade em 30 dias ou menos.

| Aplicativo | Acessar/excluir | Recusar a venda | Excluir comportamento | Documentação e outras considerações |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | A ID do cookie ou a ID do dispositivo do titular dos dados é excluída do sistema, juntamente com todos os dados de custo, clique e receita associados ao cookie. | <ul><li>[Acessar/excluir a documentação do GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Acessar/excluir documentação da CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentação de cancelamento da venda para o CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | O Adobe Analytics fornece ferramentas para rotulação de dados de acordo com sua sensibilidade e restrições contratuais. Os rótulos são uma etapa importante para:<ol><li>Identificação de titulares de dados.</li><li>Determinar quais dados retornar como parte de uma solicitação de acesso.</li><li>Identificação de campos de dados que devem ser excluídos como parte de uma solicitação de exclusão.</li></ol> | <ul><li>[Fluxo de trabalho de privacidade](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=pt-BR)</li><li>[Rotulagem do Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Opção de não participação do Analytics](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Todas as características e segmentos associados ao identificador de Audience Manager incluído na solicitação são excluídos. Além disso, os respectivos identificadores do indivíduo são recusados na coleta de dados e os respectivos mapeamentos de ID são removidos. | <ul><li>[Access](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [excluir](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) documentação</li><li>[Documentação de recusa](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[Solicitações de recusa](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=en#opt-out-requests)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir documentação](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=pt-BR)</li><li>[Documentação de recusa](../segmentation/consents.md)</li></ul> |
| Atributos do cliente do Adobe (CRS) | ✓ | N/D | Os atributos do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir a documentação do GDPR](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=pt-BR)</li><li>[Acessar/excluir documentação da CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=pt-BR)</li><li>Os atributos do cliente não têm a capacidade de transferir dados, portanto, as solicitações de cancelamento de venda não são aplicáveis.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Quando o Experience Platform recebe uma solicitação de exclusão do Privacy Service, a Platform envia uma confirmação para o Privacy Service de que a solicitação foi recebida e de que os dados afetados foram marcados para exclusão. Os registros são removidos do Data Lake ou do Armazenamento de perfis após a conclusão do trabalho de privacidade. Antes que o trabalho seja concluído, os dados são excluídos por software e, portanto, não podem ser acessados por nenhum serviço da Platform. | <ul><li>[Acessar/excluir a documentação do Data Lake](../catalog/privacy.md)</li><li>[Acessar/excluir a documentação do Serviço de identidade](../identity-service/privacy.md)</li><li>[Acessar/excluir a documentação do Perfil do cliente em tempo real](../profile/privacy.md)</li><li>[!DNL Experience Platform] honras [solicitações de recusa para segmentos de público-alvo](../segmentation/consents.md).</li></ul> |
| Autenticação Adobe Primetime | ✓ | N/D | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir documentação](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] O não tem a capacidade de transferir dados, portanto, os pedidos de recusa de venda não são aplicáveis.</li></ul> |
| Adobe Target | ✓ | N/D | Todos os dados associados à ID do titular dos dados são excluídos do Perfil do visitante. Dados agregados ou anônimos que não identificam o indivíduo ou que não estão relacionados (como dados de conteúdo) não se aplicam a solicitações de exclusão. | <ul><li>[Acessar/excluir documentação](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=pt-BR)</li><li>[!DNL Target] O não tem a capacidade de transferir dados, portanto, os pedidos de recusa de venda não são aplicáveis.</li></ul> |
| Marketo Engage | ✓ | N/D | Os dados armazenados do titular dos dados são excluídos do sistema. | <ul><li>[Acessar/excluir documentação](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] O não tem a capacidade de transferir dados, portanto, os pedidos de recusa de venda não são aplicáveis.</li></ul> |

{style="table-layout:auto"}

## Aplicativos de autoatendimento {#self-serve}

Veja a seguir uma lista de [!DNL Experience Cloud] aplicativos que não estão integrados com o [!DNL Privacy Service] e devem gerenciar internamente suas preocupações com a privacidade. São fornecidos links para a documentação de cada aplicativo, juntamente com descrições do conteúdo da documentação.

| Aplicativo | Descrição da documentação |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=pt-BR) | Uma visão geral das funcionalidades do GDPR para o Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Uma visão geral de como um administrador de privacidade do cliente ou administrador de AEM pode lidar com solicitações do GDPR. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Etapas para fazer solicitações de acesso e exclusão do GDPR usando o Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Certifique-se de que suas instalações em Magento Commerce estejam em conformidade com os requisitos de legislações de privacidade específicas. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Saiba como os regulamentos de privacidade se aplicam ao Marketo. |
| [Tags na Adobe Experience Platform](../tags/ui/client-side/consent.md) | Como desenvolvedores podem usar extensões e o construtor de regras para definir soluções de opt-in/opt-out. |
| [Workfront](https://www.workfront.com/privacy-notice) | Saiba como a Workfront coleta dados pessoais e como um titular de dados pode enviar uma solicitação de privacidade por meio de um formulário. |

{style="table-layout:auto"}
