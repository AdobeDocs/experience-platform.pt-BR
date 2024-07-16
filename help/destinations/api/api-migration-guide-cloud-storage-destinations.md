---
solution: Experience Platform
title: Guia de migração de API para destinos de armazenamento em nuvem
description: Saiba mais sobre as alterações no fluxo de trabalho para ativar destinos de armazenamento em nuvem como parte da migração para os novos cartões de destino de armazenamento em nuvem com funcionalidade adicional.
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: 4b9e7c22282a5531f2f25f3d225249e4eb0e178e
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Guia de migração de API para destinos de armazenamento em nuvem

>[!IMPORTANT]
>
>* A funcionalidade descrita nesta página está disponível para clientes que compraram os pacotes do Real-Time CDP Prime e Ultimate. Entre em contato com o representante da Adobe para obter mais informações.

## Contexto de migração {#migration-context}

A partir de [outubro de 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations), você poderá usar os novos recursos de exportação de arquivos para acessar a funcionalidade de personalização aprimorada ao exportar arquivos do Experience Platform:

* [Opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) adicionais.
* Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados através da [nova etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Capacidade de selecionar o [tipo de arquivo](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) do arquivo exportado.
* Capacidade de [personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Essa funcionalidade é compatível com os cartões de armazenamento beta na nuvem listados abaixo:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Observe que, atualmente na interface do usuário do Experience Platform, você pode ver dois cartões de destino lado a lado dos três destinos. Abaixo estão os destinos novos e herdados do [!DNL Amazon S3]. Em todos os casos, os cartões marcados com **Beta** são os novos cartões de destino.

![Imagem dos dois cartões de destino do Amazon S3 em um modo de exibição lado a lado.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Embora esses destinos com funcionalidade aprimorada tenham sido oferecidos inicialmente como um beta, o *Adobe está movendo todos os clientes do Real-Time CDP para os novos destinos de armazenamento na nuvem*. Para clientes que já estavam usando o [!DNL Amazon S3], [!DNL Azure Blob] ou SFTP, isso significa que os fluxos de dados existentes serão migrados para os novos cartões. Leia para obter mais informações sobre as alterações específicas como parte da migração.

## A quem esta página se aplica {#who-this-applies-to}

Se você já estiver usando a [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/) para exportar perfis para os destinos de armazenamento na nuvem do Amazon S3, Azure Blob ou SFTP, este guia de migração de API se aplica a você.

Se você tiver scripts em execução em seus locais de armazenamento na nuvem [!DNL Amazon S3], [!DNL Azure Blob] ou SFTP sobre os arquivos exportados do Experience Platform, esteja ciente de que alguns parâmetros estão mudando no que diz respeito às especificações de conexão e fluxo dos novos cartões, bem como em relação à etapa de mapeamento.

Por exemplo, se você estava usando um script para filtrar fluxos de dados de destino para o destino [!DNL Amazon S3], com base na especificação de conexão do destino [!DNL Amazon S3], saiba que a especificação de conexão será alterada e, portanto, será necessário atualizar seus filtros.

## Links de documentação relevantes {#relevant-documentation-links}

Esta seção inclui o tutorial de API relevante e a documentação de referência para a funcionalidade aprimorada de exportar dados para destinos de armazenamento na nuvem.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [Tutorial de API para exportar públicos-alvo para destinos de armazenamento na nuvem](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Documentação de referência da API do Serviço de Fluxo de Destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Resumo das alterações incompatíveis com versões anteriores {#summary-backwards-incompatible-changes}

Com a migração para os novos destinos, todos os fluxos de dados existentes para [!DNL Amazon S3], [!DNL Azure Blob] e destinos SFTP agora receberão novas conexões de destino e conexões de base. A etapa de mapeamento de perfil também é alterada. As alterações incompatíveis com versões anteriores são resumidas nas seções abaixo para cada destino. Consulte também o [glossário de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) para obter mais informações sobre os termos do diagrama abaixo.

![Imagem de visão geral do guia de migração](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Alterações incompatíveis com versões anteriores no destino [!DNL Amazon S3] {#changes-amazon-s3-destination}

As alterações incompatíveis com versões anteriores para os usuários da API são um `connection spec ID` e `flow spec ID` atualizados, conforme mostrado na tabela abaixo:

| [!DNL Amazon S3] | Herdados | Novo |
|---------|----------|---------|
| Especificação de fluxo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-594799c47549 |
| Especificação da conexão | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Veja os exemplos completos de conexões base e de destino herdadas e novas para [!DNL Amazon S3] nas guias abaixo. Os parâmetros necessários para criar conexões base para [!DNL Amazon S3] destinos não são alterados.

Da mesma forma, não há alterações incompatíveis com versões anteriores nos parâmetros necessários para criar conexões de destino.

>[!BEGINTABS]

>[!TAB Conexão base herdada e conexão de destino]

+++Exibir [!DNL base connection] herdado para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++Exibir [!DNL target connection] herdado para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nova conexão base e conexão de destino]

+++Exibir novos [!DNL base connection] para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++Exibir novos [!DNL target connection] para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Alterações incompatíveis com versões anteriores no destino [!DNL Azure Blob] {#changes-azure-blob-destination}

As alterações incompatíveis com versões anteriores para os usuários da API são um `connection spec ID` e `flow spec ID` atualizados, conforme mostrado na tabela abaixo:

| [!DNL Azure Blob] | Herdados | Novo |
|---------|----------|---------|
| Especificação de fluxo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| Especificação da conexão | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Veja os exemplos completos de conexões base e de destino herdadas e novas para [!DNL Azure Blob] nas guias abaixo. Os parâmetros necessários para criar conexões base para destinos do Azure Blob não são alterados.

Da mesma forma, não há alterações incompatíveis com versões anteriores nos parâmetros necessários para criar conexões de destino.

>[!BEGINTABS]

>[!TAB Conexão base herdada e conexão de destino]

+++Exibir [!DNL base connection] herdado para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++Exibir [!DNL target connection] herdado para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nova conexão base e conexão de destino]

+++Exibir novos [!DNL base connection] para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++Exibir novos [!DNL target connection] para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Alterações incompatíveis com versões anteriores no destino SFTP {#changes-sftp-destination}

As alterações incompatíveis com versões anteriores para os usuários da API são um `connection spec ID` e `flow spec ID` atualizados, conforme mostrado na tabela abaixo:

| SFTP | Herdados | Novo |
|---------|----------|---------|
| Especificação de fluxo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaa4-bf2b-43fb-9387-43785eeeb799 |
| Especificação da conexão | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Além da especificação atualizada de fluxo e conexão acima, há alterações nos parâmetros necessários ao criar conexões básicas SFTP.

* Anteriormente, a conexão básica para destinos SFTP exigia um parâmetro `host`. Este parâmetro foi renomeado para `domain`.

Veja os exemplos completos de conexões base e de destino herdados e novos para SFTP nas guias abaixo, com as linhas que mudam realçadas. Os parâmetros necessários para criar conexões de destino para destinos SFTP não são alterados.

>[!BEGINTABS]

>[!TAB Conexão base herdada e conexão de destino]

+++Exibir [!DNL base connection] herdado para SFTP - autenticação de senha

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Exibir [!DNL base connection] herdado para autenticação [!DNL SFTP - SSH key]

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Exibir [!DNL target connection] herdado para SFTP

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nova conexão base e conexão de destino]

+++Exibir novos [!DNL base connection] para [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>",
      "port": 22      
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Exibir novo [!DNL base connection] para autenticação [!DNL SFTP - SSH key]

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Exibir novo [!DNL target connection] para SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Alterações incompatíveis com versões anteriores comuns a [!DNL Amazon S3], [!DNL Azure Blob] e destinos SFTP {#changes-all-destinations}

A etapa do seletor de perfil em todos os três destinos é substituída por uma etapa de mapeamento que permite renomear os cabeçalhos de coluna nos arquivos exportados, se desejado. Consulte a imagem lado a lado abaixo com a etapa do seletor de atributos antigo à esquerda e a nova etapa de mapeamento à direita.

![Imagem de visão geral do guia de migração](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Observe como o objeto `profileSelectors` nos exemplos herdados é substituído pelo novo objeto `profileMapping`.

Encontre informações completas sobre a configuração do objeto `profileMapping` no [tutorial de API para exportação de dados para destinos de armazenamento na nuvem](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Parâmetros de transformação antigos]

+++Exibir um exemplo de parâmetros de transformação antigos

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the audience selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB Novos parâmetros de transformação]

+++Exibir um exemplo de parâmetros de transformação após a migração

Observe no exemplo de configuração abaixo como `profileSelectors` campos foram substituídos por um objeto `profileMapping`.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the audience selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## Linha do tempo de migração e itens de ação {#timeline-and-action-items}

A migração de fluxos de dados herdados para os novos cartões de destino do [!DNL Amazon S3], [!DNL Azure Blob] e destinos SFTP ocorrerá assim que sua organização estiver pronta para migração e, o mais tardar, em **26 de julho de 2023**.

Você receberá emails de lembrete do Adobe à medida que a data da migração se aproximar. Em preparação, leia a seção Itens de ação abaixo para se preparar para a migração.

### Itens de ação {#action-items}

Como preparo para a migração dos destinos de armazenamento na nuvem do [!DNL Amazon S3], [!DNL Azure Blob] e SFTP para os novos cartões, prepare-se para atualizar seus scripts e chamadas de API automatizadas, conforme sugerido abaixo.

1. Atualize todos os scripts ou chamadas de API automatizadas para qualquer destino de armazenamento na nuvem existente do [!DNL Amazon S3], [!DNL Azure Blob] ou SFTP até 26 de julho de 2023. Quaisquer chamadas ou scripts de API automatizados que utilizam as especificações de conexão ou as especificações de fluxo herdadas precisam ser atualizados para as novas especificações de conexão ou especificações de fluxo.
2. Entre em contato com o representante de conta Adobe quando seus scripts forem atualizados antes de 26 de julho.
3. Por exemplo, o `targetConnectionSpecId` pode ser usado como um sinalizador para determinar se o fluxo de dados foi migrado para o novo cartão de destino. Você poderia atualizar seus scripts com uma condição `if` para verificar as especificações de conexão de destino herdadas e atualizadas em `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` e determinar se seu fluxo de dados foi migrado. Você pode ver as IDs de especificação de conexão novas e herdadas nas seções específicas desta página para cada destino.
4. Sua equipe de conta do Adobe entrará em contato com mais informações sobre quando seus fluxos de dados serão migrados.
5. Após 26 de julho, todos os fluxos de dados serão migrados. Todos os fluxos de dados existentes agora terão novas entidades de fluxo (especificações de conexão, especificações de fluxo, conexões de base e conexões de destino). Qualquer script ou chamada de API do seu lado que use as entidades de fluxo herdadas deixará de funcionar.

## Outras considerações de migração {#other-considerations}

Observe que não há impacto na programação existente para exportações durante ou após a migração.

## Próximas etapas {#next-steps}

Ao ler esta página, agora você sabe se precisa realizar alguma ação de preparação para a migração dos destinos de armazenamento na nuvem. Você também sabe quais páginas de documentação devem ser referenciadas à medida que configura fluxos de trabalho baseados em API para exportar arquivos do Experience Platform para seus destinos de armazenamento em nuvem preferidos. Em seguida, você pode exibir o tutorial da API para [exportar dados para destinos de armazenamento na nuvem](/help/destinations/api/activate-segments-file-based-destinations.md).
