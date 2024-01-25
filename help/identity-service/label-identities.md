---
keywords: Experience Platform;página inicial;tópicos populares;identidade do rótulo;;home;popular topics;label identities
title: Rotular um campo como uma identidade na interface
description: Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade pelo Serviço de identidade. O namespace da identidade é especificado como parte da rotulagem do campo.
hide: true
hidefromtoc: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 0d111241658b4014d1ca2e6013d21a4782d81be9
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# Rotular um campo como uma identidade na interface

Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade por [!DNL Identity Service]. O namespace da identidade é especificado como parte da rotulagem do campo.

Os seguintes critérios devem ser atendidos para que um campo seja rotulado como identidade:

* Somente campos do tipo sequência podem ser usados para identidade
* As identidades só são reconhecidas nos dados de registro e de séries cronológicas
* Somente campos PII devem ser marcados como identidade. Escolher um campo que represente dados mais genéricos resultaria em relacionamentos menos precisos e potencialmente erros ao acessar identidades relacionadas no gráfico de identidade

Para obter instruções sobre como rotular campos de identidade na interface, consulte o guia em [definição de campos de identidade na interface](../xdm/ui/fields/identity.md).

## Próximas etapas

Para obter mais informações sobre a [!DNL Identity Service], consulte a [[!DNL Identity Service] visão geral](./home.md).
