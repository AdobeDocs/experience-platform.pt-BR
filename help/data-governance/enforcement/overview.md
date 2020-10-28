---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Visão geral da aplicação de políticas
topic: enforcement
description: Depois que os rótulos de uso de dados forem aplicados aos conjuntos de dados da Adobe Experience Platform e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos de controle de dados permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política. Há dois métodos de aplicação de política fornecidos pelos recursos de controle de dados na Plataforma, aplicação baseada em API e imposição automática.
translation-type: tm+mt
source-git-commit: 83f1392ffab3571ebd91325123fbe7095ad59e28
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Visão geral da aplicação de políticas

Depois que os rótulos de uso de dados forem aplicados a [!DNL Platform] conjuntos de dados e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos [!DNL Data Governance] permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política.

Existem dois métodos de execução de políticas, fornecidos por [!DNL Data Governance] elementos sobre [!DNL Platform]: Aplicação baseada em API e aplicação automática.

## Aplicação baseada em API

A [!DNL Policy Service] API fornece pontos de extremidade que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos dentro do aplicativo de experiência para aplicar adequadamente a conformidade da política de uso de dados.

Consulte o tutorial sobre a aplicação [de](api-enforcement.md) políticas para obter etapas sobre como avaliar políticas usando a API.

## Aplicação automática

Determinados aplicativos criados além de [!DNL Experience Platform] (como [!DNL Real-time Customer Data Platform]) fornecem aplicação automática para políticas de uso de dados. Cada aplicativo mantém seu próprio método de superar violações de políticas e fornecer etapas para resolver problemas.

A aplicação automática de políticas no CDP em tempo real utiliza recursos de linhagem de dados, classificação de dados e gerenciamento de políticas para avaliar e superar violações de políticas. Consulte a visão geral [do CDP Data Governance em tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) real para obter mais informações.