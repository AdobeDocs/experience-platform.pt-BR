---
title: Envio de dados para o Adobe Audience Manager
seo-title: Envio de dados para o Adobe Audience Manager com o SDK da Web Adobe Experience Platform
description: Saiba mais sobre como enviar dados para o Adobe Audience Manager com o SDK da Experience Platform Web
seo-description: Saiba mais sobre como enviar dados para o Adobe Audience Manager com o SDK da Experience Platform Web
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] no [!DNL Experience Platform Edge Network]

O Adobe Experience Platform [!DNL Web SDK] é integrado ao Adobe Audience Manager e oferece suporte ao envio e recebimento de dados de destinos de [!DNL Audience Manager]Cookie e URL e sincronização de ID.

## Ativação [!DNL Audience Manager]

Para habilitar [!DNL Audience Manager] você precisará fazer o seguinte:

- Ative [!DNL Audience Manager] a sua configuração [de borda](../../fundamentals/edge-configuration.md).
- Ative ou desative Cookie e destinos de URL.
- Especifique seu Container de sincronização de ID para sincronizações de parceiros externos (Opcional)

## Sincronizando identidades

O Adobe Experience Platform [!DNL Web SDK] suporta a capacidade de declarar IDs do cliente e seus estados de autenticação por meio do comando [SyncIdentity](../../fundamentals/identity.md) .

O método syncIdentity usa Namespaces [do Serviço de](../../../identity/../identity-service/namespaces.md) Identidade para indicar o contexto ao qual uma identidade está relacionada. Como [!DNL Audience Manager] cliente, todas as suas Fontes de Dados existentes que usam o Tipo de ID: Todos os dispositivos terão um correspondente automaticamente [!DNL Identity Namespace]. Para localizar o correspondente [!DNL Identity Namespace] para o seu [!DNL Audience Manager Data Source], faça logon no Adobe Experience Platform e navegue até a [!DNL Identities] seção.

![Visualização da interface do usuário do Namespace](../../../assets/edge_configuration_identity.png)

Aqui você pode pesquisar sua Fonte de [!DNL Audience Manager] Dados por Nome. O método syncIdentity usa o símbolo de identidade para indicar a Namespace.

Qualquer nova fonte [!DNL Audience Manager] de dados que use o Tipo de ID: Entre dispositivos gerará uma Namespace de identidade correspondente. O cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são suportados no momento. Além disso, qualquer Namespace de identidade criada no Adobe Experience Platform gerará uma Fonte [!DNL Audience Manager] de dados correspondente, mas observe que o método syncIdentity só oferece suporte a símbolos de identidade de Namespace.
