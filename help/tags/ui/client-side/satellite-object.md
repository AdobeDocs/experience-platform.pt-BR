---
title: Referência a Objeto Satélite
description: Saiba mais sobre o objeto _satellite do lado do cliente e as várias funções que você pode executar com ele em tags.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 814f853d16219021d9151458d93fc5bdc6c860fb
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 83%

---

# Referência a objeto do satélite

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Este documento serve como referência para o objeto `_satellite` do lado do cliente e as várias funções que você pode executar com ele.

## `track`

**Código**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Exemplo**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` aciona todas as regras usando o tipo de evento Chamada direta que foi configurado com o identificador especificado na extensão de tag principal. O exemplo acima aciona todas as regras usando um tipo de evento Chamada direta em que o identificador configurado é `contact_submit`. Um objeto opcional contendo informações relacionadas também é transmitido. O objeto detalhado pode ser acessado digitando `%event.detail%` em um campo de texto em uma condição ou ação ou `event.detail` dentro do editor de códigos em uma condição ou ação de código personalizado.

## `getVar`

**Código**

```javascript
_satellite.getVar(name: string) => *
```

**Exemplo**

```javascript
var product = _satellite.getVar('product');
```

No exemplo fornecido, se um elemento de dados existir com um nome correspondente, o valor do elemento de dados será retornado. Se não houver nenhum elemento de dados correspondente, ele verificará se uma variável personalizada com um nome correspondente foi definida anteriormente usando o `_satellite.setVar()`. Se uma variável personalizada correspondente for encontrada, seu valor será retornado.

Observe que, em muitos campos de formulário na interface da Coleção de dados, é possível usar a sintaxe `%%` para fazer referência a variáveis, reduzindo a necessidade de chamadas a `_satellite.getVar()`. Por exemplo, usar %product% acessará o valor do elemento de dados do produto ou a variável personalizada.

## `setVar`

**Código**

```javascript
_satellite.setVar(name: string, value: *)
```

**Exemplo**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` define uma variável personalizada com determinado nome e valor. O valor da variável pode ser acessado posteriormente usando `_satellite.getVar()`.

Como opção, é possível definir várias variáveis de uma vez transmitindo um objeto em que as chaves são nomes de variáveis e os valores são os respectivos valores de variáveis.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Código**

```javascript
_satellite.getVisitorId() => Object
```

**Exemplo**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Se a extensão [!DNL Adobe Experience Cloud ID] for instalada na propriedade, esse método retornará a instância da ID de visitante. Consulte a [documentação do Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR) para obter mais informações.

## `logger`

**Código**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Exemplo**

```javascript
_satellite.logger.error('No product ID found.');
```

O objeto `logger` permite que uma mensagem seja registrada no console do navegador. A mensagem será exibida somente se a depuração de tag for habilitada pelo usuário (chamando `_satellite.setDebug(true)` ou usando uma extensão apropriada no navegador).

### Registro de avisos de descontinuação

```javascript
_satellite.logger.deprecation(message: string)
```

**Exemplo**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Isso registra um aviso no console do navegador. A mensagem é exibida independentemente de a depuração da tag ser ou não ativada pelo usuário.

## `cookie` {#cookie}

