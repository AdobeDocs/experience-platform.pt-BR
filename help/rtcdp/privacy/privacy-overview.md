---
title: Privacidade no Perfil de dados do cliente em tempo real
seo-title: Privacidade no Perfil de dados do cliente em tempo real
description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
seo-description: O Perfil de dados do cliente em tempo real permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Privacidade na CDP em tempo real

A Plataforma de dados do cliente em tempo real (CDP em tempo real) ajuda os profissionais de marketing a unir dados de vários sistemas corporativos, permitindo que eles identifiquem, compreendam e envolvam melhor seus clientes. A Adobe mantém a privacidade dos dados do consumidor como um princípio fundamental de design e fornece vários controles para ajudar os profissionais de marketing a gerenciar a privacidade dos dados de seus clientes.

A maioria dos recursos de CDP em tempo real é capacitada pela Adobe Experience Platform. Este documento fornece informações sobre as várias tecnologias de aprimoramento de privacidade suportadas pela CDP em tempo real, com links para a documentação da plataforma Experience para obter mais informações.

## Privacy Service

O Adobe Experience Platform Privacy Service permite simplificar o processo de manter suas operações de dados em conformidade com as regras de privacidade, como o Regulamento Geral de Proteção de Dados (RGPD) e o Ato de Privacidade do Consumidor da Califórnia (CCPA). Como a CDP em tempo real utiliza os recursos da plataforma de experiência para coleta e armazenamento de dados, as solicitações de acesso e exclusão para RGPD e CCPA devem ser gerenciadas dentro da plataforma. Consulte o documento de visão geral [](../../privacy-service/home.md) do Privacy Service para obter uma introdução mais detalhada do serviço.

Existem dois métodos para enviar solicitações individuais de RGPD e CCPA para acesso e exclusão de dados do cliente:

* Use a interface do usuário [](https://gdprui.cloud.adobe.io/) do Privacy Service para criar e monitorar o acesso e a exclusão de solicitações em um espaço de trabalho visual. Consulte o tutorial [](../../privacy-service/ui/overview.md) da interface do usuário do Privacy Service para obter instruções passo a passo.
* Use a API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) do Privacy Service para gerenciar o acesso e a exclusão de solicitações com chamadas RESTful da API. Consulte o tutorial [da API do](../../privacy-service/api/getting-started.md) Privacy Service para obter instruções passo a passo.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Próximas etapas

Este documento apresentou uma breve introdução aos recursos de privacidade da CDP em tempo real. Para obter informações mais detalhadas sobre as práticas recomendadas e as etapas para enviar solicitações de acesso/exclusão, consulte a documentação [do](../../privacy-service/home.md)Privacy Service.