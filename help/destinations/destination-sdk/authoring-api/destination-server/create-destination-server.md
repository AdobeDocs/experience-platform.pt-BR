---
description: Esta página exemplifica a chamada da API usada para criar um servidor de destino por meio do Adobe Experience Platform Destination SDK.
title: Criar uma configuração de servidor de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 10%

---


# Criar uma configuração de servidor de destino

Criar um servidor de destino é a primeira etapa na criação de seu próprio destino com o Destination SDK. O servidor de destino inclui opções de configuração para a variável [server](../../functionality/destination-server/server-specs.md) e [modelo](../../functionality/destination-server/templating-specs.md) especificações, a variável [formato de mensagem](../../functionality/destination-server/message-format.md)e o [formatação de arquivo](../../functionality/destination-server/file-formatting.md) opções (para destinos com base em arquivo).

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para criar seu próprio servidor de destino usando o `/authoring/destination-servers` Ponto de extremidade da API.

Para obter uma descrição detalhada dos recursos que podem ser configurados por meio desse terminal, leia os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Especificações de modelo para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato de mensagem](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuração de formatação de arquivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do servidor de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar uma configuração de servidor de destino {#create}

Você pode criar uma nova configuração de servidor de destino fazendo uma `POST` à `/authoring/destination-servers` endpoint .

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato da API**

```http
POST /authoring/destination-servers
```

Dependendo do tipo de destino que você criar, será necessário configurar um tipo de servidor de destino diferente. Consulte nos exemplos abaixo de servidores de destino para cada tipo de destino suportado no Destination SDK.

As cargas de exemplo abaixo incluem todos os parâmetros suportados por cada tipo de servidor de destino. Não é necessário incluir todos os parâmetros na solicitação. A carga é personalizável de acordo com suas necessidades.

Selecione cada guia abaixo para exibir as solicitações de API correspondentes.

>[!BEGINTABS]

>[!TAB Tempo real (streaming)]

**Criar um servidor de destino em tempo real (streaming)**

Você precisa criar um servidor de destino em tempo real (streaming) semelhante ao mostrado abaixo ao configurar uma integração baseada em API em tempo real (streaming).

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `name` | String | *Obrigatório.* Representa um nome amigável do seu servidor, visível somente para o Adobe. Este nome não está visível para parceiros ou clientes. Exemplo `Moviestar destination server`. |
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para destinos em tempo real (streaming). |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar o URL no `value` abaixo. Use essa opção se tiver um terminal como `https://api.moviestar.com/data/{{customerData.region}}/items`, em que `region` pode ser diferente entre clientes. Nesse caso, também é necessário configurar `region` como [campo de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) no [configuração de destino](../destination-configuration/create-destination-configuration.md). </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade da API ao qual o Experience Platform deve se conectar. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o seu servidor. As opções são `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | String | *Obrigatório.* Essa é a versão sem caracteres que transforma os dados dos clientes da Platform no formato que seu serviço espera. <br> <ul><li> Para obter informações sobre como gravar o modelo, leia o [Uso da seção de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte [Padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de transformação simples, consulte [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes) transformação. </li></ul> |
| `httpTemplate.contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Esse valor provavelmente `application/json`. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Amazon S3]

**Criar um servidor de destino Amazon S3**

Você precisa criar um [!DNL Amazon S3] servidor de destino semelhante ao mostrado abaixo quando você configura um arquivo baseado em [!DNL Amazon S3] destino.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Amazon S3], defina como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | String | O nome do [!DNL Amazon S3] bucket a ser usado por este destino. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB SFTP]

**Crie um [!DNL SFTP] servidor de destino**

Você precisa criar um [!DNL SFTP] servidor de destino semelhante ao mostrado abaixo quando você configura um arquivo baseado em [!DNL SFTP] destino.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL SFTP] destinos, defina como `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | String | O diretório raiz do armazenamento de destino. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | String | O nome do host do armazenamento de destino. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser utilizada a encriptação de ficheiros. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento Azure Data Lake]

**Crie um [!DNL Azure Data Lake Storage] servidor de destino**

Você precisa criar um [!DNL Azure Data Lake Storage] servidor de destino semelhante ao mostrado abaixo quando você configura um arquivo baseado em [!DNL Azure Data Lake Storage] destino.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento Azure Blob]

**Crie um [!DNL Azure Blob Storage] servidor de destino**

Você precisa criar um [!DNL Azure Blob Storage] servidor de destino semelhante ao mostrado abaixo quando você configura um arquivo baseado em [!DNL Azure Blob Storage] destino.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Azure Blob Storage] destinos, defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do [!DNL Azure Blob Storage] contêiner a ser usado por este destino. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Zona de aterrissagem de dados (DLZ)]

**Crie um [!DNL Data Landing Zone (DLZ)] servidor de destino**

Você precisa criar um [!DNL Data Landing Zone (DLZ)] servidor de destino semelhante ao mostrado abaixo quando você configura um arquivo baseado em [!DNL Data Landing Zone (DLZ)] destino.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Data Landing Zone] destinos, defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento em nuvem Google]

**Crie um [!DNL Google Cloud Storage] servidor de destino**

Você precisa criar um [!DNL Google Cloud Storage] servidor de destino semelhante ao mostrado abaixo quando você configura um arquivo baseado em [!DNL Google Cloud Storage] destino.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Google Cloud Storage] destinos, defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Servidor de esquema dinâmico]

**Criar um servidor de esquema dinâmico**

É necessário criar um servidor de esquema dinâmico semelhante ao mostrado abaixo ao configurar um destino que recupera o esquema do perfil do seu próprio ponto de extremidade de API. Ao contrário de um schema estático, um schema dinâmico não usa um `profileFields` matriz. Em vez disso, os esquemas dinâmicos usam um servidor de esquema dinâmico que se conecta à sua própria API de onde recupera a configuração do esquema.

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `name` | String | *Obrigatório.* Representa um nome amigável para o servidor de esquema dinâmico, visível somente para Adobe. |
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para servidores de esquema dinâmicos. |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar o URL no `value` abaixo. Use essa opção se você tiver um terminal como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade da API ao qual o Experience Platform deve se conectar e recuperar os campos do esquema para preencher como campos de destino na etapa de mapeamento do fluxo de trabalho de ativação. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o seu servidor. Para servidores de esquema dinâmicos, use `GET`. |
| `responseFields.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `responseFields.value` | String | *Obrigatório.* Essa string é o modelo de transformação com escape de caractere que transforma a resposta recebida da API do parceiro no schema do parceiro que será exibido na interface do usuário da plataforma. <br> <ul><li> Para obter informações sobre como gravar o modelo, leia o [Uso da seção de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte [Padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de transformação simples, consulte [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes) transformação. </li></ul> |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!ENDTABS]

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como criar um novo servidor de destino por meio do Destination SDK `/authoring/destination-servers` Ponto de extremidade da API.

Para saber mais sobre o que você pode fazer com esse terminal, consulte os seguintes artigos:

* [Recuperar uma configuração do servidor de destino](retrieve-destination-server.md)
* [Atualizar uma configuração de servidor de destino](update-destination-server.md)
* [Excluir uma configuração de servidor de destino](delete-destination-server.md)

Para entender onde esse terminal se encaixa no processo de criação de destino, consulte os seguintes artigos:

* [Use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)