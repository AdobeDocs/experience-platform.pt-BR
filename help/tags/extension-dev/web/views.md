---
title: Exibições em extensões da Web
description: 'Saiba como definir visualizações para módulos de biblioteca em extensões da Web do Adobe Experience Platform '
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: 41efcb14df44524b58be2293d2b943bd890c1621
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 97%

---

# Visualizações em extensões da Web

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Cada tipo de evento, condição, ação ou elemento de dados pode fornecer uma visualização, o que permite ao usuário fornecer configurações. A extensão também pode ter uma [visualização de configuração de extensão](../configuration.md) de nível superior, o que permite aos usuários fornecer configurações globais para a extensão inteira. O processo de construção de uma visualização é idêntico em todos os tipos de visualizações.

## Incluir um tipo de documento

Certifique-se de incluir uma tag `doctype` no arquivo HTML. Normalmente, isso significa iniciar o arquivo HTML com o seguinte:

```xml
<!DOCTYPE html>
```

## Inclusão do script de iframe das tags

Inclua o script de iframe das tags no HTML da visualização:

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

Esse script fornece uma API de comunicação para permitir que a visualização se comunique com o aplicativo das tags.

## Registro com a API de comunicação de bridge de extensão

Depois que o script de iframe for carregado, será necessário fornecer alguns métodos para tags, que ele usará para comunicação. Chame `window.extensionBridge.register` e passe um objeto da seguinte maneira:

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

O conteúdo de cada um dos métodos precisará ser modificado para acomodar seus requisitos de visualização específicos.

### [!DNL init]

O método `init` será chamado pelas tags assim que a visualização for carregada no iframe. Será transmitido um único argumento (`info`) que deve ser um objeto com as seguintes propriedades:

