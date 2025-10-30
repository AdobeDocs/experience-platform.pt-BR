---
title: Esquemas no Real-Time Customer Data Platform B2B edition
description: Uma visão geral da função dos esquemas do Experience Data Model (XDM) no Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 8%

---

# Esquemas no Real-Time Customer Data Platform B2B edition

O Adobe Real-Time Customer Data Platform B2B edition fornece várias [classes padrão do Experience Data Model (XDM)](../../xdm/schema/composition.md#class) que capturam detalhes sobre entidades de dados B2B essenciais, como contas, oportunidades, campanhas e muito mais. Além disso, o Real-Time CDP B2B edition permite definir relações muitos-para-um entre esses esquemas para que eles possam participar de casos de uso de segmentação avançada.

>[!IMPORTANT]
>
>Esquemas B2B estão disponíveis para uso em aplicativos Experience Platform (por exemplo, em [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>No entanto, você deve ter acesso ao Real-Time CDP B2B edition para que os esquemas B2B (perfis em) participem do [Perfil de Cliente em Tempo Real](../../profile/home.md).

As seguintes classes padrão são fornecidas no Real-Time CDP B2B edition:

* [Conta de negócios XDM](../../xdm/classes/b2b/business-account.md)
* [Relação pessoal da conta de negócios XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campanha de negócios XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membros da campanha de negócios XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relação pessoal de oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing de negócios XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membros da lista de marketing de negócios XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para entender como os esquemas se encaixam no seu fluxo de trabalho B2B, consulte o [tutorial completo](../b2b-tutorial.md).

Para obter etapas sobre como criar uma relação muitos para um entre dois esquemas, consulte o tutorial em [definindo relações de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Se estiver usando uma conexão de origem B2B, você poderá usar uma ferramenta para gerar automaticamente os esquemas necessários e os relacionamentos entre eles. Consulte o guia em [namespaces B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) na documentação de origens para obter mais informações.


A tabela a seguir contém informações sobre a configuração subjacente de esquemas B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Nome do esquema | Classe base | Grupos de campos | [!DNL Profile] no esquema | Identidade principal | Namespace de identidade principal | Identidade secundária | Namespace de identidade secundário | Relação | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Conta B2B | [Conta de negócios XDM](../../xdm/classes/b2b/business-account.md) | Detalhes da conta de negócios XDM | Habilitado | `accountKey.sourceKey` na classe base | Conta B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Conta B2B | <ul><li>`accountParentKey.sourceKey` no grupo de campos Detalhes da Conta de Negócios XDM</li><li>Propriedade de destino: `/accountKey/sourceKey`</li><li>Tipo: um para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: conta B2B</li></ul> |  |
| Pessoa B2B | [Perfil individual XDM](../../xdm/classes/individual-profile.md) | <ul><li>Detalhes de pessoa de negócios XDM</li><li>Componentes de pessoa de negócios XDM</li><li>IdentityMap</li><li>Detalhes sobre consentimento e preferência</li></ul> | Habilitado | `b2b.personKey.sourceKey` no grupo de campos de detalhes de pessoa de negócios XDM | Pessoa B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` do grupo de campos Detalhes de pessoa de negócios XDM</li><li>`workEmail.address` do grupo de campos Detalhes de pessoa de negócios XDM</ol></li> | <ol><li>Pessoa B2B</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` do grupo de campos Componentes de Pessoa de Negócios XDM</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: accountKey.sourceKey</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |  |
| Oportunidade B2B | [Oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity.md) | Detalhes de oportunidades de negócios XDM | Habilitado | `opportunityKey.sourceKey` na classe base | Oportunidade B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Oportunidade B2B | <ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Oportunidades</li></ul> |  |
| Relação pessoal da oportunidade B2B | [Relação pessoal de oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | Habilitado | `opportunityPersonKey.sourceKey` na classe base | Relação pessoal da oportunidade B2B | | | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: b2b.personKey.sourceKey</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Oportunidades</li></ul>**Segundo relacionamento**<ul><li>`opportunityKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: Oportunidade B2B </li><li>Namespace: oportunidade B2B </li><li>Propriedade de destino: `opportunityKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Oportunidade</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |  |
| Campanha B2B | [Campanha de negócios XDM](../../xdm/classes/b2b/business-campaign.md) | Detalhes da campanha de negócios XDM | Habilitado | `campaignKey.sourceKey` na classe base | Campanha B2B | | | | |
| Membro da campanha B2B | [Membros da campanha de negócios XDM](../../xdm/classes/b2b/business-campaign-members.md) | Detalhes do membro da campanha de negócios XDM | Habilitado | `ccampaignMemberKey.sourceKey` na classe base | Membro da campanha B2B | | | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Campanhas</li></ul>**Segundo relacionamento**<ul><li>`campaignKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: campanha B2B</li><li>Namespace: campanha B2B</li><li>Propriedade de destino: `campaignKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Campanha</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |  |
| Lista de marketing B2B | [Lista de marketing de negócios XDM](../../xdm/classes/b2b/business-marketing-list.md) | None | Habilitado | `marketingListKey.sourceKey` na classe base | Lista de marketing B2B | None | None | None | A Lista Estática não está sincronizada a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Membro da lista de marketing B2B | [Membros da Lista de Marketing Comercial XDM](../../xdm/classes/b2b/business-marketing-list-members.md) | None | Habilitado | `marketingListMemberKey.sourceKey` na classe base | Membro da lista de marketing B2B | None | None | **Primeiro relacionamento**<ul><li>`PersonKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Listas de marketing</li></ul>**Segundo relacionamento**<ul><li>`marketingListKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: Lista de marketing B2B</li><li>Namespace: lista de marketing B2B</li><li>Propriedade de destino: `marketingListKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Lista de marketing</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> | O membro da lista estática não é sincronizado a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Relação pessoal da conta B2B | [Relação pessoal da conta comercial XDM](../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidade | Habilitado | `accountPersonKey.sourceKey` na classe base | Relação pessoal da conta B2B | None | None | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.SourceKey`</li><li>Nome do relacionamento do esquema atual: People</li><li>Nome do relacionamento do esquema de referência: Conta</li></ul>**Segundo relacionamento**<ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |  |

{style="table-layout:auto"}

