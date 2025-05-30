---
keywords: governança de dados rtcdp;governança de dados rtcdp;governança de dados do perfil de dados do cliente em tempo real;privacidade rtcdp;privacidade rtcdp
title: Privacidade na Real-Time Customer Data Platform
description: O Adobe Real-Time Customer Data Platform permite simplificar o processo de manter suas operações de dados em conformidade com as regulamentações de privacidade.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Privacidade na Real-Time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) ajuda os profissionais de marketing a reunir dados de vários sistemas corporativos, permitindo que eles identifiquem, compreendam e envolvam melhor seus clientes. A Adobe considera a privacidade de dados do consumidor como um princípio de design fundamental e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade de dados de seus clientes.

A maioria dos recursos do [!DNL Real-Time CDP] é da plataforma Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade com suporte no [!DNL Real-Time CDP], com links para a documentação do [!DNL Experience Platform] para obter mais informações.

## Atendimento ao acesso do cliente e solicitações de exclusão

Regulamentos legais de privacidade, como o [!DNL General Data Protection Regulation] (GDPR) e o [!DNL California Consumer Privacy Act] (CCPA), dão aos clientes o direito de solicitar acesso ou a exclusão dos dados pessoais coletados deles. Como o [!DNL Real-Time CDP] aproveita os recursos do [!DNL Experience Platform] para coleta e armazenamento de dados, as solicitações do cliente para acessar e excluir seus dados pessoais devem ser gerenciadas no [!DNL Experience Platform]. Consulte a visão geral no [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obter mais informações.

>[!IMPORTANT]
>
> As solicitações de privacidade enviadas por meio do Adobe Experience Platform Privacy Service para Adobe Marketo Engage se aplicam somente a clientes B2B do Real-Time CDP.

## Recursos de recusa

O [!DNL Real-Time CDP] permite que os clientes optem por não ter seus dados pessoais incluídos em casos de uso de segmentação. As preferências de recusa dos clientes são capturadas e armazenadas por [!DNL Real-Time Customer Profile] e podem ser aplicadas excluindo os usuários que optaram por não participar de um público-alvo usando lógica booleana (&quot;AND NOT&quot;) no predicado de segmento.

Consulte o documento sobre [atendimento às solicitações de recusa](../../segmentation/tutorials/consents.md) na documentação do Serviço de segmentação da Adobe Experience Platform para obter mais informações.

## Suporte ao IAB TCF 2.0

[!DNL Real-Time CDP] é compilado no Adobe Experience Platform, que faz parte da [lista de fornecedores](https://iabeurope.eu/vendor-list-tcf/) registrada para o [!DNL Transparency & Consent Framework (TCF)], conforme descrito pelo [!DNL Interactive Advertising Bureau (IAB)]. Em conformidade com os requisitos do TCF 2.0, o Experience Platform permite coletar dados detalhados de consentimento do cliente e integrá-los aos perfis de clientes armazenados. Esses dados de consentimento podem ser fatorados se determinados perfis são incluídos em públicos exportados, dependendo de seu caso de uso.

Consulte a visão geral sobre o [suporte ao IAB TCF 2.0 no Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma breve introdução aos recursos de privacidade do [!DNL Real-Time CDP]. Consulte a documentação vinculada a este guia para obter mais informações sobre cada recurso.
