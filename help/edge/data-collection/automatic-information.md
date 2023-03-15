---
title: Informações coletadas automaticamente no Adobe Experience Platform Web SDK
description: Uma visão geral de cada informação que o SDK da Adobe Experience Platform coleta automaticamente.
keywords: coletar informações;contexto;configurar;dispositivo;screenHeight;screenHeight;screenOrientation;screenOrientation;screenWidth;screen Width;ambiente;viewportHeight;viewportWidth;viewportWidth;crowserDetails;detalhes do navegador;detalhes da implementação;detalhes da implementação;nome;versão;placeContext;localTime;hora local;localTimezoneOffset;deslocamento do fuso horário local;carimbo de data e hora;web;url;webPageDetails;página da web;webReferrer;referenciador da web;paisagem;portador da paisagem característica;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# Informações coletadas automaticamente

O Adobe Experience Platform Web SDK coleta várias informações automaticamente sem qualquer configuração especial. No entanto, essas informações podem ser desativadas, se necessário, usando o `context` opção no `configure` comando. [Consulte Configuração do SDK](../fundamentals/configuring-the-sdk.md). Abaixo está uma lista dessas informações. O nome entre parênteses indica a cadeia de caracteres a ser usada ao configurar o contexto.

## Dispositivo (`device`)

Informações sobre o dispositivo. Isso não inclui dados que podem ser pesquisados no lado do servidor a partir da sequência do agente do usuário.

### Altura da tela

| **Caminho na carga:** | **Exemplo:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

A altura da tela (em pixels).

### Orientação da tela

| **Caminho na carga:** | **Valores possíveis:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` ou `portrait` |

A orientação da tela.

### Largura da tela

| **Caminho na carga:** | **Exemplo:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

A largura da tela (em pixels).

## Ambiente (`environment`)

Detalhes sobre o ambiente do navegador.

### Tipo de ambiente

Navegador

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

O tipo de ambiente pelo qual a experiência surgiu. O Adobe Experience Platform Web SDK sempre define isso como `browser`.

### Altura da janela de visualização

| **Caminho na carga:** | **Exemplo:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

A altura da área de conteúdo do navegador (em pixels).

### Largura da janela de visualização

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

A largura da área de conteúdo do navegador (em pixels).

## Detalhes da implementação

Informações sobre o SDK usado para coletar o evento.

### Nome

| **Caminho na carga:** | **Exemplo:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

O identificador do kit de desenvolvimento de software (SDK).  Este campo usa um URI para melhorar a exclusividade entre os identificadores fornecidos por diferentes bibliotecas de software. Quando a biblioteca independente é usada, o valor é `https://ns.adobe.com/experience/alloy`. Quando a biblioteca é usada como parte da extensão de tag, o valor é `https://ns.adobe.com/experience/alloy+reactor`.

### Versão

| **Caminho na carga:** | **Exemplo:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Quando a biblioteca independente é usada, o valor é simplesmente a versão da biblioteca. Quando a biblioteca é usada como parte da extensão de tag, essa é a versão da biblioteca e a versão da extensão de tag unida com um &quot;+&quot;. Por exemplo, se a versão da biblioteca fosse 2.1.0 e a versão da extensão de tag fosse 2.1.3, o valor seria `2.1.0+2.1.3`.

### Ambiente

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

O ambiente onde os dados foram coletados. Sempre definida como `browser`.

## Contexto do local (`placeContext`)

Informações sobre a localização do usuário final.

### Hora local

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Carimbo de data e hora local do usuário final em formato ISO simplificado e estendido [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Deslocamento de fuso horário local

| **Caminho na carga:** | **Exemplo:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Número de minutos de deslocamento do usuário em relação ao GMT.

## Carimbo de data e hora

| **Caminho na carga:** | **Exemplo:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

O carimbo de data e hora do evento.  Esta parte do contexto não pode ser removida.

Carimbo de data e hora UTC do usuário final em formato ISO estendido simplificado [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Detalhes da Web (`web`)

Detalhes sobre a página em que o usuário está.

### URL da página atual

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

O URL da página atual.

### URL do referenciador

| **Caminho na carga:** | **Exemplo:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

O URL da página visitada anteriormente.
