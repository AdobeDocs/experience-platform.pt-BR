---
title: setConsent
description: Usado em cada página para rastrear o consentimento do usuário.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

A variável `setConsent` informa ao SDK da Web se ele deve enviar dados (aceitação), descartar dados (recusa) ou usar [`defaultConsent`](configure/defaultconsent.md) (consentimento desconhecido).

O SDK da Web é compatível com os seguintes padrões:

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: os padrões 1.0 e 2.0 são compatíveis.
* **[Estrutura de transparência e consentimento do IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Se você usar esse padrão, o Perfil de cliente em tempo real do visitante será atualizado com as informações de consentimento se a implementação estiver configurada corretamente:
   1. O esquema de perfil individual XDM contém a variável [Grupo de campos de consentimento da TCF 2.0 do IAB](/help/xdm/field-groups/profile/iab.md).
   1. O esquema Evento de experiência contém a variável [Grupo de campos de consentimento da TCF 2.0 do IAB](/help/xdm/field-groups/event/iab.md).
   1. Você inclui as informações de consentimento do IAB no evento [Objeto XDM](sendevent/xdm.md). O SDK da Web não inclui automaticamente as informações de consentimento ao enviar dados do evento.

Após usar esse comando, o SDK da Web grava as preferências do usuário em um cookie. Na próxima vez que o usuário carregar o site no navegador, o SDK recuperará essas preferências persistentes para determinar se os eventos podem ser enviados para o Adobe.

A Adobe recomenda que você armazene todas as preferências da caixa de diálogo de consentimento separadamente do consentimento do SDK da Web. O SDK da Web não oferece uma maneira de recuperar o consentimento. Para garantir que as preferências do usuário permaneçam sincronizadas com o SDK, você pode chamar o `setConsent` em cada carregamento de página. O SDK da Web só faz uma chamada de servidor quando o consentimento é alterado.

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

* **`consent[]`**: uma matriz de `consent` objetos. O objeto de consentimento é formatado de forma diferente dependendo do padrão e da versão escolhidos.
* **`identityMap`**: um objeto que controla como uma ECID é gerada e a quais IDs as informações de consentimento estão vinculadas. O Adobe recomenda incluir este objeto quando `setConsent` é executado antes de outros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: um objeto que contém [substituições de configuração da sequência de dados](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 padrão `consent` objeto

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"Adobe"` para o padrão Adobe 2.0.
* **`version`**: uma string que representa a versão do padrão de consentimento. Defina esta propriedade como `"2.0"` para o padrão Adobe 2.0.
* **`value`**: um objeto que contém valores de consentimento.
   * **`value.collect.val`**: o valor de consentimento. Os valores válidos são `"y"` (aceitação) e `"n"` (opt out).
   * **`value.metadata.time`**: o carimbo de data e hora em que o usuário definiu o valor de consentimento.

```js
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

* **`standard`**: o padrão de consentimento escolhido. Defina esta propriedade como `"IAB TCF"` para o padrão IAB TCF 2.0.
* **`version`**: uma string que representa a versão do padrão de consentimento. Defina esta propriedade como `"2.0"` para o padrão IAB TCF 2.0.
* **`value`**: uma string que contém o valor de consentimento.
* **`gdprApplies`**: um booleano que determina se o GDPR se aplica a esse valor de consentimento. Seu valor padrão é `true`.
* **`gdprContainsPersonalData`**: um booleano que determina se os dados do evento associados a esse usuário contêm dados pessoais. Seu valor padrão é `false`.

```js
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
* **`value.general`**: o valor de consentimento. Os valores válidos são `"in"` (aceitação) e `"out"` (opt out).

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
