---
title: Esquemas no Real-time Customer Data Platform B2B Edition
description: Uma visão geral da função dos esquemas do Experience Data Model (XDM) no Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: f4ca1efe9c728f50008d7fbaa17aa009dfc18393
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Esquemas no Real-time Customer Data Platform B2B Edition

O Real-time Customer Data Platform B2B Edition fornece vários padrões [Classes do Experience Data Model (XDM)](../../xdm/schema/composition.md#class) que capturam detalhes sobre entidades essenciais de dados B2B, como contas, oportunidades, campanhas e muito mais. Além disso, a CDP B2B Edition em tempo real permite definir relacionamentos muitos para um entre esses esquemas para que eles possam participar de casos de uso de segmentação avançada.

As seguintes classes padrão são fornecidas na Real-time CDP B2B Edition:

* [Conta Comercial XDM](../../xdm/classes/b2b/business-account.md)
* [Relação de Pessoa da Conta Comercial XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campanha comercial XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membros da Campanha Comercial XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidade de negócios XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relação de Pessoa da Oportunidade de Negócios XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing comercial XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membros da Lista de Marketing Comercial XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para obter etapas sobre como criar uma relação muitos para um entre dois schemas, consulte o tutorial em [definição de relações de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Se estiver usando uma conexão de origem B2B, você poderá usar uma ferramenta para gerar automaticamente os esquemas necessários e os relacionamentos entre eles. Consulte o guia sobre [Namespaces B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) na documentação de fontes para obter mais informações.
