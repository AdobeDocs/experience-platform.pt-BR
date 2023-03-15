---
title: Logon do lado do servidor para dados do A4T no SDK da Web da plataforma
description: Saiba como ativar o registro do lado do servidor para o Adobe Analytics for Target (A4T) usando o SDK da Web do Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;destino;web;sdk;plataforma;registro;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Logon do lado do servidor para dados do A4T no SDK da Web da plataforma

O SDK da Web da Adobe Experience Platform permite implementar a funcionalidade Adobe Analytics for Target (A4T) na Platform Edge Network. Quando o registro no lado do servidor estiver ativado, todas as ocorrências do Analytics enviadas pela Rede de borda são aumentadas com detalhes do Target no lado do servidor, sem precisar passar pelo processo de compilação de ocorrências.

O registro do lado do servidor para o Analytics é ativado quando o Analytics é ativado na configuração da sequência de dados:

![Configuração de sequência de dados do Analytics ativada](../assets/enable-analytics-datastream.png)

O diagrama a seguir mostra como os dados fluem pelo sistema quando o log do Analytics no lado do servidor está ativado:

![Fluxo de log do lado do servidor](../assets/analytics-server-side-logging.png)

## Próximas etapas

Este guia abordou o registro no lado do servidor para dados do A4T no SDK da Web. Consulte o guia sobre [registro do lado do cliente](./client-side.md) para obter mais informações sobre como lidar com dados do A4T no lado do cliente.
