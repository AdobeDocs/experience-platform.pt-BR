---
title: Configurar o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o SDK da Web da Adobe Experience Platform.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configurar; configuração; SDK; borda; SDK da Web; configurar; edgeConfigId; contexto; Web; dispositivo; ambiente; placeContext; debugEnabled; edgeDomain; orgId; clickCollectionEnabled; onBeforeEventSend; defaultConsent; configurações de sdk da web; prehideStyle; opacity; cookieDestinationsEnabled; urlDestinations Enabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 4d0f1b3e064bd7b24e17ff0fafb50d930b128968
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 15%

---

# Configurar o SDK da Web da plataforma

A configuração do SDK é feita com a variável `configure` comando.

>[!IMPORTANT]
>
>`configure` é *always* o primeiro comando chamado.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Há muitas opções que podem ser definidas durante a configuração. Todas as opções podem ser encontradas abaixo, agrupadas por categoria.

## Opções gerais

### `edgeConfigId`

>[!NOTE]
>
>**As configurações de borda foram remarcadas para Datastreams. Uma ID de armazenamento de dados é a mesma ID de configuração.**

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | None |

{style=&quot;table-layout:auto&quot;}

Sua ID de configuração atribuída, que vincula o SDK às contas e configurações apropriadas. Ao configurar várias instâncias em uma única página, você deve configurar um `edgeConfigId` para cada instância.

### `context`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadeias de caracteres | Não | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Indica quais categorias de contexto coletar automaticamente, conforme descrito em [Informações automáticas](../data-collection/automatic-information.md). Se essa configuração não for especificada, todas as categorias serão usadas por padrão.

### `debugEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `false` |

{style=&quot;table-layout:auto&quot;}

Indica se a depuração está ativada. Configurar essa configuração como `true` habilita os seguintes recursos:

| **Recurso** | **Função** |
| ---------------------- | ------------------ |
| Registro do console | Permite que mensagens de depuração sejam exibidas no console JavaScript do navegador |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Preencha este campo com seu domínio primário. Para obter mais detalhes, consulte a [documentação](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=pt-BR).

O domínio é semelhante a `data.{customerdomain.com}` para um site em www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Caminho após o edgeDomain usado para se comunicar e interagir com os serviços da Adobe.  Geralmente, isso só seria alterado quando não fosse usado o ambiente de produção padrão.

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Não | ee |

{style=&quot;table-layout:auto&quot;}

### `orgId`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | Nenhum |

{style=&quot;table-layout:auto&quot;}

Atribuído [!DNL Experience Cloud] ID da organização. Ao configurar várias instâncias em uma página, você deve configurar um `orgId` para cada instância.

## Coleta de dados

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style=&quot;table-layout:auto&quot;}

Indica se os dados associados aos cliques em links são coletados automaticamente. Consulte [Rastreamento automático de links](../data-collection/track-links.md#automaticLinkTracking) para obter mais informações. Os links também são rotulados como links de download se incluírem um atributo de download ou se o link terminar com uma extensão de arquivo. Os qualificadores de link de download podem ser configurados com uma expressão regular. O valor padrão é `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Função | Não | () => indefinido |

{style=&quot;table-layout:auto&quot;}

Configure um retorno de chamada que seja chamado para cada evento antes de ele ser enviado. Um objeto com o campo `xdm` é enviado para o retorno de chamada. Para alterar o que é enviado, modifique o `xdm` objeto. Dentro do retorno de chamada, a variável `xdm` O objeto já tem os dados passados no comando event e as informações coletadas automaticamente. Para obter mais informações sobre o tempo desse retorno de chamada e um exemplo, consulte [Modificar eventos globalmente](tracking-events.md#modifying-events-globally).

## Opções de privacidade

### `defaultConsent` {#default-consent}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Objeto | Não | `"in"` |

{style=&quot;table-layout:auto&quot;}

Define o consentimento padrão do usuário. Use essa configuração quando não houver preferência de consentimento já salva para o usuário. Os outros valores válidos são `"pending"` e `"out"`. Esse valor padrão não é persistente no perfil do usuário. O perfil do usuário é atualizado somente quando `setConsent` é chamado.
* `"in"`: Quando essa configuração é definida ou nenhum valor é fornecido, o trabalho continua sem as preferências de consentimento do usuário.
* `"pending"`: Quando essa configuração é definida, o trabalho é enfileirado até que o usuário forneça as preferências de consentimento.
* `"out"`: Quando essa configuração é definida, o trabalho é descartado até que o usuário forneça as preferências de consentimento.
Depois que as preferências do usuário forem fornecidas, o trabalho continuará ou será abortado com base nas preferências do usuário. Consulte [Suporte ao consentimento](../consent/supporting-consent.md) para obter mais informações.

## Opções de personalização

### `prehidingStyle`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Não | Nenhum |

{style=&quot;table-layout:auto&quot;}

Usado para criar uma definição de estilo CSS que oculta as áreas de conteúdo da página da Web, enquanto o conteúdo personalizado é carregado do servidor. Se essa opção não for fornecida, o SDK não tentará ocultar nenhuma área de conteúdo enquanto o conteúdo personalizado for carregado, resultando potencialmente em &quot;oscilação&quot;.

Por exemplo, se um elemento em sua página da Web tiver uma ID de `container`, cujo conteúdo padrão você deseja ocultar enquanto o conteúdo personalizado é carregado do servidor, use o seguinte estilo de pré-ocultação:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opções de públicos

### `cookieDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style=&quot;table-layout:auto&quot;}

Habilitar [!DNL Audience Manager] destinos de cookies, que permitem a configuração de cookies com base na qualificação de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style=&quot;table-layout:auto&quot;}

Habilitar [!DNL Audience Manager] Destinos de URL, que permitem o acionamento de URLs com base na qualificação de segmento.

## Opções de identidade

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style=&quot;table-layout:auto&quot;}

Se verdadeiro, o SDK lê e define cookies AMCV antigos. Essa opção ajuda na transição para o uso do SDK da Web da Adobe Experience Platform, enquanto algumas partes do site ainda podem usar o Visitor.js. Se a API de visitante for definida na página, o SDK consultará a API de visitante para a ECID. Essa opção permite adicionar duas tags a páginas com o SDK da Web da Adobe Experience Platform e ainda ter a mesma ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style=&quot;table-layout:auto&quot;}

Ativa a configuração de cookies de terceiros do Adobe. O SDK pode manter a ID de visitante em um contexto de terceiros para permitir que a mesma ID de visitante seja usada em sites. Use essa opção se você tiver vários sites ou quiser compartilhar dados com parceiros; no entanto, às vezes, essa opção não é desejada por motivos de privacidade.
