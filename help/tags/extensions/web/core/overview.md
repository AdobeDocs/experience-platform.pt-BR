---
title: Visão geral da extensão principal
description: Saiba mais sobre a extensão de tag principal na Adobe Experience Platform.
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: 3b023dde8189d3ca6f8525d1e3366874e4ea2c67
workflow-type: tm+mt
source-wordcount: '5257'
ht-degree: 92%

---

# Visão geral da extensão principal

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A extensão de tag principal é a extensão padrão lançada com a Adobe Experience Platform.

Este documento fornece informações sobre as opções disponíveis ao usar a extensão principal para criar uma regra.

## Tipos de evento da extensão principal {#core-extension-event-types}

Este tópico descreve os tipos de evento disponíveis na extensão principal. Para obter informações sobre as opções que podem ser definidas para vários tipos de evento diferentes, consulte a seção [Opções](#options).

### Eventos no navegador

#### Tab Blur

O evento de desfoque de guia dispara a ação quando uma guia perde o foco. Não há configurações para esse tipo de evento.

#### Tab Focus

O evento de foco na guia dispara a ação quando uma guia obtém o foco. Não há configurações para esse tipo de evento.

### Formulário

#### Blur

O evento de desfoque dispara a ação quando um formulário perde o foco. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Focus

O evento de foco dispara a ação quando um formulário obtém o foco. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Submit

O evento de envio dispara a ação quando um formulário é enviado. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

### Eventos controlados por teclado

#### Key Press

O evento é acionado quando uma tecla é pressionada. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

### Eventos com base em mídia

#### Media Ended

O evento é acionado quando a mídia termina. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Dados carregados por mídia

O evento é acionado quando a mídia carrega dados. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Media Pause

O evento é acionado quando a mídia é pausada. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Media Play

O evento é acionado quando a mídia é reproduzida. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Media Stalled

O evento é acionado caso a mídia seja interrompida. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Tempo de reprodução de mídia

O evento será acionado se a mídia for reproduzida por um período específico. É preciso especificar o tempo de reprodução da mídia para acionar o evento. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.


#### Alteração de volume de mídia

O evento será acionado se o volume for aumentado ou diminuído. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

### Eventos orientados para dispositivos móveis

#### Orientation Change

O evento será acionado se a orientação do dispositivo mudar. É preciso especificar a duração da mudança de orientação para acionar o evento. Não há configurações para esse tipo de evento.

#### Zoom Change

O evento será acionado se o usuário aumentar ou diminuir o zoom. Não há configurações para esse tipo de evento.

### Eventos controlados pelo mouse

#### Click

O evento será acionado se o elemento especificado for selecionado (clicado). Como opção, você pode especificar valores de propriedade que devem ser verdadeiros para o elemento antes que o evento seja acionado.

Se o elemento for uma tag de âncora (`<a>`) para um conteúdo vinculado, você também poderá indicar se deseja atrasar a navegação por um período. Isso poderá ser útil se sua regra exigir tempo extra para ser executada e se ela normalmente não for concluída antes de ocorrer a navegação na página.

>[!WARNING]
>
>Essa opção deve ser usada com extrema cautela devido às possíveis consequências negativas que ela acarreta à experiência do usuário se usada incorretamente.

Quando você usa o atraso de link, a Platform na verdade impede que o navegador saia da página. Em seguida, ele executa um redirecionamento do JavaScript para o destino original após o tempo limite especificado. Isso é especialmente perigoso quando sua marcação de página tem tags `<a>` em que a funcionalidade desejada não leva o usuário para fora da página. Se não for possível resolver seu problema de outra forma, você deverá ser extremamente preciso na definição do seletor, para que esse evento seja disparado exatamente onde é necessário e em nenhum outro lugar.

O valor padrão de atraso do link é de 100 milissegundos. Observe que as tags sempre aguardarão o tempo especificado, e isso não está conectado de forma alguma à execução das ações da regra. É possível que o atraso obrigue o usuário a aguardar mais tempo do que o necessário e também que o atraso não seja suficientemente longo para que todas as ações da regra sejam concluídas com êxito. Atrasos maiores fornecem mais tempo para a execução da regra, mas também prejudicam a experiência do usuário.

Para acionar o atraso, é necessário fornecer o elemento selecionado que aciona o evento e o período específico antes que ele seja acionado.

Para as opções avançadas, consulte a seção [Opções](#options) para obter mais informações.

#### Hover

O evento será acionado se o usuário passar o mouse sobre um elemento especificado. Você também deve configurar se a regra é acionada imediatamente ou após determinado número de milissegundos. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

### Outros eventos

#### Custom Event

O evento será acionado se ocorrer um tipo de evento personalizado. As funções JavaScript nomeadas que são definidas em outro lugar na base de código podem ser usadas como um tipo de evento personalizado. Especifique o nome do tipo de evento personalizado e defina as outras configurações conforme descrito na seção [Opções](#options) a seguir.

#### Data Element Changed

O evento será acionado se um elemento de dados especificado for alterado. É preciso fornecer um nome para o elemento de dados. Você pode selecionar o elemento de dados digitando seu nome no campo de texto ou selecionando o ícone do elemento de dados no lado direito do campo de texto e escolhendo em uma lista fornecida na caixa de diálogo exibida.

#### Direct Call

O evento de chamada direta ignora a detecção de eventos e os sistemas de pesquisa. As regras de chamada direta são perfeitas para situações em que você deseja informar à Platform exatamente o que está acontecendo. Além disso, são adequadas quando o Platform não consegue detectar um evento no DOM, como no Adobe Flash. Especifique a string `_satellite.track` no campo de texto do identificador.

#### Element Exists

O evento será acionado se um elemento especificado existir. Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### Enters Viewport

O evento será acionado se o usuário acessar um visor especificado. Você deve fornecer um seletor de CSS como critério para direcionar elementos correspondentes. Você também deve configurar se a regra é acionada imediatamente ou após um número especificado de milissegundos e se o evento deverá ser acionado sempre que o evento ocorrer ou somente na primeira vez.

Consulte a seção [Opções](#options) para obter mais informações sobre configurações de eventos personalizáveis.

#### History Change

O evento será acionado se ocorrer um evento pushState ou hashchange. Não há configurações para esse tipo de evento.

#### Tempo gasto na página

O evento será acionado se o usuário permanecer na página por um número específico de segundos. Especifique o número de segundos que devem decorrer antes que o evento seja acionado.

### Eventos de carregamento de página

#### DOM Ready

O evento será acionado quando o DOM estiver pronto e o usuário puder interagir com a página. Não há configurações para esse tipo de evento.

#### Library Loaded (Page Top) {#library-loaded-page-top}

O evento é acionado assim que a biblioteca de tags é carregada. Não há configurações para esse tipo de evento.

#### Page Bottom {#page-bottom}

O evento será acionado quando `_satellite.pageBottom();` for chamado. Quando a biblioteca de tags é carregada de maneira assíncrona, esse tipo de evento não deve ser usado. Não há configurações para esse tipo de evento.

#### Window Loaded

O evento será acionado quando onLoad for chamado pelo navegador e a página terminar de ser carregada. Não há configurações para esse tipo de evento.

### Opções {#options}

Cada tipo de evento de formulário usa as seguintes configurações:

#### Specific Elements \| Any Element

* Se você escolher **[!UICONTROL Elementos específicos]**, as opções para selecionar os elementos e valores de propriedade serão exibidas.
* Se você escolher **[!UICONTROL Qualquer elemento]**, não serão necessárias outras opções para refinar os elementos.

#### Elements matching the CSS selector

Insira o seletor de CSS que identifica os elementos que acionam o evento.

#### And having certain property values

Se você selecionar essa opção, serão disponibilizados os seguintes parâmetros:

* `property=value`

   Especificar o valor da propriedade

* Regex

   Ative se a `property=value` for uma expressão regular.

* Add

   Adicione outro par de `property=value`.

#### Advanced options (Bubbling)

* Executar esta regra mesmo quando o evento originar de um elemento descendente
* Permitir que esta regra seja executada mesmo que o evento já tenha disparado uma regra direcionada a um elemento descendente
* Depois que a regra é executada, impedir que o evento acione regras voltadas a elementos ancestrais

## Tipos de condição de extensão principal

Esta seção descreve os tipos de condição disponíveis na extensão principal. Esses tipos de condição podem ser usados com o tipo de lógica regular ou de exceção.

### Dados

#### Cookie

Especifique o nome e o valor do cookie que deve existir para um evento acionar uma ação.

1. Especifique um nome de cookie.
1. Digite o valor que deve existir no cookie se o evento for para acionar uma ação.
1. (Opcional) Ative o Regex se esta for uma expressão regular.

#### Custom Code

Especifique qualquer código personalizado que deve existir como uma condição do evento. Use o editor de código incorporado para inserir o código personalizado.

1. Selecione **[!UICONTROL Abrir editor]**.
1. Digite o código personalizado.
1. Selecione **[!UICONTROL Salvar]**.

Uma variável nomeada `event` estará disponível automaticamente, a qual poderá fazer referência no seu código personalizado. O `event` objeto conterá informações úteis sobre o evento que acionou a regra. A maneira mais fácil de determinar quais dados de evento estão disponíveis é fazer logon `event` no console usando o código personalizado:

```javascript
console.log(event);
return true;
```

Execute a regra em um navegador e inspecione o objeto de evento registrado no console do navegador. Assim que você entender quais informações estão disponíveis, poderá usá-las para decisões programáticas no código personalizado.

*Sequência de condições*

Quando a opção &quot;Run rule components in sequence&quot; das configurações de propriedade está ativada, você pode fazer com que os componentes de regra subsequentes aguardem enquanto sua condição executa uma tarefa assíncrona.

Quando a condição retorna uma [Promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise), a próxima condição na regra não será executada até que a promessa retornada seja resolvida. Se a promessa for rejeitada, as tags considerarão essa condição como uma falha e nenhuma outra condição ou ação dessa regra será executada.

Um exemplo de uma condição que retorna uma promessa:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Comparação de valores {#value-comparison}

Compara dois valores para determinar se essa condição retorna true.

Se você tiver uma regra com várias condições, é possível que essa condição retorne &quot;true&quot;, mas a regra ainda não será acionada, pois as outras condições foram avaliadas como &quot;false&quot; ou uma das exceções teve resultado &quot;true&quot;.

1. Forneça um valor.
1. Selecione o operador. Consulte a lista de operadores de comparação de valores abaixo para obter mais detalhes.
1. (Quando necessário) Selecione se a comparação deve diferenciar maiúsculas de minúsculas.
1. Forneça outro valor para a comparação.

Os seguintes operadores de comparação de valores estão disponíveis:

**Equal:** a condição retornará true se os dois valores forem iguais usando uma comparação não estrita (em JavaScript, é o sinal ==). Os valores podem ser de qualquer tipo. Ao digitar uma palavra como _true_, _false_, _null_ ou _undefined_ em um campo de valor, a palavra é comparada como uma string de caracteres e não é convertida em seu equivalente JavaScript.

**Does Not Equal:** a condição retornará true se os dois valores não forem iguais usando uma comparação não estrita (em JavaScript, o sinal !== operador). Os valores podem ser de qualquer tipo. Ao digitar uma palavra como _true_, _false_, _null_ ou _undefined_ em um campo de valor, a palavra é comparada como uma string de caracteres e não é convertida em seu equivalente JavaScript.

**Contains:** a condição retornará true se o primeiro valor contiver o segundo valor. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;false&quot;.

**Does Not Contain:** a condição retornará true se o primeiro valor não contiver o segundo valor. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resultará na condição que retorna &quot;true&quot;.

**Starts With:** a condição retornará true se o primeiro valor começar com o segundo valor. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;false&quot;.

**Does Not Start With:** a condição retornará true se o primeiro valor não começar com o segundo valor. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;true&quot;.

**Ends With:** a condição retornará true se o primeiro valor terminar com o segundo valor. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;false&quot;.

**Does Not End With:** a condição retornará true se o primeiro valor não terminar com o segundo valor. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;true&quot;.

**Matches Regex:** a condição retornará true se o primeiro valor corresponder à expressão regular. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;false&quot;.

**Does Not Match Regex:** a condição retornará true se o primeiro valor não corresponder à expressão regular. Números são convertidos em strings. Qualquer valor diferente de um número ou uma string resulta na condição que retorna &quot;true&quot;.

**Is Less Than:** a condição retornará true se o primeiro valor for menor que o segundo valor. Strings que representam números são convertidas em números. Qualquer valor diferente de um número ou de uma string que pode ser convertida faz a condição retornar &quot;false&quot;.

**Is Less Than Or Equal To:** a condição retornará true se o primeiro valor for menor ou igual ao segundo valor. Strings que representam números são convertidas em números. Qualquer valor diferente de um número ou de uma string que pode ser convertida faz a condição retornar &quot;false&quot;.

**Is Greater Than:** a condição retornará true se o primeiro valor for maior que o segundo valor. Strings que representam números são convertidas em números. Qualquer valor diferente de um número ou de uma string que pode ser convertida faz a condição retornar &quot;false&quot;.

**Is Greater Than Or Equal To:** a condição retornará true se o primeiro valor for maior ou igual ao segundo valor. Strings que representam números são convertidas em números. Qualquer valor diferente de um número ou de uma string que pode ser convertida faz a condição retornar &quot;false&quot;.

**Is True:** a condição retornará true se o valor for um booleano com o valor true. O valor fornecido não é convertido em um booleano se for qualquer outro tipo. Qualquer valor diferente de booleano com valor &quot;true&quot; resulta na condição retornar como &quot;false&quot;.

**Is Truthy:** a condição retornará true se o valor for verdadeiro após ser convertido em um booleano. Consulte a [documentação do MDN sobre valores truthy](https://developer.mozilla.org/pt-BR/docs/Glossary/Truthy) para obter exemplos de valores truthy.

**Is False:** a condição retornará true se o valor for um booleano com o valor false. O valor fornecido não é convertido em um booleano se for qualquer outro tipo. Qualquer valor diferente de booleano com o valor &quot;false&quot; resulta na condição retornar como &quot;false&quot;.

**Is Falsy:** a condição retornará true se o valor for falso depois de ser convertido em um booleano. Consulte a [documentação do MDN sobre valores falsy](https://developer.mozilla.org/pt-BR/docs/Glossario/Falsy) para ver exemplos de valores falsy.

#### Variable

Especifique o nome e o valor da variável do JavaScript que deve existir para um evento acionar uma ação.

1. Especifique o nome da variável JavaScript.
1. Especifique o valor da variável que deve existir como uma condição para o evento.
1. (Opcional) Ative o Regex se esta for uma expressão regular.

### Envolvimento

#### Landing Page

Especifique a página que o usuário deve ser direcionado para acionar o evento.

1. Especifique a página de aterrissagem.
1. (Opcional) Ative o Regex se esta for uma expressão regular.

#### New/Returning Visitor

Especifique se o visitante deve ser um novo visitante ou um visitante recorrente para um evento acionar uma ação.

Selecione uma das opções a seguir:

* New Visitor
* Returning Visitor

#### Page Views

Configure o número de vezes que o visitante deve visualizar a página antes da ação ser acionada.

1. Selecione se o número de exibições de página deve ser maior que, igual ou inferior ao valor especificado.
1. Especifique o número de exibições de página que determina se a condição foi cumprida.
1. Configure quando as exibições de página são contadas selecionando uma das opções a seguir:
   * Lifetime
   * Current Session

#### Sessions

Acione a ação se o número de sessões do usuário atender aos critérios especificados.

1. Selecione se o número de sessões deve ser maior que, igual ou inferior ao valor especificado.
1. Especifique o número de sessões que determina se a condição foi cumprida.

#### Time On Site

Acione a ação se o número de sessões do usuário atender aos critérios especificados.

Configure por quanto tempo o visitante deve estar no site antes que a ação seja acionada.

1. Selecione se o número de minutos em que o visitante está no site deve ser maior que, igual ou menor que o valor especificado.
1. Especifique o número de minutos que determina se a condição foi cumprida.

#### Traffic Source

Acione a ação se o número de sessões do usuário atender aos critérios especificados.

Especifique a fonte do tráfego do visitante que deve ser &quot;true&quot; para que a ação seja acionada.

1. Especifique a fonte de tráfego.
1. (Opcional) Ative o Regex se esta for uma expressão regular.

### Tecnologia

#### Navegador

Selecione o navegador que o visitante deve usar para que a ação seja acionada.

Selecione um ou mais dos seguintes navegadores:

* Google Chrome
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Device Type

Selecione o tipo de dispositivo que o visitante deve usar para que a ação seja acionada.

Selecione um ou mais dos seguintes tipos de dispositivo:

* Android
* BlackBerry
* Área de trabalho
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operating System

Selecione o sistema operacional que o visitante deve usar para que a ação seja acionada.

Selecione um ou mais dos seguintes sistemas operacionais:

* Android
* BlackBerry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Screen Resolution

Selecione a resolução de tela que os visitantes devem usar em seus dispositivos para que a ação seja acionada.

1. Selecione se a largura da resolução de tela do dispositivo do visitante deve ser maior que, igual ou inferior ao valor especificado.
1. Especifique o número de pixels necessários para a largura da resolução de tela.
1. Selecione se a altura da resolução de tela do dispositivo do visitante deve ser maior que, igual ou inferior ao valor especificado.
1. Especifique o número de pixels necessários para a altura da resolução de tela.

#### Window Size

Selecione o tamanho de tela que os visitantes devem usar em seus dispositivos para que a ação seja acionada.

1. Selecione se a largura de tamanho da tela do dispositivo do visitante deve ser maior que, igual ou inferior ao valor especificado.
1. Especifique o número de pixels necessários para a largura de tamanho da janela.
1. Selecione se a altura do tamanho da tela do dispositivo do visitante deve ser maior que, igual ou inferior ao valor especificado.
1. Especifique o número de pixels necessários para a altura do tamanho da janela.

### URL

#### Domain

Especifique o domínio do visitante.

#### Hash

Especifique um ou mais padrões de hash que devem existir no URL.

>[!NOTE]
>
>Vários padrões de hash são unidos por um OR.

1. Especifique o padrão de hash.
1. (Opcional) Ative o Regex se esta for uma expressão regular.
1. Adicione outros padrões de hash.

#### Path And Query String

Especifique um ou mais caminhos que devem existir no URL. Inclui o caminho e a sequência de consulta.

>[!NOTE]
>
>Vários caminhos são unidos por um OR.

1. Especifique o caminho.
1. (Opcional) Ative o Regex se esta for uma expressão regular.
1. Adicione outros caminhos.

#### Path Without Query String

Especifique um ou mais caminhos que devem existir no URL. Inclui o caminho, mas não inclui a sequência de consulta.

>[!NOTE]
>
>Vários caminhos são unidos por um OR.

1. Especifique o caminho.
1. (Opcional) Ative o Regex se esta for uma expressão regular.
1. Adicione outros caminhos.

#### Protocolo

Especifique o protocolo usado no URL.

Selecione uma das opções a seguir:

* HTTP
* HTTPS

#### Query String Parameter

Especifique o parâmetro de URL usado no URL.

1. Especifique um nome de parâmetro de URL.
1. Especifique o valor usado para o parâmetro de URL.
1. (Opcional) Ative o Regex se esta for uma expressão regular.

#### Subdomain

Especifique um ou mais subdomínios que devem existir no URL.

>[!NOTE]
>
>Vários subdomínios são unidos por um OR.

1. Especifique o subdomínio.
1. (Opcional) Ative o Regex se esta for uma expressão regular.
1. Adicione quaisquer outros subdomínios.

### Outras

#### Date Range

Especifique um intervalo de datas. Escolha a data e a hora em que o evento ocorre depois, a data em que ocorre antes e o fuso horário.

#### Max Frequency

Especifique o número máximo de vezes que a condição retorna true. Você pode selecionar entre as opções a seguir:

* Page view
* Sessões
* Visitor
* Seconds
* Minutes
* Days
* Weeks
* Months

Para a condição de frequência máxima 1 por sessão, esses dois itens `localStorage` são comparados. Se o `visitorTracking.sessionCount` for maior que a contagem de `maxFrequency.session`, a condição de amostragem será verdadeira. Se forem iguais, a condição será falsa.

`sessionCount` é um item `visitorTracking`, portanto, a API do visitante deve estar ativada para que a condição de amostragem funcione.

#### Sampling

Especifique a porcentagem de tempo em que a condição retorna &quot;true&quot;.

## Tipos de ação da extensão principal

Esta seção descreve os tipos de ação disponíveis na extensão principal.

### Código personalizado

Forneça o código que é executado depois que o evento é acionado e as condições são avaliadas.

1. Dê um nome ao código da ação.
1. Selecione o idioma usado para definir a ação:
   * JavaScript
   * HTML
1. Selecione se o código de ação deve ser executado globalmente.
1. Selecione **[!UICONTROL Abrir editor]**.
1. Edite o código e selecione **[!UICONTROL Salvar]**.

Quando o JavaScript é selecionada como a linguagem, uma variável nomeada `event` estará disponível automaticamente, a qual poderá fazer referência no seu código personalizado. O `event` objeto conterá informações úteis sobre o evento que acionou a regra. A maneira mais fácil de determinar quais dados de evento estão disponíveis é fazer logon `event` no console usando o código personalizado:

```javascript
console.log(event);
```

Execute a regra em um navegador e inspecione o objeto de evento registrado no console do navegador. Assim que entender quais informações estão disponíveis, poderá usá-las para tomar decisões programáticas em seu código personalizado, envie uma parte do objeto `event` para um servidor, e assim por diante.

### Processamento de ação do Custom Code

A extensão principal, disponível para todos os usuários da Adobe Experience Platform, contém uma ação de Código personalizado para executar o JavaScript ou o HTML fornecido pelo usuário. Geralmente, é útil que os usuários entendam como as regras com ações Custom Code são processadas.

#### Regras que usam os eventos do início ou do final da página

O código de ações personalizadas está incorporado à biblioteca de tags principal. O código é gravado no documento usando document.write. Se uma regra tiver várias ações Custom Code, o código será escrito na ordem configurada na regra.

#### Regras que usam qualquer evento diferente dos eventos de início ou de final da página

O código de ações personalizadas é carregado a partir do servidor e gravado no documento usando [Postscribe](https://github.com/krux/postscribe). Se uma regra tiver várias ações Custom Code, o código será carregado simultaneamente a partir do servidor, mas escrito na ordem configurada na regra.

Ao usar document.write depois que uma página é carregada normalmente causa problemas, isso não é um problema para o código fornecido por meio das ações Custom Code. Você pode usar document.write nas ações Custom Code independentemente de quando o código será executado.

#### Custom Code Validation

O validador usado no editor de código de tags foi projetado para identificar problemas em código escrito pelo desenvolvedor. O código que passou por um processo de &quot;minificação&quot; — como o código AppMeasurement.js baixado do Gerenciador de código — pode ser falsamente sinalizado como tendo problemas pelo validador do, que geralmente pode ser ignorado.

#### Sequência de ação

Quando a opção &quot;Run rule components in sequence&quot; das configurações de propriedade está ativada, você pode fazer com que os componentes de regra subsequentes aguardem enquanto sua ação executa uma tarefa assíncrona. Funciona de forma diferente para código personalizado JavaScript e HTML.

*JavaScript*

Ao criar uma ação de código personalizado JavaScript, você pode retornar uma [Promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) de sua ação. A próxima ação na regra será executada somente quando a promessa retornada é resolvida. Se a promessa for rejeitada, as próximas ações da regra não serão executadas.

>[!NOTE]
>
>Isso só funciona quando o JavaScript não está definido para execução global. Se você estiver executando a ação de código personalizado no escopo global, as tags tratarão a promessa como imediatamente resolvida, avançando para o próximo item na fila de processamento.

Um exemplo de uma ação de código personalizado JavaScript que retorna uma promessa:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

Ao criar uma ação de código personalizado HTML, uma função chamada `onCustomCodeSuccess()` estará disponível para uso dentro do código personalizado. É possível chamar essa função para indicar que o código personalizado foi concluído e que as tags podem continuar a executar ações subsequentes. Por outro lado, se o código personalizado falhar de alguma forma, você pode chamar o `onCustomCodeFailure()`. Assim, as tags serão instruídas a não executar as ações subsequentes dessa regra.

Um exemplo de uma ação de código personalizado HTML que usa os novos retornos de chamada:

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

## Tipos de elementos de dados da extensão principal

Os tipos de elementos de dados são determinados pela extensão. Não há limite para os tipos que podem ser criados.

As seções a seguir descrevem os tipos de elementos de dados disponíveis na extensão principal. Outras extensões usam outros tipos de elementos de dados.

### Cookie

Todo cookie de domínio disponível pode ser referido no campo campo de nome do cookie.

#### Exemplo:

`cookieName`

### Constante

Qualquer valor constante de string que possa ser referenciado em ações ou condições.

#### Exemplo:

`string`

### Custom code

JavaScript personalizado pode ser inserido na interface selecionando Abrir editor e inserindo o código na janela do editor.

É preciso haver uma instrução de retorno na janela do editor indicando que o valor deve ser usado como aquele valor do elemento de dados. Se uma declaração de retorno não for incluída ou se os valores `null` ou `undefined` forem retornados, o valor padrão do elemento de dados será usado como o valor do elemento de dados.

**Exemplo:**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Se o elemento de dados de código personalizado estiver sendo recuperado como parte de uma execução de regra, uma variável nomeada `event` automaticamente se torna disponível, a qual poderá fazer referência no seu código personalizado. O `event` objeto conterá informações úteis sobre o evento que acionou a regra. A maneira mais fácil de determinar quais dados de evento estão disponíveis é fazer logon `event` no console usando o código personalizado:

```javascript
console.log(event);
return true;
```

Execute a regra em um navegador e inspecione o objeto de evento registrado no console do navegador. Assim que você entender quais informações estão disponíveis sob as várias regras que podem usar seu elemento de dados, você poderá usá-las para tomar decisões programáticas em seu código personalizado ou retornar uma parte do objeto `event` como o valor do elemento de dados.

### Atributo DOM

Todo valor de elemento pode ser recuperado, como uma tag div ou H1.

#### Exemplo:

Corrente do seletor de CSS:

`id#dc logo img`

Obtenha o valor de:

`src`

### variável JavaScript

Todo objeto ou variável disponíveis do JavaScript pode ser referido usando o campo de caminho.

Elementos de dados de tag podem ser usados para capturar as variáveis de JavaScript de marcação ou as propriedades do objeto. Esses valores podem ser usados em suas extensões ou regras personalizadas, fazendo referência aos elementos de dados da tag. Se a fonte de dados for alterada, será necessário apenas atualizar a referência para a fonte na interface da coleção de dados.

No exemplo abaixo, a marcação contém uma variável JavaScript chamada `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Ao criar o elemento de dados na interface da coleção de dados, forneça apenas o caminho dessa variável.

Se você usar um objeto de coleção de dados como parte da camada de dados, utilize a notação de pontos no caminho para fazer referência ao objeto e à propriedade que deseja capturar no elemento de dados, como `_myData.pageName` ou `digitalData.pageName` e assim por diante.

#### Exemplo:

`window.document.title`

### Armazenamento local

Forneça o nome do item de armazenamento local no campo Local Storage Item Name.

O armazenamento local fornece aos navegadores uma maneira de armazenar informações de página a página ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). O armazenamento local funciona de forma bem semelhante aos cookies, mas é muito maior e mais flexível.

Use o campo fornecido para especificar o valor criado para um item de armazenamento local, como `lastProductViewed.`

### Objetos Mesclados

Selecione vários elementos de dados que fornecerão um objeto cada. Esses objetos serão profundamente (recursivamente) unidos para produzir um novo objeto. Os objetos de origem não serão modificados. Se uma propriedade for encontrada no mesmo local em vários objetos de origem, o valor do último objeto será usado. Se um valor de propriedade de origem for `undefined`, ele não substituirá um valor de um objeto de origem anterior. Se as matrizes forem encontradas no mesmo local em vários objetos de origem, elas serão concatenadas.

Como exemplo, suponha que você selecione um elemento de dados que forneça o seguinte objeto:

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

Suponha que você também selecione outro elemento de dados que forneça o seguinte objeto:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

O resultado do elemento de dados Objetos Mesclados seria o seguinte objeto:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### Informações da página

Use esses pontos de dados para capturar informações de página para usar na lógica da regra ou para enviar informações ao Analytics ou aos sistemas de rastreamento externos.

Você pode selecionar um dos atributos de página a seguir para ser usado em seu elemento de dados:

* URL
* Hostname
* Pathname
* Protocolo
* Referenciador
* Title

### Query string Parameter

Especifique um único parâmetro de URL no campo URL Parameter.

Somente a seção de nome é necessária e qualquer designador especial como &quot;?&quot; ou &quot;=&quot; deve ser omitido

#### Exemplo:

`contentType`

### Número aleatório

Use esse elemento de dados para gerar um número aleatório. É usado frequentemente para amostra de dados ou para a criação de IDs, como uma ID de ocorrência. O número aleatório também pode ser usado para ofuscar ou eliminar dados confidenciais. Alguns exemplos podem incluir:

* Gerar uma ID de ocorrência
* Concatene o número para um token de usuário ou carimbo de data e hora para garantir exclusividade
* Executar um hash unidirecional em dados PII
* Decida aleatoriamente quando mostrar uma solicitação de pesquisa no site

Especifique os valores mínimos e máximos para o número aleatório.

**Padrões:**

Mínimo: 0

Máximo: 1000000000

### Armazenamento de sessão

Forneça o nome do item de armazenamento da sessão no campo Session Storage Item Name.

O armazenamento de sessão é semelhante ao armazenamento local, a diferença é que os dados são descartados depois que a sessão é encerrada, enquanto o armazenamento local ou um cookie pode reter os dados.

### Visitor behavior

De forma semelhante às informações da página, esse elemento de dados usa tipos de comportamento comuns para aprimorar a lógica nas regras além de outras soluções da Platform.

Selecione um dos seguintes atributos de comportamento do visitante:

* Landing page
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Alguns casos de uso comuns incluem:

* Mostrar uma pesquisa depois que um visitante estiver no site por cinco minutos
* Se esta for a landing page para a visita, preencher uma métrica do Analytics
* Mostrar uma nova oferta ao visitante depois do número X de Contagens de sessão
* Exibir um cadastro de informativo se for uma primeira visita

### Valor condicional

Um invólucro para a condição [Value Comparison](#value-comparison-value-comparison). Com base no resultado da comparação, o retornará um dos dois valores disponíveis no formulário. Pode, assim, lidar com &quot;If... Então.. Senão...&quot; cenários sem a necessidade de regras adicionais.

### Ambiente de tempo de execução

Permite selecionar uma das seguintes variáveis:

* Estágio do ambiente - Retorna `_satellite.environment.stage` para diferenciar entre ambientes de desenvolvimento/preparo/produção.
* Data de build da biblioteca - Retorna `turbine.buildInfo.buildDate` que contém o mesmo valor como `_satellite.buildInfo.buildDate`.
* Nome da propriedade - Retorna `_satellite.property.name` para obter o nome da propriedade do Launch.
* ID da propriedade - Retorna `_satellite.property.id` para obter a ID da propriedade do Launch
* Nome da regra - Retorna `event.$rule.name` contendo o nome da regra executada.
* ID da regra - Retorna `event.$rule.id` contendo a ID da regra executada.
* Tipo de evento - Retorna `event.$type` contendo o tipo de evento que acionou a regra.
* Carga de detalhes do evento - Retorna `event.detail` contendo a carga útil de um evento personalizado ou de uma regra de chamada direta.
* Identificador de chamada direta - Retorna `event.identifier` contendo o identificador de uma Regra de chamada direta.

### Atributos do dispositivo

Retorna um dos seguintes atributos de dispositivo do visitante:

* Tamanho da janela do navegador
* Tamanho da tela

### Ferramentas JavaScript

É um wrapper para operações comuns do JavaScript. Ele recebe um elemento de dados como uma entrada. Ele retorna o resultado de uma das seguintes transformações do valor do elemento de dados:

* Manipulação básica da sequência de caracteres (substituir, substring, correspondência de regex, primeiro e último índice, divisão, fatia)
* Operações básicas de matriz (fatia, junção, pop, turno)
* Operações universais básicas (fatia, comprimento)