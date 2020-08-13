---
title: Configuração do SDK
seo-title: Configuração do Adobe Experience Platform Web SDK
description: Saiba como configurar o SDK da Web do Experience Platform
seo-description: Saiba como configurar o SDK da Web do Experience Platform
translation-type: tm+mt
source-git-commit: b7b206573a130af70a82c73a3f9b0a0eb28a513a
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 11%

---


# Configuração do SDK

A configuração do SDK é feita com o `configure` comando.

>[!IMPORTANT]
>
>`configure` deve ser *sempre* o primeiro comando chamado.

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
| String | Sim | none |

Sua ID de configuração atribuída, que vincula o SDK às contas e configuração apropriadas.  Ao configurar várias instâncias em uma única página, você deve configurar uma diferente `edgeConfigId` para cada instância.

### `context`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de sequências de caracteres | Não | `["web", "device", "environment", "placeContext"]` |

Indica quais categorias de contexto devem ser coletadas automaticamente, conforme descrito em Informações [](../reference/automatic-information.md)automáticas.  Se essa configuração não for especificada, todas as categorias serão usadas por padrão.

### `debugEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `false` |

Indica se a depuração deve ser ativada. Configurar essa configuração para `true` ativar os seguintes recursos:

| **Recurso** | **Função** |
| ---------------------- | ------------------ |
| Validação síncrona | Valida os dados que estão sendo coletados em relação ao schema e retorna um erro na resposta sob o seguinte rótulo: `collect:error OR success` |
| Registro do console | Permite que mensagens de depuração sejam exibidas no console JavaScript do navegador |

### `edgeDomain`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ------------------ |
| String | Não | `beta.adobedc.net` |

O domínio usado para interagir com os serviços de Adobe. Isso só será usado se você tiver um domínio próprio (CNAME) que faça proxy das solicitações para a infraestrutura de borda do Adobe.

### `orgId`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | none |

Your assigned [!DNL Experience Cloud] organization ID.  Ao configurar várias instâncias em uma página, você deve configurar uma diferente `orgId` para cada instância.

## Coleta de dados

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Indica se os dados associados aos cliques em links devem ser coletados automaticamente. Para cliques que se qualificam como cliques em links, os seguintes dados de interação [da](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) Web são coletados:

| **Propriedade** | **Descrição** |
| ------------ | ----------------------------------- |
| Nome do link | Nome determinado pelo contexto do link |
| URL do link | URL normalizado |
| Tipo de link | Definir para baixar, sair ou outras |

### `onBeforeEventSend`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Função | Não | () => indefinido |

Configure isso para configurar um retorno de chamada chamado para cada evento antes de ele ser enviado.  Um objeto com o campo `xdm` é enviado para o retorno de chamada.  Modifique o `xdm` objeto para alterar o que é enviado.  Dentro do retorno de chamada, os dados do `xdm` objeto já serão transmitidos no comando do evento e as informações coletadas automaticamente.  Para obter mais informações sobre o tempo desse retorno de chamada e um exemplo, consulte [Modificando Eventos globalmente](tracking-events.md#modifying-events-globally).

## Opções de privacidade

### `defaultConsent`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Objeto | Não | `{"general": "in"}` |

Define o consentimento padrão do usuário. Isso é usado quando não há preferência de consentimento já salva para o usuário. O outro valor válido é `{"general": "pending"}`. Quando definido, o trabalho será enfileirado até que o usuário forneça as preferências de consentimento. Depois que as preferências do usuário forem fornecidas, o trabalho continuará ou será abortado com base nas preferências do usuário. Consulte [Suporte ao consentimento](supporting-consent.md) para obter mais informações.

## Opções de personalização

### `prehidingStyle`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Não | none |

Usado para criar uma definição de estilo CSS que oculta áreas de conteúdo da sua página da Web enquanto o conteúdo personalizado é carregado do servidor. Se essa opção não for fornecida, o SDK não tentará ocultar nenhuma área de conteúdo enquanto o conteúdo personalizado for carregado, resultando potencialmente em &quot;oscilação&quot;.

Por exemplo, se você tivesse um elemento em sua página da Web com uma ID cujo conteúdo padrão você gostaria de ocultar enquanto o conteúdo personalizado estiver sendo carregado do servidor, um exemplo de estilo de pré-ocultação seria o seguinte: `container`

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opções do Audiência

### `cookieDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Habilita destinos [!DNL Audience Manager] de cookies, o que permite a configuração de cookies com base na qualificação de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | `true` |

Habilita destinos [!DNL Audience Manager] de URL, o que permite acionar URLs com base na qualificação de segmentos.

## Opções de identidade

### `idMigrationEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | true |

Se verdadeiro, o SDK lerá e definirá cookies AMCV antigos. Isso ajuda na transição para o uso do SDK da Web AEP enquanto algumas partes do site ainda podem estar usando o Visitante.js. Além disso, se a API do Visitante estiver definida na página, o SDK irá a API do Visitante do query para a ECID. Isso permite que você adicione tags duplas às páginas com o SDK da Web AEP e ainda tenha o mesmo ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | Não | true |

Ativa a configuração de cookies de terceiros Adobe. O SDK tem a capacidade de persistir a ID do visitante em um contexto de terceiros para permitir que a mesma ID do visitante seja usada em sites. Isso é útil se você tem vários sites ou deseja compartilhar dados com parceiros; no entanto, às vezes isso não é desejado por motivos de privacidade.
