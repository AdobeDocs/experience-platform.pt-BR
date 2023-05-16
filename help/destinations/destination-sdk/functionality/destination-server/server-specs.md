---
description: Saiba como configurar especificações do servidor de destino no Adobe Experience Platform Destination SDK por meio do endpoint `/authoring/destination-servers`.
title: Especificações do servidor para destinos criados com o Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# Especificações do servidor para destinos criados com o Destination SDK

As especificações do servidor de destino definem o tipo de plataforma de destino que receberá os dados do Adobe Experience Platform e os parâmetros de comunicação entre o Platform e seu destino. Por exemplo:

* A [transmissão](#streaming-example) a especificação do servidor de destino define o ponto de extremidade do servidor HTTP que receberá as mensagens HTTP da Platform. Para saber como configurar como as chamadas HTTP para o endpoint são formatadas, leia a [especificações de modelos](templating-specs.md) página.
* Um [Amazon S3](#s3-example) a especificação do servidor de destino define o [!DNL S3] nome do bucket e caminho onde a Platform exportará os arquivos.
* Um [SFTP](#sftp-example) a especificação do servidor de destino define o nome do host, o diretório raiz, a porta de comunicação e o tipo de criptografia do servidor SFTP, onde a Platform exportará os arquivos.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou veja as seguintes páginas de visão geral da configuração de destino:

* [Use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Você pode configurar as especificações do servidor de destino por meio da variável `/authoring/destination-servers` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração de servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página mostra todos os tipos de servidor de destino suportados pelo Destination SDK, com todos os seus parâmetros de configuração. Ao criar seu destino, substitua os valores do parâmetro pelos seus próprios.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Sim |

When [criação](../../authoring-api/destination-server/create-destination-server.md) ou [atualização](../../authoring-api/destination-server/update-destination-server.md) Em um servidor de destino, use uma das configurações do tipo de servidor descritas nesta página. Dependendo dos requisitos de integração, substitua os valores dos parâmetros de amostra desses exemplos pelos seus próprios.

## Campos codificados permanentemente versus campos modelos {#templatized-fields}

Ao criar um servidor de destino por meio do Destination SDK, é possível definir valores de parâmetros de configuração codificando-os permanentemente na configuração ou usando campos modelos. Campos modelados permitem ler valores fornecidos pelo usuário da plataforma.

Os parâmetros do servidor de destino têm dois campos configuráveis. Essas opções determinam se você está usando valores codificados ou modelos.

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `templatingStrategy` | String | *Obrigatório.* Define se há um valor codificado permanente fornecido pelo `value` ou um valor configurável pelo usuário na interface do usuário. Valores compatíveis: <ul><li>`NONE`: Use esse valor quando estiver codificando o valor do parâmetro por meio da variável `value` (consulte a próxima linha). Exemplo:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Use esse valor quando desejar que os usuários forneçam um valor de parâmetro na interface do usuário. Exemplo: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | String | *Obrigatório*. Define o valor do parâmetro. Tipos de valor compatíveis: <ul><li>**Valor codificado permanentemente**: Use um valor codificado permanentemente (como `"value": "my-storage-bucket"`) quando não for necessário que os usuários insiram um valor de parâmetro na interface do usuário. Ao codificar um valor, `templatingStrategy` deve ser sempre definido como `NONE`.</li><li>**Valor modelo**: Use um valor templatizado (como `"value": "{{customerData.bucket}}"`) quando quiser que seus usuários forneçam um valor de parâmetro na interface do usuário. Ao usar valores modelos, `templatingStrategy` deve ser sempre definido como `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quando usar campos embutidos versus campos modelados

Tanto os campos embutidos como os templatizados têm seus próprios usos no Destination SDK, dependendo do tipo de integração que você está criando.

**Conectar-se ao seu destino sem a entrada do usuário**

Quando os usuários [conectar-se ao seu destino](../../../ui/connect-destination.md) na interface do usuário da plataforma, talvez você queira lidar com o processo de conexão de destino sem a entrada.

Para fazer isso, você pode codificar os parâmetros de conexão da plataforma de destino na especificação do servidor. Ao usar valores de parâmetro codificados na configuração do servidor de destino, a conexão entre o Adobe Experience Platform e a plataforma de destino é feita sem qualquer entrada do usuário.

No exemplo abaixo, um parceiro cria um servidor de destino de Zona de aterrissagem de dados com a variável `path.value` campo que está sendo codificado.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Como resultado, quando os usuários passam pela variável [tutorial de conexão de destino](../../../ui/connect-destination.md), eles não verão uma [etapa de autenticação](../../../ui/connect-destination.md#authenticate). Em vez disso, a autenticação é realizada pela Platform, conforme mostrado na imagem abaixo.

![Imagem da interface do usuário que mostra a tela de autenticação entre Platform e um destino DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Conectar ao seu destino com entrada do usuário**

Quando a conexão entre a Platform e seu destino deve ser estabelecida seguindo uma entrada de usuário específica na interface do usuário da plataforma, como selecionar um endpoint da API ou fornecer um valor de campo, você pode usar campos modelos na especificação do servidor para ler a entrada do usuário e se conectar à sua plataforma de destino.

No exemplo abaixo, um parceiro cria um [tempo real (streaming)](#streaming-example) integração e `url.value` O campo usa o parâmetro templatizado `{{customerData.region}}` para personalizar parte do endpoint da API com base na entrada do usuário.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Para conceder aos usuários a opção de selecionar um valor na interface do usuário da plataforma, a variável `region` também deve ser definido na variável [configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) como um campo de dados do cliente, conforme mostrado abaixo:

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Como resultado, quando os usuários passam pela variável [tutorial de conexão de destino](../../../ui/connect-destination.md), eles devem selecionar uma região para se conectarem à plataforma de destino. Quando se conectam ao destino, o campo templatizado `{{customerData.region}}` é substituída pelo valor selecionado pelo usuário na interface do usuário, como mostrado na imagem abaixo.

![Imagem da interface do usuário que mostra a tela de conexão de destino com um seletor de região.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Servidor de destino em tempo real (streaming) {#streaming-example}

Esse tipo de servidor de destino permite exportar dados do Adobe Experience Platform para seu destino por meio de solicitações HTTP. A configuração do servidor contém informações sobre o servidor que recebe as mensagens (o servidor no seu lado).

Esse processo fornece dados do usuário como uma série de mensagens HTTP para sua plataforma de destino. Os parâmetros abaixo formam o modelo de especificações do servidor HTTP.

O exemplo abaixo mostra uma configuração de servidor de destino para um destino em tempo real (streaming).

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | *Obrigatório.* Representa um nome amigável do seu servidor, visível somente para o Adobe. Este nome não está visível para parceiros ou clientes. Exemplo: `Moviestar destination server`. |
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para destinos de transmissão. |
| `templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se você estiver usando um campo templatizado em vez de um valor codificado na variável `value` campo. Use essa opção se você tiver um terminal como: `https://api.moviestar.com/data/{{customerData.region}}/items`, onde os usuários devem selecionar a região do ponto de extremidade na interface do usuário da plataforma. </li><li> Use `NONE` se nenhuma transformação templatizada for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade da API ao qual o Experience Platform deve se conectar. |

{style="table-layout:auto"}

## [!DNL Amazon S3] servidor de destino {#s3-example}

Esse servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para seu armazenamento Amazon S3.

A amostra abaixo mostra um exemplo de configuração de servidor de destino para um destino Amazon S3.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome do servidor de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para exportar arquivos para um [!DNL Amazon S3] bucket, defina isso como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `bucket.value` campo.<ul><li>Se você quiser que seus usuários insiram seu próprio nome de bucket na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `value` para ler um valor do [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um nome de bucket codificado para a integração, como `"bucket.value":"MyBucket"`, em seguida, defina esse valor como `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | String | O nome do [!DNL Amazon S3] bucket a ser usado por este destino. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `path.value` campo.<ul><li>Se você quiser que seus usuários insiram seu próprio caminho na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `path.value` para ler um valor do [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um caminho codificado para a integração, como `"bucket.value":"/path/to/MyBucket"`, em seguida, defina esse valor como `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | String | O caminho para o [!DNL Amazon S3] bucket a ser usado por este destino. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] servidor de destino {#sftp-example}

Esse servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para seu [!DNL SFTP] servidor de armazenamento.

O exemplo abaixo mostra uma configuração de servidor de destino para um destino SFTP.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome do servidor de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para exportar arquivos para um [!DNL SFTP] , defina como `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `rootDirectory.value` campo.<ul><li>Se você quiser que seus usuários insiram seu próprio caminho de diretório raiz na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `rootDirectory.value` para ler um valor fornecido pelo usuário do campo [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho de diretório raiz codificado para a integração, como `"rootDirectory.value":"Storage/MyDirectory"`, em seguida, defina esse valor como `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | String | O caminho para o diretório que hospedará os arquivos exportados. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `hostName.value` campo.<ul><li>Se você quiser que seus usuários insiram seu próprio nome de host na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `hostName.value` para ler um valor fornecido pelo usuário do campo [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um nome de host codificado para sua integração, como `"hostName.value":"my.hostname.com"`, em seguida, defina esse valor como `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | String | O nome do host do seu servidor SFTP. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `"hostName.value":"my.hostname.com"`. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser utilizada a encriptação de ficheiros. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) servidor de destino {#adls-example}

Esse servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para seu [!DNL Azure Data Lake Storage] conta.

A amostra abaixo mostra um exemplo de configuração de servidor de destino para um [!DNL Azure Data Lake Storage] destino.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `path.value` campo.<ul><li>Se você quiser que seus usuários insiram seus [!DNL ADLS] caminho da pasta na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `path.value` para ler um valor do [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um caminho codificado para a integração, como `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, em seguida, defina esse valor como `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para sua [!DNL ADLS] pasta de armazenamento. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] servidor de destino {#blob-example}

Esse servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para seu [!DNL Azure Blob Storage] contêiner.

A amostra abaixo mostra um exemplo de configuração de servidor de destino para um [!DNL Azure Blob Storage] destino.

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Azure Blob Storage] destinos, defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `path.value` campo.<ul><li>Se você quiser que seus usuários insiram seus próprios [!DNL Azure Blob] [URI da conta de armazenamento](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `path.value` para ler o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um caminho codificado para a integração, como `"path.value": "https://myaccount.blob.core.windows.net/"`, em seguida, defina esse valor como `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para sua [!DNL Azure Blob] armazenamento. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `container.value` campo.<ul><li>Se você quiser que seus usuários insiram seus próprios [!DNL Azure Blob] [nome do contêiner](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `container.value` para ler o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um nome de contêiner codificado para a integração, como `"path.value: myContainer"`, em seguida, defina esse valor como `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do contêiner de Armazenamento Azure Blob a ser usado para esse destino. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) servidor de destino {#dlz-example}

Esse servidor de destino permite exportar arquivos contendo dados da plataforma para um [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) armazenamento.

A amostra abaixo mostra um exemplo de configuração de servidor de destino para um [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Data Landing Zone] destinos, defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `path.value` campo.<ul><li>Se você quiser que seus usuários insiram seus próprios [!DNL Data Landing Zone] na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `path.value` para ler um valor do [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um caminho codificado para a integração, como `"path.value": "https://myaccount.blob.core.windows.net/"`, em seguida, defina esse valor como `NONE`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] servidor de destino {#gcs-example}

Esse servidor de destino permite exportar arquivos contendo dados da plataforma para seu [!DNL Google Cloud Storage] conta.

A amostra abaixo mostra um exemplo de configuração de servidor de destino para um [!DNL Google Cloud Storage] destino.

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Google Cloud Storage] destinos, defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `bucket.value` campo.<ul><li>Se você quiser que seus usuários insiram seus próprios [!DNL Google Cloud Storage] nome do bucket na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `bucket.value` para ler um valor do [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um nome de bucket codificado para a integração, como `"bucket.value": "my-bucket"`, em seguida, defina esse valor como `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório*. Defina esse valor de acordo com o tipo de valor usado no `path.value` campo.<ul><li>Se você quiser que seus usuários insiram seus próprios [!DNL Google Cloud Storage] caminho do bucket na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar a variável `path.value` para ler um valor do [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um caminho codificado para a integração, como `"path.value": "/path/to/my-bucket"`, em seguida, defina esse valor como `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para o [!DNL Google Cloud Storage] pasta a ser usada por este destino. Pode ser um campo templatizado que lerá o valor da variável [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchido pelo usuário (como mostrado no exemplo acima) ou um valor codificado, como `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão do que é uma especificação do servidor de destino e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações de modelo](templating-specs.md)
* [Formato de mensagem](message-format.md)
* [Configuração de formatação de arquivo](file-formatting.md)
