---
title: Assimilar dados criptografados na interface do usuário de origens do Workspace
description: Saiba como assimilar dados criptografados no espaço de trabalho da interface do usuário de origens.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# Assimilar dados criptografados na interface do usuário de origens

Leia este guia para saber como assimilar dados criptografados na Adobe Experience Platform usando fontes de armazenamento na nuvem para dados em lote.

## Pré-requisitos

* Criptografar seus dados

## Assimilar dados criptografados {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="O arquivo está criptografado?"
>abstract="Selecione este botão de alternância se estiver assimilando um arquivo que já está criptografado."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Selecionar arquivo de amostra"
>abstract="É necessário assimilar um arquivo de amostra ao assimilar dados criptografados a fim de criar um mapeamento."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID da chave de criptografia"
>abstract="Forneça a ID da chave de criptografia que corresponde à chave de criptografia usada para criptografar os dados de origem."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID da chave de verificação de assinatura"
>abstract="Forneça a ID da chave de verificação de assinatura que corresponde aos dados de origem assinados e criptografados."

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
