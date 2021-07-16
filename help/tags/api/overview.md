---
title: Guia da API do reator
description: A API de reator permite que os desenvolvedores gerenciem programaticamente todos os recursos para tags no Adobe Experience Platform. Siga este guia para saber como executar operações principais usando a API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 1%

---

# [!DNL Reactor] Guia da API

A API do reator fornece vários endpoints que permitem gerenciar programaticamente todos os recursos de tags no Adobe Experience Platform.

Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre como autenticar para a API.

Para visualizar todos os endpoints e operações CRUD disponíveis, visite a [Referência da API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml).

## Empresas

Uma empresa representa a organização de um usuário de tags, geralmente um negócio. Essas empresas correspondem a 1:1 com IMS Organization IDs. Os usuários da API só terão visibilidade sobre as empresas às quais têm acesso.

Consulte o [guia de endpoint de empresas](./endpoints/companies.md) para saber como visualizar as empresas disponíveis na API.

## Propriedades

Uma propriedade é um contêiner que contém a maioria dos outros recursos disponíveis na API do reator. Os únicos recursos que não são de propriedade de uma propriedade são eventos de auditoria, empresas, pacotes de extensão e perfis. Uma propriedade pertence a exatamente uma empresa, e uma empresa pode ter muitas propriedades.

Consulte o [guia de ponto de extremidade de propriedades](./endpoints/properties.md) para saber como gerenciar propriedades na API.

## Elementos de dados

Um elemento de dados funciona como uma variável que aponta para um dado importante em seu aplicativo. Os elementos de dados são usados nas configurações de regras e extensões. Quando a regra é acionada no tempo de execução em um navegador ou aplicativo, o valor do elemento de dados é resolvido e usado na regra.

Consulte o [guia do ponto de extremidade de elementos de dados](./endpoints/data-elements.md) para saber como gerenciar elementos de dados na API.

## Regras

As regras controlam o comportamento dos recursos contidos em uma biblioteca implantada. Uma regra é um grupo de um ou mais componentes da regra e existe para unir os componentes da regra de forma lógica.

Consulte o [guia de endpoint de regras](./endpoints/rules.md) para saber como gerenciar regras na API.

## Componentes da regra

Os componentes da regra são itens individuais que compõem uma regra. Os componentes da regra têm três tipos básicos:

* **Eventos**: O que aciona uma regra
* **Condições**: O que a regra verifica para determinar uma ação
* **Ações**: O que a regra é executada dependendo se a condição é atendida

Consulte o [guia de endpoint de regras](./endpoints/rules.md) para saber como gerenciar regras na API.

## Pacotes de extensão

Um pacote de extensão representa um agrupamento de recursos individuais que podem ser disponibilizados para um usuário de tags. Normalmente, esses recursos vêm na forma de componentes de regras e elementos de dados, mas também podem incluir módulos principais e módulos compartilhados. Os recursos fornecidos por um pacote de extensão são instalados como uma extensão quando estão incluídos em uma biblioteca.

Consulte o [guia de ponto de extremidade de pacotes de extensão](./endpoints/extension-packages.md) para saber como gerenciar pacotes de extensão na API.

## Extensões

Uma extensão representa a instância instalada de um pacote de extensão. Uma extensão disponibiliza os recursos definidos por um pacote de extensão para uma propriedade. Esses recursos são aproveitados ao criar elementos de dados e componentes de regras.

Consulte o [guia do ponto de extremidade de extensões](./endpoints/extensions.md) para saber como gerenciar extensões na API.

## Bibliotecas

Uma biblioteca é uma coleção de recursos (extensões, regras e elementos de dados) que representam o comportamento desejado de uma propriedade. As bibliotecas são compiladas em builds, e essas builds são atribuídas a ambientes diferentes conforme movem o fluxo de publicação de testes para produção.

Consulte o [guia de ponto de extremidade de bibliotecas](./endpoints/libraries.md) para saber como gerenciar bibliotecas na API.

## Builds

Uma biblioteca de tags é compilada em uma build para que seja atribuída a um ambiente para teste e implantação. O conteúdo de uma build varia dependendo dos recursos incluídos na biblioteca, da configuração do ambiente ao qual a build está atribuída e da plataforma da propriedade à qual a build pertence.

Consulte o [guia de endpoint de builds](./endpoints/builds.md) para saber como gerenciar builds na API.

## Ambientes

Um ambiente indica o host específico em que uma build pode ser implantada e se a build deve ser implantada como um conjunto de arquivos ou compactada em um formato de arquivo. Na API do Reator, os ambientes são separados dos próprios hosts, que são gerenciados pelo endpoint `/hosts`.

Consulte o [guia de endpoint de builds](./endpoints/builds.md) para saber como gerenciar builds na API.

## Hosts

Um host representa um destino hospedado, onde uma build de biblioteca pode ser entregue e implantada. Os hosts podem ser servidores Akamai ou SFTP.

Consulte o [guia de ponto de extremidade de hosts](./endpoints/hosts.md) para saber como gerenciar hosts na API.

## Configurações do aplicativo

As configurações do aplicativo permitem que as credenciais sejam armazenadas e recuperadas para uso posterior. Consulte o [guia do ponto de extremidade de configurações do aplicativo](./endpoints/app-configurations.md) para saber como gerenciar configurações do aplicativo na API.

## Eventos de auditoria

Um evento de auditoria é um registro de uma alteração específica em outro recurso de tag, gerado no momento em que a alteração é feita. Esses são eventos do sistema que podem ser inscritos por meio do uso de uma função de retorno de chamada.

Consulte o [guia de ponto de extremidade de eventos de auditoria](./endpoints/audit-events.md) para saber como gerenciar eventos de auditoria na API.

## Retornos de chamada

Um retorno de chamada é uma mensagem que a Platform envia para um host de URL sempre que um novo evento de auditoria é gerado. Consulte o [guia do ponto de extremidade de retornos de chamada](./endpoints/callbacks.md) para saber como gerenciar retornos de chamada na API.

## Notas

Notas são anotações textuais que podem ser adicionadas a determinados recursos de tags, como elementos de dados, extensões, bibliotecas, propriedades, regras e componentes de regras. Consulte o [guia de ponto de extremidade de notas](./endpoints/notes.md) para saber como gerenciar notas na API.

## Perfil

Um perfil contém todas as informações sobre o usuário conectado, incluindo todas as Orgs do Adobe às quais pertencem, os perfis de produto aos quais pertencem em cada Org e os direitos que eles têm de cada perfil de produto.

Consulte o [guia do endpoint do perfil](./endpoints/profile.md) para saber como visualizar essas informações na API.

## Pesquisa

O endpoint `/search` fornece uma maneira de encontrar recursos que correspondam a um critério desejado, expresso como uma query. Todas as consultas têm escopo para sua empresa atual e propriedades acessíveis. Consulte o [guia do endpoint de pesquisa](./endpoints/search.md) para saber como usar essa funcionalidade.

## Próximas etapas

Para começar a fazer chamadas usando a API do Registro de Schema, leia o [guia de introdução](./getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar endpoints específicos.
