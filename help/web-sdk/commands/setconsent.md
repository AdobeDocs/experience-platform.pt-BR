---
title: setConsent
description: Usado em cada página para rastrear as preferências de consentimento dos usuários.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# `setConsent`

A variável `setConsent` informa ao SDK da Web se ele deve enviar dados (aceitação), descartar dados (recusa) ou usar [`defaultConsent`](configure/defaultconsent.md) (consentimento desconhecido).

O SDK da Web é compatível com os seguintes padrões:

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: os padrões 1.0 e 2.0 são compatíveis.
* **[Estrutura de transparência e consentimento do IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Se você usar esse padrão, o Perfil de cliente em tempo real do visitante será atualizado com as informações de consentimento se a implementação estiver configurada corretamente:
   1. O esquema de perfil individual XDM contém a variável [Grupo de campos de consentimento da TCF 2.0 do IAB](/help/xdm/field-groups/profile/iab.md).
   1. O esquema Evento de experiência contém a variável [Grupo de campos de consentimento da TCF 2.0 do IAB](/help/xdm/field-groups/event/iab.md).
   1. Você inclui as informações de consentimento do IAB no evento [Objeto XDM](sendevent/xdm.md). O SDK da Web não inclui automaticamente as informações de consentimento ao enviar dados do evento.

Após usar esse comando, o SDK da Web grava as preferências do usuário em um cookie. Na próxima vez que o usuário carregar o site no navegador, o SDK recuperará essas preferências persistentes para determinar se os eventos podem ser enviados para o Adobe.

A Adobe recomenda que você armazene todas as preferências da caixa de diálogo de consentimento separadamente do consentimento do SDK da Web. O SDK da Web não oferece uma maneira de recuperar o consentimento. Para garantir que as preferências do usuário permaneçam sincronizadas com o SDK, você pode chamar o `setConsent` em cada carregamento de página. O SDK da Web só faz uma chamada de servidor quando o consentimento é alterado.

## Usar `defaultConsent` juntamente com `setConsent` {#using-consent}

O SDK da Web oferece dois comandos complementares de configuração de consentimento:

* [`defaultConsent`](configure/defaultconsent.md): este comando destina-se a capturar as preferências de consentimento dos clientes do Adobe que usam o SDK da Web.
* [`setConsent`](setconsent.md): este comando destina-se a capturar as preferências de consentimento dos visitantes do site.

Quando usadas juntas, essas configurações podem levar a diferentes resultados de coleta de dados e configuração de cookie, dependendo de seus valores configurados.

Consulte a tabela abaixo para entender quando ocorre a coleta de dados e quando os cookies são definidos, com base nas configurações de consentimento.

| defaultConsent | setConsent | Ocorre a coleta de dados | O SDK da Web define cookies do navegador |
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
| **AMCV_###@AdobeOrg** | 34128000 (395 dias) | Apresentar quando [`idMigrationEnabled`](configure/idmigrationenabled.md) está ativado. Ajuda na transição para o SDK da Web enquanto algumas partes do site ainda usam `visitor.js`. |
| **Cookie demdex** | 15552000 (180 dias) | Apresentar se a sincronização de ID estiver habilitada. O Audience Manager define este cookie para atribuir um identificador exclusivo a um visitante do site. O cookie demdex ajuda o Audience Manager a executar funções básicas, como a identificação do visitante, a sincronização de ID, a segmentação, a modelagem, a geração de relatórios etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutos) | Armazena a região do Edge Network que atende às solicitações do usuário atual. A região é usada no caminho do URL para que o Edge Network possa rotear a solicitação para a região correta. Se um usuário se conectar com um endereço IP diferente ou em uma sessão diferente, a solicitação será roteada novamente para a região mais próxima. |
| **kndct_orgid_identity** | 34128000 (395 dias) | Armazena a ECID, bem como outras informações relacionadas à ECID. |
| **kndctr_orgid_consent** | 15552000 (180 dias) | Armazena a preferência de consentimento dos usuários para o site. |
| **s_ecid** | 63115200 (2 anos) | Contém uma cópia da ID do Experience Cloud ([!DNL ECID]) ou MID. A MID é armazenada em um par de valores chave que segue a sintaxe `s_ecid=MCMID\|<ECID>`. |

## Definir o consentimento usando a extensão de tag do SDK da Web

A configuração do consentimento é executada como uma ação em uma regra na interface das tags da Coleção de dados da Adobe Experience Platform.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Definir consentimento]**.
1. Defina os campos desejados à direita, incluindo **[!UICONTROL Padrão]** e **[!UICONTROL Consentimento geral]**.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

Você pode incluir vários objetos de consentimento nesta ação.

## Definir o consentimento usando a biblioteca JavaScript do SDK da Web

Execute o `setConsent` ao chamar a instância configurada do SDK da Web. Você pode incluir os seguintes objetos nesse comando:

