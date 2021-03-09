---
title: Configurar o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o SDK da Web da Adobe Experience Platform.
seo-description: Saiba como configurar o SDK da Web da Experience Platform
keywords: configurar; configuração; SDK; borda; SDK da Web; configurar; edgeConfigId; contexto; Web; dispositivo; ambiente; placeContext; debugEnabled; edgeDomain; orgId; clickCollectionEnabled; onBeforeEventSend; defaultConsent; configurações de sdk da web; prehideStyle; opacity; cookieDestinationsEnabled; urlDestinations Enabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: f78da58ba7a593d9c161030833d9b69e2ba57c9a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 10%

---


# Configurar o SDK da Web da plataforma

A configuração do SDK é feita com o comando `configure`.

>[!IMPORTANT]
>
>`configure` deve  ** sempre ser o primeiro comando chamado.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Há muitas opções que podem ser definidas durante a configuração. Todas as opções podem ser encontradas abaixo, agrupadas por categoria.

## Opções gerais

### `edgeConfigId`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | nenhuma |

Sua ID de configuração atribuída, que vincula o SDK às contas e configurações apropriadas.  Ao configurar várias instâncias em uma única página, você deve configurar um `edgeConfigId` diferente para cada instância.

### `context`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadeias de caracteres | Não | `["web", "device", "environment", "placeContext"]` |

Indica quais categorias de contexto coletar automaticamente, conforme descrito em [Informações Automáticas](../data-collection/automatic-information.md).  Se essa configuração não for especificada, todas as categorias serão usadas por padrão.

### `debugEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `false` |

Indica se a depuração deve estar ativada. Configurar essa configuração como `true` ativa os seguintes recursos:

| **Recurso** | **Função** |
| ---------------------- | ------------------ |
| Validação síncrona | Valida os dados que estão sendo coletados em relação ao esquema e retorna um erro na resposta sob o seguinte rótulo: `collect:error OR success` |
| Registro do console | Permite que mensagens de depuração sejam exibidas no console JavaScript do navegador |

### `edgeDomain` {#edge-domain}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ------------------ |
| String | Não | `beta.adobedc.net` |
| String | Não | `omtrdc.net` |

O domínio usado para interagir com os serviços da Adobe. Isso só será usado se você tiver um domínio próprio (CNAME) que envie solicitações de proxy para a infraestrutura de borda da Adobe.

### `orgId`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | nenhuma |

Sua ID de organização [!DNL Experience Cloud] atribuída.  Ao configurar várias instâncias em uma página, você deve configurar um `orgId` diferente para cada instância.

## Coleta de dados

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Indica se os dados associados aos cliques em links devem ser coletados automaticamente. Consulte [Rastreamento automático de link](../data-collection/track-links.md#automaticLinkTracking) para obter mais informações.

### `onBeforeEventSend`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Função | Não | () => indefinido |

Defina isso para configurar um retorno de chamada que seja chamado para cada evento antes de ele ser enviado.  Um objeto com o campo `xdm` é enviado para o retorno de chamada.  Modifique o objeto `xdm` para alterar o que é enviado.  Dentro do retorno de chamada, o objeto `xdm` já terá os dados transmitidos no comando de evento e as informações coletadas automaticamente. Para obter mais informações sobre o tempo desse retorno de chamada e um exemplo, consulte [Modificando Eventos Globalmente](tracking-events.md#modifying-events-globally).

## Opções de privacidade

### `defaultConsent` {#default-consent}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Objeto | Não | `"in"` |

Define o consentimento padrão do usuário. Isso é usado quando não há preferência de consentimento já salva para o usuário. Os outros valores válidos são `"pending"` e `"out"`. Esse valor padrão não é persistente no perfil do usuário. Somente quando setConsent é chamado é que o perfil do usuário é atualizado.
* `"in"`: Quando isso é definido ou nenhum valor é fornecido, o trabalho continua sem as preferências de consentimento do usuário.
* `"pending"`: Quando definido, o trabalho será enfileirado até que o usuário forneça as preferências de consentimento.
* `"out"`: Quando definido, o trabalho será descartado até que o usuário forneça as preferências de consentimento.
Depois que as preferências do usuário forem fornecidas, o trabalho continuará ou será abortado com base nas preferências do usuário. Consulte [Suporte ao consentimento](../consent/supporting-consent.md) para obter mais informações.

## Opções de personalização

### `prehidingStyle`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Não | nenhuma |

Usado para criar uma definição de estilo CSS que oculta as áreas de conteúdo da página da Web, enquanto o conteúdo personalizado é carregado do servidor. Se essa opção não for fornecida, o SDK não tentará ocultar nenhuma área de conteúdo enquanto o conteúdo personalizado for carregado, resultando potencialmente em &quot;oscilação&quot;.

Por exemplo, se você tivesse um elemento em sua página da Web com uma ID `container` cujo conteúdo padrão gostaria de ocultar enquanto o conteúdo personalizado estiver sendo carregado do servidor, um exemplo de estilo pré-ocultado seria o seguinte:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opções de públicos

### `cookieDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Ativa [!DNL Audience Manager] destinos de cookies, o que permite a configuração de cookies com base na qualificação de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Habilita [!DNL Audience Manager] destinos de URL, o que permite o acionamento de URLs com base na qualificação de segmento.

## Opções de identidade

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | true |

Se verdadeiro, o SDK lerá e definirá cookies AMCV antigos. Isso ajuda na transição para o uso do SDK da Web da Adobe Experience Platform, enquanto algumas partes do site ainda podem estar usando o Visitor.js. Além disso, se a API de visitante for definida na página, o SDK consultará a API de visitante para a ECID. Isso permite adicionar duas páginas de tags ao SDK da Web da Adobe Experience Platform e ainda ter a mesma ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | true |

Ativa a configuração de cookies de terceiros da Adobe. O SDK tem a capacidade de persistir a ID de visitante em um contexto de terceiros para permitir que a mesma ID de visitante seja usada em sites. Isso é útil se você tem vários sites ou deseja compartilhar dados com parceiros; no entanto, às vezes isso não é desejado por motivos de privacidade.
