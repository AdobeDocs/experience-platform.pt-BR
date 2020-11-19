---
title: Sincronização de identidades com o Audience Manager e o Adobe Experience Platform
seo-title: Sincronização de identidades com o Audience Manager e o Adobe Experience Platform com o Adobe Experience Platform Web SDK
description: Saiba como sincronizar identidades com o Adobe Audience Manager com o Experience Platform Web SDK
seo-description: Saiba como sincronizar identidades com o Adobe Audience Manager com o Experience Platform Web SDK
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Sincronizando identidades

O Adobe Experience Platform Web SDK oferece suporte à capacidade de declarar IDs de clientes e seus estados de autenticação por meio do comando [sendEvent](./overview.md#syncing-identities) .

Escolha suas namespaces nas Namespaces [do Serviço de](../../identity/../identity-service/namespaces.md) Identidade para indicar o contexto ao qual uma identidade está relacionada, usando os valores na coluna Símbolo de Identidade:

![Visualização da interface do usuário do Namespace](../../assets/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas as suas Fontes de Dados existentes que usam o Tipo de ID: Todos os dispositivos têm automaticamente uma Namespace de identidade correspondente. Para localizar a Namespace de identidade correspondente para sua Fonte de dados de Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades.

Qualquer nova fonte [!DNL Audience Manager] de dados que usa o tipo de ID: Entre dispositivos gerará uma Namespace de identidade correspondente. O cookie de tipos de ID de fonte de dados e a ID de publicidade de dispositivo não são suportados no momento. Além disso, qualquer Namespace de identidade criada no Adobe Experience Platform gerará uma Fonte [!DNL Audience Manager] de dados correspondente, mas observe que o método syncIdentity suporta apenas os símbolos de identidade de Namespace.
