---
title: Variável sem turbina
description: Saiba mais sobre o objeto turbine, uma variável livre que fornece informações e utilitários específicos para o tempo de execução de tag da Adobe Experience Platform.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 27dd38cc509040ea9dc40fc7030dcdec9a182d55
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 86%

---

# Variável sem turbina

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O objeto `turbine` é uma &quot;variável livre&quot; no escopo dos módulos de biblioteca da extensão. Ela fornece informações e utilitários específicos para o tempo de execução de tag da Adobe Experience Platform e está sempre disponível para módulos de biblioteca sem usar `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` é um objeto que contém informações de build sobre a biblioteca de tempo de execução da tag atual.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Propriedade | Descrição |
| --- | --- |
| `turbineVersion` | A versão [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) usada dentro da biblioteca atual. |
| `turbineBuildDate` | A data da ISO 8601 quando a versão de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) usada no container foi criada. |
| `buildDate` | A data da ISO 8601 quando a biblioteca atual foi criada. |

{style=&quot;table-layout:auto&quot;}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` é um objeto que contém informações sobre o ambiente no qual a biblioteca é implantada.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do ambiente. |
| `stage` | O ambiente para o qual essa biblioteca foi criada. Os valores possíveis são `development`, `staging` e `production`. |

{style=&quot;table-layout:auto&quot;}

## `debugEnabled`

Um valor booleano indicando se a depuração de tag está atualmente ativada.

Se você está apenas tentando registrar mensagens, é improvável que precise usar isso. Em vez disso, sempre registre mensagens usando `turbine.logger` para garantir que as mensagens só sejam impressas no console quando a depuração de tag estiver habilitada.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Retorna o valor de um elemento de dados.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Retorna o objeto de configurações salvo pela última vez na visualização de [configuração de extensão](./configuration.md).

Observe que os valores nas configurações retornadas podem ser provenientes de elementos de dados. Por isso, chamar `getExtensionSettings()` em momentos diferentes poderá gerar resultados diferentes se os valores dos elementos de dados tiverem sido alterados. Para obter os valores mais atualizados, aguarde o máximo possível antes de chamar `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

A propriedade [hostedLibFiles](./manifest.md) pode ser definida no manifesto da extensão para hospedar vários arquivos junto com a biblioteca de tempo de execução da tag. Este módulo retorna o URL no qual o arquivo de biblioteca especificado está hospedado.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Recupera um módulo que foi compartilhado de outra extensão. Se nenhum módulo correspondente for encontrado, `undefined` será retornado. Consulte [Implementação de módulos compartilhados](./web/shared.md) para obter mais informações sobre módulos compartilhados.

## `logger`

```js
turbine.logger.error('Error!');
```

O utilitário de registro é usado para registrar mensagens no console. As mensagens serão exibidas somente no console se a depuração for ativada pelo usuário. A maneira recomendada de ativar a depuração é usar o [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). Como alternativa, o usuário pode executar o comando a seguir `_satellite.setDebug(true)` no console de desenvolvimento do navegador. O agente de log tem os seguintes métodos:

* `logger.log(message: string)`: registra uma mensagem no console.
* `logger.info(message: string)`: registra uma mensagem informativa no console.
* `logger.warn(message: string)`: registra uma mensagem de aviso no console.
* `logger.error(message: string)`: registra uma mensagem de erro no console.
* `logger.debug(message: string)`: registra uma mensagem de depuração no console. (Visível somente quando o registro `verbose` estiver ativado no console do navegador.)
* `logger.deprecation(message: string)`: Registra uma mensagem de aviso no console independentemente de a depuração de tag estar ou não habilitada pelo usuário.

## `onDebugChanged`

Se for passada uma função de retorno de chamada para `turbine.onDebugChanged`, as tags chamarão seu retorno de chamada sempre que a depuração for alternada. As tags passarão um valor booliano para a função de retorno de chamada, que será verdadeira se a depuração estiver ativada ou falsa se a depuração estiver desativada.

Se você está apenas tentando registrar mensagens, é improvável que precise usar isso. Em vez disso, sempre registre mensagens usando `turbine.logger`, e as tags garantirão que suas mensagens só sejam impressas no console quando a depuração de tag estiver habilitada.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Um objeto que contém as seguintes configurações definidas pelo usuário para a propriedade da biblioteca de tempo de execução de tags atual:

* `propertySettings.domains: Array<String>`

   Uma variedade de domínios que a propriedade abrange.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Os desenvolvedores de extensões não devem se preocupar com esse cenário.
