---
description: Esta página exemplifica a chamada à API usada para criar um servidor de destino por meio do Adobe Experience Platform Destination SDK.
title: Criar uma configuração do servidor de destino
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: e1dd6ae9bf28014e8e84de85bdf67707744ea0ad
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 6%

---

# Criar uma configuração do servidor de destino

Criar um servidor de destino é a primeira etapa na criação de seu próprio destino com o Destination SDK. O servidor de destino inclui opções de configuração para as especificações do [servidor](../../functionality/destination-server/server-specs.md) e do [modelo](../../functionality/destination-server/templating-specs.md), o [formato de mensagem](../../functionality/destination-server/message-format.md) e as opções de [formatação de arquivo](../../functionality/destination-server/file-formatting.md) (para destinos baseados em arquivo).

Esta página exemplifica a solicitação de API e a carga que você pode usar para criar seu próprio servidor de destino usando o ponto de extremidade de API `/authoring/destination-servers`.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio desse endpoint, leia os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Especificações de modelos para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato da mensagem](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuração da formatação de arquivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do servidor de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Criar uma configuração do servidor de destino {#create}

Você pode criar uma nova configuração do servidor de destino fazendo uma solicitação `POST` para o ponto de extremidade `/authoring/destination-servers`.

>[!TIP]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato da API**

```http
POST /authoring/destination-servers
```

Dependendo do tipo de destino criado, é necessário configurar um tipo de servidor de destino ligeiramente diferente.

### Criar servidores de destino de esquema estáticos {#static-destination-servers}

Consulte nas guias abaixo exemplos de servidores de destino para destinos que usam [esquemas estáticos](../../functionality/destination-configuration/schema-configuration.md#attributes-schema).

As cargas de exemplo abaixo incluem todos os parâmetros compatíveis com cada tipo de servidor de destino. Não é necessário incluir todos os parâmetros em sua solicitação. A carga é personalizável com base nas suas necessidades.

Selecione cada guia abaixo para exibir as solicitações de API correspondentes.

>[!BEGINTABS]

>[!TAB Tempo real (streaming)]

**Criar um servidor de destino (streaming) em tempo real**

Você precisa criar um servidor de destino em tempo real (transmissão) semelhante ao mostrado abaixo ao configurar uma integração baseada em API em tempo real (transmissão).

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
| `name` | String | *Obrigatório.* Representa um nome amigável do servidor, visível somente para o Adobe. Este nome não está visível para parceiros ou clientes. Exemplo `Moviestar destination server`. |
| `destinationServerType` | String | *Obrigatório.* Definido como `URL_BASED` para destinos em tempo real (streaming). |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar a URL no campo `value` abaixo. Use esta opção se você tiver um ponto de extremidade como `https://api.moviestar.com/data/{{customerData.region}}/items`, em que a parte `region` pode ser diferente entre os clientes. Nesse caso, você também precisa configurar `region` como um [campo de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) na [configuração de destino]&#x200B;(../destination-configuration/create-destination-configuration.md. </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade de API ao qual o Experience Platform deve se conectar. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. As opções são `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | String | *Obrigatório.* Esta cadeia de caracteres é a versão com caractere de escape que transforma os dados de clientes do Experience Platform no formato que seu serviço espera. <br> <ul><li> Para obter informações sobre como gravar o modelo, leia a [seção Uso de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte o [padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de uma transformação simples, consulte a transformação [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Este valor provavelmente é `application/json`. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Amazon S3]

**Criar um servidor de destino do Amazon S3**

Você precisa criar um servidor de destino [!DNL Amazon S3] semelhante ao mostrado abaixo ao configurar um destino [!DNL Amazon S3] baseado em arquivo.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Amazon S3], defina como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | String | O nome do bucket [!DNL Amazon S3] a ser usado por este destino. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB SFTP]

**Criar um [!DNL SFTP] servidor de destino**

Você precisa criar um servidor de destino [!DNL SFTP] semelhante ao mostrado abaixo ao configurar um destino [!DNL SFTP] baseado em arquivo.

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
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL SFTP], defina como `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | String | O diretório raiz do armazenamento de destino. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | String | O nome do host do armazenamento de destino. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser usada criptografia de arquivo. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento do Azure Data Lake]

**Criar um [!DNL Azure Data Lake Storage] servidor de destino**

Você precisa criar um servidor de destino [!DNL Azure Data Lake Storage] semelhante ao mostrado abaixo ao configurar um destino [!DNL Azure Data Lake Storage] baseado em arquivo.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Azure Data Lake Storage], defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento Azure Blob]

**Criar um [!DNL Azure Blob Storage] servidor de destino**

Você precisa criar um servidor de destino [!DNL Azure Blob Storage] semelhante ao mostrado abaixo ao configurar um destino [!DNL Azure Blob Storage] baseado em arquivo.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Azure Blob Storage], defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do contêiner [!DNL Azure Blob Storage] a ser usado por este destino. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB DLZ (Zona de Aterrissagem de Dados)]

**Criar um [!DNL Data Landing Zone (DLZ)] servidor de destino**

Você precisa criar um servidor de destino [!DNL Data Landing Zone (DLZ)] semelhante ao mostrado abaixo ao configurar um destino [!DNL Data Landing Zone (DLZ)] baseado em arquivo.

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
      "useCase": "dlz_destination"
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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Data Landing Zone], defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento na nuvem do Google]

**Criar um [!DNL Google Cloud Storage] servidor de destino**

Você precisa criar um servidor de destino [!DNL Google Cloud Storage] semelhante ao mostrado abaixo ao configurar um destino [!DNL Google Cloud Storage] baseado em arquivo.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para destinos [!DNL Google Cloud Storage], defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do bucket [!DNL Google Cloud Storage] a ser usado por este destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração de formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!ENDTABS]

### Criar servidores de destino de esquema dinâmico {#dynamic-schema-servers}

Os esquemas dinâmicos permitem recuperar dinamicamente os atributos de destino compatíveis e gerar esquemas com base em sua própria API. Você precisa configurar um servidor de destino para esquemas dinâmicos antes de poder configurar o esquema.

Veja na guia abaixo um exemplo de servidor de destino para destinos que usam [esquemas dinâmicos](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

A carga de exemplo abaixo inclui todos os parâmetros necessários para um servidor de esquema dinâmico.

>[!BEGINTABS]

>[!TAB Servidor de esquema dinâmico]

**Criar um servidor de esquema dinâmico**

É necessário criar um servidor de esquema dinâmico semelhante ao mostrado abaixo ao configurar um destino que recupera o esquema de perfil de seu próprio ponto de acesso de API. Ao contrário de um esquema estático, um esquema dinâmico não usa uma matriz `profileFields`. Em vez disso, os esquemas dinâmicos usam um servidor de esquema dinâmico que se conecta à sua própria API de onde recupera a configuração do esquema.

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
| `name` | String | *Obrigatório.* Representa um nome amigável do servidor de esquema dinâmico, visível somente para o Adobe. |
| `destinationServerType` | String | *Obrigatório.* Definido como `URL_BASED` para servidores de esquema dinâmicos. |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar a URL no campo `value` abaixo. Use esta opção se você tiver um ponto de extremidade como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade de API ao qual o Experience Platform deve se conectar e recuperar os campos de esquema para serem preenchidos como campos de destino na etapa de mapeamento do fluxo de trabalho de ativação. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. Para servidores de esquema dinâmicos, use `GET`. |
| `responseFields.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `responseFields.value` | String | *Obrigatório.* Esta cadeia de caracteres é o modelo de transformação com escape de caracteres que transforma a resposta recebida da API do parceiro no esquema do parceiro que será exibido na interface do usuário do Experience Platform. <br> <ul><li> Para obter informações sobre como gravar o modelo, leia a [seção Uso de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte o [padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de uma transformação simples, consulte a transformação [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++


>[!ENDTABS]


### Criar servidores de destino de lista suspensa dinâmica {#dynamic-dropdown-servers}

Use [menus suspensos dinâmicos](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) para recuperar e preencher dinamicamente campos suspensos de dados do cliente, com base em sua própria API. Por exemplo, você pode recuperar uma lista de contas de usuário existentes que deseja usar para uma conexão de destino.

Você precisa configurar um servidor de destino para menus suspensos dinâmicos antes de poder configurar o campo de dados do cliente da lista suspensa dinâmica.

Consulte na guia abaixo um exemplo de servidor de destino usado para recuperar dinamicamente os valores a serem exibidos em um seletor suspenso, de uma API.

A carga de exemplo abaixo inclui todos os parâmetros necessários para um servidor de esquema dinâmico.

>[!BEGINTABS]

>[!TAB Servidor de lista suspensa dinâmico]

**Criar um servidor suspenso dinâmico**

É necessário criar um servidor suspenso dinâmico semelhante ao mostrado abaixo ao configurar um destino que recupera os valores de um campo suspenso de dados do cliente do seu próprio ponto de acesso de API.

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
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Parâmetro | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `name` | String | *Obrigatório.* Representa um nome amigável do servidor de lista suspensa dinâmica, visível somente para o Adobe. |
| `destinationServerType` | String | *Obrigatório.* Definido como `URL_BASED` para servidores suspensos dinâmicos. |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar a URL no campo `value` abaixo. Use esta opção se você tiver um ponto de extremidade como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do ponto de extremidade de API ao qual o Experience Platform deve se conectar e recuperar os valores da lista suspensa. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. Para servidores suspensos dinâmicos, use `GET`. |
| `httpTemplate.headers` | Objeto | *Optiona.l* Inclua todos os cabeçalhos necessários para se conectar ao servidor de lista suspensa dinâmica. |
| `responseFields.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `responseFields.value` | String | *Obrigatório.* Esta cadeia de caracteres é o modelo de transformação com caractere de escape que transforma a resposta recebida de sua API nos valores que serão exibidos na interface do usuário do Experience Platform. <br> <ul><li> Para obter informações sobre como gravar o modelo, leia a [seção Uso de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte o [padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!ENDTABS]

## Manipulação de erros de API {#error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como criar um novo servidor de destino por meio do ponto de extremidade da API `/authoring/destination-servers` do Destination SDK.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Recuperar uma configuração do servidor de destino](retrieve-destination-server.md)
* [Atualizar uma configuração do servidor de destino](update-destination-server.md)
* [Excluir uma configuração do servidor de destino](delete-destination-server.md)

Para entender onde esse endpoint se encaixa no processo de criação de destino, consulte os seguintes artigos:

* [Usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
