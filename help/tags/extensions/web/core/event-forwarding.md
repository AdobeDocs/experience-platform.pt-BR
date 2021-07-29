---
title: Visão geral da extensão de encaminhamento de eventos principais
description: Saiba mais sobre a extensão de encaminhamento de eventos principais no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 92%

---

# Visão geral da extensão de encaminhamento de eventos principais

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A extensão de encaminhamento de evento principal fornece eventos, condições e tipos de dados padrão para o encaminhamento de eventos no Adobe Experience Platform.

Use essa referência para obter informações sobre as opções disponíveis ao usar esta extensão para criar uma regra.

## Tipos de condição de extensão principal

Esta seção descreve os tipos de condição disponíveis na extensão principal. Esses tipos de condição podem ser usados com o tipo de lógica regular ou de exceção.

### Custom Code

Especifique qualquer código personalizado que deve existir como uma condição do evento. Use o editor de código incorporado para inserir o código personalizado. O encaminhamento de eventos no Adobe Experience Platform é compatível com ES6.

1. Selecione **[!UICONTROL Abrir editor]**.
1. Digite o código personalizado.
1. Selecione **[!UICONTROL Salvar]**.

Para acessar o valor de um elemento de dados no código personalizado, use o método `getDataElementValue`. Por exemplo, para recuperar o valor de um elemento de dados chamado `productName`, escreva o seguinte: 

```javascript
getDataElementValue('productName') 
```

#### objeto ruleStash

Em seu código personalizado, você também pode usar o objeto `ruleStash`.

```javascript
arc.ruleStash: Object<string, *>`
```

```javascript
logger.log(context.arc.ruleStash);
```

`ruleStash` é um objeto que coleta todos os resultados dos módulos de ação.

Cada extensão tem seu próprio namespace. Por exemplo, se sua extensão tiver o nome `send-beacon`, todos os resultados das ações `send-beacon` serão armazenados no namespace `ruleStash['send-beacon']`.

O namespace é exclusivo para cada extensão e tem o valor `undefined` no início.

O namespace será substituído pelo resultado retornado de cada ação. Não se trata de mágica do namespace. Por exemplo, se você tiver uma extensão `transform` contendo duas ações: `generate-fullname` e `generate-fulladdress`, adicione as duas ações a uma regra.

Se o resultado da ação `generate-fullname` for `Firstname Lastname`, o stash da regra será exibido da seguinte forma depois que a ação for concluída:

```js
{
  transform: 'Firstname Lastname`
}
```

Se o resultado da ação `generate-address` for `3900 Adobe Way`, o stash da regra será exibido da seguinte forma depois que a ação for concluída:

```js
{
  transform: '3900 Adobe Way`
}
```

Observe que `Firstname Lastname` não existe mais no stash da regra. Isso ocorre porque a ação `generate-address` o substituiu pelo endereço.

Se quiser armazenar os resultados de ambas as ações no namespace `transform` no `ruleStash`, você poderá escrever seu módulo de ação como no seguinte exemplo:

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

Na primeira vez que essa ação é executada, `ruleStash` é `undefined` e é inicializada com um objeto vazio. Na próxima vez que a ação for executada, `ruleStash` será retornado pela ação quando ela tiver sido chamada anteriormente. Usar um objeto como `ruleStash` permite que você adicione novos dados sem perder dados previamente definidos por outras ações da extensão.

Nesse caso, é necessário ter cuidado para retornar sempre o stash da regra da extensão completa. Se você retornasse apenas um valor (por exemplo, 5), o stash da regra seria:

```js
{
  transform: 5
}
```

### Comparação de valores {#value-comparison}

Compara dois valores para determinar se essa condição retorna true.

Se você tiver uma regra com várias condições, é possível que essa condição retorne &quot;true&quot;, mas a regra ainda não será acionada, pois as outras condições foram avaliadas como &quot;false&quot; ou uma das exceções teve resultado &quot;true&quot;.

1. Forneça um valor.
1. Selecione o operador. Consulte a lista de operadores de comparação de valores abaixo para obter mais detalhes.
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



## Tipos de ação da extensão principal

Esta seção descreve os tipos de ação disponíveis na extensão principal.

### Código personalizado

Forneça o código que é executado depois que o evento é acionado e as condições são avaliadas. O encaminhamento de eventos no Adobe Experience Platform é compatível com ES6.

1. Dê um nome ao código da ação.
1. Selecione **[!UICONTROL Abrir editor]**.
1. Edite o código e selecione **[!UICONTROL Salvar]**.

Para acessar o valor de um elemento de dados no código personalizado, use o método `getDataElementValue`. Por exemplo, para recuperar o valor de um elemento de dados chamado `productName`, escreva o seguinte: 

```javascript
getDataElementValue('productName') 
```

As ações de encaminhamento de eventos são executadas sequencialmente. Também é possível que o código personalizado em uma ação retorne um valor que pode ser usado em uma ação subsequente. O valor retornado pode vir do código nessa ação ou do corpo da resposta de uma chamada feita a uma origem externa. Para referenciar dados de uma ação executada anteriormente em uma única regra em que a extensão Core é usada, crie um elemento de dados do tipo `Path` e use o seguinte caminho para fazer referência ao valor de uma variável chamada `productCategory` definida no código personalizado na extensão Core:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Tipos de elementos de dados da extensão principal

Os tipos de elementos de dados são determinados pela extensão. Não há limite para os tipos que podem ser criados.

As seções a seguir descrevem os tipos de elementos de dados disponíveis na extensão principal. Outras extensões usam outros tipos de elementos de dados.

### Custom code

JavaScript personalizado pode ser inserido na interface selecionando **[!UICONTROL Abrir editor]** e inserindo o código na janela do editor.

É preciso haver uma instrução de retorno na janela do editor para indicar qual valor deve ser usado como o valor do elemento de dados. Se uma declaração de retorno não for incluída ou o valor `null` ou `undefined` for retornado, o valor padrão do elemento de dados refletirá `null` ou `undefined`.

Para acessar o valor de um elemento de dados no código personalizado, use o método `getDataElementValue`. Por exemplo, para recuperar o valor de um elemento de dados chamado `productName`, escreva o seguinte: 

```javascript
getDataElementValue('productName') 
```

**Exemplo:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Path

Um caminho para um par de valor-chave em um evento enviado para o Adobe Experience Platform Edge Network pode ser referenciado usando o tipo de elemento de dados Caminho.

Para fazer referência ao objeto inteiro de um evento, digite `arc` como o caminho. O acrônimo `arc` significa Contexto de recursos da Adobe e é o caminho de nível superior para um evento enviado ao Adobe Experience Platform Edge Network.

Por exemplo, dada a chamada `interact` do cliente para o Edge Network, a seguinte solicitação é exibida no console do navegador:

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Para inserir um caminho que faça referência a `pageName`, insira o seguinte no campo de caminho:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>A chamada `interact` do cliente tem `events`, mas para o encaminhamento do evento é necessário `event`. Isso ocorre porque o encaminhamento de eventos inspeciona cada evento individualmente e não como um lote de vários eventos, como mostrado no cliente.
