---
title: Implementação de bibliotecas de terceiros
description: Saiba mais sobre os diferentes métodos de hospedagem de bibliotecas de terceiros nas extensões de tags da Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 69%

---

# Implementação de bibliotecas de terceiros

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Um dos principais objetivos das extensões de tags no Adobe Experience Platform é permitir que você implemente facilmente as tecnologias de marketing (bibliotecas) existentes no seu site. Usando extensões, você pode implementar bibliotecas fornecidas por redes de entrega de conteúdo (CDNs) de terceiros sem precisar editar manualmente o HTML do seu site.

Existem vários métodos para hospedar bibliotecas de terceiros (fornecedores) nas suas extensões. Este documento fornece uma visão geral desses diferentes métodos de implementação, incluindo os prós e contras de cada um.

## Pré-requisitos

Este documento requer uma compreensão funcional das extensões nas tags, incluindo o que elas podem fazer e como são compostas. Consulte a [visão geral do desenvolvimento de extensão](./overview.md) para obter mais informações.

## Processo de carregamento do código base

Fora do contexto de tags, é importante entender como as tecnologias de marketing normalmente são carregadas em um site. Fornecedores de bibliotecas de terceiros fornecem um snippet de código (chamado de código base) que deve ser incorporado no HTML do seu site para carregar as funcionalidades da biblioteca.

Em geral, os códigos base para tecnologias de marketing executam alguma variante do seguinte processo ao serem carregados em seu site:

1. Configurar uma função global que possa ser usada para interagir com a biblioteca do fornecedor.
1. Carregar a biblioteca do fornecedor.
1. Fazer uma série de chamadas iniciais em fila para a função global para fins de configuração e rastreamento.

Quando a função global é configurada inicialmente, você ainda pode fazer chamadas para a função antes que a biblioteca termine de ser carregada. Todas as chamadas feitas são adicionadas ao mecanismo de enfileiramento do código base e, em seguida, são executadas em ordem sequencial quando a biblioteca é carregada.

Quando a biblioteca terminar de ser carregada, a função global será substituída por uma nova que ignora a fila e, em vez disso, processa imediatamente quaisquer chamadas futuras para a função.

### Exemplo de código base

O seguinte JavaScript é um exemplo de um código base não minificado para a [tag de conversão do Pinterest](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), que será referenciada posteriormente neste documento para demonstrar como o código base será adaptado para diferentes estratégias de implementação com tags:

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

