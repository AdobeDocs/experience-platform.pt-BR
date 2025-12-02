---
title: Monitoramento de ganchos do Adobe Experience Platform Web SDK
description: Saiba como usar os ganchos de monitoramento fornecidos pelo Adobe Experience Platform Web SDK para depurar sua implementação e capturar logs do Web SDK.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 9b2ecedfafbafed042eba73a034cb9b9e95af579
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# Monitorar ganchos do Web SDK

O Adobe Experience Platform Web SDK inclui ganchos de monitoramento que podem ser usados para monitorar vários eventos do sistema. Essas ferramentas são úteis para desenvolver suas próprias ferramentas de depuração e capturar logs do Web SDK.

O Web SDK aciona as funções de monitoramento independentemente de você ter ativado a [depuração](commands/configure/debugenabled.md).

## `onInstanceCreated` {#onInstanceCreated}

Essa função de retorno de chamada é disparada quando você cria com êxito uma nova instância do Web SDK. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.instance` | Função | A função da instância usada para chamar comandos do Web SDK. |

## `onInstanceConfigured` {#onInstanceConfigured}

Esta função de retorno de chamada é disparada pelo Web SDK quando o comando [`configure`](commands/configure/overview.md) é resolvido com êxito. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.config` | Objeto | Um objeto que contém a configuração usada para a instância do Web SDK. Estas são as opções passadas para o comando [`configure`](commands/configure/overview.md) com todos os valores padrão adicionados. |

## `onBeforeCommand` {#onBeforeCommand}

Essa função de retorno de chamada é acionada pelo Web SDK antes da execução de qualquer outro comando. Você pode usar essa função para recuperar as opções de configuração de um comando específico. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.commandName` | String | O nome do comando do Web SDK antes do qual essa função é executada. |
| `data.options` | Objeto | Um objeto que contém as opções transmitidas ao comando do Web SDK. |

## `onCommandResolved` {#onCommandResolved}

Essa função de retorno de chamada é acionada ao resolver promessas de comando. Você pode usar essa função para ver as opções de comando e o resultado. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.commandName` | String | O nome do comando executado do Web SDK. |
| `data.options` | Objeto | Um objeto que contém as opções transmitidas ao comando do Web SDK. |
| `data.result` | Objeto | Um objeto que contém o resultado do comando Web SDK. |

## `onCommandRejected` {#onCommandRejected}

Essa função de retorno de chamada é acionada antes da rejeição de uma promessa de comando e contém informações sobre o motivo da rejeição do comando. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.commandName` | String | O nome do comando executado do Web SDK. |
| `data.options` | Objeto | Um objeto que contém as opções transmitidas ao comando do Web SDK. |
| `data.error` | Objeto | Um objeto contendo a mensagem de erro retornada da chamada de rede do navegador (`fetch` na maioria dos casos), juntamente com o motivo pelo qual o comando foi rejeitado. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Essa função de retorno de chamada é disparada antes da execução de uma solicitação de rede. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.requestId` | String | O `requestId` gerado pelo Web SDK para habilitar a depuração. |
| `data.url` | String | O URL solicitado. |
| `data.payload` | Objeto | O objeto de carga de solicitação de rede que será convertido no formato JSON e enviado no corpo da solicitação, por meio de um método `POST`. |

## `onNetworkResponse` {#onNetworkResponse}

Essa função de retorno de chamada é acionada quando o navegador recebe uma resposta. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.requestId` | String | O `requestId` gerado pelo Web SDK para habilitar a depuração. |
| `data.url` | String | O URL solicitado. |
| `data.payload` | Objeto | O objeto de carga que será convertido no formato JSON e enviado no corpo da solicitação, por meio de um método `POST`. |
| `data.body` | String | O corpo da resposta no formato de string. |
| `data.parsedBody` | Objeto | Um objeto que contém o corpo da resposta analisada. Se ocorrer um erro ao analisar o corpo da resposta, esse parâmetro será indefinido. |
| `data.status` | String | O código de resposta em formato inteiro. |
| `data.retriesAttempted` | Número inteiro | O número de tentativas ao enviar a solicitação. Zero significa que a solicitação foi bem-sucedida na primeira tentativa. |

## `onNetworkError` {#onNetworkError}

Essa função de retorno de chamada é disparada quando a solicitação de rede falha. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.requestId` | String | O `requestId` gerado pelo Web SDK para habilitar a depuração. |
| `data.url` | String | O URL solicitado. |
| `data.payload` | Objeto | O objeto de carga que será convertido no formato JSON e enviado no corpo da solicitação, por meio de um método `POST`. |
| `data.error` | Objeto | Um objeto contendo a mensagem de erro retornada da chamada de rede do navegador (`fetch` na maioria dos casos), juntamente com o motivo pelo qual o comando foi rejeitado. |

