---
title: Guia da API do Privacy Service
description: Saiba como usar a API do Privacy Service para gerenciar programaticamente tarefas de privacidade para aplicativos Adobe Experience Cloud compatíveis.
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# [!DNL Privacy Service] Manual da API

A API do Privacy Service fornece vários endpoints que permitem gerenciar programaticamente tarefas de privacidade para sua organização. Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

>[!NOTE]
>
>Este guia aborda como usar o [!DNL Privacy Service] API. Para obter detalhes sobre como usar a interface do usuário, consulte o [Visão geral da interface do usuário do Privacy Service](../ui/overview.md).

Para exibir todos os endpoints e operações CRUD disponíveis, visite a [Referência da API do Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Trabalhos de privacidade

Quando o Privacy Service recebe uma solicitação para acessar ou excluir os dados pessoais de um assunto, o sistema cria trabalhos de privacidade para atender a essa solicitação. Cada tarefa de privacidade contém informações de identidade relacionadas ao titular dos dados, metadados sobre o produto Adobe Experience Cloud ao qual a tarefa se aplica e o status de processamento da tarefa.

O `/jobs` O endpoint permite criar e recuperar tarefas de privacidade da organização. Para saber como usar esse terminal, consulte a [guia do endpoint de tarefas de privacidade](./privacy-jobs.md).

## Consentimento

Determinadas regulamentações exigem consentimento explícito do cliente para que seus dados pessoais possam ser coletados. O `/consent` O endpoint permite processar solicitações de consentimento do cliente e integrá-las ao workflow de privacidade. Consulte a [guia do endpoint de consentimento](./consent.md) para saber mais.

## Próximas etapas

Para começar a fazer chamadas usando a API do Privacy Service, leia o [guia de introdução](./getting-started.md) em seguida, selecione um dos guias de endpoint para saber como usar endpoints específicos.
