---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guia do desenvolvedor da API de Registro do schema
description: 'A API de Registro de Schemas permite gerenciar programaticamente todos os schemas e os recursos XDM relacionados disponíveis para você no Experience Platform. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Schema Registry] Guia do desenvolvedor da API

O [!DNL Schema Registry] é usado para acessar a Biblioteca de Schemas no Adobe Experience Platform, fornecendo uma interface do usuário e uma RESTful API a partir da qual todos os recursos disponíveis da biblioteca estão acessíveis.

A API de Registro do Schema fornece vários pontos de extremidade que permitem gerenciar programaticamente todos os schemas e os recursos relacionados do Modelo de Dados de Experiência (XDM) disponíveis para você na Plataforma. Isso inclui aqueles definidos por Adobe, [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa.

Esses pontos finais são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler amostras de chamadas de API e muito mais.

>[!IMPORTANT]
>
>O XDM usa a formatação do Schema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Antes de trabalhar com a API do Registro do Schema, recomenda-se que você leia a [documentação oficial do Schema JSON](https://json-schema.org/) para obter uma melhor compreensão dessa tecnologia subjacente.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, visite a [referência da API do Registro do Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Esquemas

Os schemas XDM representam e validam a estrutura e o formato dos dados ingeridos na Plataforma. Um schema é composto de uma classe e zero ou mais combinações. Você pode criar, visualização, editar e excluir schemas usando o terminal `/schemas`. Para saber como usar esse terminal, consulte o [guia de ponto de extremidade de schemas](./schemas.md).

Para obter um guia passo a passo sobre como criar um schema completo na API do Registro do Schema, incluindo a criação e adição de mixins e tipos de dados, consulte o tutorial de [criação do schema da API](../tutorials/create-schema-api.md).

## Comportamentos

Os comportamentos definem a natureza dos dados que um schema descreve. Cada classe XDM deve fazer referência a um comportamento específico, que todos os schemas que empregam essa classe herdarão. Consulte o guia de ponto de extremidade [comportamentos](./behaviors.md) para saber como visualização os comportamentos disponíveis na API.

## Classes

Uma classe define a estrutura básica das propriedades comuns que todos os schemas baseados nessa classe devem conter e determina quais combinações são elegíveis para uso nesses schemas. Cada classe deve estar associada a um comportamento existente. Consulte o guia de ponto de extremidade [classes](./classes.md) para obter detalhes sobre como trabalhar com classes na API.

## Misturas

As misturas são componentes reutilizáveis que definem um ou mais campos que representam um conceito específico, como uma pessoa individual, um endereço de correspondência ou um ambiente de navegador da Web. As misturas devem ser incluídas como parte de um schema que implementa uma classe compatível, dependendo do comportamento dos dados que representam (registro ou série cronológica). Consulte o [guia de ponto de extremidade do mixins](./mixins.md) para saber como trabalhar com mixins na API.

## Tipos de dados

Os tipos de dados são usados como campos do tipo de referência em classes ou combinações da mesma forma que os campos literais básicos, com a principal diferença de que os tipos de dados podem definir vários subcampos. Embora semelhantes às misturas, na medida em que permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do schema, enquanto as combinações só podem ser adicionadas no nível raiz. Consulte o [guia de ponto de extremidade de tipos de dados](./data-types.md) para obter mais informações sobre como trabalhar com tipos de dados na API.

## Descritores

Descritores são conjuntos de metadados que são atribuídos a campos específicos em um schema, fornecendo vários detalhes contextuais, incluindo como esses campos (e o próprio schema) são relacionados a outros schemas. Cada schema pode ter uma ou mais entidades de descritor aplicadas a ele, e existem vários tipos diferentes de descritor para servir a finalidades diferentes. Consulte o [guia de ponto de extremidade dos descritores](./descriptors.md) para obter mais informações sobre como trabalhar com descritores na API e uma visão geral dos diferentes tipos de descritores e seus casos de uso.

## Uniões

Embora a Plataforma permita que você componha schemas para casos de uso específicos, ela também permite que você componha uma &quot;união&quot; de schemas pertencentes a uma classe específica. Uma schema união agregação os campos de todos os schemas que compartilham a mesma classe em uma única representação. Ao habilitar um schema para uso com [Perfil do cliente em tempo real](../../profile/home.md), esse schema é incluído na união de sua classe específica. Dessa forma, os schemas de união não podem ser editados diretamente e só podem ser afetados pela inclusão ou exclusão de schemas para uso no Perfil.

Para saber como visualização uniões na API do Registro do Schema, consulte o [guia do ponto de extremidade do união](./unions.md).

## Exportar/Importar

A API do Registro de Schemas permite que você transfira e compartilhe recursos XDM entre caixas de proteção e organizações IMS. Para qualquer schema, combinação ou tipo de dados, é possível gerar uma carga de exportação que contenha a estrutura do recurso e quaisquer recursos dependentes. Essa carga pode ser usada para importar o recurso para uma caixa de proteção de destino e uma Organização IMS.

Consulte a [referência da API do Registro do Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) para obter mais informações sobre o uso deste terminal.

## Dados de amostra

Você pode gerar dados de amostra para qualquer schema especificado na Biblioteca de Schemas. O objeto de resposta retornado pode ser usado como uma fonte de ingestão de dados.

Consulte a [referência da API do Registro do Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) para obter mais informações sobre o uso deste terminal.

## Log de auditoria

O Registro de Schemas mantém um log de todas as alterações que ocorreram em um recurso (classe, mixagem, tipo de dados ou schema) entre diferentes atualizações. Você pode recuperar o log de um recurso específico fornecendo seu `$id` ou `meta:altId` no caminho de uma solicitação de GET para esse terminal.

Consulte a [referência da API do Registro do Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) para obter mais informações sobre o uso deste terminal.

## Próximas etapas

Para começar a fazer chamadas usando a API do Registro do Schema, leia o [guia de introdução](./getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar pontos de extremidade específicos.