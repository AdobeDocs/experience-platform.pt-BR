---
keywords: Experience Platform;página inicial;tópicos populares;identidade do rótulo;;home;popular topics;label identities
title: Rotular um campo como uma identidade na interface
description: Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade pelo Serviço de identidade. O namespace da identidade é especificado como parte da rotulagem do campo.
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Rotular um campo como uma identidade na interface

Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade por [!DNL Identity Service]. O namespace da identidade é especificado como parte da rotulagem do campo.

Os seguintes critérios devem ser atendidos para que um campo seja rotulado como identidade:

* Somente campos do tipo sequência podem ser usados para identidade
* As identidades só são reconhecidas nos dados de registro e de séries cronológicas
* Somente campos PII devem ser marcados como identidade. Escolher um campo que represente dados mais genéricos resultaria em relacionamentos menos precisos e potencialmente erros ao acessar identidades relacionadas no gráfico de identidade

Para obter instruções sobre como rotular campos de identidade na interface, consulte o guia em [definição de campos de identidade na interface](../../xdm/ui/fields/identity.md).

## Próximas etapas

Para obter mais informações sobre [!DNL Identity Service], consulte o [[!DNL Identity Service] visão geral](../home.md).
