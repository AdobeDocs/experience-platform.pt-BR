---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Privacidade no Perfil de dados do cliente em tempo real
seo-title: Privacidade no Perfil de dados do cliente em tempo real
description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
seo-description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Privacidade na CDP em tempo real

[!DNL Real-time Customer Data Platform] (CDP em tempo real) ajuda os profissionais de marketing a unir dados de vários sistemas corporativos, permitindo que eles identifiquem, entendam e engajem melhor seus clientes. A Adobe mantém a privacidade dos dados do consumidor como um princípio fundamental de design e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade dos dados de seus clientes.

A maioria dos recursos de CDP em tempo real é capacitada pela Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade suportadas pela CDP em tempo real, com links para a [!DNL Experience Platform] documentação para obter mais informações.

## [!DNL Privacy Service]

A Adobe Experience Platform [!DNL Privacy Service] permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade, como o [!DNL General Data Protection Regulation] (RGPD) e o [!DNL California Consumer Privacy Act] (CCPA). Como a CDP em tempo real utiliza [!DNL Experience Platform] recursos para coleta e armazenamento de dados, as solicitações de acesso e exclusão para RGPD e CCPA devem ser gerenciadas dentro [!DNL Platform]. Consulte o documento de visão geral [do](../../privacy-service/home.md) Privacy Service para obter uma introdução mais detalhada do serviço.

Existem dois métodos para enviar solicitações individuais de RGPD e CCPA para acesso e exclusão de dados do cliente:

* Use a [[!DNL Privacy Service UI]](https://gdprui.cloud.adobe.io/) para criar e monitorar o acesso e excluir solicitações em um espaço de trabalho visual. Consulte o tutorial [da interface do usuário do](../../privacy-service/ui/overview.md) Privacy Service para obter instruções passo a passo.
* Use a [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) para gerenciar o acesso e a exclusão de solicitações com chamadas RESTful API. Consulte o tutorial [da API de](../../privacy-service/api/getting-started.md) Privacy Service para obter instruções passo a passo.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Próximas etapas

Este documento apresentou uma breve introdução aos recursos de privacidade da CDP em tempo real. Para obter informações mais detalhadas sobre as práticas recomendadas e as etapas para enviar solicitações de acesso/exclusão, consulte a documentação [do](../../privacy-service/home.md)Privacy Service.