---
title: Visão geral do desenvolvimento de extensões
description: Saiba mais sobre os componentes principais de diferentes tipos de extensão de tag e o processo de desenvolvimento de extensão no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 69%

---

# Visão geral do desenvolvimento de extensões

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um dos objetivos principais da Adobe Experience Platform é criar um ecossistema aberto, onde engenheiros fora da equipe de engenharia principal possam expor funcionalidades adicionais por meio de tags. Isso é feito por meio de extensões do Reactor. Depois que uma extensão é instalada em uma propriedade de tag por um usuário, a funcionalidade dessa extensão fica disponível para uso por todos os usuários da propriedade.

Este documento descreve os componentes principais de diferentes tipos de extensão e fornece links para mais documentação para orientá-lo sobre o processo de desenvolvimento de extensão.

## Módulos da biblioteca

Os módulos de biblioteca são pedaços de código reutilizável fornecidos por uma extensão que são emitidos dentro da biblioteca de tempo de execução de tags. Dependendo de você estar desenvolvendo uma extensão da Web ou uma extensão de borda, os tipos de módulo disponíveis e seus casos de uso serão diferentes. Consulte as seguintes subseções para obter uma visão geral dos módulos para cada tipo de extensão:

* [Módulos para extensões da Web](#web-modules)
* [Módulos para extensões de borda](#edge-modules)

### Módulos para extensões da Web {#web-modules}

Em extensões da Web, as regras são acionadas por meio de eventos, que poderão executar ações específicas se um determinado conjunto de condições for atendido. Consulte a visão geral do [fluxo do módulo em extensões da Web](./web/flow.md) para obter mais informações.

Além dos [módulos principais](./web/core.md) fornecidos pela Adobe, você pode definir seus próprios módulos de biblioteca nas extensões da Web:

* [Tipos de evento](#web-event)
* [Tipos de condição](#web-condition)
* [Tipos de ação](#web-action)
* [Tipos de elementos de dados](#web-data-element)
* [Módulos compartilhados](#shared)

>[!NOTE]
>
>Para obter mais detalhes sobre o formato necessário para implementar módulos de biblioteca na sua extensão, consulte a [visão geral de formato do módulo](./web/format.md).

#### Tipos de evento {#web-event}

Um evento de regra é uma atividade que deve ocorrer antes de uma regra ser acionada.

Como exemplo, uma extensão pode fornecer um tipo de evento de &quot;gesto&quot; que observa a ocorrência de determinado gesto de toque ou mouse. Quando o gesto ocorre, a lógica do evento aciona a regra.

Os tipos de evento normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleção de dados que permite que os usuários modifiquem as configurações do evento e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução de tags para interpretar as configurações e observar uma determinada atividade ocorrer.

[Saiba mais](./web/event-types.md)

#### Tipos de condição {#web-condition}

Uma condição de regra é avaliada após a ocorrência de um evento de regra. Todas as condições devem retornar verdadeiro para que a regra continue a ser processada. A exceção é quando os usuários colocam as condições explicitamente em um bucket de &quot;exceção&quot;. Nesse caso, todas as condições no bucket devem retornar falso para que a regra continue o processamento.

Como exemplo, uma extensão pode fornecer um tipo de condição &quot;visor contém&quot;, na qual o usuário do poderia especificar um seletor de CSS. Quando a condição é avaliada no site do cliente, a extensão pode encontrar elementos que correspondam ao seletor de CSS e retornar se algum deles está contido no visor do usuário.

Os tipos de condição normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleta de dados que permite que os usuários modifiquem as configurações da condição e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução da tag para interpretar as configurações e avaliar uma condição.

[Saiba mais](./web/condition-types.md)

#### Tipos de ação {#web-action}

Uma ação de regra é algo que é executado depois que o evento de regra ocorre e as condições passam na avaliação.

Por exemplo, uma extensão pode fornecer um tipo de ação &quot;mostrar o bate-papo de suporte&quot;, que pode exibir uma caixa de diálogo de bate-papo de suporte para ajudar usuários que estejam com dificuldades ao fazer check-out.

Os tipos de ação normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleção de dados que permite que os usuários modifiquem as configurações da ação e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução da tag para interpretar as configurações e executar uma ação.

[Saiba mais](./web/action-types.md)

#### Tipos de elementos de dados {#web-data-element}

Os elementos de dados são, essencialmente, aliases de dados em uma página, independentemente de esses dados serem encontrados em parâmetros de sequência de consulta, cookies, elementos DOM ou algum outro lugar. Um elemento de dados pode ser referenciado por regras e atua como uma abstração para acessar esses dados. Quando a localização dos dados for alterada no futuro (por exemplo, de `innerHTML` de um elemento DOM para o valor de uma variável JavaScript), um único elemento de dados poderá ser reconfigurado, enquanto todas as regras que referenciam esse elemento de dados poderão permanecer inalteradas.

Um tipo de elemento de dados permite que os usuários configurem elementos de dados para acessar dados de maneira específica. Por exemplo, uma extensão pode fornecer um tipo de elemento de dados &quot;item de armazenamento local&quot; no qual o usuário do pode especificar um nome de item de armazenamento local. Quando o elemento de dados é referenciado por uma regra, a extensão pode procurar o valor do item do armazenamento local usando o nome do item do armazenamento local fornecido pelo usuário ao configurar o elemento de dados.

Os tipos de elementos de dados normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleta de dados que permite que os usuários modifiquem as configurações do elemento de dados e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução da tag para interpretar as configurações e recuperar partes de dados.

[Saiba mais](./web/data-element-types.md)

#### Módulos compartilhados {#shared}

Um módulo compartilhado é um módulo exposto por uma extensão para ser acessado por outra. Esse pode ser um mecanismo muito útil para a comunicação entre extensões. Por exemplo, a Extensão A pode carregar dados de forma assíncrona e disponibilizá-los para a Extensão B por meio de uma [promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Os módulos compartilhados são incluídos na biblioteca mesmo quando nunca são chamados de dentro de outras extensões. Para não aumentar desnecessariamente o tamanho da biblioteca, tenha cuidado com o que você expõe como um módulo compartilhado.

Os módulos compartilhados não têm um componente de visualização.

[Saiba mais](./web/shared.md)

### Módulos para extensões de borda {#edge-modules}

Em extensões de borda, as regras são acionadas por meio de verificações de condição, que, em seguida, executarão ações específicas se essas verificações forem bem-sucedidas. Consulte a visão geral do [fluxo do módulo em extensões de borda](./edge/flow.md) para obter mais informações.

Você pode definir seus próprios módulos de biblioteca nas extensões de borda. Eles podem ser classificados como os seguintes tipos:

* [Tipos de condição](#condition)
* [Tipos de ação](#action)
* [Tipos de elementos de dados](#data-element)

>[!NOTE]
>
>Para obter mais detalhes sobre o formato necessário para implementar módulos de biblioteca na sua extensão, consulte a [visão geral de formato do módulo](./edge/format.md).

#### Tipos de condição {#condition}

Uma condição de regra é avaliada após a ocorrência de um evento de regra. Todas as condições devem retornar verdadeiro para que a regra continue a ser processada. A exceção é quando os usuários colocam as condições explicitamente em um bucket de &quot;exceção&quot;. Nesse caso, todas as condições no bucket devem retornar falso para que a regra continue o processamento.

Como exemplo, uma extensão pode fornecer um tipo de condição &quot;visor contém&quot;, na qual o usuário do poderia especificar um seletor de CSS. Quando a condição é avaliada no site do cliente, a extensão pode encontrar elementos que correspondam ao seletor de CSS e retornar se algum deles está contido no visor do usuário.

Os tipos de condição normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleta de dados que permite que os usuários modifiquem as configurações da condição e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução da tag para interpretar as configurações e avaliar uma condição.

[Saiba mais](./web/condition-types.md)

#### Tipos de ação {#action}

Uma ação de regra é algo que é executado depois que o evento de regra ocorre e as condições são aprovadas na avaliação.

Por exemplo, uma extensão pode fornecer um tipo de ação &quot;mostrar o bate-papo de suporte&quot;, que pode exibir uma caixa de diálogo de bate-papo de suporte para ajudar usuários que estejam com dificuldades ao fazer check-out.

Os tipos de ação normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleção de dados que permite que os usuários modifiquem as configurações da ação e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução da tag para interpretar as configurações e executar uma ação.

[Saiba mais](./web/action-types.md)

#### Tipos de elementos de dados {#data-element}

Essencialmente, os elementos de dados são aliases de dados em uma página, independentemente de onde esses dados se encontrem no evento recebido pelo servidor. Um elemento de dados pode ser referenciado por regras e atua como uma abstração para acessar esses dados. Quando a localização dos dados for alterada no futuro (por exemplo, a chave de evento que contém o valor for alterada), um único elemento de dados poderá ser reconfigurado, enquanto todas as regras que referenciam esse elemento de dados poderão permanecer inalteradas.

Os tipos de elementos de dados normalmente consistem em (1) uma exibição mostrada na interface do usuário da coleta de dados que permite que os usuários modifiquem as configurações do elemento de dados e (2) um módulo de biblioteca emitido na biblioteca de tempo de execução da tag para interpretar as configurações e recuperar partes de dados.

[Saiba mais](./web/data-element-types.md)

## Configuração de extensão

A configuração de uma extensão se refere à maneira pela qual ela coleta as configurações globais de um usuário. Por exemplo, considere uma extensão que permita ao usuário enviar um beacon usando uma ação Enviar beacon, e o beacon sempre deve conter uma ID de conta. Não queremos causar problemas aos usuários solicitando-lhes a ID da conta sempre que configurarem uma ação Enviar beacon. Em vez disso, a extensão deve solicitar a ID da conta uma vez na visualização de configuração da extensão. Sempre que um beacon é enviado, o módulo da biblioteca de ação Enviar beacon pode obter a ID da conta por meio da configuração de extensão e adicioná-la ao beacon.

Quando os usuários instalam uma extensão em uma propriedade de tag, eles são mostrados na visualização de configuração de extensão. Eles não podem concluir a instalação da extensão sem concluir a configuração da extensão.

A configuração da extensão consiste em um componente de exibição que exportará configurações que são emitidas na biblioteca de tempo de execução de tags como um objeto simples.

[Saiba mais](./configuration.md)

## Estrutura da extensão

Uma extensão consiste em um diretório de arquivos. A seguir é fornecida uma visão geral de como esses arquivos devem ser estruturados. Detalhes sobre o conteúdo do arquivo podem ser encontrados em outras seções.

Um arquivo [`extension.json`](./manifest.md) deve existir na raiz do diretório. Entre outros, esse arquivo descreverá a composição da extensão e onde determinados arquivos estão localizados no diretório. Isso tem algumas semelhanças com um arquivo [`package.json`](https://docs.npmjs.com/files/package.json) em [npm](https://www.npmjs.com/).

Cada módulo de biblioteca (a lógica a ser emitida na biblioteca de tempo de execução da tag) deve ser seu próprio arquivo, cujo conteúdo segue o [módulo CommonJS padrão](http://wiki.commonjs.org/wiki/Modules/1.1.1). Por exemplo, se estamos criando um tipo de ação &quot;enviar beacon&quot;, precisamos ter um arquivo que contenha a lógica de envio do beacon. O conteúdo desse arquivo será emitido na biblioteca de tempo de execução da tag. Você pode chamá-lo de `sendBeacon.js`. O local do arquivo no diretório não é importante, pois `extension.json` descreverá sua localização.

Cada exibição deve ser um arquivo HTML capaz de ser carregado em um iframe dentro do aplicativo de tags. A exibição deve incluir um script fornecido pelas tags e estar em conformidade com uma pequena API para se comunicar com o aplicativo. Não há restrições quanto às bibliotecas usadas nas visualizações. Em outras palavras, você pode usar jQuery, Underscore, React, Angular, Bootstrap ou outras bibliotecas. No entanto, esperamos que sua extensão tenha uma aparência semelhante à do aplicativo.

É recomendado colocar todos os arquivos relacionados à visualização (HTML, CSS, JavaScript) em um único subdiretório que esteja isolado dos arquivos do módulo da biblioteca. Em `extension.json`, você descreverá onde está localizado esse subdiretório de visualização. A Platform enviará esse subdiretório (e somente esse subdiretório) de seus servidores da Web.
