---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da aplicação de políticas
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Visão geral da aplicação de políticas

Depois que os rótulos de uso de dados forem aplicados a [!DNL Platform] conjuntos de dados e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos [!DNL Data Governance] permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política.

Existem dois métodos de execução de políticas, fornecidos por [!DNL Data Governance] elementos sobre [!DNL Platform]: **Aplicação** baseada em API e aplicação **** automática.

## Aplicação baseada em API

A [!DNL Policy Service] API fornece pontos de extremidade que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos dentro do aplicativo de experiência para aplicar adequadamente a conformidade da política de uso de dados.

Consulte o tutorial sobre a aplicação [de](api-enforcement.md) políticas para obter etapas sobre como avaliar políticas usando a API.

## Aplicação automática

Determinados aplicativos criados além de [!DNL Experience Platform] (como [!DNL Real-time Customer Data Platform]) fornecem aplicação automática para políticas de uso de dados. Cada aplicativo mantém seu próprio método de superar violações de políticas e fornecer etapas para resolver problemas.

Consulte a documentação do aplicativo [!DNL Platform]baseado que você está usando para obter mais informações sobre a aplicação automática da política de uso de dados. Para obter informações sobre a aplicação automática de políticas na CDP em tempo real, consulte a visão geral [da CDP Data Governance em tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.