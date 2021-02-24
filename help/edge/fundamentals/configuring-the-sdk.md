---
title: Configurar o Adobe Experience Platform Web SDK
description: Saiba como configurar o Adobe Experience Platform Web SDK.
seo-description: Saiba como configurar o SDK da Web do Experience Platform
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;ambiente;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehideStyle;opacity;cookieDestinationsEnabled;url Destinations ationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 11%

---


# Configurar o SDK da Web da plataforma

A configuração do SDK é feita com o comando `configure`.

>[!IMPORTANT]
>
>`configure` deve ser  ** sempre o primeiro comando chamado.

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

Sua ID de configuração atribuída, que vincula o SDK às contas e configuração apropriadas.  Ao configurar várias instâncias em uma única página, você deve configurar um `edgeConfigId` diferente para cada instância.

### `context`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de sequências de caracteres | Não | `["web", "device", "environment", "placeContext"]` |

Indica quais categorias de contexto devem ser coletadas automaticamente, conforme descrito em [Informações Automáticas](../data-collection/automatic-information.md).  Se essa configuração não for especificada, todas as categorias serão usadas por padrão.

### `debugEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `false` |

Indica se a depuração deve ser ativada. A configuração para `true` ativa os seguintes recursos:

| **Recurso** | **Função** |
| ---------------------- | ------------------ |
| Validação síncrona | Valida os dados que estão sendo coletados em relação ao schema e retorna um erro na resposta sob o seguinte rótulo: `collect:error OR success` |
| Registro do console | Permite que mensagens de depuração sejam exibidas no console JavaScript do navegador |

### `edgeDomain` {#edge-domain}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ------------------ |
| String | Não | `beta.adobedc.net` |
| String | Não | `omtrdc.net` |

O domínio usado para interagir com os serviços de Adobe. Isso só será usado se você tiver um domínio próprio (CNAME) que faça proxy das solicitações para a infraestrutura de borda do Adobe.

### `orgId`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | nenhuma |

Sua ID de empresa [!DNL Experience Cloud] atribuída.  Ao configurar várias instâncias em uma página, você deve configurar um `orgId` diferente para cada instância.

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

Configure isso para configurar um retorno de chamada chamado para cada evento antes de ele ser enviado.  Um objeto com o campo `xdm` é enviado para o retorno de chamada.  Modifique o objeto `xdm` para alterar o que é enviado.  Dentro do retorno de chamada, o objeto `xdm` já terá os dados transmitidos no comando do evento e as informações coletadas automaticamente. Para obter mais informações sobre o tempo desse retorno de chamada e um exemplo, consulte [Modificando Eventos Globalmente](tracking-events.md#modifying-events-globally).

## Opções de privacidade

### `defaultConsent` {#default-consent}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Objeto | Não | `"in"` |

Define o consentimento padrão do usuário. Isso é usado quando não há preferência de consentimento já salva para o usuário. O outro valor válido é `"pending"`. Quando definido, o trabalho será enfileirado até que o usuário forneça as preferências de consentimento. Depois que as preferências do usuário forem fornecidas, o trabalho continuará ou será abortado com base nas preferências do usuário. Consulte [Consentimento de suporte](../consent/supporting-consent.md) para obter mais informações.

## Opções de personalização

### `prehidingStyle`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Não | nenhuma |

Usado para criar uma definição de estilo CSS que oculta áreas de conteúdo da sua página da Web enquanto o conteúdo personalizado é carregado do servidor. Se essa opção não for fornecida, o SDK não tentará ocultar nenhuma área de conteúdo enquanto o conteúdo personalizado for carregado, resultando potencialmente em &quot;oscilação&quot;.

Por exemplo, se você tivesse um elemento em sua página da Web com uma ID de `container` cujo conteúdo padrão você gostaria de ocultar enquanto o conteúdo personalizado estiver sendo carregado do servidor, um exemplo de estilo de pré-ocultação seria o seguinte:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opções do Audiência

### `cookieDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Habilita [!DNL Audience Manager] destinos de cookies, o que permite a configuração de cookies com base na qualificação de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Habilita [!DNL Audience Manager] destinos de URL, o que permite o acionamento de URLs com base na qualificação de segmentos.

## Opções de identidade

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | true |

Se verdadeiro, o SDK lerá e definirá cookies AMCV antigos. Isso ajuda na transição para o uso do SDK da Web do Adobe Experience Platform enquanto algumas partes do site ainda podem estar usando o Visitante.js. Além disso, se a API do Visitante estiver definida na página, o SDK irá a API do Visitante do query para a ECID. Isso permite que você adicione tags duplas às páginas com o SDK da Web da Adobe Experience Platform e ainda tenha o mesmo ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | true |

Ativa a configuração de cookies de terceiros Adobe. O SDK tem a capacidade de persistir a ID do visitante em um contexto de terceiros para permitir que a mesma ID do visitante seja usada em sites. Isso é útil se você tem vários sites ou deseja compartilhar dados com parceiros; no entanto, às vezes isso não é desejado por motivos de privacidade.
