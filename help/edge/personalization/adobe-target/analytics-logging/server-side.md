---
title: Registro do lado do servidor para dados A4T no SDK da Web da plataforma
description: Saiba como habilitar o registro do lado do servidor para o Adobe Analytics for Target (A4T) usando o SDK da Web do Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t; target; web; sdk; plataforma; registro;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Registro do lado do servidor para dados A4T no SDK da Web da plataforma

O SDK da Web da Adobe Experience Platform permite implementar a funcionalidade Adobe Analytics for Target (A4T) na Rede de borda da plataforma. Quando o registro no lado do servidor é ativado, todas as ocorrências do Analytics enviadas pela Edge Network são aumentadas com os detalhes do Target no lado do servidor, sem precisar passar pelo processo de identificação de ocorrências.

O registro do lado do servidor para o Analytics é ativado quando o Analytics é ativado na configuração do conjunto de dados:

![Configuração de armazenamento de dados do Analytics habilitada](../assets/enable-analytics-datastream.png)

O diagrama a seguir mostra como os dados fluem pelo sistema quando o Registro de análises do servidor está ativado:

![Fluxo de registro do lado do servidor](../assets/analytics-server-side-logging.png)

## Próximas etapas

Este guia cobriu o registro do lado do servidor para dados A4T no SDK da Web. Consulte o guia sobre [registro no lado do cliente](./client-side.md) para obter mais informações sobre como lidar com dados do A4T no lado do cliente.
