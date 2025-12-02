---
title: Enviar assinatura por push
description: Registre, envie e colete dados para assinaturas por push do navegador.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# Enviar assinatura por push

>[!AVAILABILITY]
>
>As notificações por push para o Web SDK estão atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

A ação **[!UICONTROL Send push subscription]** registra assinaturas de notificação por push com o Adobe Experience Platform. Ela lida com a recuperação de detalhes da assinatura push do navegador e os envia para o fluxo de dados configurado. Ela está disponível na extensão do Web SDK versão 2.32.0 ou posterior.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action Type] como **[!UICONTROL Send push subscription]**.

A ação não tem configurações além da seleção de uma instância do SDK.

Defina uma [chave pública VAPID](../configure/push-notifications.md) válida ao configurar a extensão antes de usar este comando.

Esta ação é a extensão de marca equivalente ao comando [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md). Consulte a página vinculada para obter informações sobre pré-requisitos, frequência de execução recomendada, como o comando funciona e tratamento de erros.

>[!MORELIKETHIS]
>
>* [Configurar notificações por push](../configure/push-notifications.md)
>* [Especificação da API de push da Web](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [API do Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
