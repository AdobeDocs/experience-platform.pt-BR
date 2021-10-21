---
title: Manual da API do Reactor
description: A API do Reactor permite que os desenvolvedores gerenciem de forma programática todos os recursos de tags na Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 95%

---

# [!DNL Reactor] Manual da API

A API do Reactor fornece vários endpoints que permitem gerenciar de forma programática todos os recursos de tags na Adobe Experience Platform.

Esses endpoints são descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre como realizar a autenticação para a API.

Para exibir todos os endpoints e operações CRUD disponíveis, acesse a página de [Referência da API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Empresas

Uma empresa representa a organização de um usuário de tags, geralmente um negócio. Essas empresas correspondem inteiramente às IDs de organização IMS. Os usuários da API só terão visibilidade das empresas às quais tiverem acesso.

Consulte o [manual de endpoint de empresas](./endpoints/companies.md) para saber como visualizar as empresas disponíveis na API.

## Propriedades

Uma propriedade é um container que armazena a maioria dos outros recursos disponíveis na API do Reactor. Os únicos recursos que não pertencem a uma propriedade são eventos de auditoria, empresas, pacotes de extensão e perfis. Uma propriedade pertence a apenas uma empresa, mas uma empresa pode ter muitas propriedades.

Consulte o [manual de endpoint de propriedades](./endpoints/properties.md) para saber como gerenciar propriedades na API.

## Elementos de dados

Um elemento de dados funciona como uma variável que aponta para dados importantes em seu aplicativo. Os elementos de dados são usados em configurações de extensões e regras. Quando a regra é acionada no tempo de execução em um navegador ou aplicativo, o valor do elemento de dados é definido e usado na regra.

Consulte o [manual de endpoint de elementos de dados](./endpoints/data-elements.md) para saber como gerenciar elementos de dados na API.

## Regras

As regras controlam o comportamento dos recursos contidos em uma biblioteca implantada. Uma regra é um grupo de um ou mais componentes de regra e existe para unir os componentes de regra de forma lógica.

Consulte o [manual de endpoint de regras](./endpoints/rules.md) para saber como gerenciar regras na API.

## Componentes da regra

Os componentes de regra são itens individuais que compõem uma regra. Há três tipos básicos de componentes de regra:

* **Eventos**: o que aciona uma regra
* **Condições**: o que a regra verifica para determinar uma ação
* **Ações**: o que a regra executa dependendo de a condição ser atendida ou não

Consulte o [manual de endpoint de regras](./endpoints/rules.md) para saber como gerenciar regras na API.

## Pacotes de extensão

Um pacote de extensão representa um agrupamento de recursos individuais que podem ser disponibilizados para um usuário de tags. Normalmente, esses recursos vêm na forma de componentes de regras e elementos de dados, mas também podem incluir módulos principais e compartilhados. Os recursos fornecidos por um pacote de extensão são instalados como uma extensão quando ele é incluído em uma biblioteca.

Consulte o [manual de endpoint dos pacotes de extensão](./endpoints/extension-packages.md) para saber como gerenciar pacotes de extensão na API.

## Extensões

Uma extensão representa a instância instalada de um pacote de extensão. Uma extensão disponibiliza os recursos definidos por um pacote de extensão para uma propriedade. Esses recursos são aproveitados ao serem criados elementos de dados e componentes de regras.

Consulte o [manual de endpoint de extensões](./endpoints/extensions.md) para saber como gerenciar extensões na API.

## Bibliotecas

Uma biblioteca é uma coleção de recursos (extensões, regras e elementos de dados) que representam o comportamento desejado de uma propriedade. As bibliotecas são compiladas em builds, que são atribuídos a diferentes ambientes conforme percorrem o fluxo de publicação, dos testes à produção.

Consulte o [manual de endpoint de bibliotecas](./endpoints/libraries.md) para saber como gerenciar bibliotecas na API.

## Builds

Uma biblioteca de tags é compilada em um build para ser atribuída a um ambiente de teste e implantação. O conteúdo de um build varia dependendo dos recursos incluídos na biblioteca, da configuração do ambiente ao qual o build é atribuído e da plataforma da propriedade à qual o build pertence.

Consulte o [manual de endpoint de builds](./endpoints/builds.md) para saber como gerenciar builds na API.

## Ambientes

Um ambiente indica o host específico em que um build pode ser implantado e se deve ser implantado como um conjunto de arquivos ou compactado em um formato de arquivo. Na API do Reactor, os ambientes são separados dos próprios hosts, que são gerenciados pelo endpoint `/hosts`.

Consulte o [manual de endpoint de builds](./endpoints/builds.md) para saber como gerenciar builds na API.

## Hosts

Um host representa um destino de hospedagem, em que um build de biblioteca pode ser entregue e implantado. Os hosts podem ser servidores Akamai ou SFTP.

Consulte o [manual de endpoint de hosts](./endpoints/hosts.md) para saber como gerenciar hosts na API.

## Configurações do aplicativo

As configurações de aplicativo permitem que as credenciais sejam armazenadas e recuperadas para uso posterior. Consulte o [manual de endpoint de configurações de aplicativo](./endpoints/app-configurations.md) para saber como gerenciar configurações de aplicativo na API.

## Eventos de auditoria

Um evento de auditoria é um registro de uma alteração específica em outro recurso de tag, gerado no momento em que a alteração é feita. Trata-se de eventos do sistema que é possível assinar por meio do uso de uma função de retorno de chamada.

Consulte o [manual de endpoint de eventos de auditoria](./endpoints/audit-events.md) para saber como gerenciar eventos de auditoria na API.

## Retornos de chamada

Um retorno de chamada é uma mensagem que a Platform envia a um host de URL sempre que um novo evento de auditoria é gerado. Consulte o [manual de endpoint de retornos de chamada](./endpoints/callbacks.md) para saber como gerenciar retornos de chamada na API.

## Notas

As notas são anotações textuais que podem ser adicionadas a determinados recursos de tags, como elementos de dados, extensões, bibliotecas, propriedades, regras e componentes de regras. Consulte o [manual de endpoint de notas](./endpoints/notes.md) para saber como gerenciar notas na API.

## Perfil

Um perfil contém todas as informações sobre o usuário conectado, incluindo todas as organizações da Adobe e perfis de produto aos quais ele pertence em cada organização, além dos direitos que ele tem em cada perfil de produto.

Consulte o [manual de endpoint de perfil](./endpoints/profile.md) para saber como exibir essas informações na API.

## Pesquisa

O endpoint `/search` fornece uma maneira de encontrar recursos que correspondem a um critério desejado, expresso como uma consulta. Todas as consultas têm como escopo sua empresa atual e as propriedades acessíveis. Consulte o [manual de endpoint de pesquisa](./endpoints/search.md) para saber como usar essa funcionalidade.

## Segredos

Um segredo contém credenciais que permitem o encaminhamento de eventos para autenticação em outro sistema para troca de dados segura. Consulte a [guia de segredos](./guides/secrets.md) para obter uma visão geral sobre como os segredos funcionam no encaminhamento de eventos, e a variável [guia do endpoint de segredos](./endpoints/secrets.md) para saber como gerenciá-los na API do Reator.

## Próximas etapas

Para começar a fazer chamadas usando a API do registro de esquema, leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
