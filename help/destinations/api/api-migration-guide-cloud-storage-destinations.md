---
solution: Experience Platform
title: Guia de migração de API para destinos de armazenamento em nuvem
description: Saiba mais sobre as alterações no workflow para ativar destinos de armazenamento em nuvem como parte da migração para os novos cartões de destino de armazenamento em nuvem com funcionalidade adicional.
type: Tutorial
source-git-commit: 6ed78a96f099fb4552716ac4a598c43f4d65cf37
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---

# Guia de migração de API para destinos de armazenamento em nuvem

>[!IMPORTANT]
>
>* A funcionalidade descrita nesta página está disponível para clientes que compraram os pacotes Real-Time CDP Prime e Ultimate. Entre em contato com o representante da Adobe para obter mais informações.


## Contexto de migração {#migration-context}

Início [Outubro de 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations), você pode usar os novos recursos de exportação de arquivos para acessar a funcionalidade de personalização aprimorada ao exportar arquivos do Experience Platform:

* Adicional [opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Capacidade de definir cabeçalhos de arquivo personalizados em seus arquivos exportados por meio do [nova etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Capacidade de selecionar a variável [tipo de arquivo](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) do arquivo exportado.
* Capacidade de [personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Essa funcionalidade é compatível com os cartões de armazenamento da nuvem beta listados abaixo:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Observe que, atualmente na interface do usuário do Experience Platform, você pode ver duas placas de destino lado a lado dos três destinos. Mostrado abaixo é o [!DNL Amazon S3] destinos herdados e novos. Em todos os casos, os cartões marcados com **Beta** são os novos cartões de destino.

![Imagem das duas placas de destino Amazon S3 em uma exibição lado a lado.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Embora esses destinos com funcionalidade aprimorada tenham sido oferecidos inicialmente como um beta, *O Adobe agora está movendo todos os clientes do Real-Time CDP para os novos destinos de armazenamento em nuvem*. Para clientes que já estavam usando [!DNL Amazon S3], [!DNL Azure Blob]ou SFTP, isso significa que os fluxos de dados existentes serão migrados para os novos cartões. Leia para obter mais informações sobre as alterações específicas como parte da migração.

## A quem esta página se aplica {#who-this-applies-to}

Se você já estiver usando o [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/) para exportar perfis para os destinos de armazenamento em nuvem Amazon S3, Azure Blob ou SFTP, esse guia de migração de API se aplica a você.

Se você tiver scripts em execução em [!DNL Amazon S3], [!DNL Azure Blob]ou locais de armazenamento em nuvem SFTP sobre os arquivos exportados do Experience Platform, esteja ciente de que alguns parâmetros estão mudando em relação às especificações de conexão e fluxo dos novos cartões, bem como em relação à etapa de mapeamento.

Por exemplo, se você estava usando um script para filtrar os fluxos de dados de destino para a variável [!DNL Amazon S3] destino, com base na especificação da conexão do [!DNL Amazon S3] de destino, esteja ciente de que a especificação da conexão será alterada para que você precise atualizar seus filtros.

## Links de documentação relevantes {#relevant-documentation-links}

Esta seção inclui o tutorial de API relevante e a documentação de referência para a funcionalidade aprimorada de exportar dados para destinos de armazenamento em nuvem.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [Tutorial de API para exportar segmentos para destinos de armazenamento em nuvem](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Documentação de referência da API do Serviço de fluxo de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Resumo de alterações retroativas incompatíveis {#summary-backwards-incompatible-changes}

Com a migração para novos destinos, todos os seus fluxos de dados existentes fluem para o [!DNL Amazon S3], [!DNL Azure Blob]Agora, os destinos e SFTP receberão novas conexões de destino e conexões básicas. A etapa de mapeamento de perfil também muda. As alterações incompatíveis com o fundo são resumidas nas seções abaixo para cada destino. Exibir também a [glossário de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) para obter mais informações sobre os termos no diagrama abaixo.

![Imagem de visão geral do guia de migração](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Alterações retroativamente incompatíveis no [!DNL Amazon S3] destino {#changes-amazon-s3-destination}

As alterações retroativas incompatíveis para os usuários da API são uma atualização `connection spec ID` e `flow spec ID` conforme mostrado na tabela abaixo:

| [!DNL Amazon S3] | Herdado | Novo |
|---------|----------|---------|
| Especificação de fluxo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Especificação de conexão | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Veja os exemplos completos de conexão herdada e nova base e de conexão de destino para [!DNL Amazon S3] nas guias abaixo. Os parâmetros necessários para criar conexões básicas para [!DNL Amazon S3] os destinos não são alterados.

Da mesma forma, não há alterações retroativas incompatíveis nos parâmetros necessários para criar conexões de público-alvo.

>[!BEGINTABS]

>[!TAB Conexão básica e de destino herdadas]

+++Exibir legado [!DNL base connection] para [!DNL Amazon S3]

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

+++Exibir legado [!DNL target connection] para [!DNL Amazon S3]

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

>[!TAB Nova conexão básica e de destino]

+++Exibir novo [!DNL base connection] para [!DNL Amazon S3]

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

+++Exibir novo [!DNL target connection] para [!DNL Amazon S3]

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

### Alterações retroativas incompatíveis para [!DNL Azure Blob] destino {#changes-azure-blob-destination}

As alterações retroativas incompatíveis para os usuários da API são uma atualização `connection spec ID` e `flow spec ID` conforme mostrado na tabela abaixo:

| [!DNL Azure Blob] | Herdado | Novo |
|---------|----------|---------|
| Especificação de fluxo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Especificação de conexão | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Veja os exemplos completos de conexão herdada e nova base e de conexão de destino para [!DNL Azure Blob] nas guias abaixo. Os parâmetros necessários para criar conexões básicas para destinos do Azure Blob não são alterados.

Da mesma forma, não há alterações retroativas incompatíveis nos parâmetros necessários para criar conexões de público-alvo.

>[!BEGINTABS]

>[!TAB Conexão básica e de destino herdadas]

+++Exibir legado [!DNL base connection] para [!DNL Azure Blob]

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

+++Exibir legado [!DNL target connection] para [!DNL Azure Blob]

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

>[!TAB Nova conexão básica e de destino]

+++Exibir novo [!DNL base connection] para [!DNL Azure Blob]

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

+++Exibir novo [!DNL target connection] para [!DNL Azure Blob]

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

### Alterações retroativas incompatíveis no destino SFTP {#changes-sftp-destination}

As alterações retroativas incompatíveis para os usuários da API são uma atualização `connection spec ID` e `flow spec ID` conforme mostrado na tabela abaixo:

| SFTP | Herdado | Novo |
|---------|----------|---------|
| Especificação de fluxo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 354d6aad-4754-46e4-a576-1b384561c440 |
| Especificação de conexão | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Além da especificação de fluxo e conexão atualizada acima, há alterações nos parâmetros necessários ao criar conexões base SFTP.

* Anteriormente, a conexão base para destinos SFTP exigia uma `host` parâmetro. Esse parâmetro foi renomeado para `domain`.
* Para a opção autenticação com chave SSH, os parâmetros de autenticação na conexão base exigiam uma `port` opção. Esse parâmetro agora está obsoleto e não é mais necessário.

Exiba os exemplos completos de conexão herdada e nova base e conexão de destino para SFTP nas guias abaixo, com as linhas que mudam realçadas. Os parâmetros necessários para criar conexões de destino para destinos SFTP não são alterados.

>[!BEGINTABS]

>[!TAB Conexão básica e de destino herdadas]

+++Exibir legado [!DNL base connection] para SFTP - autenticação por senha

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

+++Exibir legado [!DNL base connection] para [!DNL SFTP - SSH key] autenticação

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

+++Exibir legado [!DNL target connection] para SFTP

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

>[!TAB Nova conexão básica e de destino]

+++Exibir novo [!DNL base connection] para [!DNL SFTP - password authentication]

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
      "password": "<your-password>"
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

+++Exibir novo [!DNL base connection] para [!DNL SFTP - SSH key] autenticação

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

### Alterações retroativas incompatíveis comuns a [!DNL Amazon S3], [!DNL Azure Blob]e destinos SFTP {#changes-all-destinations}

A etapa do seletor de perfil em todos os três destinos é substituída por uma etapa de mapeamento que permite renomear os cabeçalhos da coluna em seus arquivos exportados, se desejado. Consulte a imagem lado a lado abaixo com a etapa antiga do seletor de atributos à esquerda e a nova etapa de mapeamento à direita.

![Imagem de visão geral do guia de migração](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Observe como a função `profileSelectors` nos exemplos herdados é substituído pelo novo `profileMapping` objeto.

Encontre informações completas sobre a configuração da variável `profileMapping` na [Tutorial de API para exportar dados para destinos de armazenamento em nuvem](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Parâmetros de transformação antigos]

+++Visualizar um exemplo de parâmetros de transformação antigos

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
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

+++Visualize um exemplo de parâmetros de transformação após a migração

Observe no exemplo de configuração abaixo como `profileSelectors` foram substituídos por `profileMapping` objeto.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
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

## Linha do tempo e itens de ação da migração {#timeline-and-action-items}

A migração de fluxos de dados herdados para os novos cartões de destino para [!DNL Amazon S3], [!DNL Azure Blob]e os destinos SFTP ocorrerão assim que sua organização estiver pronta para migrar e até **30 de junho de 2023**.

Você receberá emails de lembrete do Adobe à medida que a data de migração se aproxima. Em preparação, leia a seção Itens de ação abaixo para se preparar para a migração.

### Itens de ação {#action-items}

Em preparação para a migração do [!DNL Amazon S3], [!DNL Azure Blob]e os destinos de armazenamento em nuvem SFTP para os novos cartões, prepare-se para atualizar seus scripts e chamadas de API automatizadas, conforme sugerido abaixo.

1. Atualize qualquer script ou chamada de API automatizada para qualquer [!DNL Amazon S3], [!DNL Azure Blob]ou destinos de armazenamento em nuvem SFTP até 30 de junho de 2023. Qualquer chamada ou script de API automatizada que aproveite as especificações ou especificações de fluxo de conexão herdadas precisa ser atualizada para as novas especificações de conexão ou especificações de fluxo.
2. Entre em contato com seu representante de conta do Adobe quando seus scripts tiverem sido atualizados antes de 30 de junho.
3. Por exemplo, a variável `targetConnectionSpecId` pode ser usado como um sinalizador para determinar se o fluxo de dados foi migrado para o novo cartão de destino. Você pode atualizar seus scripts com um `if` condição para examinar as especificações de conexão herdadas e atualizadas do target em `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` e determinam se o seu fluxo de dados foi migrado. Você pode ver as IDs de especificação de conexão herdadas e novas nas seções específicas desta página para cada destino.
4. Sua equipe de conta do Adobe entrará em contato com mais informações sobre quando seus fluxos de dados serão migrados.
5. Após 30 de junho, todos os fluxos de dados serão migrados. Todos os seus fluxos de dados existentes agora terão novas entidades de fluxo (especificações de conexão, especificações de fluxo, conexões básicas e conexões de destino). Qualquer script ou chamada de API do seu lado que use as entidades de fluxo herdadas deixará de funcionar.

## Outras considerações sobre migração {#other-considerations}

Observe que não há impacto na programação existente de exportações durante ou após a migração.

## Próximas etapas {#next-steps}

Ao ler esta página, agora você sabe se precisa tomar alguma ação em preparação para a migração dos destinos de armazenamento em nuvem. Você também sabe quais páginas de documentação fazer referência conforme configura workflows com base em API para exportar arquivos do Experience Platform para seus destinos de armazenamento em nuvem preferidos. Em seguida, você pode visualizar o tutorial de API em [exportar dados para destinos de armazenamento em nuvem](/help/destinations/api/activate-segments-file-based-destinations.md).