`_satellite.cookie` contém funções para ler e gravar cookies. Essa é uma cópia exposta do js-cookie de biblioteca de terceiros. Para obter detalhes sobre o uso mais avançado desta biblioteca, consulte a [documentação do cookie js](https://www.npmjs.com/package/js-cookie#basic-usage).

### Definir um cookie {#cookie-set}

Para definir um cookie, use `_satellite.cookie.set()`.

**Código**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>No método antigo [`setCookie`](#setCookie) de configuração de cookies, o terceiro argumento (opcional) para essa chamada de função era um número inteiro que indicava o TTL (time-to-live) do cookie em dias. Nesse novo método, um objeto &quot;attributes&quot; é aceito como um terceiro argumento. Para definir um TTL para um cookie usando o novo método, você deve fornecer uma propriedade `expires` no objeto attributes e defini-la com o valor desejado. Isso é demonstrado no exemplo abaixo.

**Exemplo**

A chamada de função a seguir grava um cookie que expira em uma semana.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Recuperar um cookie {#cookie-get}

Para recuperar um cookie, use `_satellite.cookie.get()`.

**Código**

```javascript
_satellite.cookie.get(name: string) => string
```

**Exemplo**

A chamada de função a seguir lê um cookie definido anteriormente.

```javascript
var product = _satellite.cookie.get('product');
```

### Remover um cookie {#cookie-remove}

Para remover um cookie, use `_satellite.cookie.remove()`.

**Código**

```javascript
_satellite.cookie.remove(name: string)
```

**Exemplo**

A chamada de função a seguir remove um cookie definido anteriormente.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Código**

```javascript
_satellite.buildInfo
```

Esse objeto contém informações sobre o build da biblioteca de tempo de execução de tag atual. O objeto contém as seguintes propriedades:

### `turbineVersion`

Isso fornece a versão [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) usada na biblioteca atual.

### `turbineBuildDate`

A data da ISO 8601 quando a versão de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) usada no container foi criada.

### `buildDate`

A data da ISO 8601 quando a biblioteca atual foi criada.

Este exemplo demonstra os valores do objeto:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Esse objeto contém informações sobre o ambiente em que a biblioteca de tempo de execução de tags atual está implantada.

**Código**

```javascript
_satellite.environment
```

O objeto contém as seguintes propriedades:

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do ambiente. |
| `stage` | O ambiente para o qual essa biblioteca foi criada. Os valores possíveis são `development`, `staging` e `production`. |

## `notify`

>[!NOTE]
>
>Esse método foi substituído. Em vez disso, use `_satellite.logger.log()`.

**Código**

```javascript
_satellite.notify(message: string[, level: number])
```

**Exemplo**

```javascript
_satellite.notify('Hello world!');
```

`notify` registra uma mensagem no console do navegador. A mensagem será exibida somente se a depuração de tag for habilitada pelo usuário (chamando `_satellite.setDebug(true)` ou usando uma extensão de navegador apropriada).

Um nível de registro opcional poderá ser passado, o que afetará o estilo e a filtragem da mensagem que está sendo registrada. Os níveis suportados são os seguintes:

3 - Mensagens informativas.

4 - Mensagens de aviso.

5 - Mensagens de erro.

Se você não fornecer um nível de registro ou passar qualquer outro valor de nível, a mensagem será registrada como uma mensagem regular.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Esse método foi substituído. Em vez disso, use [`_satellite.cookie.set()`](#cookie-set).

**Código**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Exemplo**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Isso define um cookie no navegador do usuário. O cookie persistirá pelo número de dias especificados.

## `readCookie`

>[!IMPORTANT]
>
>Esse método foi substituído. Em vez disso, use [`_satellite.cookie.get()`](#cookie-get).

**Código**

```javascript
_satellite.readCookie(name: string) => string
```

**Exemplo**

```javascript
var product = _satellite.readCookie('product');
```

Isso lê um cookie do navegador do usuário.

## `removeCookie`

>[!NOTE]
>
>Esse método foi substituído. Em vez disso, use [`_satellite.cookie.remove()`](#cookie-remove).

**Código**

```javascript
_satellite.removeCookie(name: string)
```

**Exemplo**

```javascript
_satellite.removeCookie('product');
```

Isso remove um cookie do navegador do usuário.

## Funções de depuração

As funções a seguir não devem ser acessadas do código de produção. Elas são destinados apenas à depuração e serão alteradas ao longo do tempo, conforme necessário.

### `container`

**Código**

```javascript
_satellite._container
```

**Exemplo**

>[!IMPORTANT]
>
>Essa função não deve ser acessada do código de produção. Ela é destinada apenas à depuração e será alterada ao longo do tempo, conforme necessário.

### `monitor`

**Código**

```javascript
_satellite._monitors
```

**Exemplo**

>[!IMPORTANT]
>
>Essa função não deve ser acessada do código de produção. Ela é destinada apenas à depuração e será alterada ao longo do tempo, conforme necessário.

**Amostra**

Na página da Web que está executando uma biblioteca de tags, adicione um trecho de código ao HTML. Normalmente, o código é inserido no elemento `<head>` antes do elemento `<script>` que carrega a biblioteca de tags. Isso permite que o monitor capture os primeiros eventos do sistema que ocorrerem na biblioteca de tags. Por exemplo:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

No elemento do primeiro script, como a biblioteca de tags ainda não foi carregada, o objeto `_satellite` é criado e uma matriz é inicializada em `_satellite._monitors`. O script então adiciona um objeto de monitor a essa matriz. O objeto do monitor pode especificar os seguintes métodos que serão chamados posteriormente pela biblioteca de tags:

### `ruleTriggered`

Essa função é chamada depois que um evento aciona uma regra, mas antes de as condições e ações da regra terem sido processadas. O objeto do evento transmitido para `ruleTriggered` contém informações sobre a regra que foi acionada.

### `ruleCompleted`

Essa função é chamada depois que uma regra é totalmente processada. Em outras palavras, o evento ocorreu, todas as condições foram passadas e todas as ações foram executadas. O objeto do evento passado para `ruleCompleted` contém informações sobre a regra que foi concluída.

### `ruleConditionFailed`

Essa função é chamada depois que uma regra é acionada e uma de suas condições falha. O objeto do evento transmitido para `ruleConditionFailed` contém informações sobre a regra que foi acionada e a condição que falhou.

Se `ruleTriggered` for chamado, `ruleCompleted` ou `ruleConditionFailed` será chamado logo depois disso.

>[!NOTE]
>
>Um monitor não precisa especificar todos os três métodos (`ruleTriggered`, `ruleCompleted` e `ruleConditionFailed`). As tags no Adobe Experience Platform funcionam com quaisquer métodos compatíveis que o monitor tenha fornecido.

### Teste do monitor

O exemplo acima especifica todos os três métodos no monitor. Quando são chamados, o monitor faz logout de informações relevantes. Para testar isso, configure duas regras na biblioteca de tags:

1. Uma regra com um evento de clique e uma condição do navegador que é transmitida somente se o navegador for [!DNL Chrome].
1. Uma regra com um evento de clique e uma condição do navegador que é transmitida somente se o navegador for [!DNL Firefox].

Se você abrir a página em [!DNL Chrome], abrir o console do navegador e selecionar a página, você verá o seguinte no console:

![](../../images/debug.png)

É possível adicionar trechos ou informações suplementares a esses manipuladores, conforme necessário.
