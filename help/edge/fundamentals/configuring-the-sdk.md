---
title: Configurar o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o Adobe Experience Platform Web SDK.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configurar;configuração;SDK;borda;SDK da Web;configurar;edgeConfigId;contexto;web;dispositivo;ambiente;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;configurações do sdk da Web;prehideStyle;opacidade;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: a192a746fa227b658fcdb8caa07ea6fb4ac1a944
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 9%

---

# Configurar o SDK da Web da plataforma

A configuração do SDK é feita com o `configure` comando.

>[!IMPORTANT]
>
>`configure` é *sempre* o primeiro comando chamado.

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
>**As Configurações de borda foram remarcadas para Datastreams. Uma ID de sequência de dados é a mesma de uma ID de configuração.**

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| String | Sim | None |

{style="table-layout:auto"}

Sua ID de configuração atribuída, que vincula o SDK às contas e configurações apropriadas. Ao configurar várias instâncias em uma única página, você deve configurar uma instância `edgeConfigId` para cada instância.

### `context` {#context}

| **Tipo** | Obrigatório | **Valor padrão** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadeias de caracteres | Não | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Indica quais categorias de contexto coletar automaticamente, conforme descrito em [Informações Automáticas](../data-collection/automatic-information.md). Se essa configuração não for especificada, todas as categorias serão usadas por padrão.

>[!IMPORTANT]
>
>Todas as propriedades de contexto, com exceção de `highEntropyUserAgentHints`, são ativados por padrão. Se você especificou propriedades de contexto manualmente na configuração do SDK da Web, deve habilitar todas as propriedades de contexto para continuar coletando as informações necessárias.

Para habilitar [dicas do cliente de alta entropia](user-agent-client-hints.md#enabling-high-entropy-client-hints) na implantação do SDK da Web, você deve incluir os `highEntropyUserAgentHints` opção de contexto, junto com a configuração existente.

Por exemplo, para recuperar dicas de cliente de alta entropia de propriedades da Web, sua configuração seria semelhante a:

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `false` |

{style="table-layout:auto"}

Indica se a depuração está habilitada. Definindo esta configuração como `true` habilita os seguintes recursos:

| **Recurso** | **Função** |
| ---------------------- | ------------------ |
| Logon no console | Permite que as mensagens de depuração sejam exibidas no console JavaScript do navegador |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Preencha este campo com seu domínio primário. Para obter mais detalhes, consulte [documentação](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=pt-BR).

O domínio é semelhante a `data.{customerdomain.com}` para obter um site em www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Caminho após o edgeDomain usado para se comunicar e interagir com os serviços da Adobe.  Geralmente, isso só é alterado quando o ambiente de produção padrão não é usado.

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| String | Não | ee |

{style="table-layout:auto"}

### `orgId`

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| String | Sim | None |

{style="table-layout:auto"}

Seu atribuído [!DNL Experience Cloud] ID da organização. Ao configurar várias instâncias em uma página, você deve configurar uma instância diferente `orgId` para cada instância.

## Coleta de dados

### `clickCollectionEnabled` {#clickCollectionEnabled}

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style="table-layout:auto"}

