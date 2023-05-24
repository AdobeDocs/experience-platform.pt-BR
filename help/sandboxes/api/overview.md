---
keywords: Experience Platform;página inicial;tópicos populares;guia do desenvolvedor de sandbox
solution: Experience Platform
title: Guia da API de sandbox
description: As sandboxes na Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar o ambiente de produção.
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# [!DNL Sandbox] Manual da API

A variável [!DNL Sandbox] A API fornece vários endpoints que permitem gerenciar programaticamente todas as sandboxes disponíveis para você na organização. Esses endpoints são descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para ver todos os endpoints e operações CRUD disponíveis, visite o [[!DNL Sandbox] Referência da API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandboxes disponíveis

O ponto de acesso das sandboxes disponíveis permite exibir uma lista de todas as sandboxes disponíveis para o usuário atual, incluindo informações sobre o nome, o título, o estado, o tipo e a região de cada sandbox. O endpoint de sandboxes disponível no [!DNL Sandbox] A API pode ser acessada por todos os usuários, incluindo aqueles sem permissões de acesso de Administração de sandbox. Consulte a [guia de endpoint de sandboxes disponível](./available.md) para saber como visualizar sandboxes disponíveis na API.

## Gerenciamento de sandbox

Uma sandbox é uma partição virtual dentro de uma única instância do Adobe Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Você pode criar, exibir, editar, redefinir e excluir sandboxes de produção e desenvolvimento usando o `/sandboxes` terminal. Para saber como usar este endpoint, consulte a [guia de endpoint de sandboxes](./sandboxes.md).

## Tipos de sandbox

Atualmente, os tipos de sandbox compatíveis no Experience Platform são sandboxes de produção e desenvolvimento. Uma licença padrão da Platform concede um total de cinco sandboxes, que você pode classificar como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total. Consulte a [guia de endpoint de tipos de sandbox](./types.md) para saber como visualizar os tipos de sandbox compatíveis com sua organização na API.

## Próximas etapas

Para começar a fazer chamadas usando o [!DNL Sandbox] API, leia as [guia de introdução](./getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar endpoints específicos.
