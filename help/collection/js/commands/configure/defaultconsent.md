---
title: defaultConsent
description: Defina o método de coleta de consentimento padrão para a propriedade da Web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# `defaultConsent`

A propriedade `defaultConsent` determina como você lida com o consentimento da coleta de dados antes de chamar o comando [`setConsent`](../setconsent.md). Essa propriedade é importante quando você não deseja coletar dados acidentalmente de indivíduos que residem em áreas onde o consentimento é necessário antes de coletar dados.

Se você tiver um visitante que não esteja na jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão poderá ser definido como `in`. Os visitantes dentro da jurisdição do GDPR podem ter seu consentimento padrão definido como `pending`. Sua Plataforma de Gerenciamento de Consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para a TCF 2.0 do IAB. Esse sinalizador pode ser usado para definir o consentimento padrão.

Defina a propriedade da cadeia de caracteres `defaultConsent` com o nível de consentimento desejado ao executar o comando `configure`. Esta propriedade diferencia maiúsculas e minúsculas e oferece suporte apenas aos três valores a seguir: `"in"`, `"out"` e `"pending"`. Se você tentar usar qualquer outro valor, a biblioteca emitirá um erro. Se não estiver definido no comando `configure`, o valor padrão será **`in`**.

>[!IMPORTANT]
>
>O valor `defaultConsent` não persiste entre os carregamentos de página. Defina o consentimento padrão desejado sempre que chamar o comando `configure`. Por outro lado, o consentimento resolvido de um visitante (definido por meio do [`setConsent`](../setconsent.md)) é mantido em um cookie e aplicado automaticamente em carregamentos de páginas subsequentes.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: A coleta de dados opera normalmente até que o usuário opte por não participar.
* **`out`**: os dados são descartados permanentemente até que o usuário opte por entrar.
* **`pending`**: os dados são armazenados localmente até que o usuário opte por usar o comando [`setConsent`](../setconsent.md).

>[!NOTE]
>
>Embora a Adobe planeje criar um conjunto mais robusto de finalidades ou categorias que correspondam aos recursos e ofertas de produtos da Adobe, a implementação atual é uma abordagem do tipo &quot;tudo ou nada&quot; para a aceitação. Essa limitação se aplica somente ao Web SDK e não a outras bibliotecas JavaScript do Adobe.

## Usando `defaultConsent` junto com `setConsent` {#using-consent}

Quando usados em conjunto, o `defaultConsent` e o `setConsent` produzem coleta de dados, configuração de cookie e resultados de identidade diferentes, dependendo de seus valores configurados. Consulte [Consentimento e identidade na Coleção de dados](/help/collection/identity/consent.md#how-consent-affects-identity) para obter uma tabela de interação completa.

## Definindo consentimento padrão com base em `gdprApplies`

Algumas CMPs fornecem a capacidade de determinar se o Regulamento Geral sobre a Proteção de Dados (GDPR) se aplica ao cliente. Se você quiser assumir o consentimento para clientes aos quais o GDPR não se aplica, poderá usar o sinalizador `gdprApplies` em uma chamada de API TCF. Por exemplo:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

No bloco de código acima, o comando `configure` é chamado depois que `tcData` é obtido da API TCF. Se `gdprApplies` for verdadeiro, o consentimento padrão será definido como `pending`. Se `gdprApplies` for falso, o consentimento padrão será definido como `in`. Preencha a variável `alloyConfiguration` com sua configuração.

## Consentimento padrão usando a extensão de tag do Web SDK

Consulte [Configurações de consentimento](/help/tags/extensions/client/web-sdk/configure/consent.md) na documentação da extensão de tag do Web SDK para saber como executar essas ações usando tags.
