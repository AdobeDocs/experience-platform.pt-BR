---
keywords: Experience Platform;home;popular topics;label identities
solution: Experience Platform
title: Rotular um campo como identidade
topic: api guide
description: Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade pelo Serviço de identidade. A namespace da identidade é especificada como parte da rotulagem do campo.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# Rotular um campo como identidade

Os campos que contêm informações de identificação pessoal (PII) podem ser rotulados como campos de identidade. Um valor fornecido em um campo de identidade é interpretado como uma identidade por [!DNL Identity Service]. A namespace da identidade é especificada como parte da rotulagem do campo.

Os seguintes critérios devem ser atendidos para que um campo seja rotulado como identidade:

- Somente campos de tipo de string podem ser usados para identidade
- As identidades só são reconhecidas nos dados de registro e de série cronológica
- Somente campos PII devem ser marcados como identidade. A escolha de um campo que representa dados mais genéricos resultaria em relacionamentos menos precisos e possíveis erros ao acessar identidades relacionadas do gráfico de identidade

Para obter instruções sobre como usar a API do Registro do Schema para rotular um campo como identidade, visite [Criar um descritor](../../xdm/api/descriptors.md).

## Próximas etapas

Vá para o próximo tutorial para [lista de identidades de cluster](./list-cluster-identites.md)