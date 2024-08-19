---
title: contexto
description: Colete automaticamente dados de dispositivo, ambiente ou local.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 7%

---

# `context`

A propriedade `context` é uma matriz de cadeias de caracteres que determina o que o SDK da Web pode coletar automaticamente. Embora esses dados possam fornecer grande valor, a omissão de alguns deles pode ser benéfica para que você possa cumprir a política de privacidade da sua organização.

## Palavras-chave de contexto e elementos XDM

Se você incluir determinada palavra-chave de contexto, o SDK da Web preencherá automaticamente todos os elementos XDM associados. Se você quiser omitir um elemento XDM específico enquanto permite outros, limpe os valores usando [`onBeforeEventSend`](onbeforeeventsend.md). Se você enviar vários eventos em uma página, o SDK da Web incluirá esses campos em cada chamada do `SendEvent`.

### Web

A palavra-chave `"web"` coleta informações sobre a página atual.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| URL da página | O URL da página atual. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL do referenciador | O URL da página visitada anteriormente. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Dispositivo

A palavra-chave `"device"` coleta informações sobre o dispositivo do usuário.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Altura da tela | A altura da tela em pixels. | `xdm.device.screenHeight` | `900` |
| Largura da tela | A largura da tela em pixels. | `xdm.device.screenWidth` | `1440` |
| Orientação da tela | A orientação da tela. | `xdm.device.screenOrientation` | `landscape` ou `portrait` |

{style="table-layout:auto"}

### Ambiente

A palavra-chave `"environment"` coleta informações sobre o navegador do usuário.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Tipo de ambiente | O tipo de ambiente pelo qual a experiência surgiu. O SDK da Web sempre define esse campo como `browser`. | `xdm.environment.type` | `browser` |
| Altura da janela de visualização | A altura da área de conteúdo do navegador em pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Largura da janela de visualização | A largura da área de conteúdo do navegador em pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contexto de lugar

A palavra-chave `"placeContext"` coleta informações sobre a localização do usuário.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Hora local | Carimbo de data/hora local do usuário final no formato simplificado estendido [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Deslocamento de fuso horário local | O número de minutos em que o usuário está deslocado do GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Código do país | O código do país do usuário final. | `xdm.placeContext.geo.countryCode` | `US` |
| Província do estado | O código de província de estado do usuário final. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Latitude | A latitude da localização do usuário final. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Longitude | A longitude da localização do usuário final. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### Carimbo de data e hora

A palavra-chave `timestamp` coleta informações sobre o carimbo de data/hora do evento. Esta parte do contexto não pode ser removida.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Carimbo de data e hora do evento | Carimbo de data/hora UTC do usuário final no formato simplificado estendido [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### Detalhes de implementação

A palavra-chave `implementationDetails` coleta informações sobre a versão do SDK usada para coletar o evento.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Nome | O identificador do kit de desenvolvimento de software (SDK). Este campo usa um URI para melhorar a exclusividade entre os identificadores fornecidos por diferentes bibliotecas de software. | `xdm.implementationDetails.name` | Quando a biblioteca independente é usada, o valor é `https://ns.adobe.com/experience/alloy`. Quando a biblioteca é usada como parte da extensão de tag, o valor é `https://ns.adobe.com/experience/alloy+reactor`. |
| Versão | A versão do kit de desenvolvimento de software (SDK). | `xdm.implementationDetails.version` | Quando a biblioteca independente é usada, o valor é a versão da biblioteca. Quando a biblioteca é usada como parte da extensão de tag, o valor é a versão da biblioteca e a versão da extensão de tag unida com um `+`. Por exemplo, se a versão da biblioteca for `2.1.0` e a versão da extensão de tag for `2.1.3`, o valor será `2.1.0+2.1.3`. |
| Ambiente | O ambiente onde os dados foram coletados. Isto é sempre configurado para `browser`. | `xdm.implementationDetails.environment` | `browser` |


### Dicas do cliente de alta entropia {#high-entropy-client-hints}

>[!TIP]
>
>Consulte a documentação em [user agent client hints](../../use-cases/client-hints.md) para obter informações detalhadas sobre como configurá-las.

A palavra-chave `"highEntropyUserAgentHints"` coleta informações detalhadas sobre o dispositivo do usuário. Esses dados são incluídos no cabeçalho HTTP da solicitação enviada para o Adobe. Depois que os dados chegam à rede do Edge, o objeto XDM preenche seu respectivo caminho XDM. Se você definir o respectivo caminho XDM na chamada do `sendEvent`, ele terá prioridade sobre o valor do cabeçalho HTTP.

Se você usar pesquisas de dispositivo ao [configurar sua sequência de dados](/help/datastreams/configure.md), os dados poderão ser apagados em favor dos valores de pesquisa do dispositivo. Alguns campos de dica do cliente e de pesquisa de dispositivo não podem existir na mesma ocorrência.

| Propriedade | Descrição | Cabeçalho HTTP | Caminho XDM | Exemplo |
| --- | --- | --- | --- | --- |
| Versão do sistema operacional | A versão do sistema operacional. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Arquitetura | A arquitetura subjacente da CPU. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Modelo do dispositivo | O nome do dispositivo usado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Bitness | O número de bits que a arquitetura subjacente da CPU suporta. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Fornecedor do navegador | A empresa que criou o navegador. A dica de baixa entropia `Sec-CH-UA` também coleta esse elemento. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Nome do navegador | O navegador usado. A dica de baixa entropia `Sec-CH-UA` também coleta esse elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Versão do navegador | A versão significativa do navegador. A dica de baixa entropia `Sec-CH-UA` também coleta esse elemento. A versão exata do navegador não é coletada automaticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

{style="table-layout:auto"}

## Coletar informações de contexto usando a extensão de tag do SDK da Web

A configuração de informações de contexto é uma combinação de botões de opção e caixas de seleção ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Cada caixa de seleção mapeia para uma palavra-chave de contexto.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Coleta de Dados] e selecione **[!UICONTROL Todas as informações de contexto padrão]** ou **[!UICONTROL Informações de contexto específicas]**.
1. Se você selecionar **[!UICONTROL Informações de contexto específicas]**, marque a caixa de seleção ao lado de cada elemento de informações de contexto desejado.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Coletar informações de contexto usando a biblioteca JavaScript do SDK da Web

Defina a matriz de cadeias de caracteres `context` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK, todas as informações de contexto, exceto `"highEntropyUserAgentHints"`, serão coletadas por padrão. Defina essa propriedade se quiser coletar dicas de cliente de alta entropia ou se quiser omitir outras informações de contexto da coleta de dados. As cadeias de caracteres podem ser incluídas em qualquer ordem.

>[!NOTE]
>
>Para coletar todas as informações de contexto, incluindo dicas de cliente de alta entropia, você deve incluir cada valor na cadeia de caracteres da matriz `context`. O valor padrão `context` omite `highEntropyUserAgentHints` e, se você definir a propriedade `context`, quaisquer valores omitidos não coletarão dados.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
