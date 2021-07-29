---
title: Variável sem turbina
description: Saiba mais sobre o objeto turbine, uma variável gratuita que fornece informações e utilitários específicos para o tempo de execução da tag do Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 51%

---

# Variável sem turbina

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O objeto `turbine` é uma &quot;variável livre&quot; no escopo dos módulos de biblioteca da extensão. Ele fornece informações e utilitários específicos para o tempo de execução da tag do Adobe Experience Platform e está sempre disponível para módulos de biblioteca sem usar `require()`.

## [!DNL buildInfo]

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` é um objeto que contém informações de criação sobre a biblioteca de tempo de execução de tags atual.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z",
    environment: "development"
}
```

| Propriedade | Descrição |
| --- | --- |
| `turbineVersion` | A versão [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) usada dentro da biblioteca atual. |
| `turbineBuildDate` | A data da ISO 8601 quando a versão de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) usada no container foi criada. |
| `buildDate` | A data da ISO 8601 quando a biblioteca atual foi criada. |
| `environment` | O ambiente para o qual essa biblioteca foi criada. Os valores aceitos são `development`, `staging` e `production`. |


## [!DNL debugEnabled]

Se a depuração de tag está ativada no momento.

Se você está apenas tentando registrar mensagens, é improvável que precise usar isso. Em vez disso, sempre registre mensagens usando `turbine.logger` para garantir que suas mensagens só sejam impressas no console quando a depuração de tag estiver ativada.

### [!DNL getDataElementValue]

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Retorna o valor de um elemento de dados.

### [!DNL getExtensionSettings] {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Retorna o objeto de configurações salvo pela última vez na visualização de [configuração de extensão](./configuration.md).

Observe que os valores nas configurações retornadas podem ser provenientes de elementos de dados. Por isso, chamar `getExtensionSettings()` em momentos diferentes poderá gerar resultados diferentes se os valores dos elementos de dados tiverem sido alterados. Para obter os valores mais atualizados, aguarde o máximo possível antes de chamar `getExtensionSettings()`.

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

A propriedade [hostedLibFiles](./manifest.md) pode ser definida no manifesto da extensão para hospedar vários arquivos junto com a biblioteca de tempo de execução da tag. Este módulo retorna o URL no qual o arquivo de biblioteca especificado está hospedado.

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Recupera um módulo que foi compartilhado de outra extensão. Se nenhum módulo correspondente for encontrado, `undefined` será retornado. Consulte [Implementação de módulos compartilhados](./web/shared.md) para obter mais informações sobre módulos compartilhados.

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

O utilitário de registro é usado para registrar mensagens no console. As mensagens serão exibidas somente no console se a depuração for ativada pelo usuário. A maneira recomendada de ativar a depuração é usar o [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). Como alternativa, o usuário pode executar o seguinte comando `_satellite.setDebug(true)` dentro do console do desenvolvedor do navegador. O agente de log tem os seguintes métodos:

* `logger.log(message: string)`: registra uma mensagem no console.
* `logger.info(message: string)`: registra uma mensagem informativa no console.
* `logger.warn(message: string)`: registra uma mensagem de aviso no console.
* `logger.error(message: string)`: registra uma mensagem de erro no console.
* `logger.debug(message: string)`: registra uma mensagem de depuração no console. (Visível somente quando o registro `verbose` estiver ativado no console do navegador.)

### [!DNL onDebugChanged]

Passando uma função de retorno de chamada para `turbine.onDebugChanged`, as tags chamarão seu retorno de chamada sempre que a depuração for acionada. As tags passarão um booleano para a função de retorno de chamada que será verdadeira se a depuração tiver sido ativada ou falsa se a depuração tiver sido desativada.

Se você está apenas tentando registrar mensagens, é improvável que precise usar isso. Em vez disso, sempre registre mensagens usando `turbine.logger` e as tags garantirão que suas mensagens só sejam impressas no console quando a depuração de tag estiver ativada.

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Um objeto que contém as seguintes configurações definidas pelo usuário para a propriedade da biblioteca de tempo de execução de tags atual:

* `propertySettings.domains: Array<String>`

   Uma variedade de domínios que a propriedade abrange.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Os desenvolvedores de extensões não devem se preocupar com esse cenário.
