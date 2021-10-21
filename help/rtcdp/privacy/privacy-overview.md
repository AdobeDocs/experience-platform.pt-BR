---
keywords: governança de dados rtcdp; governança de dados rtcdp; governança de dados de perfil de cliente em tempo real; privacidade rtcdp; privacidade rtcdp
title: Privacidade no Real-time Customer Data Platform
seo-title: Privacy in Real-time Customer Data Platform
description: O Real-time Customer Data Platform permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
seo-description: Real-time Customer Data Platform allows you to streamline the process of keeping your data operations compliant with privacy regulations.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: e3519817559dca372e228ed19bba4f9adf279768
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Privacidade no Real-time Customer Data Platform

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) ajuda os profissionais de marketing a unir dados de vários sistemas empresariais, permitindo que eles identifiquem, compreendam e engajem melhor seus clientes. O Adobe mantém a privacidade dos dados do consumidor como um princípio fundamental de design e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade dos dados de seus clientes.

A maioria dos [!DNL Real-time CDP] Os recursos do são fornecidos pela Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade compatíveis com o [!DNL Real-time CDP], com links para [!DNL Experience Platform] documentação para obter mais informações.

## Respeito às solicitações de acesso e exclusão do cliente

Regulamentos legais de privacidade, como o [!DNL General Data Protection Regulation] (GDPR) e o [!DNL California Consumer Privacy Act] (CCPA) concede aos clientes o direito de solicitar acesso ou excluir os dados pessoais coletados deles. Since [!DNL Real-time CDP] aproveitadores [!DNL Experience Platform] recursos para coleta e armazenamento de dados, as solicitações do cliente para acessar e excluir seus dados pessoais devem ser gerenciadas em [!DNL Platform]. Consulte a visão geral em [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obter mais informações.

>[!IMPORTANT]
>
> As solicitações de privacidade enviadas pelo Adobe Experience Platform Privacy Service para o Adobe Marketo Engage aplicam-se somente aos clientes da CDP B2B em tempo real.

## Recursos de rejeição

[!DNL Real-time CDP] O permite que os clientes optem por não ter seus dados pessoais incluídos em casos de uso de segmentação. As preferências de não participação dos clientes são capturadas e armazenadas pelo [!DNL Real-time Customer Profile]e podem ser aplicadas excluindo usuários que optaram por não participar de um segmento usando a lógica booleana (&quot;E NÃO&quot;) no predicado do segmento.

Consulte o documento em [atender às solicitações de recusa](../../segmentation/consents.md) na documentação do Serviço de segmentação do Adobe Experience Platform para obter mais informações.

## Suporte ao IAB TCF 2.0

[!DNL Real-time CDP] O é criado no Adobe Experience Platform, que faz parte do [lista de fornecedores](https://iabeurope.eu/vendor-list-tcf-v2-0/) para [!DNL Transparency & Consent Framework (TCF)], conforme descrito pelo [!DNL Interactive Advertising Bureau (IAB)]. Em conformidade com os requisitos do TCF 2.0, o Platform permite coletar dados detalhados de consentimento do cliente e integrá-los aos perfis de cliente armazenados. Esses dados de consentimento podem ser fatorado para determinar se determinados perfis estão incluídos em segmentos de público-alvo exportados, dependendo do caso de uso.

Consulte a visão geral em [Suporte ao IAB TCF 2.0 no Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma breve introdução aos recursos de privacidade da [!DNL Real-time CDP]. Revise a documentação vinculada a este guia para obter mais informações sobre cada recurso.
