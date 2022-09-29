---
title: Sincronização de identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
description: Saiba como sincronizar identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager; aam; identidades; sincronizar identidades; namespace;
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Sincronização de identidades entre o Audience Manager e o Experience Platform

O SDK da Web da Adobe Experience Platform oferece suporte à capacidade de declarar IDs do cliente e seus estados de autenticação por meio do [sendEvent](./overview.md#syncing-identities) comando.

Escolha seus namespaces no [Namespaces do serviço de identidade](../../identity/../identity-service/namespaces.md) para indicar o contexto ao qual uma identidade está relacionada, usando os valores na coluna Símbolo de identidade:

![Exibição da interface do usuário do Namespaces](../assets/identity/edge_namespaceUI_identity-symbol.png)

Como cliente do Audience Manager, todas as suas fontes de dados existentes que usam o Tipo de ID: O Cross-Device tem automaticamente um Namespace de identidade correspondente. Para encontrar o Namespace de identidade correspondente para sua Fonte de dados do Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades .

Qualquer novo [!DNL Audience Manager] Fonte de dados que usa o Tipo de ID: O Cross-Device gerará um Namespace de identidade correspondente. No momento, o cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são compatíveis. Além disso, qualquer Namespace de identidade criado no Adobe Experience Platform gerará um [!DNL Audience Manager] Fonte de dados, mas observe que o método syncIdentity só oferece suporte a símbolos de identidade de namespace.
