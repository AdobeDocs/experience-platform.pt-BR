---
title: Envio de dados para o Adobe Audiência Manager
seo-title: Envio de dados para o Adobe Audiência Manager com o Adobe Experience Platform Web SDK
description: Saiba como enviar dados para o Adobe Audiência Manager com o Experience Platform Web SDK
seo-description: Saiba como enviar dados para o Adobe Audiência Manager com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: dfe9ea2889b3ba2e74f8b10296bfb2d123ad9d57
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 2%

---


# (Beta) Gerenciador de Audiências na Rede de Borda da Experience Platform

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O SDK da Web da plataforma Adobe Experience é integrado ao Adobe Audiência Manager e oferece suporte ao envio e recebimento de dados do Audiência Manager, dos destinos do Cookie e URL e da sincronização de ID.

## Ativação do Gerenciador de Audiências

Para ativar o Gerenciador de Audiências, é necessário fazer o seguinte:

- Ative o Gerenciador de Audiências na configuração [da](../../fundamentals/edge-configuration.md)borda.
- Ative ou desative Cookie e destinos de URL.
- Especifique seu Container de sincronização de ID para sincronizações de parceiros externos (Opcional)

## Sincronizando identidades

O SDK da Web da plataforma Adobe Experience oferece suporte à capacidade de declarar IDs do cliente e seus estados de autenticação por meio do comando [SyncIdentity](../../fundamentals/identity.md) .

O método syncIdentity usa Namespaces [do Serviço de](../../../identity/../identity-service/namespaces.md) Identidade para indicar o contexto ao qual uma identidade está relacionada. Como cliente do Gerenciador de Audiências, todas as suas Fontes de Dados existentes usam o Tipo de ID: Todos os dispositivos terão automaticamente uma Namespace de identidade correspondente. Para localizar a Namespace de identidade correspondente para a Fonte de Dados do Audiência Manager, faça logon na Adobe Experience Platform e navegue até a seção Identidades.

![Visualização da interface do usuário do Namespace](../../../assets/edge_configuration_identity.png)

Aqui você pode pesquisar sua Fonte de Dados do Gerenciador de Audiências por Nome. O método syncIdentity usa o símbolo de identidade para indicar a Namespace.

Qualquer nova Fonte de Dados do Gerenciador de Audiências que use o Tipo de ID: Entre dispositivos gerará uma Namespace de identidade correspondente. O cookie de tipos de ID de fonte de dados e a ID de publicidade do dispositivo não são suportados no momento. Além disso, qualquer Namespace de identidade criada na Adobe Experience Platform gerará uma Fonte de Dados do Audiência Manager correspondente, mas observe que o método syncIdentity suporta apenas os Símbolos de identidade de Namespace.
