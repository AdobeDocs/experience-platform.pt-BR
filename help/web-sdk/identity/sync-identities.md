---
title: Sincronização de identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
description: Saiba como sincronizar identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identidades;sincronizar identidades;namespace;audience manager;aam;identities;sync identities;namespace;
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Sincronização de identidades entre Audience Manager e Experience Platform

O SDK da Web da Adobe Experience Platform é compatível com a capacidade de declarar IDs do cliente e seus estados de autenticação por meio do [sendEvent](./overview.md#syncing-identities) comando.

Escolha seus namespaces na [Namespaces do serviço de identidade](../../identity/../identity-service/features/namespaces.md) para indicar o contexto ao qual uma identidade está relacionada, usando os valores da coluna Símbolo de Identidade:

![Exibição da interface do Namespaces](../assets/identity/edge_namespaceUI_identity-symbol.png)

Como cliente do Audience Manager, todas as Fontes de dados existentes que usam o Tipo de ID: entre dispositivos têm automaticamente um Namespace de identidade correspondente. Para localizar o Namespace de identidade correspondente à sua Fonte de dados do Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades.

Qualquer novo [!DNL Audience Manager] Fonte de dados que usa o tipo de ID: o entre dispositivos gerará um namespace de identidade correspondente. No momento, não há suporte para os tipos de ID de fonte de dados Cookie e ID de anúncio de dispositivo. Além disso, qualquer namespace de identidade criado no Adobe Experience Platform gerará um [!DNL Audience Manager] Fonte de dados, mas observe que o método syncIdentity é compatível apenas com Símbolos de identidade de namespace.
