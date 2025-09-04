---
title: sendPushSubscription
description: Registre assinaturas de notificação por push com o Adobe Experience Platform.
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
> As notificações por push para o Web SDK estão atualmente em **beta**. A funcionalidade e a documentação podem mudar.

O comando `sendPushSubscription` registra assinaturas de notificação por push com o Adobe Experience Platform. Esse comando manipula a recuperação dos detalhes da assinatura push do navegador e os envia para o fluxo de dados configurado.

## Pré-requisitos {#prerequisites}

Antes de usar o `sendPushSubscription`, verifique se você tem:

1. **Notificações por push configuradas**: configure a propriedade de configuração [`pushNotifications`](configure/pushnotifications.md) com sua chave pública VAPID
2. **Permissão de usuário**: os usuários devem ter concedido permissão de notificação (`Notification.permission === "granted"`)
3. **Service worker**: um service worker registrado deve estar disponível no site
4. **Suporte ao Push Manager**: o navegador deve aceitar notificações por push e ter a API do PushManager disponível

## Registrar assinatura push usando a extensão de tag do Web SDK {#register-push-subscription-tag-extension}

O envio de dados de subscrição por push é executado como uma ação em uma regra na interface Tags da coleção de dados da Adobe Experience Platform.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar Assinatura por Push]**.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

## Registrar assinatura push usando a biblioteca JavaScript do Web SDK {#register-push-subscription-javascript}

Execute o comando `sendPushSubscription` ao chamar a instância configurada do Web SDK. Chame o comando [`configure`](configure/overview.md) com notificações por push configuradas antes de chamar o comando `sendPushSubscription`.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Frequência de execução recomendada {#recommended-execution-frequency}

Para obter a funcionalidade ideal de notificação por push, a Adobe recomenda executar o comando `sendPushSubscription` **uma vez por dia**. Isso garante que:

- Os detalhes da assinatura permanecem atuais no Adobe Experience Platform
- Todas as alterações nos tokens de push ou no status da assinatura são capturadas
- O perfil do usuário permanece atualizado com as preferências de notificação por push mais recentes

Você pode implementar isso usando uma abordagem semelhante à abaixo:

```js
// Check if we've sent subscription data today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Como funciona {#how-it-works}

O comando `sendPushSubscription` executa as seguintes ações:

1. **Valida pré-requisitos**: verifica se as notificações por push estão configuradas e se a permissão de usuário foi concedida
2. **Aguarda identidade**: aguarda a ECID do usuário estar disponível
3. **Recupera a assinatura**: obtém a assinatura push ativa do service worker usando a chave VAPID configurada
4. **Verificações de alterações**: compara os detalhes da assinatura atual com os valores em cache (ECID + detalhes da assinatura). Se os detalhes da assinatura não tiverem sido alterados, o comando registrará uma mensagem de informações e retornará sem fazer uma solicitação de rede
5. **Envia para a sequência de dados**: se forem detectadas alterações, transmitirá os dados da assinatura para a sequência de dados configurada do Adobe Experience Platform
6. **Atualiza o cache**: armazena os detalhes da nova assinatura para comparação futura

## Tratamento de erros {#error-handling}

Condições de erro comuns e suas mensagens:

| Erro | Causa |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | Configuração de pushNotifications ausente ou inválida |
| `"Service workers are not supported in this browser."` | O navegador não oferece suporte a trabalhadores de serviço |
| `"Push notifications are not supported in this browser."` | O navegador não é compatível com notificações por push ou API de notificação |
| `"The user has not given permission to send push notifications."` | O usuário não concedeu permissão para notificação |
| `"No service worker registration was found."` | Nenhum trabalhador de serviço está registrado para a origem atual |
| `"No VAPID public key was provided."` | A chave pública VAPID está ausente da configuração |

## Carga de dados {#data-payload}

O comando envia dados de notificação por push no seguinte formato:

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Documentação relacionada

- [Configurar notificações por push](configure/pushnotifications.md)
- [Especificação da API de push da Web](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
- [API do Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