Indica se os dados associados aos cliques em links são coletados automaticamente. Consulte [Rastreamento automático de link](../data-collection/track-links.md#automaticLinkTracking) para obter mais informações. Os links também são rotulados como links de download se incluírem um atributo de download ou se o link terminar com uma extensão de arquivo. Os qualificadores de link de download podem ser configurados com uma expressão regular. O valor padrão é `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Função | Não | () => indefinido |

{style="table-layout:auto"}

Configure um retorno de chamada que seja chamado para cada evento antes que ele seja enviado. Um objeto com o campo `xdm` é enviado para o retorno de chamada. Para alterar o que é enviado, modifique o `xdm` objeto. Dentro do retorno de chamada, a variável `xdm` O objeto já transmitiu os dados no comando de evento e as informações coletadas automaticamente. Para obter mais informações sobre o tempo desse retorno de chamada e um exemplo, consulte [Modificar eventos globalmente](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Função | Não | () => indefinido |

{style="table-layout:auto"}

Configure um retorno de chamada que seja chamado para cada evento de rastreamento de cliques em links antes de ser enviado. O retorno de chamada envia um objeto com a variável `xdm`, `clickedElement`, e `data` campos.

Ao filtrar o rastreamento de link usando a estrutura de elementos DOM, você pode usar o `clickElement` comando. `clickedElement` é o nó do elemento DOM que foi clicado e encapsulou a árvore de nós principais.

Para alterar quais dados são enviados, modifique o `xdm` e/ou `data` objetos. Dentro do retorno de chamada, a variável `xdm` O objeto já transmitiu os dados no comando de evento e as informações coletadas automaticamente.

* Qualquer valor diferente de `false` permitirá que o evento seja processado e o retorno de chamada seja enviado.
* Se o retorno de chamada retornar a variável `false` for, o processamento do evento será interrompido, sem um erro, e o evento não será enviado. Esse mecanismo permite que determinados eventos sejam filtrados examinando os dados do evento e retornando `false` caso o evento não deva ser enviado.
* Se o retorno de chamada lançar uma exceção, o processamento do evento será interrompido e o evento não será enviado.


## Opções de privacidade

### `defaultConsent` {#default-consent}

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Objeto | Não | `"in"` |

{style="table-layout:auto"}

Define o consentimento padrão do usuário. Use esta configuração quando não houver preferência de consentimento já salva para o usuário. Os outros valores válidos são `"pending"` e `"out"`. Este valor padrão não é mantido no perfil do usuário. O perfil do usuário é atualizado somente quando `setConsent` é chamado.
* `"in"`: quando essa configuração é definida ou nenhum valor é fornecido, o trabalho continua sem as preferências de consentimento do usuário.
* `"pending"`: quando essa configuração é definida, o trabalho é enfileirado até que o usuário forneça preferências de consentimento.
* `"out"`: quando essa configuração é definida, o trabalho é descartado até que o usuário forneça preferências de consentimento.
Após as preferências do usuário serem fornecidas, o trabalho continua ou é interrompido com base nas preferências do usuário. Consulte [Suporte ao consentimento](../consent/supporting-consent.md) para obter mais informações.

## Opções de personalização {#personalization}

### `prehidingStyle` {#prehidingStyle}

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| String | Não | None |

{style="table-layout:auto"}

Usado para criar uma definição de estilo CSS que oculta as áreas de conteúdo da sua página da Web enquanto o conteúdo personalizado é carregado do servidor. Se essa opção não for fornecida, o SDK não tentará ocultar áreas de conteúdo enquanto o conteúdo personalizado for carregado, possivelmente resultando em &quot;oscilação&quot;.

Por exemplo, se um elemento na página da Web tiver uma ID de `container`, cujo conteúdo padrão você deseja ocultar enquanto o conteúdo personalizado é carregado do servidor, use o seguinte estilo de pré-ocultação:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Essa opção deve ser usada ao migrar páginas individuais do [!DNL at.js] para o SDK da Web.

Use esta opção para permitir que o SDK da Web leia e grave o conteúdo herdado `mbox` e `mboxEdgeCluster` cookies usados pelo [!DNL at.js]. Isso ajuda a manter o perfil do visitante ao mover de uma página que usa o SDK da Web para uma página que usa o [!DNL at.js] e vice-versa.

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `false` |

## Opções de públicos

### `cookieDestinationsEnabled`

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style="table-layout:auto"}

Habilita [!DNL Audience Manager] destinos de cookies, que permite a configuração de cookies com base na qualificação de segmentos.

### `urlDestinationsEnabled`

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style="table-layout:auto"}

Habilita [!DNL Audience Manager] Destinos de URL, que permitem o acionamento de URLs com base na qualificação de segmento.

## Opções de identidade

### `idMigrationEnabled` {#id-migration-enabled}

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style="table-layout:auto"}

Se verdadeiro, o SDK lê e define cookies AMCV antigos. Essa opção ajuda na transição para o uso do SDK da Web da Adobe Experience Platform, enquanto algumas partes do site ainda podem usar Visitor.js.

Se a API do visitante for definida na página, o SDK consultará a API do visitante para a ECID. Essa opção permite que você adicione páginas com tags duplas com o SDK da Web da Adobe Experience Platform e ainda tenha a mesma ECID.

### `thirdPartyCookiesEnabled`

| Tipo | Obrigatório | Valor padrão |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

{style="table-layout:auto"}

Ativa a configuração de cookies de terceiros do Adobe. O SDK pode manter a ID de visitante em um contexto de terceiros para permitir que a mesma ID de visitante seja usada em todos os sites. Use essa opção se tiver vários sites ou se quiser compartilhar dados com parceiros; no entanto, às vezes essa opção não é desejada por motivos de privacidade.
