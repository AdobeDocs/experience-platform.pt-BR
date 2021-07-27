---
title: Visão geral do desenvolvimento de extensões
description: Saiba mais sobre os componentes principais de diferentes tipos de extensão de tag e o processo de desenvolvimento de extensão no Adobe Experience Platform.
source-git-commit: a165f0c254885b17db734ab09bf6523175a11dfb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 21%

---

# Visão geral do desenvolvimento de extensões

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um dos principais objetivos das tags no Adobe Experience Platform é criar um ecossistema aberto, onde engenheiros fora do Adobe possam expor funcionalidades adicionais em seus sites e aplicativos móveis. Isso é feito por meio das extensões de tag. Depois que uma extensão é instalada em uma propriedade de tag, a funcionalidade dessa extensão fica disponível para uso por todos os usuários da propriedade.

Este documento descreve os componentes principais de uma extensão e fornece links para outra documentação que ajuda a orientá-lo sobre o processo de desenvolvimento da extensão.

## Estrutura da extensão

Uma extensão consiste em um diretório de arquivos. Especificamente, uma extensão consiste em um arquivo manifest, módulos de biblioteca e visualizações.

### Arquivo manifest

Um arquivo manifest ([`extension.json`](./manifest.md)) deve existir na raiz do diretório. Este arquivo descreve a composição da extensão e onde determinados arquivos estão localizados no diretório . O manifesto funciona de forma semelhante a um arquivo [`package.json`](https://docs.npmjs.com/files/package.json) em um projeto [npm](https://www.npmjs.com/).

### Módulos da biblioteca

Os módulos de biblioteca são os arquivos que descrevem os [componentes](#components) diferentes que uma extensão fornece (em outras palavras, a lógica a ser emitida na biblioteca de tempo de execução da tag). O conteúdo de cada arquivo de módulo de biblioteca deve seguir o [módulo CommonJS padrão](http://wiki.commonjs.org/wiki/Modules/1.1.1).

Por exemplo, se você estiver criando um tipo de ação chamado &quot;enviar beacon&quot;, deverá ter um arquivo que contenha a lógica que envia o beacon. Se estiver usando JavaScript, o arquivo pode ser chamado `sendBeacon.js`. O conteúdo desse arquivo será emitido na biblioteca de tempo de execução da tag.

Você pode colocar os arquivos do módulo de biblioteca em qualquer lugar que desejar no diretório de extensão, desde que descreva sua localização em `extension.json`.

### Exibições

Uma exibição é um arquivo HTML que pode ser carregado em um elemento [`iframe`](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/iframe) no aplicativo de tags, especificamente por meio da interface do usuário da coleta de dados. A exibição deve incluir um script fornecido pela extensão e estar em conformidade com uma pequena API para se comunicar com o aplicativo.

O arquivo de visualização mais importante para qualquer extensão é sua configuração. Consulte a seção sobre [configurações de extensão](#configuration) para obter mais informações.

Não há restrições quanto às bibliotecas usadas nas visualizações. Em outras palavras, você pode usar jQuery, Sublinhado, Reagir, Angular, Bootstrap ou outras. No entanto, ainda é recomendável fazer com que sua extensão tenha uma aparência semelhante à interface do usuário da coleta de dados.

É recomendado colocar todos os arquivos relacionados à visualização (HTML, CSS, JavaScript) em um único subdiretório que esteja isolado dos arquivos do módulo da biblioteca. Em `extension.json`, você pode descrever onde esse subdiretório de exibição está localizado. A Platform enviará esse subdiretório (e somente esse subdiretório) de seus servidores da Web.

## Componentes da biblioteca {#components}

Cada extensão define um conjunto de funcionalidades. Essas funcionalidades são implementadas ao serem incluídas em uma [biblioteca](../ui/publishing/libraries.md) que é implantada no seu site ou aplicativo. As bibliotecas são uma coleção de componentes individuais, incluindo condições, ações, elementos de dados e muito mais. Cada componente da biblioteca é uma parte do código reutilizável (fornecido por uma extensão) que é emitida dentro do tempo de execução da tag.

Dependendo de você estar desenvolvendo uma extensão da Web ou uma extensão de borda, os tipos disponíveis de componentes e seus casos de uso são diferentes. Consulte as subseções abaixo para obter uma visão geral de quais componentes estão disponíveis para cada tipo de extensão.

### Componentes para extensões da Web {#web}

Em extensões da Web, as regras são acionadas por meio de eventos, que poderão executar ações específicas se um determinado conjunto de condições for atendido. Consulte a visão geral do [fluxo do módulo em extensões da Web](./web/flow.md) para obter mais informações.

Além dos [módulos principais](./web/core.md) fornecidos pelo Adobe, você pode definir os seguintes componentes de biblioteca nas extensões da Web:

* [Eventos](./web/event-types.md)
* [Condições](./web/condition-types.md)
* [Ações](./web/action-types.md)
* [Elementos de dados](./web/data-element-types.md)
* [Módulos compartilhados](./web/shared.md)

>[!NOTE]
>
>Para obter detalhes sobre o formato necessário para implementar componentes de biblioteca em extensões da Web, consulte a [visão geral do formato do módulo](./web/format.md).

### Componentes para extensões de borda {#edge}

Em extensões de borda, as regras são acionadas por meio de verificações de condição, que, em seguida, executarão ações específicas se essas verificações forem bem-sucedidas. Consulte a visão geral no [fluxo de extensão de borda](./edge/flow.md) para obter mais informações.

Você pode definir os seguintes componentes de biblioteca nas extensões de borda:

* [Condições](./edge/condition-types.md)
* [Ações](./edge/action-types.md)
* [Elementos de dados](./edge/data-element-types.md)

>[!NOTE]
>
>Para obter mais detalhes sobre o formato necessário para implementar módulos de biblioteca na sua extensão, consulte a [visão geral de formato do módulo](./edge/format.md).

## Configuração de extensão {#configuration}

A configuração de uma extensão se refere à maneira pela qual ela coleta as configurações globais de um usuário. A configuração consiste em um componente de exibição que exporta e emite configurações na biblioteca de tempo de execução de tags como um objeto simples.

Por exemplo, considere uma extensão que permite ao usuário enviar um beacon usando uma ação &quot;Enviar beacon&quot; e o beacon sempre deve conter uma ID da conta. Em vez de solicitar aos usuários uma ID de conta toda vez que configurarem uma ação &quot;Enviar beacon&quot;, a extensão deve solicitar a ID da conta uma vez na visualização de configuração da extensão. Cada vez que um beacon é enviado, a ação &quot;Enviar beacon&quot; pode extrair a ID da conta da configuração da extensão e adicioná-la ao beacon.

Quando os usuários instalam uma extensão em uma propriedade na interface do usuário, eles recebem a visualização de configuração de extensão, que devem ser concluídas para concluir a instalação.

Para saber mais, consulte o guia sobre [configurações de extensão](./configuration.md).

## Envio de extensões

Quando terminar de criar sua extensão, você poderá enviá-la para ser listada no catálogo de extensões na Platform. Consulte a [visão geral do processo de envio da extensão](./submit/overview.md) para obter mais informações.