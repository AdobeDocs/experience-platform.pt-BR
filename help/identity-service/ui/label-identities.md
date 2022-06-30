---
keywords: Experience Platform, home, tópicos populares, identidades de etiquetas
title: Rotular um campo como uma identidade na interface do usuário
description: Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade pelo Serviço de identidade. O namespace da identidade é especificado como parte da rotulagem do campo.
source-git-commit: ae51c9bd07944f26be2809a6d15f9d9e8c2fd5a1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Rotular um campo como uma identidade na interface do usuário

Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade por [!DNL Identity Service]. O namespace da identidade é especificado como parte da rotulagem do campo.

Os seguintes critérios devem ser atendidos para que um campo seja rotulado como identidade:

* Somente campos do tipo string podem ser usados para identidade
* As identidades são reconhecidas apenas nos dados de registro e de série de tempo
* Somente campos PII devem ser marcados como identidade. A escolha de um campo representando dados mais genéricos resultaria em relacionamentos menos precisos e possíveis erros ao acessar identidades relacionadas do gráfico de identidade

Para obter instruções sobre como rotular campos de identidade na interface do usuário, consulte o guia em [definição de campos de identidade na interface do usuário](../../xdm/ui/fields/identity.md).

## Próximas etapas

Para obter mais informações sobre [!DNL Identity Service], consulte o [[!DNL Identity Service] visão geral](../home.md).
