---
description: Use as configurações de autenticação compatíveis no Adobe Experience Platform Destination SDK para autenticar usuários e ativar dados no terminal de destino.
title: Configuração de autenticação
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Configuração de autenticação {#credentials}

## Tipos de autenticação compatíveis {#supported-authentication-types}

A configuração de autenticação selecionada determina como o Experience Platform é autenticado no seu destino, na interface do usuário da plataforma.

O Adobe Experience Platform Destination SDK suporta vários tipos de autenticação:

* [Autenticação do portador](#bearer)
* [[!DNL Amazon S3] autenticação](#s3)
* [[!DNL Azure Blob] Armazenamento](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP com chave SSH](#sftp-ssh)
* [SFTP com senha](#sftp-password)
* [OAuth 2 com código de autorização](#oauth2)
* [OAUth 2 com concessão de senha](#oauth2)
* [OAuth 2 com concessão de credenciais de cliente](#oauth2)

Você pode configurar as informações de autenticação para o seu destino por meio da variável `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint .

Consulte as seguintes seções para obter detalhes sobre a configuração de autenticação para cada tipo de destino:

* [Configurações de autenticação para destinos de transmissão](destination-configuration.md#customer-authentication-configurations)
* [Configurações de autenticação para destinos com base em arquivo](file-based-destination-configuration.md#customer-authentication-configurations)

## Autenticação do portador {#bearer}

A autenticação portador é compatível com destinos de transmissão em Experience Platform.

Para configurar a autenticação de tipo de portador para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] autenticação {#s3}

[!DNL Amazon S3] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Para configurar [!DNL Amazon S3] para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Para configurar [!DNL Azure Blob] para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Para configurar [!DNL Azure Data Lake Storage] Autenticação (ADLS) para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] autenticação com [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] autenticação com [!DNL SSH] A chave é compatível com destinos com base em arquivo no Experience Platform.

Para configurar a autenticação SFTP com chave SSH para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] autenticação com senha {#sftp-password}

[!DNL SFTP] a autenticação com senha é compatível com destinos com base em arquivo no Experience Platform.

Para configurar a autenticação SFTP com senha para seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] autenticação {#oauth2}

[!DNL OAuth 2] a autenticação é compatível com destinos de transmissão no Experience Platform.

Para obter informações sobre como configurar os vários [!DNL OAuth 2] fluxos, bem como para fluxos personalizados [!DNL OAuth 2] suporte, leia a documentação do Destination SDK em [[!DNL OAuth 2] autenticação](./oauth2-authentication.md).


## Quando usar a variável `/credentials` Ponto de extremidade da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você *não* precisam usar o `/credentials` Ponto de extremidade da API. Em vez disso, você pode configurar as informações de autenticação para o seu destino por meio do `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint .

O `/credentials` O endpoint da API é fornecido aos desenvolvedores de destino para os casos em que há um sistema de autenticação global entre o Adobe e seu destino e [!DNL Platform] Os clientes do não precisam fornecer credenciais de autenticação para se conectarem ao seu destino.

Nesse caso, é necessário criar um objeto de credenciais usando o `/credentials` Ponto de extremidade da API. Você também deve selecionar `PLATFORM_AUTHENTICATION` no [configuração de destino](./destination-configuration.md#destination-delivery). Ler [Operações de endpoint da API de credenciais](./credentials-configuration-api.md) para obter uma lista completa de operações que podem ser executadas na `/credentials` endpoint .
