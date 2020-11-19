---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Privacidade no Perfil de dados do cliente em tempo real
seo-title: Privacidade no Perfil de dados do cliente em tempo real
description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
seo-description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
translation-type: tm+mt
source-git-commit: bdd80b15258bf4e3c0dee1e260fd3469c76d5885
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Privacidade em [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) ajuda os profissionais de marketing a unir dados de vários sistemas empresariais, permitindo que eles identifiquem, compreendam e engajem melhor seus clientes. A Adobe mantém a privacidade dos dados do consumidor como um princípio fundamental de design e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade dos dados de seus clientes.

A maioria dos [!DNL Real-time CDP] recursos é fornecida pela Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de melhoria da privacidade suportadas pela [!DNL Real-time CDP], com links para a [!DNL Experience Platform] documentação para obter mais informações.

## Atendimento às solicitações de acesso e exclusão do cliente

Os regulamentos legais de privacidade, como o [!DNL General Data Protection Regulation] (RGPD) e o [!DNL California Consumer Privacy Act] (CCPA), concedem aos clientes o direito de solicitar acesso ou a exclusão dos dados pessoais que você coletar deles. Como [!DNL Real-time CDP] aproveita [!DNL Experience Platform] os recursos para coleta e armazenamento de dados, as solicitações do cliente para acessar e excluir seus dados pessoais devem ser gerenciadas dentro [!DNL Platform]. Consulte a visão geral do [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obter mais informações.

## Recursos de opção de não participação

[!DNL Real-time CDP] permite que os clientes opt out por ter seus dados pessoais incluídos em casos de uso de segmentação. As preferências de não participação dos clientes são capturadas e armazenadas por [!DNL Real-time Customer Profile], e podem ser aplicadas excluindo os usuários que se opt out de um segmento usando a lógica booleana (&quot;E NÃO&quot;) no predicado do segmento.

Consulte o documento sobre como [atender às solicitações](../../segmentation/honoring-opt-outs.md) de não participação na documentação do Adobe Experience Platform Segmentation Service para obter mais informações.

## Suporte a IAB TCF 2.0

[!DNL Real-time CDP] faz parte da lista [do](https://iabeurope.eu/vendor-list-tcf-v2-0/) fornecedor registrado para o [!DNL Transparency & Consent Framework (TCF)], conforme descrito pelo [!DNL Interactive Advertising Bureau (IAB)]. Em conformidade com os requisitos do TCF 2.0, [!DNL Real-time CDP] permite coletar dados detalhados de consentimento do cliente e integrá-los aos perfis armazenados do cliente. Esses dados de consentimento podem ser tidos em conta para determinar se determinados perfis estão incluídos em segmentos de audiência exportados, dependendo de seu caso de uso.

Consulte a visão geral sobre o suporte ao [IAB TCF 2.0 em [!DNL Real-time CDP]](./iab/overview.md) para obter mais informações.

## Próximas etapas

Este documento apresentou uma breve introdução aos recursos de privacidade do [!DNL Real-time CDP]. Consulte a documentação vinculada em todo este guia para obter mais informações sobre cada recurso.