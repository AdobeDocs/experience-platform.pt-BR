---
keywords: Experience Platform;home;popular topics;Aplicação automática;Aplicação baseada em API;controle de dados
solution: Experience Platform
title: Visão geral da aplicação de políticas
topic: guide
description: Depois que os rótulos de uso de dados forem aplicados aos conjuntos de dados da Adobe Experience Platform e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos de controle de dados permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política. Há dois métodos de aplicação de política fornecidos pelos recursos de controle de dados na Plataforma, aplicação baseada em API e imposição automática.
translation-type: tm+mt
source-git-commit: acc4fa59a4808ed9a32c2aaf664039e0d12dc1d8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Visão geral da aplicação de políticas

Depois que os rótulos de uso de dados forem aplicados a [!DNL Platform] conjuntos de dados e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos [!DNL Data Governance] permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política.

Há dois métodos de imposição de política fornecidos pelos recursos [!DNL Data Governance] em [!DNL Platform]: Aplicação baseada em API e aplicação automática.

## Aplicação baseada em API

A API [!DNL Policy Service] fornece pontos de extremidade que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos dentro do aplicativo de experiência para aplicar adequadamente a conformidade da política de uso de dados.

Consulte o tutorial em [Aplicação baseada em API](./api-enforcement.md) para obter etapas sobre como avaliar políticas usando a API.

## Aplicação automática

O Experience Platform utiliza recursos de linhagem de dados, classificação de dados e gerenciamento de políticas para avaliar e destacar automaticamente violações de políticas. Consulte a visão geral em [aplicação automática de política](./auto-enforcement.md) para obter mais informações.