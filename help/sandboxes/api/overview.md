---
keywords: Experience Platform;página inicial;tópicos populares;guia do desenvolvedor de sandbox
solution: Experience Platform
title: Guia da API de sandbox
description: As sandboxes na Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar o ambiente de produção.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# [!DNL Sandbox] Manual da API

A API [!DNL Sandbox] fornece vários endpoints que permitem gerenciar programaticamente todas as sandboxes disponíveis para você em sua organização. Esses endpoints são descritos abaixo. Visite os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para ver todos os pontos de extremidade e operações CRUD disponíveis, visite a [[!DNL Sandbox] Referência de API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandboxes disponíveis

O ponto de acesso das sandboxes disponíveis permite exibir uma lista de todas as sandboxes disponíveis para o usuário atual, incluindo informações sobre o nome, o título, o estado, o tipo e a região de cada sandbox. O ponto de extremidade de sandboxes disponível na API [!DNL Sandbox] pode ser acessado por todos os usuários, incluindo aqueles sem permissões de acesso de Administração de sandbox. Consulte o [manual de endpoint de sandboxes disponível](./available.md) para saber como visualizar sandboxes disponíveis na API.

## Gerenciamento de sandbox

Uma sandbox é uma partição virtual dentro de uma única instância do Adobe Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Você pode criar, exibir, editar, redefinir e excluir sandboxes de produção e desenvolvimento usando o ponto de extremidade `/sandboxes`. Para saber como usar este ponto de extremidade, consulte o [manual de ponto de extremidade de sandboxes](./sandboxes.md).

## Tipos de sandbox

Atualmente, os tipos de sandbox compatíveis no Experience Platform são sandboxes de produção e desenvolvimento. Uma licença padrão do Experience Platform concede um total de cinco sandboxes, que você pode classificar como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total. Consulte o [manual de endpoint de tipos de sandbox](./types.md) para saber como visualizar os tipos de sandbox compatíveis para sua organização na API.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Sandbox], leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
