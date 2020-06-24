---
title: Envio de dados para o Adobe Audience Manager
seo-title: Envio de dados para o Adobe Audience Manager com o SDK da Web Adobe Experience Platform
description: Saiba mais sobre como enviar dados para o Adobe Audience Manager com o SDK da Experience Platform Web
seo-description: Saiba mais sobre como enviar dados para o Adobe Audience Manager com o SDK da Experience Platform Web
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager na rede Experience Platform Edge

O Adobe Experience Platform Web SDK é integrado ao Adobe Audience Manager e oferece suporte ao envio e recebimento de dados de destinos de Audience Manager, cookie e URL e sincronização de ID.

## Ativação do Audience Manager

Para ativar o Audience Manager, é necessário fazer o seguinte:

- Ative o Audience Manager na configuração [da](../../fundamentals/edge-configuration.md)borda.
- Ative ou desative Cookie e destinos de URL.
- Especifique seu Container de sincronização de ID para sincronizações de parceiros externos (Opcional)

## Sincronizando identidades

O Adobe Experience Platform Web SDK oferece suporte à capacidade de declarar IDs de clientes e seus estados de autenticação por meio do comando [SyncIdentity](../../fundamentals/identity.md) .

O método syncIdentity usa Namespaces [do Serviço de](../../../identity/../identity-service/namespaces.md) Identidade para indicar o contexto ao qual uma identidade está relacionada. Como cliente Audience Manager, todas as suas Fontes de Dados existentes que usam o Tipo de ID: Todos os dispositivos terão automaticamente uma Namespace de identidade correspondente. Para localizar a Namespace de identidade correspondente para sua Fonte de dados de Audience Manager, faça logon no Adobe Experience Platform e navegue até a seção Identidades.

![Visualização da interface do usuário do Namespace](../../../assets/edge_configuration_identity.png)

Aqui você pode pesquisar sua Fonte de Dados de Audience Manager por Nome. O método syncIdentity usa o símbolo de identidade para indicar a Namespace.

Qualquer nova fonte de dados de Audience Manager que use o tipo de ID: Entre dispositivos gerará uma Namespace de identidade correspondente. O cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são suportados no momento. Além disso, qualquer Namespace de identidade criada no Adobe Experience Platform gerará uma Fonte de dados Audience Manager correspondente, mas observe que o método syncIdentity só oferece suporte a Símbolos de identidade de Namespace.
