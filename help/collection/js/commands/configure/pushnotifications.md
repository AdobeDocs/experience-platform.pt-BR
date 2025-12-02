---
title: notificações por push
description: Configure notificações por push para que o Web SDK ative as mensagens por push baseadas em navegador.
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>As notificações por push para o Web SDK estão atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

A propriedade `pushNotifications` permite configurar notificações por push para aplicativos web. Esse recurso permite que o aplicativo web receba mensagens enviadas por um servidor, mesmo quando o site não estiver carregado no navegador.

## Pré-requisitos {#prerequisites}

Antes de configurar notificações por push, verifique se você tem:

1. **Permissão de usuário**: os usuários devem conceder permissão para notificações explicitamente
2. **Service worker**: um service worker registrado é necessário para que as notificações por push funcionem
3. **Chaves VAPID**: gerar chaves VAPID (Identificação Voluntária do Servidor de Aplicativos) para comunicação segura
4. **ID do Aplicativo**: a ID do aplicativo usada ao salvar as chaves VAPID dentro do Adobe Journey Optimizer -> Canais -> Configurações de push -> Credenciais de push
5. **ID do conjunto de dados de rastreamento**: a ID do conjunto de dados do sistema com o nome &quot;Conjunto de Dados de Evento de Experiência de Rastreamento por Push do AJO&quot;. Obtenha isso da Adobe Journey Optimizer -> Conjuntos de dados

## Gerar chaves VAPID {#generate-vapid-keys}

Para gerar chaves VAPID, instale o pacote NPM `web-push` e execute:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Essa ação gera um par de chaves públicas e privadas. Use a chave pública na configuração do Web SDK e armazene a chave privada no canal de notificações por push do Adobe Journey Optimizer.

## Instalar o service worker

O código do service worker deve ser distribuído a partir do mesmo domínio que o site. Baixe o código do service worker do CDN da Adobe e hospede o arquivo do JavaScript em seu próprio servidor. O código do service worker do Web SDK está disponível usando a seguinte estrutura de URL:

- **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Cheio**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Este é um exemplo de como instalar o service worker:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Implementação

Definir o objeto `pushNotifications` ao executar o comando `configure`:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Propriedades {#properties}

| Propriedade | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| **`vapidPublicKey`** | String | Sim | A chave pública VAPID usada para assinaturas push. Deve ser uma cadeia de caracteres codificada na Base64. |
| **`applicationId`** | String | Sim | A ID do aplicativo associada à chave pública VAPID. |
| **`trackingDatasetId`** | String | Sim | A ID do conjunto de dados do sistema usada para rastreamento de notificação por push. |

## Considerações importantes {#important-considerations}

- **Segurança**: as assinaturas por push estão vinculadas à chave pública VAPID específica usada durante a assinatura. Se você alterar as chaves VAPID, as assinaturas existentes serão automaticamente canceladas e recriadas com a nova chave.
- **Armazenamento em cache**: o Web SDK gerencia automaticamente as atualizações de assinatura comparando a ECID atual e os detalhes de assinatura com os valores em cache. Os dados de assinatura são enviados somente quando alterações são detectadas.
- **Requisito do service worker**: as notificações por push exigem um service worker registrado. Verifique se o service worker está configurado corretamente para lidar com eventos de push.

## Configurar notificações por push usando a extensão de tag do Web SDK {#configure-push-notifications-tag-extension}

A extensão de tag do Web SDK equivalente a esta propriedade é a seção [[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) ao configurar a extensão.

## Próximas etapas {#next-steps}

Após configurar as notificações por push, use o comando [sendPushSubscription](../sendpushsubscription.md) para registrar assinaturas por push com o Adobe Experience Platform.
