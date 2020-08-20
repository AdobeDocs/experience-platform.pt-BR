---
title: Envio de dados para a Adobe Audience Manager
seo-title: Envio de dados para o Adobe Audience Manager com o Adobe Experience Platform Web SDK
description: Saiba como enviar dados para a Adobe Audience Manager com o Experience Platform Web SDK
seo-description: Saiba como enviar dados para a Adobe Audience Manager com o Experience Platform Web SDK
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] no [!DNL Experience Platform Edge Network]

O Adobe Experience Platform [!DNL Web SDK] é integrado ao Adobe Audience Manager e oferece suporte ao envio e recebimento de dados de destinos [!DNL Audience Manager], cookies e URL e sincronização de ID.

## Ativação [!DNL Audience Manager]

Para habilitar [!DNL Audience Manager] você precisará fazer o seguinte:

- Ative [!DNL Audience Manager] a sua configuração [de borda](../../fundamentals/edge-configuration.md).
- Ative ou desative Cookie e destinos de URL.
- Especifique seu Container de sincronização de ID para sincronizações de parceiros externos (Opcional)

## Sincronizando identidades

O Adobe Experience Platform Web SDK oferece suporte à capacidade de declarar IDs do cliente e seus estados de autenticação por meio do comando [sendEvent](../../fundamentals/identity.md#syncing-identities) .

Escolha suas namespaces nas Namespaces [do Serviço de](../../../identity/../identity-service/namespaces.md) Identidade para indicar o contexto ao qual uma identidade está relacionada, usando os valores na coluna Símbolo de Identidade:

![Visualização da interface do usuário do Namespace](../../../assets/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas as suas Fontes de Dados existentes que usam o Tipo de ID: Todos os dispositivos têm automaticamente uma Namespace de identidade correspondente. Para localizar a Namespace de identidade correspondente para sua Fonte de dados de Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades.

Qualquer nova fonte [!DNL Audience Manager] de dados que usa o tipo de ID: Entre dispositivos gerará uma Namespace de identidade correspondente. O cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são suportados no momento. Além disso, qualquer Namespace de identidade criada no Adobe Experience Platform gerará uma Fonte de [!DNL Audience Manager] dados correspondente, mas observe que o método syncIdentity suporta apenas os símbolos de identidade de Namespace.
