---
keywords: Experience Platform, home, tópicos populares, guia do desenvolvedor do sandbox
solution: Experience Platform
title: Guia da API do Sandbox
topic-legacy: developer guide
description: As sandboxes no Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar seu ambiente de produção.
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Sandbox] Guia da API

A API [!DNL Sandbox] fornece vários endpoints que permitem gerenciar programaticamente todas as sandboxes disponíveis na organização de IMS. Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para ver todos os endpoints e operações CRUD disponíveis, visite a [[!DNL Sandbox] referência da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml).

## sandboxes disponíveis

O endpoint de sandboxes disponível permite exibir uma lista de todas as sandboxes disponíveis para o usuário atual, incluindo informações sobre o nome, o título, o estado, o tipo e a região de cada sandbox. O endpoint de sandboxes disponível na API [!DNL Sandbox] pode ser acessado por todos os usuários, incluindo aqueles sem permissões de acesso à Administração de sandbox. Consulte o [guia de ponto de extremidade de sandboxes disponível](./available.md) para saber como exibir as sandboxes disponíveis na API.

## Gerenciamento de sandbox

Uma sandbox é uma partição virtual em uma única instância do Adobe Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Você pode criar, exibir, editar, redefinir e excluir sandboxes de produção e desenvolvimento usando o endpoint `/sandboxes`. Para saber como usar esse endpoint, consulte o [guia do endpoint de sandboxes](./sandboxes.md).

## Tipos de sandbox

Atualmente, os tipos de sandbox compatíveis no Experience Platform são sandboxes de produção e desenvolvimento. Uma licença padrão da Platform concede um total de cinco sandboxes, que podem ser classificadas como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total. Consulte o [guia de ponto de extremidade dos tipos de sandbox](./types.md) para saber como exibir os tipos de sandbox suportados da sua organização na API.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Sandbox], leia o [guia de introdução](./getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar endpoints específicos.