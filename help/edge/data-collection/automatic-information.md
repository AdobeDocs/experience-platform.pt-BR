---
title: Coleta automática de informações no Adobe Experience Platform Web SDK
description: Uma visão geral de cada informação que o SDK do Adobe Experience Platform coleta automaticamente.
keywords: coletar informações;contexto;configurar;dispositivo;screenHeight;screenHeight;screenOrientation;screenOrientation;screenWidth;screenWidth;screenWidth;screen;screenHeight;viewportHeight;viewportWidth;viewport Width;crowserDetails;browser details;implementationDetails;implementationDetails;nome;version;localTime;localOfffzone set;local Deslocamento do fuso horário;carimbo de data e hora;web;url;webPageDetails;web Page Details;webReferrer;web Quem indicou;landscape;portrait;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 8%

---


# Informações automaticamente coletadas

O Adobe Experience Platform Web SDK coleta várias informações automaticamente sem nenhuma configuração especial. No entanto, essas informações podem ser desativadas se necessário usando a opção `context` no comando `configure`. [Consulte Configuração do SDK](../fundamentals/configuring-the-sdk.md). Abaixo está uma lista dessas informações. O nome entre parênteses indica a string a ser usada ao configurar o contexto.

## Dispositivo (`device`)

Informações sobre o dispositivo. Isso não inclui dados que podem ser pesquisados no lado do servidor a partir da string do agente do usuário.

### Altura da tela

| **Caminho na carga:** | **Exemplo:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

A altura em pixels da tela.

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

O tipo de ambiente pelo qual a experiência surgiu. O Adobe Experience Platform Web SDK sempre define para `browser`.

### Altura do visor

| **Caminho na carga:** | **Exemplo:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

A altura da área de conteúdo do navegador (em pixels).

### Largura do visor

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

O identificador do kit de desenvolvimento de software (SDK).  Este campo usa um URI para melhorar a exclusividade entre identificadores fornecidos por diferentes bibliotecas de software.

### Versão

| **Caminho na carga:** | **Exemplo:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### Ambiente

| **Caminho na carga:** | **Exemplo:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## Inserir contexto (`placeContext`)

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

### URL de quem indicou

| **Caminho na carga:** | **Exemplo:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

O URL da página anterior visitada.
