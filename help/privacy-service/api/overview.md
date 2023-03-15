---
title: Guia da API do Privacy Service
description: Saiba como usar a API do Privacy Service para gerenciar programaticamente processos de privacidade para aplicativos compatíveis da Adobe Experience Cloud.
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: bda8d0ee1db4b58b4b856a23a8790cd7f76c0656
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# [!DNL Privacy Service] Manual da API

A API de Privacy Service fornece vários endpoints que permitem gerenciar programaticamente os processos de privacidade da sua organização. Esses endpoints são descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

>[!NOTE]
>
>Este guia aborda como usar o [!DNL Privacy Service] API. Para obter detalhes sobre como usar a interface, consulte a [Visão geral da interface do Privacy Service](../ui/overview.md).

Para exibir todos os endpoints e operações CRUD disponíveis, visite o [Referência da API do Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Trabalhos de privacidade

Quando o Privacy Service recebe uma solicitação para acessar ou excluir os dados pessoais de um indivíduo, o sistema cria processos de privacidade para atender a essa solicitação. Cada trabalho de privacidade contém informações de identidade relacionadas ao titular dos dados, metadados sobre o produto do Adobe Experience Cloud ao qual o trabalho se aplica e o status de processamento do trabalho.

A variável `/jobs` O endpoint permite criar e recuperar processos de privacidade para sua organização. Para saber como usar este endpoint, consulte a [manual de endpoint de processos de privacidade](./privacy-jobs.md).

## Consentimento

Certos regulamentos exigem o consentimento explícito do cliente antes que seus dados pessoais possam ser coletados. A variável `/consent` O endpoint permite processar solicitações de consentimento do cliente e integrá-las ao seu fluxo de trabalho de privacidade. Consulte a [manual de endpoint de consentimento](./consent.md) para saber mais.

## Próximas etapas

Para começar a fazer chamadas usando a API do Privacy Service, leia o [guia de introdução](./getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar endpoints específicos.
