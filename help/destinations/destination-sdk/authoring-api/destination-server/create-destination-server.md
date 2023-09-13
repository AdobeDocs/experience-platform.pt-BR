---
description: Esta página exemplifica a chamada à API usada para criar um servidor de destino por meio do Adobe Experience Platform Destination SDK.
title: Criar uma configuração do servidor de destino
source-git-commit: 03ec0e919304c9d46ef88d606eed9e12d1824856
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 9%

---


# Criar uma configuração do servidor de destino

A criação de um servidor de destino é a primeira etapa na criação de seu próprio destino com o Destination SDK. O servidor de destino inclui opções de configuração para o [server](../../functionality/destination-server/server-specs.md) e [modelos](../../functionality/destination-server/templating-specs.md) especificações, a variável [formato da mensagem](../../functionality/destination-server/message-format.md), e o [formatação de arquivo](../../functionality/destination-server/file-formatting.md) (para destinos baseados em arquivo).

Esta página exemplifica a solicitação de API e a carga que você pode usar para criar seu próprio servidor de destino usando o `/authoring/destination-servers` Endpoint da API.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio desse endpoint, leia os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Especificações de modelos para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato de mensagem](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuração da formatação de arquivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do servidor de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Criar uma configuração do servidor de destino {#create}

Você pode criar uma nova configuração do servidor de destino fazendo uma `POST` solicitação à `/authoring/destination-servers` terminal.

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

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

>[!TAB Tempo real (transmissão)]

**Criar um servidor de destino (transmissão) em tempo real**

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
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para destinos em tempo real (transmissão). |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Uso `PEBBLE_V1` se o Adobe precisar transformar o URL no `value` abaixo. Use esta opção se você tiver um terminal como `https://api.moviestar.com/data/{{customerData.region}}/items`, em que o `region` pode diferir entre os clientes. Nesse caso, também é necessário configurar `region` as a [campo de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) no [configuração de destino]../destination-configuration/create-destination-configuration.md. </li><li> Uso `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do endpoint da API ao qual o Experience Platform deve se conectar. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. As opções são `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | String | *Obrigatório.* Essa string é a versão com escape de caracteres que transforma os dados de clientes da Platform no formato esperado pelo seu serviço. <br> <ul><li> Para obter informações sobre como gravar o template, leia o [Uso da seção de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte o [RFC JSON padrão, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de uma transformação simples, consulte [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes) transformação. </li></ul> |
| `httpTemplate.contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Este valor é mais provável `application/json`. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Amazon S3]

**Criar um servidor de destino do Amazon S3**

É necessário criar um [!DNL Amazon S3] servidor de destino semelhante ao mostrado abaixo ao configurar um servidor baseado em [!DNL Amazon S3] destino.

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
| `fileBasedS3Destination.bucket.value` | String | O nome do [!DNL Amazon S3] bucket a ser usado por esse destino. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB SFTP]

**Criar um [!DNL SFTP] servidor de destino**

É necessário criar um [!DNL SFTP] servidor de destino semelhante ao mostrado abaixo ao configurar um servidor baseado em [!DNL SFTP] destino.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL SFTP] destinos, defina como `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | String | O diretório raiz do armazenamento de destino. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | String | O nome do host do armazenamento de destino. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser usada criptografia de arquivo. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | N/D | Consulte [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento Azure Data Lake]

**Criar um [!DNL Azure Data Lake Storage] servidor de destino**

É necessário criar um [!DNL Azure Data Lake Storage] servidor de destino semelhante ao mostrado abaixo ao configurar um servidor baseado em [!DNL Azure Data Lake Storage] destino.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento Azure Blob]

**Criar um [!DNL Azure Blob Storage] servidor de destino**

É necessário criar um [!DNL Azure Blob Storage] servidor de destino semelhante ao mostrado abaixo ao configurar um servidor baseado em [!DNL Azure Blob Storage] destino.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Azure Blob Storage] destinos, defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do [!DNL Azure Blob Storage] contêiner a ser usado por este destino. |
| `fileConfigurations` | N/D | Consulte [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Zona de aterrissagem de dados (DLZ)]

**Criar um [!DNL Data Landing Zone (DLZ)] servidor de destino**

É necessário criar um [!DNL Data Landing Zone (DLZ)] servidor de destino semelhante ao mostrado abaixo ao configurar um servidor baseado em [!DNL Data Landing Zone (DLZ)] destino.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Data Landing Zone] destinos, defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!TAB Armazenamento em nuvem Google]

