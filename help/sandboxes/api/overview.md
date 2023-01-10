---
keywords: Experience Platform, home, tópicos populares, guia do desenvolvedor do sandbox
solution: Experience Platform
title: Guia da API do Sandbox
description: As sandboxes no Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar seu ambiente de produção.
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# [!DNL Sandbox] Manual da API

O [!DNL Sandbox] A API fornece vários endpoints que permitem gerenciar programaticamente todas as sandboxes disponíveis na organização IMS. Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para ver todos os endpoints e operações CRUD disponíveis, visite a [[!DNL Sandbox] Referência da API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## sandboxes disponíveis

O endpoint de sandboxes disponível permite exibir uma lista de todas as sandboxes disponíveis para o usuário atual, incluindo informações sobre o nome, o título, o estado, o tipo e a região de cada sandbox. O endpoint de sandboxes disponível na variável [!DNL Sandbox] A API pode ser acessada por todos os usuários, incluindo aqueles sem permissões de acesso à Administração de sandbox. Consulte a [guia de endpoint de sandboxes disponíveis](./available.md) para saber como exibir sandboxes disponíveis na API.

## Gerenciamento de sandbox

Uma sandbox é uma partição virtual em uma única instância do Adobe Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Você pode criar, exibir, editar, redefinir e excluir sandboxes de produção e desenvolvimento usando o `/sandboxes` endpoint . Para saber como usar esse terminal, consulte a [guia de endpoint de sandboxes](./sandboxes.md).

## Tipos de sandbox

Atualmente, os tipos de sandbox compatíveis no Experience Platform são sandboxes de produção e desenvolvimento. Uma licença padrão da Platform concede um total de cinco sandboxes, que podem ser classificadas como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total. Consulte a [guia de endpoint tipos de sandbox](./types.md) para saber como exibir os tipos de sandbox suportados da sua organização na API.

## Próximas etapas

Para começar a fazer chamadas usando a variável [!DNL Sandbox] Leia a API do [guia de introdução](./getting-started.md) em seguida, selecione um dos guias de endpoint para saber como usar endpoints específicos.
