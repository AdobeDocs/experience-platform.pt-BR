---
keywords: governança de dados rtcdp;governança de dados rtcdp;governança de dados do perfil de dados do cliente em tempo real;privacidade rtcdp;privacidade rtcdp
title: Privacidade na Real-time Customer Data Platform
description: O Adobe Real-time Customer Data Platform permite simplificar o processo de manter suas operações de dados em conformidade com as regulamentações de privacidade.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Privacidade na Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) ajuda os profissionais de marketing a unir dados de vários sistemas corporativos, permitindo que eles identifiquem, compreendam e envolvam melhor seus clientes. O Adobe mantém a privacidade de dados do consumidor como um princípio de design fundamental e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade de dados de seus clientes.

A maioria dos [!DNL Real-Time CDP] Os recursos do são fornecidos pelo Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade compatíveis com o [!DNL Real-Time CDP], com links para [!DNL Experience Platform] para obter mais informações.

## Atendimento ao acesso do cliente e solicitações de exclusão

Regulamentos legais de privacidade, como o [!DNL General Data Protection Regulation] (GDPR) e o [!DNL California Consumer Privacy Act] A (CCPA) oferece aos clientes o direito de solicitar acesso ou a exclusão dos dados pessoais coletados deles. Desde [!DNL Real-Time CDP] aproveita [!DNL Experience Platform] recursos para coleta e armazenamento de dados, as solicitações dos clientes para acessar e excluir seus dados pessoais devem ser gerenciadas dentro do [!DNL Platform]. Consulte a visão geral em [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obter mais informações.

>[!IMPORTANT]
>
> As solicitações de privacidade enviadas por meio do Adobe Experience Platform Privacy Service para Adobe Marketo Engage se aplicam somente a clientes B2B do Real-Time CDP.

## Recursos de recusa

[!DNL Real-Time CDP] O permite que os clientes optem por não ter seus dados pessoais incluídos em casos de uso de segmentação. As preferências de cancelamento dos clientes são capturadas e armazenadas pelo [!DNL Real-Time Customer Profile], e podem ser aplicadas excluindo usuários que optaram por não participar de um segmento usando lógica booleana (&quot;AND NOT&quot;) no predicado do segmento.

Consulte o documento sobre [atender às solicitações de recusa](../../segmentation/consents.md) na documentação do Adobe Experience Platform Segmentation Service para obter mais informações.

## Suporte ao IAB TCF 2.0

[!DNL Real-Time CDP] O é construído no Adobe Experience Platform, que faz parte da [lista de fornecedores](https://iabeurope.eu/vendor-list-tcf-v2-0/) para o [!DNL Transparency & Consent Framework (TCF)], conforme delineado pela [!DNL Interactive Advertising Bureau (IAB)]. Em conformidade com os requisitos do TCF 2.0, a Platform permite coletar dados detalhados de consentimento do cliente e integrá-los aos perfis de clientes armazenados. Esses dados de consentimento podem ser fatorados se determinados perfis são incluídos em segmentos de público-alvo exportados, dependendo do caso de uso.

Consulte a visão geral em [Suporte IAB TCF 2.0 no Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma breve introdução aos recursos de privacidade do [!DNL Real-Time CDP]. Consulte a documentação vinculada a este guia para obter mais informações sobre cada recurso.
