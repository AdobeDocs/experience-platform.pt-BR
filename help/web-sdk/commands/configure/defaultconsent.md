---
title: defaultConsent
description: Defina o método de coleta de consentimento padrão.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

A variável `defaultConsent` determina como você lida com o consentimento da coleta de dados antes de chamar a [`setConsent`](../setconsent.md) comando. Essa propriedade é importante quando você não deseja coletar dados acidentalmente de indivíduos que residem em áreas onde o consentimento é necessário antes de coletar dados.

Essa propriedade permite três valores:

* **Entrada**: a coleta de dados continua normalmente, até que o usuário opte por não participar.
* **Saída**: os dados são descartados permanentemente até que o usuário opte por entrar.
* **Pending**: os dados são armazenados localmente até que o usuário opte por usar o [`setConsent`](../setconsent.md) comando. Os dados não persistem entre os carregamentos de página.

Se você tiver um visitante que não esteja na jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão poderá ser definido como `in`. Os visitantes dentro da jurisdição do GDPR podem ter seu consentimento padrão definido como `pending`. Sua Plataforma de gerenciamento de consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para o IAB TCF 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão.

## Definir o consentimento padrão usando a extensão de tag do SDK da Web

Selecione o botão de opção desejado em **[!UICONTROL Consentimento padrão]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Privacidade] e selecione a opção desejada **[!UICONTROL Consentimento padrão]**.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Definir o consentimento padrão usando a biblioteca JavaScript do SDK da Web

Defina o `defaultConsent` para o nível de consentimento desejado ao executar a variável `configure` comando. Essa propriedade diferencia maiúsculas e minúsculas e oferece suporte apenas aos três valores a seguir: `"in"`, `"out"`, e `"pending"`. Se você tentar usar qualquer outro valor, a biblioteca emitirá um erro.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