**Criar um [!DNL Google Cloud Storage] servidor de destino**

É necessário criar um [!DNL Google Cloud Storage] servidor de destino semelhante ao mostrado abaixo ao configurar um servidor baseado em [!DNL Google Cloud Storage] destino.

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
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Google Cloud Storage] destinos, defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do [!DNL Google Cloud Storage] bucket a ser usado por esse destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | N/D | Consulte [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) para obter informações detalhadas sobre como definir essas configurações. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++

>[!ENDTABS]

### Criar servidores de destino de esquema dinâmico {#dynamic-schema-servers}

Os esquemas dinâmicos permitem recuperar dinamicamente os atributos de destino compatíveis e gerar esquemas com base em sua própria API. Você precisa configurar um servidor de destino para esquemas dinâmicos antes de poder configurar o esquema.

Consulte na guia abaixo um exemplo de servidor de destino para destinos que usam [esquemas dinâmicos](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

A carga de exemplo abaixo inclui todos os parâmetros necessários para um servidor de esquema dinâmico.

>[!BEGINTABS]

>[!TAB Servidor de esquema dinâmico]

**Criar um servidor de esquema dinâmico**

É necessário criar um servidor de esquema dinâmico semelhante ao mostrado abaixo ao configurar um destino que recupera o esquema de perfil de seu próprio ponto de acesso de API. Ao contrário de um esquema estático, um esquema dinâmico não usa um `profileFields` matriz. Em vez disso, os esquemas dinâmicos usam um servidor de esquema dinâmico que se conecta à sua própria API de onde recupera a configuração do esquema.

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
| `name` | String | *Obrigatório.* Representa um nome amigável do servidor de esquema dinâmico, visível somente para Adobe. |
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para servidores de esquema dinâmicos. |
| `urlBasedDestination.url.templatingStrategy` | String | *Obrigatório.* <ul><li>Uso `PEBBLE_V1` se o Adobe precisar transformar o URL no `value` abaixo. Use essa opção se você tiver um terminal como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Uso `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | String | *Obrigatório.* Preencha o endereço do endpoint da API ao qual o Experience Platform deve se conectar e recupere os campos de esquema para preencher como campos de destino na etapa de mapeamento do fluxo de trabalho de ativação. |
| `httpTemplate.httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. Para servidores de esquema dinâmicos, use `GET`. |
| `responseFields.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `responseFields.value` | String | *Obrigatório.* Essa string é o modelo de transformação com escape de caracteres que transforma a resposta recebida da API do parceiro no esquema do parceiro que será exibido na interface do usuário da Platform. <br> <ul><li> Para obter informações sobre como gravar o template, leia o [Uso da seção de modelos](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obter mais informações sobre o escape de caracteres, consulte o [RFC JSON padrão, seção sete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para obter um exemplo de uma transformação simples, consulte [Atributos do perfil](../../functionality/destination-server/message-format.md#attributes) transformação. </li></ul> |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração do servidor de destino recém-criado.

+++


>[!ENDTABS]

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, você sabe como criar um novo servidor de destino por meio do Destination SDK `/authoring/destination-servers` Endpoint da API.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Recuperar uma configuração do servidor de destino](retrieve-destination-server.md)
* [Atualizar uma configuração do servidor de destino](update-destination-server.md)
* [Excluir uma configuração do servidor de destino](delete-destination-server.md)

Para entender onde esse endpoint se encaixa no processo de criação de destino, consulte os seguintes artigos:

* [Usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)