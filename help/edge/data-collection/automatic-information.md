---
title: Coletar automaticamente informações no SDK da Web da Adobe Experience Platform
description: Uma visão geral de cada parte das informações que o SDK da Adobe Experience Platform coleta automaticamente.
keywords: coletar informações, contexto, configurar, dispositivo, screenHeight, screen Height, screenOrientation, screenOrientation, screenWidth, screen Width, ambiente, viewportHeight, viewport Height, viewportWidth, viewport Width, crowserDetails, detalhes do navegador, implementationDetails, implementation Details, nome, version, placeContext, localTime, localTimezoneOffset;Deslocamento de fuso horário local;timestamp;web;url;webPageDetails;web Page Details;web Page Reference;web Referrer;web Referrer;landscape;portrait;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 6%

---

# Informações coletadas automaticamente

O SDK da Web da Adobe Experience Platform coleta várias informações automaticamente sem qualquer configuração especial. No entanto, essas informações podem ser desativadas se necessário usando a opção `context` no comando `configure`. [Consulte Configuração do SDK](../fundamentals/configuring-the-sdk.md). Abaixo está uma lista dessas informações. O nome entre parênteses indica a string a ser usada ao configurar o contexto.

## Dispositivo (`device`)

Informações sobre o dispositivo. Isso não inclui dados que podem ser pesquisados no lado do servidor a partir da sequência de agente do usuário.

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

Browser

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

O tipo de ambiente pelo qual a experiência surgiu. O SDK da Web da Adobe Experience Platform sempre define isso como `browser`.

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

O identificador do kit de desenvolvimento de software (SDK).  Este campo usa um URI para melhorar a exclusividade entre identificadores fornecidos por diferentes bibliotecas de software. Quando a biblioteca independente é usada, o valor é `https://ns.adobe.com/experience/alloy`. Quando a biblioteca é usada como parte da extensão do Platform launch, o valor é `https://ns.adobe.com/experience/alloy+reactor`.

### Versão

| **Caminho na carga:** | **Exemplo:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Quando a biblioteca independente é usada, o valor é simplesmente a versão da biblioteca. Quando a biblioteca é usada como parte da extensão do Platform launch, essa é a versão da biblioteca e a versão da extensão do Platform launch unida com um &quot;+&quot;. Por exemplo, se a versão da biblioteca fosse 2.1.0 e a versão da extensão do Platform launch fosse 2.1.3, o valor seria `2.1.0+2.1.3`.

### Ambiente

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

O ambiente em que os dados foram coletados. Isso é sempre definido como `browser`.

## Colocar contexto (`placeContext`)

Informações sobre a localização do usuário final.

### Hora local

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Carimbo de data e hora local para o usuário final em formato ISO simplificado e estendido [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Deslocamento do fuso horário local

| **Caminho na carga:** | **Exemplo:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Número de minutos em que o usuário é deslocado do GMT.

## Carimbo de data e hora

| **Caminho na carga:** | **Exemplo:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

O carimbo de data e hora do evento.  Esta parte do contexto não pode ser removida.

Carimbo de data e hora UTC para o usuário final em formato ISO simplificado e estendido [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

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

O URL da página anterior visitada.
