---
title: Informações coletadas automaticamente
description: Uma visão geral dos dados que o SDK da Web da Adobe Experience Platform coleta automaticamente.
source-git-commit: 89b981104e3cbe597d1556484f4365866bf2a11d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 3%

---

# Informações coletadas automaticamente

O Adobe Experience Platform Web SDK coleta automaticamente algumas informações prontas para uso. Se a organização não quiser coletar esses dados automaticamente, você poderá usar o `context` opção no [`configure` comando](../fundamentals/configuring-the-sdk.md).

Palavras-chave excluídas do `context` não estão incluídas na coleção de dados. Se a variável `context` a matriz não existe no `configure` , todos os dados na tabela abaixo serão coletados automaticamente.

| Nome | Descrição | `context` palavra-chave de matriz | Caminho XDM | Valor de exemplo |
| --- | --- | --- | --- | --- |
| Altura da tela | A altura da tela em pixels. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Largura da tela | A largura da tela em pixels. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Orientação da tela | A orientação da tela. | `device` | `events[].xdm.device.screenOrientation` | `landscape` ou `portrait` |
| Tipo de ambiente | O tipo de ambiente pelo qual a experiência surgiu. O Adobe Experience Platform Web SDK sempre define esse campo como `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Altura da janela de visualização | A altura da área de conteúdo do navegador em pixels. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Largura da janela de visualização | A largura da área de conteúdo do navegador em pixels. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| Nome do SDK | O identificador do SDK. Este campo usa um URI para melhorar a exclusividade entre os identificadores fornecidos por diferentes bibliotecas de software. Quando a biblioteca independente é usada, o valor é `https://ns.adobe.com/experience/alloy`. Quando a biblioteca é usada como parte da extensão de tag, o valor é `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| Versão do SDK | Quando a biblioteca independente é usada, o valor é a versão da biblioteca. Quando a biblioteca é usada como parte da extensão de tag, o valor é uma concatenação da versão da biblioteca e da versão da extensão de tag. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Ambiente | O ambiente onde os dados foram coletados. O Adobe Experience Platform Web SDK sempre define esse campo como `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Hora local | Carimbo de data e hora local do usuário final em formato ISO simplificado e estendido [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Deslocamento de fuso horário local | Número de minutos de deslocamento do usuário em relação ao GMT. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Carimbo de data e hora | O carimbo de data e hora UTC do usuário final em formato ISO estendido simplificado [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Sempre incluído | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| URL da página atual | O URL da página atual. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL do referenciador | O URL da página visitada anteriormente. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
