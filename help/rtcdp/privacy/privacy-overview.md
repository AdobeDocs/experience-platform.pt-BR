---
keywords: governança de dados rtcdp; governança de dados rtcdp; governança de dados de perfil de cliente em tempo real; privacidade rtcdp; privacidade rtcdp
title: Privacidade na plataforma de dados do cliente em tempo real
seo-title: Privacidade na plataforma de dados do cliente em tempo real
description: A Plataforma de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
seo-description: A Plataforma de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Privacidade na plataforma de dados do cliente em tempo real

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) ajuda os profissionais de marketing a unir dados de vários sistemas empresariais, permitindo que eles identifiquem, compreendam e envolvam melhor seus clientes. O Adobe mantém a privacidade dos dados do consumidor como um princípio fundamental de design e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade dos dados de seus clientes.

A maioria dos recursos [!DNL Real-time CDP] é fornecida pela Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade compatíveis com [!DNL Real-time CDP], com links para a documentação [!DNL Experience Platform] para obter mais informações.

## Respeito às solicitações de acesso e exclusão do cliente

Regulamentos legais de privacidade como [!DNL General Data Protection Regulation] (GDPR) e [!DNL California Consumer Privacy Act] (CCPA) dão aos clientes o direito de solicitar acesso ou excluir os dados pessoais coletados deles. Como [!DNL Real-time CDP] aproveita os recursos [!DNL Experience Platform] para coleta e armazenamento de dados, as solicitações do cliente para acessar e excluir seus dados pessoais devem ser gerenciadas em [!DNL Platform]. Consulte a visão geral em [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obter mais informações.

## Recursos de rejeição

[!DNL Real-time CDP] O permite que os clientes optem por não ter seus dados pessoais incluídos em casos de uso de segmentação. As preferências de não participação dos clientes são capturadas e armazenadas por [!DNL Real-time Customer Profile], e podem ser aplicadas excluindo usuários que optaram por não participar de um segmento usando a lógica booleana (&quot;E NÃO&quot;) no predicado do segmento.

Consulte o documento sobre [solicitações de recusa](../../segmentation/consents.md) na documentação do Serviço de segmentação do Adobe Experience Platform para obter mais informações.

## Suporte ao IAB TCF 2.0

[!DNL Real-time CDP] O é criado na Adobe Experience Platform, que faz parte da lista de  [fornecedores registrados ](https://iabeurope.eu/vendor-list-tcf-v2-0/) para o  [!DNL Transparency & Consent Framework (TCF)], conforme descrito pelo  [!DNL Interactive Advertising Bureau (IAB)]. Em conformidade com os requisitos do TCF 2.0, o Platform permite coletar dados detalhados de consentimento do cliente e integrá-los aos perfis de cliente armazenados. Esses dados de consentimento podem ser fatorado para determinar se determinados perfis estão incluídos em segmentos de público-alvo exportados, dependendo do caso de uso.

Consulte a visão geral do suporte ao [IAB TCF 2.0 no Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma breve introdução aos recursos de privacidade de [!DNL Real-time CDP]. Revise a documentação vinculada a este guia para obter mais informações sobre cada recurso.