Em resumo, o código base acima fornece uma [expressão de função imediatamente invocada (IIFE)](https://developer.mozilla.org/pt-BR/docs/Glossary/IIFE) que cria uma função global para interagir com a biblioteca (`window.pintrk`). Também atribui a uma variável `scriptURL` o valor de `https://s.pinimg.com/ct/core.js`, que é o local onde a biblioteca está localizada. Como explicado anteriormente, todas as funções que são chamadas antes de a biblioteca ser carregada são colocadas em uma fila (`window.pintrk.queue`) para serem executadas em sequência assim que a biblioteca estiver disponível.

A seguinte parte do código base é a mais relevante quando se trata de entender como a biblioteca é carregada no seu site:

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

O código base cria um elemento de script, define-o para ser carregado de forma assíncrona e define o `src` URL como `https://s.pinimg.com/ct/core.js`. Em seguida, adiciona o elemento de script ao documento inserindo-o antes do primeiro elemento de script já presente no documento.

## Opções de implementação de tags

As seções abaixo demonstram as diferentes maneiras de carregar bibliotecas de fornecedores em suas extensões, usando o código base do Pinterest mostrado anteriormente como exemplo. Cada um desses exemplos envolve a criação de um tipo de ação [para uma extensão da Web](./web/action-types.md) que carrega a biblioteca no seu site.

>[!NOTE]
>
>Embora os exemplos abaixo usem tipos de ação para fins de demonstração, você pode aplicar os mesmos princípios a qualquer função que carregue a biblioteca de tags no site.


Os métodos seguintes são abrangidos:

- [Implementação de bibliotecas de terceiros](#implementing-third-party-libraries)
   - [Pré-requisitos](#prerequisites)
   - [Processo de carregamento do código base](#base-code-loading-process)
      - [Exemplo de código base](#base-code-example)
   - [Opções de implementação de tags](#tags-implementation-options)
      - [Carregar no tempo de execução do host do fornecedor {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Carregar no tempo de execução do host da biblioteca de tags](#load-at-runtime-from-the-tag-library-host)
      - [Incorporar a biblioteca diretamente](#embed-the-library-directly)
   - [Próximas etapas](#next-steps)

### Carregar no tempo de execução do host do fornecedor {#vendor-host}

O método mais comum para a hospedagem da biblioteca do fornecedor é usar a CDN do fornecedor. Como o código base da maioria das bibliotecas de fornecedores já está configurado para carregar a biblioteca por meio da CDN do fornecedor, você pode configurar sua extensão para carregar a biblioteca do mesmo local.

Essa abordagem geralmente é a mais fácil de manter, pois todas as atualizações feitas no arquivo no CDN serão carregadas automaticamente pela extensão.

Ao usar esse método, basta colar o código base inteiro diretamente em um tipo de ação como:

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Como opção, você pode seguir etapas adicionais para reconsiderar essa implementação. Como as variáveis `scriptElement` e `firstScriptElement` agora têm escopo para a função exportada, você pode remover o IIFE, pois essas variáveis não correm o risco de se tornarem globais.

Além disso, as tags fornecem vários [módulos principais](./web/core.md) que são utilitários que qualquer extensão pode usar. Especificamente, o módulo `@adobe/reactor-load-script` carrega um script de um local remoto criando um elemento de script e adicionando-o ao documento. Usando esse módulo para o processo de carregamento do script, você pode refatorar o código de ação ainda mais:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Carregar no tempo de execução do host da biblioteca de tags

O uso de um CDN de fornecedor para hospedagem de biblioteca apresenta vários riscos: o CDN pode falhar, o arquivo pode ser atualizado com um erro crítico a qualquer momento ou o arquivo pode ser comprometido para fins prejudiciais.

Para resolver essas preocupações, você pode optar por incluir a biblioteca do fornecedor como um arquivo separado na extensão. A extensão pode ser configurada para que o arquivo seja hospedado junto com a biblioteca principal de tags. No tempo de execução, a extensão carrega a biblioteca do fornecedor do mesmo servidor que entregou a biblioteca principal ao site.

>[!IMPORTANT]
>
>Em alguns casos, a biblioteca do fornecedor pode carregar código adicional de servidores de terceiros, como acontece com a biblioteca de fornecedores do Pinterest. Nesses casos, o agrupamento da biblioteca de fornecedores com sua extensão pode não resolver totalmente todas as preocupações relacionadas ao risco.

Para implementar isso, você deve primeiro baixar a biblioteca de fornecedores em seu computador. No caso do Pinterest, a biblioteca de fornecedores é encontrada em [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). Depois de baixar o arquivo, você deve colocá-lo no projeto de extensão. No exemplo abaixo, o arquivo é denominado `pinterest.js` e está localizado em uma pasta `vendor` no diretório do projeto.

Depois que o arquivo de biblioteca estiver em seu projeto, você deverá atualizar seu [manifesto de extensão](./manifest.md) (`extension.json`) para indicar que a biblioteca do fornecedor deve ser entregue junto com a biblioteca principal de tags. Isso é feito adicionando o caminho ao arquivo de biblioteca a uma matriz `hostedLibFiles`:

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Por fim, você deve configurar seu código de ação para carregar a biblioteca de fornecedores do mesmo servidor que hospeda a biblioteca principal. O exemplo abaixo usa o código de ação criado na [seção anterior](#vendor-host) como ponto de partida. Usando o [objeto turbine](./turbine.md), você deve passar o nome de arquivo (sem nenhum caminho) do arquivo do fornecedor, da seguinte maneira:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

É importante observar que, ao usar esse método, você deve atualizar manualmente o arquivo do fornecedor baixado sempre que a biblioteca for atualizada no CDN e liberar as alterações em uma nova versão da extensão.

### Incorporar a biblioteca diretamente

Você pode ignorar a necessidade de carregar a biblioteca do fornecedor por completo, incorporando diretamente o código da biblioteca ao próprio código de ação, o que efetivamente o torna parte da biblioteca de tags principal. O uso desse método aumenta o tamanho da biblioteca principal, mas evita a necessidade de fazer uma solicitação HTTP adicional para recuperar um arquivo separado.

Usando o código de ação criado na [seção anterior](#vendor-host) como ponto de partida, você pode substituir a linha em que o script é carregado pelo conteúdo do próprio script:

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Próximas etapas

Este documento forneceu uma visão geral dos diferentes métodos de hospedagem de bibliotecas de terceiros nas extensões de tags. Embora os exemplos fornecidos tenham se concentrado nas bibliotecas, essas técnicas se aplicam a qualquer parte do código que sua extensão possa utilizar.

Consulte a documentação vinculada a este guia para saber mais sobre as ferramentas para configurar suas extensões, incluindo os tipos de ação, o manifesto da extensão, os módulos principais e o objeto turbine.
