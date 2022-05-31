---
keywords: Experience Platform, home, tópicos populares, api, controle de acesso baseado em atributos, Controle de acesso baseado em atributos
solution: Experience Platform
title: Guia da API de controle de acesso com base em atributos
description: A API de controle de acesso baseada em atributos permite gerenciar programaticamente funções e políticas no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 5%

---

# Guia da API de controle de acesso com base em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível em uma versão limitada para clientes de assistência médica com base nos EUA. Esse recurso estará disponível para todos os clientes da Real-time Customer Data Platform assim que for totalmente lançado.

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

A API de controle de acesso com base em atributos é usada para acessar funções, produtos, categorias de permissão e conjuntos de permissões no Adobe Experience Platform, fornecendo uma interface de usuário e uma RESTful API da qual todos os recursos de biblioteca disponíveis são acessíveis.

Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

## Funções

As funções definem o acesso que um administrador, especialista ou usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões e os membros da organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de acesso de exibição ou gravação necessário. Consulte a [guia do endpoint de funções](./roles.md) para obter mais informações sobre como trabalhar com funções na API.

## Políticas

Políticas são declarações que reúnem atributos para estabelecer ações admissíveis e não permissíveis. As políticas podem ser locais ou globais e podem substituir outras políticas. O `/policies` O endpoint permite gerenciar programaticamente as políticas em sua organização. Consulte a [guia do endpoint de políticas](./policies.md) para obter mais informações sobre como trabalhar com políticas na API.

## Produtos

O `/products` O endpoint na API de controle de acesso baseada em atributos permite gerenciar programaticamente produtos, bem como categorias de permissão e conjuntos de permissões associados a produtos em sua organização. Consulte a [guia do endpoint de produtos](./products.md) para obter mais informações sobre como trabalhar com produtos e suas correspondentes categorias de permissão e conjuntos de permissões na API.

## Próximas etapas

Para começar a fazer chamadas usando a API de controle de acesso baseada em atributo, leia a [guia de introdução](./getting-started.md) em seguida, selecione um dos guias de endpoint para saber como usar endpoints específicos.
