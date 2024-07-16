---
title: Guia da API do Privacy Service
description: Saiba como usar a API do Privacy Service para gerenciar programaticamente processos de privacidade para aplicativos compatíveis da Adobe Experience Cloud.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---

# [!DNL Privacy Service] Manual da API

A API de Privacy Service fornece vários endpoints que permitem gerenciar programaticamente os processos de privacidade da sua organização. Esses endpoints são descritos abaixo. Visite os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

>[!NOTE]
>
>Este guia aborda como usar a API [!DNL Privacy Service]. Para obter detalhes sobre como usar a interface, consulte a [visão geral sobre a interface do Privacy Service](../ui/overview.md).

Para exibir todos os pontos de extremidade e operações CRUD disponíveis, visite a [referência da API Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Processos de privacidade

Quando o Privacy Service recebe uma solicitação para acessar ou excluir os dados pessoais de um indivíduo, o sistema cria processos de privacidade para atender a essa solicitação. Cada trabalho de privacidade contém informações de identidade relacionadas ao titular dos dados, metadados sobre o produto do Adobe Experience Cloud ao qual o trabalho se aplica e o status de processamento do trabalho.

O ponto de extremidade `/jobs` permite criar e recuperar trabalhos de privacidade para sua organização. Para saber como usar este ponto de extremidade, consulte o [manual do ponto de extremidade de trabalhos de privacidade](./privacy-jobs.md).

## Consentimento

Certos regulamentos exigem o consentimento explícito do cliente antes que seus dados pessoais possam ser coletados. O ponto de extremidade `/consent` permite processar solicitações de consentimento do cliente e integrá-las ao seu fluxo de trabalho de privacidade. Consulte o [manual de endpoint de consentimento](./consent.md) para saber mais.

## Próximas etapas

Para começar a fazer chamadas usando a API Privacy Service, leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
