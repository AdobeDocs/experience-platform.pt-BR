---
title: Sincronizando identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
description: Saiba como sincronizar identidades entre o Audience Manager e o Adobe Experience Platform usando o SDK da Web da plataforma
seo-description: Saiba como sincronizar identidades com o Adobe Audience Manager com o Experience Platform Web SDK
keywords: gerenciador de audiências;aam;identities;sincronizar identidades;namespace;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Sincronização de identidades entre Audience Manager e Experience Platform

O Adobe Experience Platform Web SDK oferece suporte à capacidade de declarar IDs de clientes e seus estados de autenticação por meio do comando [sendEvent](./overview.md#syncing-identities).

Escolha suas namespaces de [Namespaces do Serviço de Identidade](../../identity/../identity-service/namespaces.md) para indicar o contexto ao qual uma identidade está relacionada, usando os valores na coluna Símbolo de Identidade:

![Visualização da interface do usuário do Namespace](../../assets/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas as suas Fontes de Dados existentes que usam o Tipo de ID: Todos os dispositivos têm automaticamente uma Namespace de identidade correspondente. Para localizar a Namespace de identidade correspondente para sua Fonte de dados de Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades.

Qualquer nova fonte de dados [!DNL Audience Manager] que use o Tipo de ID: Entre dispositivos gerará uma Namespace de identidade correspondente. O cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são suportados no momento. Além disso, qualquer Namespace de identidade criada no Adobe Experience Platform gerará uma Fonte de Dados [!DNL Audience Manager] correspondente, mas observe que o método syncIdentity só oferece suporte a Símbolos de identidade de Namespace.
