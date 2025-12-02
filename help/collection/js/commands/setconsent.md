---
title: setConsent
description: Usado em cada página para rastrear as preferências de consentimento dos usuários.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 3%

---


# `setConsent`

O comando `setConsent` informa ao Web SDK se ele deve enviar dados (aceitação), descartar dados (recusa) ou usar [`defaultConsent`](configure/defaultconsent.md) (consentimento desconhecido).

O Web SDK é compatível com os seguintes padrões:

* **[Padrão do Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: os padrões 1.0 e 2.0 são compatíveis.
* **[Estrutura de transparência e consentimento do IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: se você usar esse padrão, o Perfil de cliente em tempo real do visitante será atualizado com as informações de consentimento se a implementação estiver configurada corretamente:
   1. O esquema de perfil individual XDM contém o [Grupo de campos de Consentimento do TCF 2.0 do IAB](/help/xdm/field-groups/profile/iab.md).
   1. O esquema do Evento de experiência contém o [Grupo de campos de Consentimento da TCF 2.0 do IAB](/help/xdm/field-groups/event/iab.md).
   1. Você inclui as informações de consentimento do IAB no evento [objeto XDM](sendevent/xdm.md). O Web SDK não inclui automaticamente as informações de consentimento ao enviar dados do evento.

Após usar esse comando, o Web SDK grava as preferências do usuário em um cookie. Na próxima vez que o usuário carregar o site no navegador, o SDK recuperará essas preferências persistentes para determinar se os eventos podem ser enviados para o Adobe.

A Adobe recomenda que você armazene todas as preferências da caixa de diálogo de consentimento separadamente do consentimento do Web SDK. O Web SDK não oferece uma maneira de recuperar o consentimento. Para garantir que as preferências do usuário permaneçam sincronizadas com o SDK, você pode chamar o comando `setConsent` em cada carregamento de página. O Web SDK só faz uma chamada de servidor quando o consentimento é alterado.

## Considerações sobre a sincronização de identidade {#identity-considerations}

O comando `setConsent` usa somente `ECID` do mapa de identidade, pois o comando opera no nível do dispositivo. Outras identidades do mapa de identidades não são consideradas pelo comando `setConsent`.

## Usando `defaultConsent` junto com `setConsent` {#using-consent}

O Web SDK oferece dois comandos complementares de configuração de consentimento:

* [`defaultConsent`](configure/defaultconsent.md): este comando destina-se a capturar as preferências de consentimento dos clientes do Adobe que usam o Web SDK.
* [`setConsent`](setconsent.md): este comando tem como objetivo capturar as preferências de consentimento dos visitantes do site.

Quando usadas juntas, essas configurações podem levar a diferentes resultados de coleta de dados e configuração de cookie, dependendo de seus valores configurados.

Consulte a tabela abaixo para entender quando ocorre a coleta de dados e quando os cookies são definidos, com base nas configurações de consentimento.

| `defaultConsent` | `setConsent` | Ocorre a coleta de dados | O Web SDK define cookies do navegador |
|---------|----------|---------|---------|
| `in` | `in` | Sim | Sim |
| `in` | `out` | Não | Sim |
| `in` | Não definido | Sim | Sim |
| `pending` | `in` | Sim | Sim |
| `pending` | `out` | Não | Sim |
| `pending` | Não definido | Não | Não |
| `out` | `in` | Sim | Sim |
| `out` | `out` | Não | Sim |
| `out` | Não definido | Não | Não |

Os seguintes cookies são definidos quando a configuração de consentimento permite:

| Nome | Idade máxima | Descrição |
|---|---|---|
| **`AMCV_###@AdobeOrg`** | 34128000 (395 dias) | Presente quando [`idMigrationEnabled`](configure/idmigrationenabled.md) estiver habilitado. Ajuda na transição para o Web SDK enquanto algumas partes do site ainda usam o `visitor.js`. |
| **`Demdex cookie`** | 15552000 (180 dias) | Apresentar se a sincronização de ID estiver habilitada. O Audience Manager define este cookie para atribuir um identificador exclusivo a um visitante do site. O cookie demdex ajuda o Audience Manager a executar funções básicas, como a identificação do visitante, a sincronização de ID, a segmentação, a modelagem, a geração de relatórios etc. |
| **`kndctr_orgid_cluster`** | 1800 (30 minutos) | Armazena a região do Edge Network que atende às solicitações do usuário atual. A região é usada no caminho do URL para que o Edge Network possa rotear a solicitação para a região correta. Se um usuário se conectar com um endereço IP diferente ou em uma sessão diferente, a solicitação será roteada novamente para a região mais próxima. |
| **`kndct_orgid_identity`** | 34128000 (395 dias) | Armazena a ECID, bem como outras informações relacionadas à ECID. |
| **`kndctr_orgid_consent`** | 15552000 (180 dias) | Armazena a preferência de consentimento dos usuários para o site. |
| **`s_ecid`** | 63115200 (2 anos) | Contém uma cópia da Experience Cloud ID ([!DNL ECID]) ou MID. A MID é armazenada em um par de valores chave que segue a sintaxe `s_ecid=MCMID\|<ECID>`. |

Execute o comando `setConsent` ao chamar a instância configurada do Web SDK. Você pode incluir os seguintes objetos nesse comando:

* **`consent[]`**: uma matriz de `consent` objetos. O objeto de consentimento é formatado de forma diferente dependendo do padrão e da versão escolhidos. Consulte as guias abaixo para obter exemplos de cada objeto de consentimento, dependendo do padrão de consentimento.
* **`identityMap`**: um objeto que controla como uma ECID é gerada e a quais IDs as informações de consentimento estão vinculadas. A Adobe recomenda incluir esse objeto quando `setConsent` for executado antes de outros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Um objeto que contém [substituições de configuração de sequência de dados](configure/edgeconfigoverrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Objeto do Adobe 2.0 standard `consent`

Se enviar dados para a Adobe Experience Platform, você deverá incluir um grupo de campos de esquema de privacidade no esquema do seu perfil. Consulte [Governança, privacidade e segurança no Adobe Experience Platform](/help/landing/governance-privacy-security/overview.md) para obter mais informações sobre o padrão Adobe 2.0. Você pode adicionar dados dentro do objeto de valor abaixo correspondente ao esquema do campo `consents` do grupo de campos de perfil [!UICONTROL Consents and Preferences].

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"Adobe"` para o padrão Adobe 2.0.
* **`version`**: uma cadeia de caracteres que representa a versão do padrão de consentimento. Defina esta propriedade como `"2.0"` para o padrão Adobe 2.0.
* **`value`**: um objeto contendo valores de consentimento.
   * **`value.collect.val`**: o valor de consentimento. Defina como `"y"` quando os usuários optarem por entrar e como `"n"` quando os usuários optarem por não participar.
   * **`value.metadata.time`**: O carimbo de data/hora quando os usuários atualizaram suas configurações de consentimento pela última vez.

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB TCF do IAB 2.0]

### Objeto `consent` padrão IAB TCF 2.0

Para registrar as preferências de consentimento do usuário fornecidas por meio do padrão Estrutura de transparência e consentimento (TCF) do Interative Advertising Bureau Europe (IAB), defina a string de consentimento como mostrado abaixo.

Quando o consentimento é definido dessa forma, o Perfil do cliente em tempo real é atualizado com as informações de consentimento. Para que isso funcione, o esquema XDM do perfil precisa conter o [grupo de campos de esquema Privacidade do perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Ao enviar eventos, as informações de consentimento do IAB precisam ser adicionadas manualmente ao objeto XDM do evento. O Web SDK não inclui automaticamente as informações de consentimento nos eventos.

Para enviar as informações de consentimento nos eventos, você deve adicionar o grupo de campos Privacidade de eventos de experiência ao esquema [!DNL Profile] habilitado para [!DNL XDM ExperienceEvent]. Consulte a seção sobre [atualização do esquema ExperienceEvent](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema) no guia de preparação do conjunto de dados para obter etapas sobre como configurar isso.

* **`standard`**: o padrão de consentimento escolhido. Defina essa propriedade como `"IAB TCF"` para o padrão IAB TCF 2.0.
* **`version`**: uma cadeia de caracteres que representa a versão do padrão de consentimento. Defina essa propriedade como `"2.0"` para o padrão IAB TCF 2.0.
* **`value`**: uma cadeia de caracteres que contém o valor de consentimento.
* **`gdprApplies`**: um booleano que determina se o GDPR se aplica a este valor de consentimento. Seu valor padrão é `true`.
* **`gdprContainsPersonalData`**: um booleano que determina se os dados do evento associados a este usuário contêm dados pessoais. Seu valor padrão é `false`.

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

A API da TCF do IAB 2.0 fornece um evento para quando o consentimento é atualizado pelo cliente. Isso ocorre quando o cliente define inicialmente suas preferências e quando o cliente atualiza suas preferências. Você pode adicionar um ouvinte de eventos para executar o comando `setConsent`:

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

O bloco de código acima escuta o evento `useractioncomplete` e define o consentimento, transmitindo a cadeia de consentimento e o sinalizador `gdprApplies`. Se você tiver identidades personalizadas para seus clientes, preencha a variável `identityMap`.

>[!TAB Adobe 1.0]

### Objeto `consent` padrão do Adobe 1.0

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"Adobe"` para o padrão Adobe 1.0.
* **`version`**: uma cadeia de caracteres que representa a versão do padrão de consentimento. Defina esta propriedade como `"1.0"` para o padrão Adobe 1.0.
* **`value.general`**: o valor de consentimento. Defina como `"in"` quando os usuários optarem por entrar e como `"out"` quando os usuários optarem por não participar.

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### Envio de vários padrões em uma solicitação {#multiple-standards}

O Web SDK também permite enviar mais de um objeto de consentimento em uma solicitação, conforme mostrado no exemplo abaixo.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## Persistência das preferências de consentimento {#persistence}

Depois de comunicar as preferências do usuário ao Web SDK usando o comando `setConsent`, o SDK mantém as preferências do usuário para um cookie. Na próxima vez que o usuário carregar o site no navegador, o Web SDK recuperará e usará essas preferências persistentes para determinar se os eventos podem ou não ser enviados para o Adobe.

Armazenar as preferências do usuário de forma independente para que você possa mostrar a caixa de diálogo de consentimento com as preferências atuais. Não há como recuperar as preferências do usuário no Web SDK. Para garantir que as preferências do usuário permaneçam sincronizadas com o SDK, você pode chamar o comando `setConsent` em cada carregamento de página. O Web SDK só faz uma chamada de servidor se as preferências forem alteradas.

## Definir consentimento usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente a este comando é a ação [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md).
