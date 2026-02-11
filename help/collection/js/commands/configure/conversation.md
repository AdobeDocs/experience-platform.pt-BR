---
title: conversa
description: Defina as configurações de chat do Brand Concierge.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 4%

---

# `conversation`

>[!AVAILABILITY]
>
>O Brand Concierge para o Web SDK está atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

O objeto `conversation` contém opções de configuração para sessões de chat do Brand Concierge. Esse objeto tem suporte nas versões 2.31.0 ou posteriores do Web SDK.

## Propriedades

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| **`stickyConversationSession`** | `boolean` | Determina se o Web SDK define um cookie de sessão para preservar as sessões de chat do Brand Concierge em carregamentos de página. O padrão é `false`. Se omitido ou definido como `false`, o chat do Brand Concierge inicia uma nova sessão a cada carregamento de página. |

## Exemplo

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    stickyConversationSession: true
  }
});
```

## Definir configurações de conversa usando a extensão de tag do Web SDK

Essas configurações podem ser definidas na extensão de tag do Web SDK usando [configurações do Brand Concierge](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
