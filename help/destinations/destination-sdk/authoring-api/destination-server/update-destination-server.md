---
description: Esta página exemplifica a chamada da API usada para atualizar uma configuração de servidor de destino existente por meio do Adobe Experience Platform Destination SDK.
title: Atualizar uma configuração de servidor de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 12%

---


# Atualizar uma configuração de servidor de destino

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para atualizar uma configuração de servidor de destino existente, usando o `/authoring/destination-servers` Ponto de extremidade da API.

>[!TIP]
>
>Qualquer operação de atualização em destinos produzidos/públicos é visível somente após o uso da variável [API de publicação](../../publishing-api/create-publishing-request.md) e envie a atualização para revisão do Adobe.

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

## Atualizar uma configuração de servidor de destino {#update}

Você pode atualizar um [existente](create-destination-server.md) configuração do servidor de destino fazendo uma `PUT` à `/authoring/destination-servers` endpoint com a carga útil atualizada.

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Para obter uma configuração de servidor de destino existente e sua correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperar uma configuração de servidor de destino](retrieve-destination-server.md).

**Formato da API**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração do servidor de destino que você deseja atualizar. Para obter uma configuração de servidor de destino existente e sua correspondente `{INSTANCE_ID}`, consulte [Recuperar uma configuração do servidor de destino](retrieve-destination-server.md). |

As solicitações a seguir atualizam uma configuração de servidor de destino existente, configurada pelos parâmetros fornecidos no payload.

Selecione cada guia abaixo para visualizar a carga correspondente.

>[!BEGINTABS]

>[!TAB Tempo real (streaming)]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
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
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar o URL no `value` abaixo. Use essa opção se você tiver um terminal como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade da API ao qual o Experience Platform deve se conectar. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o seu servidor. As opções são `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | String | *Obrigatório.* Essa é a versão sem caracteres que transforma os dados dos clientes da Platform no formato que seu serviço espera. <br> <ul><li> Para obter informações sobre como gravar o modelo, leia o [Uso da seção de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte [Padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de transformação simples, consulte [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes) transformação. </li></ul> |
| `httpTemplate.contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Esse valor provavelmente `application/json`. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!TAB Amazon S3]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!TAB SFTP]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!TAB Armazenamento Azure Data Lake]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!TAB Armazenamento Azure Blob]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!TAB Zona de aterrissagem de dados (DLZ)]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!TAB Armazenamento em nuvem Google]

+++Solicitação

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração atualizada do servidor de destino.

+++

>[!ENDTABS]

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como atualizar uma configuração de servidor de destino por meio do Destination SDK `/authoring/destination-servers` Ponto de extremidade da API.

Para saber mais sobre o que você pode fazer com esse terminal, consulte os seguintes artigos:

* [Criar uma configuração de servidor de destino](create-destination-server.md)
* [Recuperar uma configuração do servidor de destino](retrieve-destination-server.md)
* [Atualizar uma configuração de servidor de destino](update-destination-server.md)