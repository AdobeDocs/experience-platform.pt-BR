---
title: contexto
description: Colete automaticamente dados de dispositivo, ambiente ou local.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: dc2a2ecf7b602d2fcfd3b6c93cecdb6f3368a3f9
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 5%

---

# `context`

A variável `context` é uma matriz de strings que determina o que o SDK da Web pode coletar automaticamente. Embora esses dados possam fornecer grande valor, a omissão de alguns deles pode ser benéfica para que você possa cumprir a política de privacidade da sua organização.

## Palavras-chave de contexto e elementos XDM

Se você incluir determinada palavra-chave de contexto, o SDK da Web preencherá automaticamente todos os elementos XDM associados. Se quiser omitir um elemento XDM específico e permitir que outros elementos, você poderá apagar os valores usando [`onBeforeEventSend`](onbeforeeventsend.md). Se você enviar vários eventos em uma página, o SDK da Web incluirá esses campos em cada `SendEvent` chame.

### Web

A variável `"web"` A palavra-chave coleta informações sobre a página atual.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| URL da página | O URL da página atual. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL do referenciador | O URL da página visitada anteriormente. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Dispositivo

A variável `"device"` A palavra-chave coleta informações sobre o dispositivo do usuário.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Altura da tela | A altura da tela em pixels. | `xdm.device.screenHeight` | `900` |
| Largura da tela | A largura da tela em pixels. | `xdm.device.screenWidth` | `1440` |
| Orientação da tela | A orientação da tela. | `xdm.device.screenOrientation` | `landscape` ou `portrait` |

{style="table-layout:auto"}

### Ambiente

A variável `"environment"` A palavra-chave coleta informações sobre o navegador do usuário.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Tipo de ambiente | O tipo de ambiente pelo qual a experiência surgiu. O SDK da Web sempre define esse campo como `browser`. | `xdm.environment.type` | `browser` |
| Altura da janela de visualização | A altura da área de conteúdo do navegador em pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Largura da janela de visualização | A largura da área de conteúdo do navegador em pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contexto do local

A variável `"placeContext"` A palavra-chave coleta informações sobre a localização do usuário.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Hora local | Carimbo de data e hora local para o usuário final em formato simplificado e estendido [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) formato. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Deslocamento de fuso horário local | O número de minutos em que o usuário está deslocado do GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Código do país | O código do país do usuário final. | `xdm.placeContext.geo.countryCode` | `US` |
| Província do estado | O código de província de estado do usuário final. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Latitude | A latitude da localização do usuário final. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Longitude | A longitude da localização do usuário final. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### Carimbo de data e hora

A variável `timestamp` A palavra-chave coleta informações sobre o carimbo de data e hora do evento. Esta parte do contexto não pode ser removida.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Carimbo de data e hora do evento | Carimbo de data e hora UTC do usuário final em formato simplificado e estendido [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) formato. | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### Detalhes da implementação

A variável `implementationDetails` A palavra-chave coleta informações sobre a versão do SDK usada para coletar o evento.

| Dimensão | Descrição | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- |
| Nome | O identificador do kit de desenvolvimento de software (SDK). Este campo usa um URI para melhorar a exclusividade entre os identificadores fornecidos por diferentes bibliotecas de software. | `xdm.implementationDetails.name` | Quando a biblioteca independente é usada, o valor é `https://ns.adobe.com/experience/alloy`. Quando a biblioteca é usada como parte da extensão de tag, o valor é `https://ns.adobe.com/experience/alloy+reactor`. |
| Versão | A versão do kit de desenvolvimento de software (SDK). | `xdm.implementationDetails.version` | Quando a biblioteca independente é usada, o valor é a versão da biblioteca. Quando a biblioteca é usada como parte da extensão de tag, o valor é a versão da biblioteca e a versão da extensão de tag unida com um `+`. Por exemplo, se a versão da biblioteca for `2.1.0` e a versão da extensão de tag for `2.1.3`, o valor seria `2.1.0+2.1.3`. |
| Ambiente | O ambiente onde os dados foram coletados. Sempre definida como `browser`. | `xdm.implementationDetails.environment` | `browser` |


### Dicas do cliente de alta entropia

A variável `"highEntropyUserAgentHints"` A palavra-chave coleta informações detalhadas sobre o dispositivo do usuário. Esses dados são incluídos no cabeçalho HTTP da solicitação enviada para o Adobe. Depois que os dados chegam à rede de borda, o objeto XDM preenche seu respectivo caminho XDM. Se você definir o respectivo caminho XDM na sua `sendEvent` chamada, tem prioridade sobre o valor do cabeçalho HTTP.

Se você usar pesquisas de dispositivo quando [configuração do seu fluxo de dados](/help/datastreams/configure.md), os dados podem ser apagados em favor dos valores de pesquisa do dispositivo. Alguns campos de dica do cliente e de pesquisa de dispositivo não podem existir na mesma ocorrência.

| Dimensão | Descrição | Cabeçalho HTTP | Caminho XDM | Exemplo de valor |
| --- | --- | --- | --- | --- |
| Versão do sistema operacional | A versão do sistema operacional. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Arquitetura | A arquitetura subjacente da CPU. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Modelo do dispositivo | O nome do dispositivo usado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Bitness | O número de bits que a arquitetura subjacente da CPU suporta. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Fornecedor do navegador | A empresa que criou o navegador. A dica de baixa entropia `Sec-CH-UA` O também coleta esse elemento. | `Sec-CH-UA-Full-Version-List` | | |
| Nome do navegador | O navegador usado. A dica de baixa entropia `Sec-CH-UA` O também coleta esse elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Versão do navegador | A versão significativa do navegador. A dica de baixa entropia `Sec-CH-UA` O também coleta esse elemento. A versão exata do navegador não é coletada automaticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Coletar informações de contexto usando a extensão de tag do SDK da Web

A configuração de informações de contexto é uma combinação de botões de opção e caixas de seleção quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Cada caixa de seleção mapeia para uma palavra-chave de contexto.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e selecione **[!UICONTROL Todas as informações de contexto padrão]** ou **[!UICONTROL Informações de contexto específicas]**.
1. Se você selecionar **[!UICONTROL Informações de contexto específicas]**, ative a caixa de seleção ao lado de cada elemento de informações de contexto desejado.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Coletar informações de contexto usando a biblioteca JavaScript do SDK da Web

Defina o `context` matriz de strings ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK, todas as informações de contexto, exceto `"highEntropyUserAgentHints"` é coletado por padrão. Defina essa propriedade se quiser coletar dicas de cliente de alta entropia ou se quiser omitir outras informações de contexto da coleta de dados. As cadeias de caracteres podem ser incluídas em qualquer ordem.

>[!NOTE]
>
>Se quiser coletar todas as informações de contexto, incluindo dicas de cliente de alta entropia, você deve incluir todos os valores no `context` string da matriz. O padrão `context` o valor omite `highEntropyUserAgentHints`, e se você definir a variável `context` qualquer valor omitido não coletará dados.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
