---
keywords: Experience Platform;página inicial;tópicos populares;api;controle de acesso baseado em atributos;Controle de acesso baseado em atributos
solution: Experience Platform
title: Guia da API de controle de acesso baseado em atributo
description: A API de controle de acesso baseado em atributos permite gerenciar programaticamente funções e políticas de acesso no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 15%

---

# Guia da API de controle de acesso baseado em atributos

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

A API de controle de acesso baseada em atributos é usada para acessar funções, produtos, categorias de permissão e conjuntos de permissões no Adobe Experience Platform, fornecendo uma interface de usuário e a API RESTful a partir da qual todos os recursos de biblioteca disponíveis estão acessíveis.

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos não deve ser confundido com os recursos de governança de dados do Experience Platform, que permitem usar rótulos e políticas para controlar como os dados são usados na Platform, em vez de quais usuários em sua organização têm acesso a eles. Consulte a [Guia da API do Serviço de política](../../../data-governance/api/overview.md) para obter etapas sobre como aproveitar programaticamente esses recursos.

Esses endpoints são descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

## Funções

As funções definem o acesso que um administrador, um especialista ou um usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões, e os membros da organização podem ter uma ou mais funções atribuídas, dependendo do escopo do acesso de visualização ou gravação necessário. Consulte a [guia de endpoint de funções](./roles.md) para obter mais informações sobre como trabalhar com funções na API.

## Políticas

Políticas são declarações que reúnem atributos para estabelecer ações permitidas e não permitidas. As políticas podem ser locais ou globais e podem substituir outras políticas. A variável `/policies` O endpoint permite gerenciar políticas de forma programática em sua organização. Consulte a [manual de endpoint de políticas](./policies.md) para obter mais informações sobre como trabalhar com políticas na API.

## Produtos

A variável `/products` O endpoint na API de controle de acesso baseada em atributos permite gerenciar de forma programática os produtos, bem como as categorias de permissões e os conjuntos de permissões associados aos produtos em sua organização. Consulte a [manual de endpoint de produtos](./products.md) para obter mais informações sobre como trabalhar com produtos e suas categorias de permissão e conjuntos de permissões correspondentes na API.

## Próximas etapas

Para começar a fazer chamadas usando a API de controle de acesso baseada em atributos, leia a [guia de introdução](./getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar endpoints específicos.
