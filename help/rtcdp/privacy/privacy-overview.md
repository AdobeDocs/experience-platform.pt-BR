---
keywords: controle de dados rtcdp;controle de dados rtcdp;controle de dados de perfil de dados de cliente em tempo real;privacidade rtcdp;rtcdp privacidade
title: Privacidade no Perfil de dados do cliente em tempo real
seo-title: Privacidade no Perfil de dados do cliente em tempo real
description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
seo-description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Privacidade em [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) ajuda os profissionais de marketing a unir dados de vários sistemas empresariais, permitindo que eles identifiquem, compreendam e engajem melhor seus clientes. A Adobe mantém a privacidade dos dados do consumidor como um princípio fundamental de design e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade dos dados de seus clientes.

A maioria dos recursos [!DNL Real-time CDP] é capacitada pela Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade suportadas por [!DNL Real-time CDP], com links para a documentação [!DNL Experience Platform] para obter mais informações.

## Atendimento às solicitações de acesso e exclusão do cliente

Os regulamentos legais de privacidade, como o [!DNL General Data Protection Regulation] (GDPR) e o [!DNL California Consumer Privacy Act] (CCPA), concedem aos clientes o direito de solicitar acesso ou a exclusão dos dados pessoais coletados deles. Como [!DNL Real-time CDP] aproveita os recursos [!DNL Experience Platform] para coleta e armazenamento de dados, as solicitações do cliente para acessar e excluir seus dados pessoais devem ser gerenciadas em [!DNL Platform]. Consulte a visão geral em [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obter mais informações.

## Recursos de opção de não participação

[!DNL Real-time CDP] permite que os clientes opt out por ter seus dados pessoais incluídos em casos de uso de segmentação. As preferências de não participação dos clientes são capturadas e armazenadas por [!DNL Real-time Customer Profile], e podem ser aplicadas excluindo os usuários que se opt out de um segmento usando a lógica booleana (&quot;E NÃO&quot;) no predicado do segmento.

Consulte o documento em [cumprimento de solicitações de não participação](../../segmentation/honoring-opt-outs.md) na documentação do Adobe Experience Platform Segmentation Service para obter mais informações.

## Suporte a IAB TCF 2.0

[!DNL Real-time CDP] é desenvolvida na Adobe Experience Platform, que faz parte da lista de  [fornecedores registrados ](https://iabeurope.eu/vendor-list-tcf-v2-0/) para o  [!DNL Transparency & Consent Framework (TCF)], conforme descrito pelo  [!DNL Interactive Advertising Bureau (IAB)]. Em conformidade com os requisitos do TCF 2.0, a Plataforma permite coletar dados detalhados de consentimento do cliente e integrá-los aos perfis armazenados do cliente. Esses dados de consentimento podem ser tidos em conta para determinar se determinados perfis estão incluídos em segmentos de audiência exportados, dependendo de seu caso de uso.

Consulte a visão geral sobre o suporte a [IAB TCF 2.0 em Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma breve introdução aos recursos de privacidade do [!DNL Real-time CDP]. Consulte a documentação vinculada em todo este guia para obter mais informações sobre cada recurso.