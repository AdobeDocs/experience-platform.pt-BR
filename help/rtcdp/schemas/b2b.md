---
title: Esquemas na Plataforma de dados do cliente em tempo real B2B Edition
description: Uma visão geral da função dos esquemas do Experience Data Model (XDM) na Plataforma de dados do cliente em tempo real B2B Edition.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Esquemas na Plataforma de dados do cliente em tempo real B2B Edition (Beta)

>[!IMPORTANT]
>
>A Plataforma de dados do cliente em tempo real B2B Edition está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

A Plataforma de dados do cliente em tempo real B2B Edition fornece várias classes padrão [Experience Data Model (XDM)](../../xdm/schema/composition.md#class) que capturam detalhes sobre entidades essenciais de dados B2B, como contas, oportunidades, campanhas e muito mais. Além disso, a CDP B2B Edition em tempo real permite definir relacionamentos muitos para um entre esses esquemas para que eles possam participar de casos de uso de segmentação avançada.

As seguintes classes padrão são fornecidas na Real-time CDP B2B Edition:

* [Conta Comercial XDM](../../xdm/classes/b2b/business-account.md)
* [Relação de Pessoa da Conta Comercial XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campanha comercial XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membros da Campanha Comercial XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relação de Pessoa da Oportunidade de Negócios XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing comercial XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membros da Lista de Marketing Comercial XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para obter etapas sobre como criar uma relação muitos para um entre dois schemas, consulte o tutorial em [definindo relações de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Se estiver usando uma conexão de origem B2B, você poderá usar uma ferramenta para gerar automaticamente os esquemas necessários e os relacionamentos entre eles. Consulte o guia em [namespaces B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) na documentação de fontes para obter mais informações.
