---
title: Sincronização de identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
description: Saiba como sincronizar identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
seo-description: Saiba como sincronizar identidades com o Adobe Audience Manager com o Experience Platform Web SDK
keywords: audience manager; aam; identidades; sincronizar identidades; namespace;
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Sincronização de identidades entre o Audience Manager e o Experience Platform

O Adobe Experience Platform Web SDK oferece suporte à capacidade de declarar IDs do cliente e seus estados de autenticação por meio do comando [sendEvent](./overview.md#syncing-identities).

Escolha seus namespaces no [Namespaces do serviço de identidade](../../identity/../identity-service/namespaces.md) para indicar o contexto ao qual uma identidade está relacionada, usando os valores na coluna Símbolo de identidade:

![Exibição da interface do usuário do Namespaces](../images/identity/edge_namespaceUI_identity-symbol.png)

Como cliente do Audience Manager, todas as suas fontes de dados existentes que usam o Tipo de ID: O Cross-Device tem automaticamente um Namespace de identidade correspondente. Para encontrar o Namespace de identidade correspondente para sua Fonte de dados do Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades .

Qualquer nova fonte de dados [!DNL Audience Manager] que use o Tipo de ID: O Cross-Device gerará um Namespace de identidade correspondente. No momento, o cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são compatíveis. Além disso, qualquer Namespace de identidade criado no Adobe Experience Platform gerará uma Fonte de Dados [!DNL Audience Manager] correspondente, mas observe que o método syncIdentity só oferece suporte a Símbolos de identidade de namespace.
