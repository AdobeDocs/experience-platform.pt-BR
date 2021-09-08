---
description: Essa configuração determina como os usuários do Adobe Experience Platform são autenticados no terminal de destino para ativar os dados.
title: Opções de configuração para credenciais no SDK de destino
source-git-commit: 11f6421665acc2041aa9483b1e0efb6fe48b6dfb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Configuração de autenticação {#credentials}

## Tipos de autenticação compatíveis {#supported-authentication-types}

O Adobe Experience Platform oferece suporte a vários tipos de autenticação:

* Autenticação do portador
* OAuth 2 com código de autorização
* OAUth 2 com concessão de senha
* OAuth 2 com concessão de credenciais de cliente

Para os vários fluxos OAuth 2 suportados, bem como para o suporte OAuth 2 personalizado, leia a documentação do SDK de destino em [Autenticação OAuth 2](./oauth2-authentication.md).

Você pode configurar as informações de autenticação para seu destino por meio dos parâmetros `customerAuthenticationConfigurations` do endpoint `/destinations`. Consulte a seção [configurações de autenticação de cliente](./destination-configuration.md#customer-authentication-configurations) no artigo de configuração de destino.

## Quando usar o endpoint da API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, *não* precisa usar o endpoint da API `/credentials`. Em vez disso, você pode configurar as informações de autenticação para seu destino por meio dos parâmetros `customerAuthenticationConfigurations` do endpoint `/destinations`.

Use o ponto de extremidade da API `activation/authoring/credentials` e selecione `PLATFORM_AUTHENTICATION` na [configuração de destino](./destination-configuration.md#destination-delivery) se houver um sistema de autenticação global entre o Adobe e seu destino e o cliente [!DNL Platform] não precisar fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o ponto de extremidade da API `/credentials`. Leia [Operações de ponto de extremidade da API de credenciais](./credentials-configuration-api.md) para obter uma lista completa de operações que podem ser executadas no ponto de extremidade `/credentials`.