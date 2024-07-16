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

O Adobe Experience Platform Web SDK oferece suporte à capacidade de declarar IDs do cliente e seus estados de autenticação por meio do comando [sendEvent](./overview.md#syncing-identities).

Escolha seus namespaces nos [Namespaces do Serviço de Identidade](../../identity/../identity-service/features/namespaces.md) para indicar o contexto ao qual uma identidade está relacionada, usando os valores na coluna Símbolo de Identidade:

![Exibição da interface do Namespaces](../assets/identity/edge_namespaceUI_identity-symbol.png)

Como cliente do Audience Manager, todas as Fontes de dados existentes que usam o Tipo de ID: entre dispositivos têm automaticamente um Namespace de identidade correspondente. Para localizar o Namespace de identidade correspondente ao seu Audience Manager Data Source, faça logon no Adobe Experience Platform e navegue até a seção Identidades.

Qualquer novo Source de Dados [!DNL Audience Manager] que use o Tipo de ID: Entre Dispositivos gerará um Namespace de Identidade correspondente. Os tipos de dados Source ID Cookie e Device Advertising ID não são suportados no momento. Além disso, qualquer Namespace de identidade criado no Adobe Experience Platform gerará um Source de dados [!DNL Audience Manager] correspondente, mas observe que o método syncIdentity suporta apenas Símbolos de identidade de namespace.
