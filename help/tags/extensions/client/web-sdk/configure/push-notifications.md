---
title: Configurações de notificação por push
description: Defina as configurações de notificação por push para a extensão de tag do Web SDK.
source-git-commit: 0b3f4ec51cac182b637c79b9fcb883e5f8f78d02
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Configurações de notificação por push

>[!AVAILABILITY]
>
>As notificações por push para o Web SDK estão atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

Esta seção de configuração permite definir uma chave pública VAPID para autenticação de notificação por push.

>[!NOTE]
>
>Primeiro, este recurso deve ser habilitado com o uso de [Componentes de compilação personalizados](custom-build-components.md); ele é desabilitado por padrão.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e clique em **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Expanda **[!UICONTROL Custom build components]** e habilite **[!UICONTROL Push notifications]**.
1. Em [!UICONTROL SDK instances], role para baixo para localizar a seção [!UICONTROL Push Notifications].
1. Insira sua chave pública VAPID no campo **[!UICONTROL VAPID Public Key]**.

![Imagem mostrando configurações de notificações por push usando a extensão de marca Web SDK](../assets/push-notifications.png)

Os seguintes campos estão disponíveis:

## [!UICONTROL VAPID public key]

A chave pública VAPID usada para assinaturas push. É uma string codificada na Base64.

## [!UICONTROL Application ID]

A ID do aplicativo associada à chave pública VAPID.

## [!UICONTROL Tracking dataset ID]

A ID do conjunto de dados para rastreamento e análise de notificação por push.

## Notificações por push usando a biblioteca do JavaScript

Esta seção é o equivalente da tag [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) ao configurar a biblioteca JavaScript. A página vinculada também fornece informações sobre pré-requisitos e a geração de uma chave pública VAPID.
