---
keywords: Experience Platform;página inicial;tópicos populares;identidade do rótulo;;home;popular topics;label identities
solution: Experience Platform
title: Rotular um campo como uma identidade
description: Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade pelo Serviço de identidade. O namespace da identidade é especificado como parte da rotulagem do campo.
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Rotular um campo como identidade

Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade por [!DNL Identity Service]. O namespace da identidade é especificado como parte da rotulagem do campo.

Os seguintes critérios devem ser atendidos para que um campo seja rotulado como identidade:

- Somente campos do tipo sequência podem ser usados para identidade
- As identidades só são reconhecidas nos dados de registro e de séries cronológicas
- Somente campos PII devem ser marcados como identidade. Escolher um campo que represente dados mais genéricos resultaria em relacionamentos menos precisos e potencialmente erros ao acessar identidades relacionadas no gráfico de identidade

Para obter instruções sobre como usar a API do Registro de esquema para rotular um campo como identidade, visite [guia de endpoint de descritores](../../xdm/api/descriptors.md#create).

## Próximas etapas

Prosseguir para o próximo tutorial para [listar identidades de cluster](./list-cluster-identites.md)
