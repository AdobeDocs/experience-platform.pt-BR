---
title: Visão geral do desenvolvimento de extensões
description: Saiba mais sobre os componentes principais de diferentes tipos de extensão de tag e o processo de desenvolvimento de extensão no Adobe Experience Platform.
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 20%

---

# Visão geral do desenvolvimento de extensões

Um dos principais objetivos das tags na Adobe Experience Platform é criar um ecossistema aberto em que os engenheiros fora da Adobe possam expor funcionalidades adicionais em seus sites e aplicativos móveis. Isso é feito por meio de extensões de tag. Depois que uma extensão é instalada em uma propriedade de tag, a funcionalidade dessa extensão fica disponível para uso por todos os usuários da propriedade.

Este documento descreve os componentes principais de uma extensão e fornece links para documentação adicional para ajudar a orientá-lo sobre o processo de desenvolvimento da extensão.

## Estrutura da extensão

Uma extensão consiste em um diretório de arquivos. Especificamente, uma extensão consiste em um arquivo de manifesto, módulos de biblioteca e exibições.

### Arquivo de manifesto

Um arquivo de manifesto ([`extension.json`](./manifest.md)) deve existir na raiz do diretório. Esse arquivo descreve a composição da extensão e onde determinados arquivos estão localizados no diretório. O manifesto funciona de forma semelhante a um arquivo [`package.json`](https://docs.npmjs.com/files/package.json) em um projeto [npm](https://www.npmjs.com/).

### Módulos da biblioteca

Os módulos da biblioteca são os arquivos que descrevem os diferentes [componentes](#components) fornecidos por uma extensão (em outras palavras, a lógica a ser emitida na biblioteca de tempo de execução de tag). O conteúdo de cada arquivo de módulo de biblioteca deve seguir o [padrão de módulo CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules).

Por exemplo, se você estiver criando um tipo de ação chamado &quot;enviar beacon&quot;, deverá ter um arquivo que contenha a lógica de envio do beacon. Se estiver usando o JavaScript, o arquivo pode ser chamado de `sendBeacon.js`. O conteúdo desse arquivo será emitido na biblioteca de tempo de execução de tag.

Você pode colocar os arquivos de módulo de biblioteca em qualquer lugar que desejar no diretório de extensão, desde que descreva seus locais em `extension.json`.

### Exibições

Uma exibição é um arquivo HTML que pode ser carregado em um [`iframe` elemento](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/iframe) no aplicativo de marcas, especificamente por meio da interface do usuário da Experience Platform e da interface da Coleção de Dados. A visualização deve incluir um script fornecido pela extensão e estar em conformidade com uma pequena API para se comunicar com o aplicativo.

O arquivo de visualização mais importante para qualquer extensão é sua configuração. Consulte a seção sobre [configurações de extensão](#configuration) para obter mais informações.

Não há restrições quanto às bibliotecas usadas nas visualizações. Em outras palavras, você pode usar jQuery, Underscore, React, Angular, Bootstrap ou outros. No entanto, ainda é recomendável fazer com que sua extensão tenha uma aparência semelhante à interface do usuário.

É recomendado colocar todos os arquivos relacionados à visualização (HTML, CSS, JavaScript) em um único subdiretório que esteja isolado dos arquivos do módulo da biblioteca. Em `extension.json`, você pode descrever onde está localizado esse subdiretório de exibição. O Experience Platform fornecerá esse subdiretório (e somente ele) por meio de seus servidores da Web.

## Componentes da biblioteca {#components}

Cada extensão define um conjunto de funcionalidades. Essas funcionalidades são implementadas sendo incluídas em uma [biblioteca](../ui/publishing/libraries.md) implantada em seu site ou aplicativo. As bibliotecas são uma coleção de componentes individuais, incluindo condições, ações, elementos de dados e muito mais. Cada componente da biblioteca é um código reutilizável (fornecido por uma extensão) emitido no tempo de execução da tag.

Dependendo de você estar desenvolvendo uma extensão da Web ou uma extensão de borda, os tipos disponíveis de componentes e seus casos de uso serão diferentes. Consulte as subseções abaixo para obter uma visão geral de quais componentes estão disponíveis para cada tipo de extensão.

### Componentes para extensões da Web {#web}

Em extensões da Web, as regras são acionadas por meio de eventos, que poderão executar ações específicas se um determinado conjunto de condições for atendido. Consulte a visão geral do [fluxo do módulo em extensões da Web](./web/flow.md) para obter mais informações.

Além dos [módulos principais](./web/core.md) fornecidos pela Adobe, você pode definir os seguintes componentes de biblioteca nas extensões da Web:

* [Eventos](./web/event-types.md)
* [Condições](./web/condition-types.md)
* [Ações](./web/action-types.md)
* [Elementos de dados](./web/data-element-types.md)
* [Módulos compartilhados](./web/shared.md)

>[!NOTE]
>
>Para obter mais detalhes sobre o formato necessário para implementar componentes de biblioteca na sua extensão, consulte a [visão geral de formato do módulo](./web/format.md).

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

A configuração de uma extensão se refere à maneira pela qual ela coleta as configurações globais de um usuário. A configuração consiste em um componente de visualização que exporta e emite configurações na biblioteca de tempo de execução de tag como um objeto simples.

Por exemplo, considere uma extensão que permita ao usuário enviar um beacon usando uma ação &quot;Enviar beacon&quot;, e o beacon sempre deva conter uma ID de conta. Em vez de solicitar aos usuários uma ID de conta sempre que eles configurarem uma ação &quot;Enviar beacon&quot;, a extensão deverá solicitar a ID de conta uma vez na visualização de configuração de extensão. Sempre que um beacon é enviado, a ação &quot;Enviar beacon&quot; pode obter a ID da conta da configuração de extensão e adicioná-la ao beacon.

Quando os usuários instalam uma extensão de uma propriedade na interface do usuário, eles exibem a visualização de configuração de extensão, que deve ser concluída para concluir a instalação.

Para saber mais, consulte o guia em [configurações de extensão](./configuration.md).

## Envio de extensões

Depois de concluir a criação da extensão, você pode enviá-la para ser listada no catálogo de extensões no Experience Platform. Consulte a [visão geral do processo de envio de extensão](./submit/overview.md) para obter mais informações.
