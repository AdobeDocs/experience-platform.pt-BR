---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da aplicação de políticas
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# Visão geral da aplicação de políticas

Depois que os rótulos de uso de dados forem aplicados aos conjuntos de dados da plataforma e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos de controle de dados permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política.

Há dois métodos de aplicação de política fornecidos pelos recursos de controle de dados na plataforma: Aplicação **baseada em** API e imposição **** automática.

## Aplicação baseada em API

A API do Serviço de Política fornece pontos de extremidade que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos dentro do aplicativo de experiência para aplicar adequadamente a conformidade da política de uso de dados.

Consulte o tutorial sobre a aplicação [de](api-enforcement.md) políticas para obter etapas sobre como avaliar políticas usando a API.

## Aplicação automática

Determinados aplicativos criados sobre a Plataforma de experiência (como a Plataforma de dados do cliente em tempo real) fornecem aplicação automática para políticas de uso de dados. Cada aplicativo mantém seu próprio método de superar violações de políticas e fornecer etapas para resolver problemas.

Consulte a documentação do aplicativo baseado na plataforma que você está usando para obter mais informações sobre a aplicação automática da política de uso de dados. Para obter informações sobre a aplicação automática de políticas na CDP em tempo real, consulte a visão geral [da CDP Data Governance em tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.