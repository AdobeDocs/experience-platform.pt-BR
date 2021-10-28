---
description: Use as configurações de autenticação compatíveis no SDK de Destino do Adobe Experience Platform para autenticar usuários e ativar dados no terminal de destino.
title: Configuração de autenticação
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Configuração de autenticação {#credentials}

## Tipos de autenticação compatíveis {#supported-authentication-types}

O Adobe Experience Platform Destination SDK oferece suporte a vários tipos de autenticação:

* Autenticação do portador
* OAuth 2 com código de autorização
* OAUth 2 com concessão de senha
* OAuth 2 com concessão de credenciais de cliente

Você pode configurar as informações de autenticação para o seu destino por meio da variável `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint . Consulte a [seção de configurações de autenticação do cliente](./destination-configuration.md#customer-authentication-configurations) no artigo de configuração de destino e nas seções abaixo para obter detalhes sobre as configurações de cada tipo de autenticação.

## Autenticação do portador {#bearer}

Para configurar a autenticação de tipo de portador para seus destinos, basta configurar o `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## Autenticação OAuth 2 {#oauth2}

Para obter informações sobre como configurar os vários fluxos OAuth 2 suportados, bem como para suporte OAuth 2 personalizado, leia a documentação do SDK de destino em [Autenticação OAuth 2](./oauth2-authentication.md).


## Quando usar a variável `/credentials` Ponto de extremidade da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você *não* precisam usar o `/credentials` Ponto de extremidade da API. Em vez disso, você pode configurar as informações de autenticação para o seu destino por meio do `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint .

O `/credentials` O endpoint da API é fornecido aos desenvolvedores de destino para os casos em que há um sistema de autenticação global entre o Adobe e seu destino e [!DNL Platform] Os clientes do não precisam fornecer credenciais de autenticação para se conectarem ao seu destino.

Nesse caso, é necessário criar um objeto de credenciais usando o `/credentials` Ponto de extremidade da API. Você também deve selecionar `PLATFORM_AUTHENTICATION` no [configuração de destino](./destination-configuration.md#destination-delivery). Ler [Operações de endpoint da API de credenciais](./credentials-configuration-api.md) para obter uma lista completa de operações que podem ser executadas na `/credentials` endpoint .
