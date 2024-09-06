---
title: Assimilar dados criptografados na interface do usuário de origens do Workspace
description: Saiba como assimilar dados criptografados no espaço de trabalho da interface do usuário de origens.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 7%

---

# Assimilar dados criptografados na interface do usuário de origens

>[!AVAILABILITY]
>
>O suporte para assimilação de dados criptografados na interface do usuário de origens está na versão beta e pode não estar disponível para sua organização. O recurso e a documentação estão sujeitos a alterações.

Você pode assimilar arquivos e pastas de dados criptografados para a Adobe Experience Platform usando fontes de lote de armazenamento na nuvem. Com a assimilação de dados criptografados, você pode aproveitar os mecanismos assimétricos de criptografia para transferir com segurança os dados em lote para o Experience Platform. Atualmente, os mecanismos de criptografia assimétrica compatíveis são PGP e GPG.

Esse recurso está disponível para as seguintes fontes:

* [Amazon S3]
* [Blob do Azure]
* [Armazenamento do Azure Data Lake Gen2]
* [Armazenamento de Arquivos do Azure]
* [Zona de Aterrissagem de Dados]
* [FTP]
* [Armazenamento na nuvem do Google]
* [HDFS]
* [Armazenamento de Objetos de Oracle]
* [SFTP]

Leia este guia para saber como assimilar dados criptografados com fontes em lote de armazenamento na nuvem usando a interface do.

## Introdução

É útil conhecer os seguintes recursos e conceitos de Experience Platform antes de trabalhar com a assimilação de dados criptografados na interface do usuário do:

* [Fontes](../../home.md): use fontes no Experience Platform para assimilar dados de um Aplicativo Adobe ou de uma fonte de dados de terceiros.
* [Fluxos de dados](../../../dataflows/home.md): Fluxos de dados são representações de trabalhos de dados que movem dados pelo Experience Platform. Você pode usar o espaço de trabalho de origens para criar fluxos de dados que assimilam dados de uma determinada origem para o Experience Platform.
* [Sandboxes](../../../sandboxes/home.md): use sandboxes no Experience Platform para criar partições virtuais entre as instâncias do Experience Platform e criar ambientes dedicados ao desenvolvimento ou produção.

### Estrutura de tópicos de alto nível

1. Crie um par de chaves de criptografia usando o espaço de trabalho de origens na interface de usuário do Experience Platform. Como opção, você também pode criar um par de chaves de verificação de assinatura para fornecer uma camada adicional de segurança para seus dados criptografados.
2. Use a chave pública para criptografar seus dados.
3. Coloque os dados criptografados no provedor de armazenamento na nuvem. Durante essa etapa, você também deve garantir que tenha um arquivo de amostra que possa ser usado como referência para mapear seus dados de origem para um esquema do Experience Data Model (XDM).
4. Assimile seus dados criptografados no Experience Platform criando uma conexão de origem.
5. Ao criar sua conexão de origem, forneça a ID da chave que corresponde à chave pública usada para criptografar seus dados. Se você também usou o mecanismo de par de chaves de verificação de sinal, forneça também a ID da chave de verificação de sinal que corresponde aos dados criptografados.
6. Continue com as etapas de criação do fluxo de dados.

## Criar um par de chaves de criptografia {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID da chave de criptografia"
>abstract="Forneça a ID da chave de criptografia que corresponde à chave de criptografia usada para criptografar os dados de origem."

* Na interface da Platform, navegue até o espaço de trabalho de origens e selecione [!UICONTROL Pares de Chaves] no cabeçalho superior.
* Você é direcionado a uma página que exibe uma lista de pares de chaves de criptografia existentes em sua organização. Esta página fornece informações sobre o título, ID, tipo, algoritmo de criptografia, expiração e status de uma determinada chave. Para criar um novo par de chaves, selecione **[!UICONTROL Criar chave]**.
* Em seguida, escolha o tipo de chave que deseja criar. Para criar uma chave de criptografia, selecione **[!UICONTROL Chave de Criptografia]** e forneça um título e uma senha para sua chave de criptografia. A senha é uma camada adicional de proteção para suas chaves de criptografia. Após a criação, o Experience Platform armazena a senha em um cofre seguro diferente da chave pública. Você deve fornecer uma sequência de caracteres não vazia como senha.

### Criar uma chave de verificação de assinatura {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID da chave de verificação de assinatura"
>abstract="Forneça a ID da chave de verificação de assinatura que corresponde aos dados de origem assinados e criptografados."

## Assimilar dados criptografados {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="O arquivo está criptografado?"
>abstract="Selecione este botão de alternância se estiver assimilando um arquivo que já está criptografado."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Selecionar arquivo de amostra"
>abstract="É necessário assimilar um arquivo de amostra ao assimilar dados criptografados a fim de criar um mapeamento."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