| Propriedade | Descrição |
| --- | --- |
| `settings` | Um objeto que contém as configurações que foram salvas anteriormente dessa visualização. Se `settings` for `null`, isso indicará que o usuário está criando as configurações iniciais em vez de carregar uma versão salva. Se `settings` for um objeto, você deverá usá-lo para preencher sua visualização, pois o usuário optou por editar as configurações persistidas anteriormente. |
| `extensionSettings` | Configurações salvas da visualização de configuração de extensão. Isso pode ser útil para acessar configurações de extensão em visualizações que não sejam a de configuração de extensão. Se a visualização atual for a de configuração de extensão, use `settings`. |
| `propertySettings` | Um objeto que contém configurações da propriedade. Consulte o [guia de objetos de turbina](../turbine.md#property-settings) para obter detalhes sobre o que está contido nesse objeto. |
| `tokens` | Um objeto que contém tokens de API. Para acessar as APIs da Adobe na visualização, geralmente é necessário usar um token IMS em `tokens.imsAccess`. Esse token será disponibilizado somente para extensões desenvolvidas pela Adobe. Se você for um funcionário da Adobe que representa uma extensão criada pela Adobe, [envie um email à equipe de engenharia de coleta de dados](mailto:reactor@adobe.com) e forneça o nome da extensão para que seja possível adicioná-la à lista de permissões. |
| `company` | Um objeto que contém uma única propriedade, `orgId`, que representa ela mesma sua Adobe Experience Cloud ID (uma sequência alfanumérica de 24 caracteres). |
| `schema` | Um objeto no formato de [esquema JSON](https://json-schema.org/). Este objeto será proveniente do [manifesto da extensão](../manifest.md) e pode ser útil para validar o formulário. |

A visualização deve usar essas informações para renderizar e gerenciar o formulário. É provável que você só precise lidar com `info.settings`, mas as outras informações são fornecidas, caso sejam necessárias.

### [!DNL validate]

O método `validate` será chamado depois que o usuário clicar no botão &quot;Salvar&quot;. Ele deve retornar uma das seguintes opções:

* Um booliano que indica se a entrada do usuário é válida.
* Uma promessa a ser resolvida posteriormente com um booliano que indica se a entrada do usuário é válida.

Como desenvolvedor da extensão, você deve determinar o que constitui uma entrada válida, já que seu módulo da biblioteca atuará em relação a essa entrada.

Se a entrada do usuário for inválida, mostre alguma indicação disso na visualização para que os usuários saibam o que precisa ser corrigido.

### [!DNL getSettings]

O método `getSettings` será chamado depois que o usuário clicar no botão &quot;Salvar&quot; e a visualização for validada. A função deve retornar uma das seguintes opções:

* Um objeto que contém configurações com base na entrada do usuário.
* Uma promessa a ser resolvida posteriormente com um objeto que contém configurações com base na entrada do usuário.

Esse objeto de configurações será emitido posteriormente na biblioteca de tempo de execução da tag. O conteúdo desse objeto fica a seu critério. O objeto deve ser serializável e desserializável de e para JSON. Valores como funções ou instâncias [RegExp](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/RegExp) não atendem a esses critérios e, portanto, não são permitidos.

## Aproveitamento de visualizações compartilhadas

O objeto `window.extensionBridge` tem vários métodos que permitem aproveitar as visualizações existentes disponíveis por meio das tags, para que não seja necessário reproduzi-las na visualização. As opções disponíveis são as seguintes:

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

Chamar esse método mostrará um modal que permite ao usuário editar um trecho de código. Quando o usuário terminar de editar o código, a promessa será resolvida com o código atualizado. Se o usuário fechar o editor de código sem optar por salvar as alterações, a promessa nunca será resolvida. O objeto `options` deve ser estruturado da seguinte maneira:

| Propriedade | Descrição |
| --- | --- |
| `code` | Código que deve ser mostrado no editor. Normalmente, isso é fornecido quando o usuário está editando o código existente. Caso isso não seja fornecido, o editor de código ficará vazio quando aberto. |
| `language` | A linguagem do código que será editado. As opções válidas são `javascript`, `html`, `css`, `json` e `plaintext`. Caso isso não seja fornecido, `javascript` será presumido. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

Chamar esse método mostrará um modal que permite ao usuário testar e modificar um padrão de expressão regular. Quando o usuário terminar de editar a expressão normal, a promessa será resolvida com o padrão de expressão regular atualizado. Se o usuário fechar o testador regex sem optar por salvar as alterações, a promessa nunca será resolvida. O objeto `options` deve conter as seguintes propriedades:

| Propriedade | Descrição |
| --- | --- |
| `pattern` | O padrão de expressão regular que deve ser usado como o valor inicial do campo de padrão no testador. Normalmente, isso é fornecido quando o usuário edita uma expressão regular existente. Se isso não for fornecido, o campo padrão estará inicialmente vazio. |
| `flags` | Os sinalizadores de expressão regular que devem ser usados pelo testador. Por exemplo, `gi` indicaria o sinalizador de correspondência global e o sinalizador para ignorar maiúsculas e minúsculas. Esses sinalizadores não podem ser modificados pelo usuário no testador, mas são usados para demonstrar os sinalizadores específicos que a extensão usará ao executar a expressão regular. Se isso não for fornecido, nenhum sinalizador será usado no testador. Consulte a [Documentação de RegExp do MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) para obter mais informações sobre sinalizadores de expressão regular.<br><br>Um cenário comum é uma extensão que permite aos usuários ativar e desativar a detecção de maiúsculas e minúsculas de uma expressão regular. Para oferecer suporte a isso, normalmente a extensão fornece uma caixa de seleção na respectiva visualização que, quando marcada, ativa a opção de não detectar maiúsculas e minúsculas (representada pelo sinalizador `i`). O objeto de configurações salvo pela visualização precisaria representar se a caixa de seleção estava marcada para que o módulo da biblioteca que executa a expressão regular pudesse saber se o sinalizador `i` deve ser usado. Além disso, quando a visualização de extensão desejar abrir o testador de expressões regulares, será necessário passar o sinalizador `i` se a caixa de seleção para não detectar maiúsculas e minúsculas estiver marcada. Isso permite que o usuário teste corretamente a expressão regular com a opção de não detectar maiúsculas e minúsculas ativada. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

Chamar esse método mostrará um modal que permite ao usuário selecionar um elemento de dados. Quando o usuário terminar de selecionar um elemento de dados, a promessa será resolvida com o nome do elemento de dados selecionado (por padrão, o nome estará entre sinais de porcentagem). Se o usuário fechar o seletor de elementos sem optar por salvar as alterações, a promessa nunca será resolvida.

O objeto `options` deve conter uma única propriedade booliana, `tokenize`. Essa propriedade indica se o nome do elemento de dados selecionado deve ser colocado entre sinais de porcentagem antes de resolver a promessa. Consulte a seção sobre [elementos de dados de suporte](#supporting-data-elements) para saber por que isso é útil. O padrão dessa opção é `true`.

## Elementos de dados de suporte {#supporting-data-elements}

Provavelmente, suas visualizações têm campos de formulário nos quais os usuários gostariam de aproveitar elementos de dados. Por exemplo, caso a visualização tenha um campo de texto no qual o usuário deva digitar um nome de produto, talvez não faça sentido que o usuário digite um valor embutido em código no campo. Em vez disso, eles podem desejar que o valor do campo seja dinâmico (determinado no tempo de execução) e podem fazer isso usando um elemento de dados.

Como exemplo, suponha que estejamos construindo uma extensão que envia um sinal para rastrear uma conversão. Vamos supor também que um dos dados que nosso beacon envia é um nome de produto. Nossa visualização de extensão que permite ao usuário configurar o beacon provavelmente terá um campo de texto para o nome do produto. Normalmente, não faria muito sentido para o usuário do Platform digitar um nome de produto estático, como &quot;Calzone Oven XL&quot;, porque o nome do produto provavelmente depende da página da qual o beacon será enviado. Este é um caso ideal para um elemento de dados.

Se um usuário quiser usar o elemento de dados chamado `productname` como o valor do nome do produto, ele poderá digitar o nome do elemento de dados com sinais de porcentagem em ambos os lados (`%productname%`). Nós nos referimos ao nome do elemento de dados com sinal de porcentagem como um &quot;token de elemento de dados&quot;. Os usuários da Platform geralmente estão familiarizados com essa construção. Por sua vez, a extensão salvaria o token do elemento de dados dentro do objeto `settings` exportado. Seu objeto de configurações pode ter a seguinte aparência:

```js
{
  productName: '%productname%'
}
```

No tempo de execução, antes de passar o objeto de configurações para o módulo da biblioteca, o objeto de configurações é digitalizado e todos os tokens de elemento de dados são substituídos pelos respectivos valores. Se, no tempo de execução, o valor do elemento de dados `productname` fosse `Ceiling Medallion Pro 2000`, o objeto de configurações passado para o módulo de biblioteca seria o seguinte:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Para indicar onde pode ser útil para os usuários usar elementos de dados e facilitar a inserção de um elemento de dados, é altamente recomendável adicionar um botão de ícone ao lado desses campos, como mostrado aqui:

![campo de elemento de dados](../images/data-element-field.png)

>[!NOTE]
>
>Para baixar o ícone apropriado, navegue até o [página de ícones no Adobe Spectrum](https://spectrum.adobe.com/page/icons/) e pesquisar por &quot;[!DNL Data]&quot;.

Quando um usuário clicar no botão ao lado do campo de texto, chamar `window.extensionBridge.openDataElementSelector` como [descrito acima](#open-data-element). Isso exibirá uma lista dos elementos de dados do usuário que ele pode escolher, em vez de forçá-lo a lembrar o nome e digitar os sinais de porcentagem. Depois que o usuário selecionar um elemento de dados, você receberá o nome do elemento de dados selecionado encapsulado em sinais de porcentagem (a menos que a opção `tokenize` esteja definida como `false`). Recomendamos que você preencha o campo de texto com o resultado.

### Substituição de tokens de elementos de dados

Conforme descrito anteriormente, se um objeto de configurações persistidas consistisse no seguinte:

```js
{
  productName: '%productname%'
}
```

E, se no tempo de execução, o valor do elemento de dados `productname` fosse `Ceiling Medallion Pro 2000`, então o objeto de configurações passado para seu módulo de biblioteca seria o seguinte:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Sempre que for encontrado um valor em um objeto de configurações que consista em um sinal de porcentagem, em seguida, uma sequência de caracteres, um sinal de porcentagem, _e nada mais_, ele será substituído pelo valor do elemento de dados _sem alterar o tipo do valor do elemento de dados_.

Por exemplo, se o valor de `productname` no tempo de execução fosse o número `538` (não uma sequência de caracteres), o objeto de configurações passado para o módulo da biblioteca seria o seguinte:

```js
{
  productName: 538
}
```

Observe que o `538` resultante é um número aqui e não uma sequência de caracteres. Da mesma maneira, se o valor do elemento de dados em tempo de execução fosse uma função (um caso de uso raro, mas possível), o objeto de configurações resultante seria o seguinte:

```js
{
  productName: function() { … }
}
```

Por outro lado, vamos supor que os objetos de configurações persistentes sejam os seguintes:

```js
{
  productName: '%productname% - %modelnumber%'
}
```

Nesse caso, como o valor de `productName` é maior que um token de elemento de dados único, o resultado sempre será uma sequência de caracteres. Cada token de elemento de dados será substituído pelo respectivo valor depois de ser convertido em uma sequência de caracteres. Se, no tempo de execução, o valor de `productname` fosse `Ceiling Medallion Pro` (uma sequência de caracteres) e `modelnumber` fosse `2000` (um número), o objeto de configurações resultante passado para o módulo de biblioteca seria:

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Evitar a navegação

A comunicação entre a visualização de extensão e a interface do usuário que contém a coleta de dados depende da ausência de navegação na visualização de extensão. Assim, evite adicionar algo à sua visualização de extensão que permita ao usuário navegar para fora da página HTML da visualização de extensão. Por exemplo, se você fornecer um link na visualização de extensão, verifique se ele abre uma nova janela do navegador (normalmente adicionando `target="_blank"` à tag de âncora). Se você optar por usar um elemento `form` na visualização de extensão, garanta que o formulário nunca seja enviado. O envio do formulário poderá ocorrer acidentalmente se você tiver um elemento `button` no formulário e não adicionar `type="button"` a ele. O envio de um formulário na visualização de extensão faria com que o documento HTML fosse atualizado, resultando em uma experiência do usuário com problemas.
