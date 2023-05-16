---
description: Saiba como configurar um mecanismo de autenticação para o seu destino e obter informações sobre o que os usuários verão na interface do usuário, dependendo do método de autenticação selecionado.
title: Configuração de autenticação do cliente
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# Configuração de autenticação do cliente

O Experience Platform oferece grande flexibilidade nos protocolos de autenticação disponíveis para parceiros e clientes. Você pode configurar seu destino para suportar qualquer um dos métodos de autenticação padrão do setor, como [!DNL OAuth2], autenticação de token portador, autenticação de senha e muito mais.

Esta página explica como configurar seu destino usando o método de autenticação preferencial. Com base na configuração de autenticação usada ao criar o destino, os clientes verão diferentes tipos de páginas de autenticação ao se conectarem ao destino na interface do usuário do Experience Platform.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou veja as seguintes páginas de visão geral da configuração de destino:

* [Use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Antes que os clientes possam exportar dados da Platform para seu destino, eles devem criar uma nova conexão entre o Experience Platform e seu destino, seguindo as etapas descritas na [conexão de destino](../../../ui/connect-destination.md) tutorial.

When [criação de um destino](../../authoring-api/destination-configuration/create-destination-configuration.md) por Destination SDK, a `customerAuthenticationConfigurations` define o que os clientes veem na seção [tela de autenticação](../../../ui/connect-destination.md#authenticate). Dependendo do tipo de autenticação de destino, os clientes devem fornecer vários detalhes de autenticação, como:

* Para destinos usando [autenticação básica](#basic), os usuários devem fornecer um nome de usuário e senha diretamente na página de autenticação da interface do usuário do Experience Platform.
* Para destinos usando [autenticação do portador](#bearer), os usuários devem fornecer um token portador.
* Para destinos usando [Autenticação OAuth2](#oauth2), os usuários são redirecionados para a página de logon do seu destino, onde podem fazer logon com suas credenciais.
* Para [Amazon S3](#s3) destinos, os usuários devem fornecer seus [!DNL Amazon S3] chave de acesso e chave secreta.
* Para [Azure Blob](#blob) destinos, os usuários devem fornecer seus [!DNL Azure Blob] string de conexão.

Você pode configurar os detalhes de autenticação do cliente por meio do `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as configurações de autenticação de cliente compatíveis que você pode usar para seu destino e mostra o que os clientes verão na interface do usuário do Experience Platform com base no método de autenticação configurado para seu destino.

>[!IMPORTANT]
>
>A configuração de autenticação do cliente não requer que você configure quaisquer parâmetros. Você pode copiar e colar os trechos mostrados nesta página nas chamadas de API quando [criação](../../authoring-api/destination-configuration/create-destination-configuration.md) ou [atualização](../../authoring-api/destination-configuration/update-destination-configuration.md) uma configuração de destino, e seus usuários verão a tela de autenticação correspondente na interface do usuário da plataforma.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Sim |

## Configuração da regra de autenticação {#authentication-rule}

Ao usar qualquer uma das configurações de autenticação de cliente descritas nesta página, sempre defina a variável `authenticationRule` em [entrega de destino](destination-delivery.md) para `"CUSTOMER_AUTHENTICATION"`, conforme mostrado abaixo.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Autenticação básica {#basic}

A autenticação básica é compatível com integrações em tempo real (streaming) no Experience Platform.

Ao configurar o tipo de autenticação básico, os usuários são solicitados a inserir um nome de usuário e senha para se conectarem ao seu destino.

![Renderização da interface do usuário com autenticação básica](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Para configurar a autenticação básica para o seu destino, configure a variável `customerAuthenticationConfigurations` seção por meio da `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticação do portador {#bearer}

Ao configurar o tipo de autenticação do portador, os usuários são solicitados a inserir o token do portador que obtêm do seu destino.

![Renderização da interface do usuário com autenticação do portador](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Para configurar a autenticação de tipo de portador para o seu destino, configure a variável `customerAuthenticationConfigurations` seção por meio da `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## Autenticação OAuth 2 {#oauth2}

Usuários selecionados **[!UICONTROL Ligar ao destino]** para acionar o fluxo de autenticação do OAuth 2 para o seu destino, conforme mostrado no exemplo abaixo para o destino Públicos personalizados do Twitter. Para obter informações detalhadas sobre como configurar a autenticação OAuth 2 para o terminal de destino, leia o [Página de autenticação do Destination SDK OAuth 2](oauth2-authentication.md).

![Renderização da interface do usuário com autenticação OAuth 2](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Para configurar [!DNL OAuth2] para o seu destino, configure a variável `customerAuthenticationConfigurations` seção por meio da `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Autenticação Amazon S3 {#s3}

[!DNL Amazon S3] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Ao configurar o tipo de autenticação do Amazon S3, os usuários são solicitados a inserir suas credenciais do S3.

![Renderização da interface do usuário com autenticação S3](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Para configurar [!DNL Amazon S3] para o seu destino, configure a variável `customerAuthenticationConfigurations` seção por meio da `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Autenticação do Azure Blob  {#blob}

[!DNL Azure Blob Storage] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Ao configurar o tipo de autenticação Azure Blob, os usuários são solicitados a inserir a string de conexão.

![Renderização da interface do usuário com autenticação de Blob](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Para configurar [!DNL Azure Blob] para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] autenticação {#adls}

[!DNL Azure Data Lake Storage] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Ao configurar o [!DNL Azure Data Lake Storage] tipo de autenticação, os usuários devem inserir as credenciais do Serviço do Azure e as informações do locatário.

![renderizar a interface do usuário com [!DNL Azure Data Lake Storage] autenticação](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Para configurar [!DNL Azure Data Lake Storage] Autenticação (ADLS) para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP com autenticação de senha

[!DNL SFTP] a autenticação com senha é compatível com destinos com base em arquivo no Experience Platform.

Ao configurar o SFTP com o tipo de autenticação por senha, os usuários são solicitados a inserir o nome de usuário e a senha do SFTP, bem como o domínio e a porta do SFTP (a porta padrão é 22).

![Renderização da interface com o SFTP com autenticação de senha](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Para configurar a autenticação SFTP com senha para seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP com autenticação de chave SSH

[!DNL SFTP] autenticação com [!DNL SSH] A chave é compatível com destinos com base em arquivo no Experience Platform.

Ao configurar o SFTP com o tipo de autenticação de chave SSH, os usuários são solicitados a inserir o nome de usuário e a chave SSH SFTP, bem como o domínio e a porta SFTP (a porta padrão é 22).

![Renderização da interface com o SFTP com autenticação de chave SSH](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Para configurar a autenticação SFTP com chave SSH para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] autenticação {#gcs}

[!DNL Google Cloud Storage] a autenticação é compatível com destinos com base em arquivo no Experience Platform.

Ao configurar o [!DNL Google Cloud Storage] tipo de autenticação, os usuários são solicitados a inserir seus [!DNL Google Cloud Storage] [!UICONTROL ID da chave de acesso] e [!UICONTROL chave de acesso secreta].

![Renderização da interface do usuário com a autenticação do Google Cloud Storage](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Para configurar [!DNL Google Cloud Storage] para o seu destino, configure a variável `customerAuthenticationConfigurations` no `/destinations` endpoint como mostrado abaixo:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão de como pode configurar a autenticação de usuário na plataforma de destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)