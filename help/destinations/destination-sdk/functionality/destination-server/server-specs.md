---
description: Saiba como configurar especificações do servidor de destino no Adobe Experience Platform Destination SDK por meio do endpoint &grave;/authoring/destination-servers&grave;.
title: Especificações do servidor para destinos criados com o Destination SDK
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: 455886806d46a227eddb5ba060c15e1a00e13edf
workflow-type: tm+mt
source-wordcount: '2775'
ht-degree: 2%

---

# Especificações do servidor para destinos criados com o Destination SDK

As especificações do servidor de destino definem o tipo de plataforma de destino que receberá os dados do Adobe Experience Platform e os parâmetros de comunicação entre o Experience Platform e seu destino. Por exemplo:

* Uma especificação do servidor de destino de [transmissão](#streaming-example) define o ponto de extremidade do servidor HTTP que receberá as mensagens HTTP do Experience Platform. Para saber como as chamadas HTTP para o ponto de extremidade são formatadas, leia a página [especificações do modelo](templating-specs.md).
* Uma especificação do servidor de destino do [Amazon S3](#s3-example) define o nome e o caminho do bucket do [!DNL S3] para o qual o Experience Platform exportará os arquivos.
* Uma especificação do servidor de destino [SFTP](#sftp-example) define o nome do host, o diretório raiz, a porta de comunicação e o tipo de criptografia do servidor SFTP para o qual o Experience Platform exportará os arquivos.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação das [opções de configuração](../configuration-options.md) ou consulte as seguintes páginas de visão geral da configuração de destino:

* [Usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Você pode configurar as especificações do servidor de destino por meio do ponto de extremidade `/authoring/destination-servers`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração do servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página mostra todos os tipos de servidor de destino compatíveis com o Destination SDK, com todos os seus parâmetros de configuração. Ao criar seu destino, substitua os valores de parâmetro pelos seus próprios.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

Ao [criar](../../authoring-api/destination-server/create-destination-server.md) ou [atualizar](../../authoring-api/destination-server/update-destination-server.md) um servidor de destino, use uma das configurações de tipo de servidor descritas nesta página. Dependendo dos seus requisitos de integração, substitua os valores de parâmetro de amostra desses exemplos pelos seus próprios.

## Campos codificados permanentemente em comparação a campos de modelo {#templatized-fields}

Ao criar um servidor de destino por meio do Destination SDK, você pode definir os valores dos parâmetros de configuração codificando-os na configuração ou usando campos de modelo. Campos modelados permitem que você leia os valores fornecidos pelo usuário na interface do usuário do Experience Platform.

Os parâmetros do servidor de destino têm dois campos configuráveis. Essas opções determinam se você está usando valores codificados ou com modelos.

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `templatingStrategy` | String | *Obrigatório.* Define se há um valor embutido em código fornecido pelo campo `value` ou um valor configurável pelo usuário na interface. Valores compatíveis: <ul><li>`NONE`: Use esse valor quando estiver codificando o valor do parâmetro através do parâmetro `value` (veja a próxima linha). Exemplo:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Use esse valor quando quiser que os usuários forneçam um valor de parâmetro na interface. Exemplo: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | String | *Obrigatório*. Define o valor do parâmetro. Tipos de valores suportados: <ul><li>**Valor embutido em código**: use um valor embutido em código (como `"value": "my-storage-bucket"`) quando não precisar que os usuários insiram um valor de parâmetro na interface. Ao codificar permanentemente um valor, `templatingStrategy` deve sempre ser definido como `NONE`.</li><li>**Valor com modelo**: use um valor com modelo (como `"value": "{{customerData.bucket}}"`) quando quiser que os usuários forneçam um valor de parâmetro na interface. Ao usar valores de modelos, `templatingStrategy` deve sempre ser definido como `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quando usar campos embutidos em código ou com modelos

Os campos embutidos em código e em modelo têm seus próprios usos no Destination SDK, dependendo do tipo de integração que está sendo criada.

**Conectando ao seu destino sem entrada de usuário**

Quando os usuários [se conectam ao seu destino](../../../ui/connect-destination.md) na interface do usuário do Experience Platform, talvez você queira manipular o processo de conexão de destino sem suas entradas.

Para fazer isso, você pode codificar os parâmetros de conexão da plataforma de destino na especificação do servidor. Quando você usa valores de parâmetro embutidos em código na configuração do servidor de destino, a conexão entre o Adobe Experience Platform e a plataforma de destino é manipulada sem nenhuma entrada do usuário.

No exemplo abaixo, um parceiro cria um servidor de destino da Zona de aterrissagem de dados com o campo `path.value` codificado.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "dlz_destination"
   }
}
```

Como resultado, quando os usuários passam pelo [tutorial de conexão de destino](../../../ui/connect-destination.md), eles não veem uma [etapa de autenticação](../../../ui/connect-destination.md#authenticate). Em vez disso, a autenticação é realizada pelo Experience Platform, como mostrado na imagem abaixo.

![Imagem da interface do usuário mostrando a tela de autenticação entre o Experience Platform e um destino DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Conectando ao seu destino com a entrada do usuário**

Quando a conexão entre o Experience Platform e seu destino deve ser estabelecida seguindo uma entrada de usuário específica na interface do usuário do Experience Platform, como selecionar um endpoint de API ou fornecer um valor de campo, você pode usar campos modelos na especificação do servidor para ler a entrada do usuário e se conectar à plataforma de destino.

No exemplo abaixo, um parceiro cria uma integração [em tempo real (streaming)](#streaming-example) e o campo `url.value` usa o parâmetro de modelo `{{customerData.region}}` para personalizar parte do ponto de extremidade da API com base na entrada do usuário.

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

Para dar aos usuários a opção de selecionar um valor na interface do usuário do Experience Platform, o parâmetro `region` também deve ser definido na [configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) como um campo de dados do cliente, conforme mostrado abaixo:

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

Como resultado, quando os usuários passam pelo [tutorial de conexão de destino](../../../ui/connect-destination.md), eles devem selecionar uma região antes de se conectarem à plataforma de destino. Quando se conectam ao destino, o campo de modelo `{{customerData.region}}` é substituído pelo valor selecionado pelo usuário na interface, como mostrado na imagem abaixo.

![Imagem da interface do usuário mostrando a tela de conexão de destino com um seletor de região.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Servidor de destino (transmissão) em tempo real {#streaming-example}

Esse tipo de servidor de destino permite exportar dados do Adobe Experience Platform para o seu destino por meio de solicitações HTTP. A configuração do servidor contém informações sobre o servidor que recebe as mensagens (o servidor do seu lado).

Esse processo fornece dados do usuário como uma série de mensagens HTTP para a plataforma de destino. Os parâmetros abaixo formam o modelo de especificações do servidor HTTP.

A amostra abaixo mostra um exemplo de uma configuração de servidor de destino para um destino em tempo real (transmissão).

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
| `name` | String | *Obrigatório.* Representa um nome amigável do servidor, visível somente para o Adobe. Este nome não está visível para parceiros ou clientes. Exemplo: `Moviestar destination server`. |
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para destinos de streaming. |
| `templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se estiver usando um campo de modelo em vez de um valor embutido em código no campo `value`. Use esta opção se você tiver um ponto de extremidade como: `https://api.moviestar.com/data/{{customerData.region}}/items`, em que os usuários devem selecionar a região do ponto de extremidade na interface do usuário do Experience Platform. </li><li> Use `NONE` se nenhuma transformação com modelo for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade de API ao qual o Experience Platform deve se conectar. |

{style="table-layout:auto"}

## [!DNL Amazon S3] servidor de destino {#s3-example}

Esse servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para o armazenamento do Amazon S3.

A amostra abaixo mostra um exemplo de uma configuração de servidor de destino para um destino Amazon S3.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para exportar arquivos para um bucket [!DNL Amazon S3], configure-o como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `bucket.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio nome de bucket na interface do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `value` para ler um valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um nome de bucket embutido em código para a integração, como `"bucket.value":"MyBucket"`, defina esse valor como `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | String | O nome do bucket [!DNL Amazon S3] a ser usado por este destino. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `path.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio caminho na interface do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `path.value` para ler um valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho embutido em código para sua integração, como `"bucket.value":"/path/to/MyBucket"`, então defina esse valor como `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | String | O caminho para o bucket [!DNL Amazon S3] a ser usado por este destino. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] servidor de destino {#sftp-example}

Este servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para o servidor de armazenamento do [!DNL SFTP].

O exemplo abaixo mostra um exemplo de configuração de servidor de destino para um destino SFTP.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para exportar arquivos para um destino [!DNL SFTP], defina como `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `rootDirectory.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio caminho de diretório raiz na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `rootDirectory.value` para ler um valor fornecido pelo usuário dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho de diretório raiz embutido em código para a integração, como `"rootDirectory.value":"Storage/MyDirectory"`, defina esse valor como `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | String | O caminho para o diretório que hospedará os arquivos exportados. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `hostName.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio nome de host na interface do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `hostName.value` para ler um valor fornecido pelo usuário dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um nome de host codificado para sua integração, como `"hostName.value":"my.hostname.com"`, defina esse valor como `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | String | O nome do host do servidor SFTP. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `"hostName.value":"my.hostname.com"`. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser usada criptografia de arquivo. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) servidor de destino {#adls-example}

Este servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para sua conta do [!DNL Azure Data Lake Storage].

A amostra abaixo mostra um exemplo de uma configuração de servidor de destino para um destino [!DNL Azure Data Lake Storage].

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Azure Data Lake Storage], defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `path.value`.<ul><li>Se você quiser que seus usuários insiram o caminho de pasta [!DNL ADLS] na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `path.value` para ler um valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho embutido em código para sua integração, como `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, então defina esse valor como `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para a pasta de armazenamento do [!DNL ADLS]. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] servidor de destino {#blob-example}

Este servidor de destino permite exportar arquivos contendo dados do Adobe Experience Platform para o container [!DNL Azure Blob Storage].

A amostra abaixo mostra um exemplo de uma configuração de servidor de destino para um destino [!DNL Azure Blob Storage].

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Azure Blob Storage], defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `path.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio [!DNL Azure Blob] [URI da conta de armazenamento](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) na interface do Experience Platform, defina este valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `path.value` para ler o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho embutido em código para sua integração, como `"path.value": "https://myaccount.blob.core.windows.net/"`, então defina esse valor como `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para o armazenamento do [!DNL Azure Blob]. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `container.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio [!DNL Azure Blob] [nome do contêiner](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) na interface do Experience Platform, defina este valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `container.value` para ler o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um nome de contêiner embutido em código para sua integração, como `"path.value: myContainer"`, defina esse valor como `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do contêiner do Armazenamento Azure Blob a ser usado para esse destino. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) servidor de destino {#dlz-example}

Este servidor de destino permite exportar arquivos contendo dados do Experience Platform para um armazenamento do [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md).

A amostra abaixo mostra um exemplo de uma configuração de servidor de destino para um destino [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "dlz_destination"
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Data Landing Zone], defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `path.value`.<ul><li>Se você quiser que seus usuários insiram sua própria conta do [!DNL Data Landing Zone] na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `path.value` para ler um valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho embutido em código para sua integração, como `"path.value": "https://myaccount.blob.core.windows.net/"`, então defina esse valor como `NONE`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileBasedDlzDestination.useCase` | String | *Obrigatório*. Defina como `"dlz_destination"`. Esta propriedade identifica o destino como um destino [!DNL Data Landing Zone]. Esta propriedade só é usada ao criar um destino [!DNL Data Landing Zone]. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] servidor de destino {#gcs-example}

Este servidor de destino permite exportar arquivos contendo dados do Experience Platform para sua conta do [!DNL Google Cloud Storage].

A amostra abaixo mostra um exemplo de uma configuração de servidor de destino para um destino [!DNL Google Cloud Storage].

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Google Cloud Storage], defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `bucket.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio nome de bucket [!DNL Google Cloud Storage] na interface do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `bucket.value` para ler um valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se você estiver usando um nome de bucket embutido em código para a integração, como `"bucket.value": "my-bucket"`, defina esse valor como `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do bucket [!DNL Google Cloud Storage] a ser usado por este destino. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório*. Defina este valor de acordo com o tipo de valor usado no campo `path.value`.<ul><li>Se você quiser que seus usuários insiram seu próprio caminho de bucket de [!DNL Google Cloud Storage] na interface do usuário do Experience Platform, defina esse valor como `PEBBLE_V1`. Nesse caso, você deve modelar o campo `path.value` para ler um valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário. Esse caso de uso é mostrado no exemplo acima.</li><li>Se estiver usando um caminho embutido em código para sua integração, como `"path.value": "/path/to/my-bucket"`, então defina esse valor como `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para a pasta [!DNL Google Cloud Storage] a ser usada por este destino. Pode ser um campo de modelo que lerá o valor dos [campos de dados do cliente](../destination-configuration/customer-data-fields.md) preenchidos pelo usuário (como mostrado no exemplo acima), ou um valor embutido em código, como `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você terá que entender melhor o que é uma especificação de servidor de destino e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações de modelo](templating-specs.md)
* [Formato da mensagem](message-format.md)
* [Configuração da formatação de arquivo](file-formatting.md)