* **`consent[]`**: uma matriz de `consent` objetos. O objeto de consentimento é formatado de forma diferente dependendo do padrão e da versão escolhidos. Consulte as guias abaixo para obter exemplos de cada objeto de consentimento, dependendo do padrão de consentimento.
* **`identityMap`**: um objeto que controla como uma ECID é gerada e a quais IDs as informações de consentimento estão vinculadas. O Adobe recomenda incluir este objeto quando `setConsent` é executado antes de outros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: um objeto que contém [substituições de configuração da sequência de dados](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 padrão `consent` objeto

Se você estiver usando o Adobe Experience Platform, precisará incluir um grupo de campos de esquema de privacidade no esquema do perfil. Consulte [Governança, privacidade e segurança no Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) para obter mais informações sobre o padrão Adobe 2.0. Você pode adicionar dados dentro do objeto de valor abaixo correspondente ao esquema da variável `consents` do campo [!UICONTROL Consentimentos e preferências] grupo de campos de perfil.

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"Adobe"` para o padrão Adobe 2.0.
* **`version`**: uma string que representa a versão do padrão de consentimento. Defina esta propriedade como `"2.0"` para o padrão Adobe 2.0.
* **`value`**: um objeto que contém valores de consentimento.
   * **`value.collect.val`**: o valor de consentimento. Defina isso como `"y"` quando os usuários optam por entrar e `"n"` quando os usuários optam por não participar.
   * **`value.metadata.time`**: o carimbo de data e hora em que os usuários atualizaram as configurações de consentimento pela última vez.

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

### IAB TCF 2.0 padrão `consent` objeto

Para registrar as preferências de consentimento do usuário fornecidas por meio do padrão Estrutura de transparência e consentimento (TCF) do Interative Advertising Bureau Europe (IAB), defina a cadeia de consentimento como mostrado abaixo.

Quando o consentimento é definido dessa forma, o Perfil do cliente em tempo real é atualizado com as informações de consentimento. Para que isso funcione, o esquema XDM do perfil precisa conter a variável [Grupo de campos de esquema de privacidade de perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Ao enviar eventos, as informações de consentimento do IAB precisam ser adicionadas manualmente ao objeto XDM do evento. O SDK da Web não inclui automaticamente as informações de consentimento nos eventos.

Para enviar as informações de consentimento nos eventos, você deve adicionar o grupo de campos Privacidade de evento de experiência ao seu [!DNL Profile]-habilitado [!DNL XDM ExperienceEvent] esquema. Consulte a seção sobre [atualização do esquema ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) no guia de preparação do conjunto de dados, para obter etapas sobre como configurar isso.

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"IAB TCF"` para o padrão IAB TCF 2.0.
* **`version`**: uma string que representa a versão do padrão de consentimento. Defina esta propriedade como `"2.0"` para o padrão IAB TCF 2.0.
* **`value`**: uma string que contém o valor de consentimento.
* **`gdprApplies`**: um booleano que determina se o GDPR se aplica a esse valor de consentimento. Seu valor padrão é `true`.
* **`gdprContainsPersonalData`**: um booleano que determina se os dados do evento associados a esse usuário contêm dados pessoais. Seu valor padrão é `false`.

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

>[!TAB Adobe 1.0]

### Adobe 1.0 padrão `consent` objeto

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"Adobe"` para o padrão Adobe 1.0.
* **`version`**: uma string que representa a versão do padrão de consentimento. Defina esta propriedade como `"1.0"` para o padrão Adobe 1.0.
* **`value.general`**: o valor de consentimento. Defina isso como `"in"` quando os usuários optam por entrar e `"out"` quando os usuários optam por não participar.

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

O SDK da Web também permite enviar mais de um objeto de consentimento em uma solicitação, como mostrado no exemplo abaixo.

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
                time: "2021-03-17T15:48:42-07:00"
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

Depois de comunicar as preferências do usuário ao SDK da Web usando o `setConsent` , o SDK mantém as preferências do usuário em um cookie. Na próxima vez que o usuário carregar o site no navegador, o SDK da Web recuperará e usará essas preferências persistentes para determinar se os eventos podem ou não ser enviados para o Adobe.

Você precisará armazenar as preferências do usuário independentemente para poder mostrar a caixa de diálogo de consentimento com as preferências atuais. Não há como recuperar as preferências do usuário no SDK da Web. Para garantir que as preferências do usuário permaneçam sincronizadas com o SDK, você pode chamar o `setConsent` em cada carregamento de página. O SDK da Web só fará uma chamada de servidor se as preferências tiverem sido alteradas.

## Sincronização de identidades ao definir o consentimento {#sync-identities}

Quando o consentimento padrão (definido por meio do [defaultConsent](configure/defaultconsent.md) parameter) estiver definido como `pending` ou `out`, o `setConsent` configurar pode ser a primeira solicitação que sai e estabelece a identidade. Por isso, pode ser importante sincronizar identidades na primeira solicitação. É possível adicionar o mapa de identidade à variável `setConsent` exatamente como no `sendEvent` comando. Consulte [uso do identityMap](../identity/overview.md#using-identitymap) para obter um exemplo de como incluir o mapa de identidade no comando.
