---
title: Esquemas no Real-Time Customer Data Platform B2B edition
description: Uma visão geral da função dos esquemas do Experience Data Model (XDM) no Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 09f671af0d04251ab7b0a71528cb4b9745594b1c
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 12%

---

# Esquemas no Real-Time Customer Data Platform B2B edition

O Adobe Real-Time Customer Data Platform B2B edition fornece várias [classes padrão do Experience Data Model (XDM)](../../xdm/schema/composition.md#class) que capturam detalhes sobre entidades de dados B2B essenciais, como contas, oportunidades, campanhas e muito mais. Além disso, o Real-Time CDP B2B edition permite definir relações muitos-para-um entre esses esquemas para que eles possam participar de casos de uso de segmentação avançada.

>[!IMPORTANT]
>
>Esquemas B2B estão disponíveis para uso em aplicativos Experience Platform (por exemplo, em [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>No entanto, você deve ter acesso ao Real-Time CDP B2B edition para que os esquemas B2B (perfis em) participem do [Perfil de Cliente em Tempo Real](../../profile/home.md).

As seguintes classes padrão são fornecidas no Real-Time CDP B2B edition:

* [Conta de negócios XDM](../../xdm/classes/b2b/business-account.md)
* [Relação pessoal da conta de negócios XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campanha de negócios XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membros da campanha de negócios XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relação pessoal de oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing de negócios XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membros da lista de marketing empresarial XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para entender como os esquemas se encaixam no seu fluxo de trabalho B2B, consulte o [tutorial completo](../b2b-tutorial.md).

Para obter etapas sobre como criar uma relação muitos para um entre dois esquemas, consulte o tutorial em [definindo relações de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Se estiver usando uma conexão de origem B2B, você poderá usar uma ferramenta para gerar automaticamente os esquemas necessários e os relacionamentos entre eles. Consulte o guia em [namespaces B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) na documentação de origens para obter mais informações.
