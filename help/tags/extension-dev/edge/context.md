---
title: Contexto em módulos de extensão de borda
description: Saiba mais sobre o objeto de contexto e a função que ele desempenha ao interagir com módulos de biblioteca nas extensões de tag das propriedades de borda.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 84%

---

# Contexto em módulos de extensão de borda

>[!NOTE]
>
> O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Todos os módulos de biblioteca em extensões de borda recebem um objeto `context` quando são executados. Este documento aborda as propriedades fornecidas pelo objeto `context` e a função que desempenham nos módulos de biblioteca.

## Contexto de solicitação da Adobe (arc)

A propriedade `arc` é um objeto que fornece informações sobre o evento que aciona a regra. As seções abaixo abrangem as várias subpropriedades contidas nesse objeto.

### [!DNL event]

O objeto `event` representa o evento que acionou a regra e contém os seguintes valores:

```js
logger.log(context.arc.event);
```

| Propriedade | Descrição |
| --- | --- |
| `xdm` | O objeto XDM do evento. |
| `data` | A camada de dados personalizada. |

### [!DNL request]

Para não ser confundido com uma solicitação do dispositivo cliente, `request` é um objeto ligeiramente modificado que vem da rede de borda da Adobe Experience Platform.

```js
logger.log(context.arc.request)
```

O objeto `request` tem duas propriedades de nível superior: `body` e `head`. A propriedade `body` contém informações do modelo de dados de experiência (XDM) e pode ser inspecionado no Adobe Experience Platform Debugger quando você navega até o **[!UICONTROL Launch]** e seleciona a guia **[!UICONTROL Traço de borda]**.

### [!DNL ruleStash] {#rulestash}

`ruleStash` é um objeto que coletará todos os resultados dos módulos de ação.

```js
logger.log(context.arc.ruleStash);
```

Cada extensão tem seu próprio namespace. Por exemplo, se a extensão tiver o nome `send-beacon`, todos os resultados das ações `send-beacon` serão armazenados no namespace `ruleStash['send-beacon']`.

O namespace é exclusivo para cada extensão e tem um valor de `undefined` no início.

O namespace é substituído pelo resultado retornado de cada ação. Por exemplo, considere uma extensão `transform` que contém duas ações: `generate-fullname` e `generate-fulladdress`. Essas duas ações são adicionadas a uma regra.

Se o resultado da ação `generate-fullname` for `Firstname Lastname`, o stash da regra será mostrado da seguinte maneira depois que a ação for concluída:

```js
{
  transform: 'Firstname Lastname'
}
```

Se o resultado da ação `generate-address` for `3900 Adobe Way`, o stash da regra será mostrado da seguinte maneira depois que a ação for concluída:

```js
{
  transform: '3900 Adobe Way'
}
```

Observe que &quot;Nome Sobrenome&quot; não existe mais no stash da regra, pois a ação `generate-address` o substituiu por um novo valor.

Se desejar que `ruleStash` armazene os resultados de ambas as ações no namespace `transform`, você poderá escrever seu módulo de ação como o seguinte exemplo:

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

Na primeira vez que essa ação é executada, `ruleStash` é iniciado como `undefined` e, portanto, inicializado como um objeto vazio. Na próxima vez em que a ação for executada, ela receberá `ruleStash` que foi retornado quando a ação foi chamada anteriormente. Usar um objeto como `ruleStash` permite que você adicione novos dados sem perder dados previamente definidos por outras ações de nossa extensão.

>[!NOTE]
>
>Tenha sempre cuidado para retornar o estash completo da regra de extensão ao usar essa estratégia. Se, em vez disso, você retornar apenas um valor, ele substituirá quaisquer outras propriedades que você tenha definido.

## Utilitários

A propriedade `utils` representa um objeto que fornece utilitários específicos para o tempo de execução da tag.

### [!DNL logger]

O utilitário `logger` permite registrar mensagens que serão exibidas durante as sessões de depuração ao usar o [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

O agente de log tem os seguintes métodos, em que `message` é a mensagem que você deseja registrar:

| Método | Descrição |
| --- | --- |
| `log(message)` | registra uma mensagem no console. |
| `info(message)` | registra uma mensagem informativa no console. |
| `warn(message)` | registra uma mensagem de aviso no console. |
| `error(message)` | registra uma mensagem de erro no console. |
| `debug(message)` | registra uma mensagem de depuração no console. Visível somente quando o registro `verbose` estiver ativado no console do navegador. |

### [!DNL fetch]

Esse utilitário implementa a [API Fetch](https://developer.mozilla.org/pt-BR/docs/Web/API/Fetch_API). Você pode usar a função para fazer solicitações a pontos de extremidade de terceiros.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Esse utilitário retorna um objeto contendo informações sobre a build da biblioteca de tempo de execução de tag atual.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

O objeto contém os seguintes valores:

| Propriedade | Descrição |
| --- | --- |
| `turbineVersion` | A versão [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) usada dentro da biblioteca atual. |
| `turbineBuildDate` | A data da ISO 8601 quando a versão de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) usada no container foi criada. |
| `buildDate` | A data da ISO 8601 quando a biblioteca atual foi criada. |
| `environment` | O ambiente para o qual essa biblioteca foi criada. Os valores possíveis incluem `development`, `staging` e `production.` |

Veja um exemplo de objeto `getBuildInfo` para demonstrar os valores retornados:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Esse utilitário retorna o último objeto `settings` salvo na visualização de [configuração de extensão](../configuration.md).

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Esse utilitário retorna o objeto `settings` que foi salvo pela última vez na visualização do módulo de biblioteca correspondente.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Esse utilitário retorna um objeto que contém informações sobre a regra que está acionando o módulo.

```js
logger.log(context.utils.getRule());
```

O objeto conterá os seguintes valores:

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID da regra. |
| `name` | O nome da regra. |