## `onBeforeLog` {#onBeforeLog}

Essa função de retorno de chamada é acionada antes que o Web SDK registre qualquer item no console. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.componentName` | String | O nome do componente que gerou a mensagem de log. |
| `data.level` | String | O nível de log. Níveis com suporte: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Matriz de string | Os argumentos da mensagem de log. |


## `onContentRendering` {#onContentRendering}

Esta função de retorno de chamada é disparada pelo componente `personalization` em vários estágios de renderização. A carga pode diferir, dependendo do parâmetro `status`. Consulte a amostra abaixo para obter detalhes sobre os parâmetros da função.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.componentName` | String | O nome do componente que gerou a mensagem de log. |
| `data.payload` | Objeto | O objeto de carga que será convertido no formato JSON e enviado no corpo da solicitação, por meio de um método `POST`. |
| `data.status` | String | O componente `personalization` notifica o Web SDK sobre o status da renderização.  Valores compatíveis: <ul><li>`rendering-started`: indica que o Web SDK está prestes a renderizar apresentações. Antes que o Web SDK comece a renderizar um escopo de decisão ou uma exibição, no objeto `data` você pode ver as propostas que serão renderizadas pelo componente `personalization` e o nome do escopo.</li><li>`no-offers`: indica que nenhuma carga foi recebida para os parâmetros solicitados.</li> <li>`rendering-failed`: indica que o Web SDK falhou ao renderizar uma proposta.</li><li>`rendering-succeeded`: indica que a renderização foi concluída para um escopo de decisão.</li> <li>`rendering-redirect`: indica que o Web SDK renderizará uma apresentação de redirecionamento.</li></ul> |

## `onContentHiding` {#onContentHiding}

Essa função de retorno de chamada é acionada quando um estilo pré-ocultação é aplicado ou removido.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|----------|
| `data.instanceName` | String | O nome da variável global onde a instância do Web SDK está armazenada. |
| `data.componentName` | String | O nome do componente que gerou a mensagem de log. |
| `data.status` | String | O componente `personalization` notifica o Web SDK sobre o status da renderização. Valores compatíveis: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Como especificar ganchos de monitoramento ao usar o pacote NPM {#specify-monitoring-npm}

Se você estiver usando o Web SDK por meio do [pacote NPM](install/npm.md), poderá especificar ganchos de monitoramento na função `createInstance`, conforme mostrado abaixo.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Exemplo {#example}

O Web SDK procura uma matriz de objetos em uma variável global chamada `__alloyMonitors`.

Para capturar todos os eventos do Web SDK, você deve definir os ganchos de monitoramento antes que o código do Web SDK seja carregado na página. Cada método de monitoramento captura um evento do Web SDK.

Você pode definir trechos de monitoramento *após* o carregamento de código do Web SDK na sua página, mas todos os trechos que foram acionados antes do carregamento da página *não* serão capturados.

Ao definir seu objeto de gancho de monitoramento, você só precisa definir os métodos para os quais deseja definir uma lógica especial.
Por exemplo, se você só se importa com `onContentRendering`, pode apenas definir esse método. Não é necessário usar todos os ganchos de monitoramento de uma só vez.

Você pode definir vários objetos de gancho de monitoramento. Todos os objetos com o método fornecido serão chamados quando o evento correspondente for acionado.

>[!TIP]
>
>Veja abaixo um exemplo de página com todos os ganchos de monitoramento implementados.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
