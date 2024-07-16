---
title: Esquemas no Real-time Customer Data Platform B2B Edition
description: Uma visão geral da função dos esquemas do Experience Data Model (XDM) no Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 13%

---

# Esquemas no Real-time Customer Data Platform B2B Edition

O Adobe Real-time Customer Data Platform B2B Edition fornece várias [classes do Experience Data Model (XDM)](../../xdm/schema/composition.md#class) padrão que capturam detalhes sobre entidades de dados B2B essenciais, como contas, oportunidades, campanhas e muito mais. Além disso, o Real-Time CDP B2B Edition permite definir relações muitos para um entre esses esquemas para que eles possam participar de casos de uso de segmentação avançada.

>[!IMPORTANT]
>
>Você deve ter acesso ao Real-Time CDP B2B Edition para que os esquemas B2B participem do [Perfil do cliente em tempo real](../../profile/home.md).

As seguintes classes padrão são fornecidas no Real-Time CDP B2B Edition:

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
