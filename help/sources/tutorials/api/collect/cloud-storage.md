---
keywords: Experience Platform;página inicial;tópicos populares;dados de armazenamento na nuvem
solution: Experience Platform
title: Criar um fluxo de dados para fontes de armazenamento na nuvem usando a API do serviço de fluxo
type: Tutorial
description: Este tutorial aborda as etapas para recuperar dados de um armazenamento em nuvem de terceiros e trazê-los para a Experience Platform usando conectores de origem e APIs.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 02a22362b9ecbfc5fd7fcf17dc167309a0ea45d5
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 2%

---

# Criar um fluxo de dados para fontes de armazenamento na nuvem usando a API [!DNL Flow Service]

Este tutorial aborda as etapas para recuperar dados de uma fonte de armazenamento na nuvem e trazê-los para a Experience Platform usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Para criar um fluxo de dados, você já deve ter uma ID de conexão base válida com uma fonte de armazenamento na nuvem. Se você não tiver essa ID, consulte a [visão geral das fontes](../../../home.md#cloud-storage) para obter uma lista de fontes de armazenamento na nuvem com as quais você pode criar uma conexão base.

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Guia do desenvolvedor do Registro de Esquema](../../../../xdm/api/getting-started.md): inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro de Esquema. Isso inclui o `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Aceitar e seus valores possíveis).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo é o sistema de registro para localização e linhagem de dados no Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): a API de assimilação em lote permite assimilar dados na Experience Platform como arquivos em lote.
- [Sandboxes](../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../landing/api-guide.md).

## Criar uma conexão de origem {#source}

Você pode criar uma conexão de origem fazendo uma solicitação POST para o ponto de extremidade `sourceConnections` da API [!DNL Flow Service] enquanto fornece a ID de conexão básica, o caminho para o arquivo de origem que você deseja assimilar e a ID de especificação de conexão correspondente da sua origem.

Ao criar uma conexão de origem, você também deve definir um valor de enumeração para o atributo de formato de dados.

Use os seguintes valores de enumeração para fontes baseadas em arquivo:

| Formato dos dados | Valor de enumeração |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todas as fontes baseadas em tabela, defina o valor como `tabular`.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file",
          "cdcEnabled": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `baseConnectionId` | A ID de conexão básica da sua fonte de armazenamento na nuvem. |
| `data.format` | O formato dos dados que você deseja trazer para o Experience Platform. Os valores com suporte são: `delimited`, `JSON` e `parquet`. |
| `data.properties` | (Opcional) Um conjunto de propriedades que você pode aplicar aos seus dados ao criar uma conexão de origem. |
| `data.properties.columnDelimiter` | (Opcional) Um delimitador de coluna de caractere único que você pode especificar ao coletar arquivos simples. Qualquer valor de caractere único é um delimitador de coluna permitido. Se não for fornecido, uma vírgula (`,`) será usada como valor padrão. **Observação**: a propriedade `columnDelimiter` só pode ser usada ao assimilar arquivos delimitados. |
| `data.properties.encoding` | (Opcional) Uma propriedade que define o tipo de codificação a ser usado ao assimilar seus dados na Experience Platform. Os tipos de codificação com suporte são: `UTF-8` e `ISO-8859-1`. **Observação**: o parâmetro `encoding` só está disponível ao assimilar arquivos CSV delimitados. Outros tipos de arquivos serão assimilados com a codificação padrão, `UTF-8`. |
| `data.properties.compressionType` | (Opcional) Uma propriedade que define o tipo de arquivo compactado para assimilação. Os tipos de arquivos compactados com suporte são: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` e `tar`. **Observação**: a propriedade `compressionType` só pode ser usada ao assimilar arquivos delimitados ou JSON. |
| `params.path` | O caminho do arquivo de origem que você está acessando. Esse parâmetro aponta para um arquivo individual ou uma pasta inteira.  **Observação**: você pode usar um asterisco no lugar do nome do arquivo para especificar a assimilação de uma pasta inteira. Por exemplo: `/acme/summerCampaign/*.csv` assimilará toda a pasta `/acme/summerCampaign/`. |
| `params.type` | O tipo do arquivo de dados de origem que você está assimilando. Use o tipo `file` para assimilar um arquivo individual e use o tipo `folder` para assimilar uma pasta inteira. |
| `params.cdcEnabled` | Um valor booleano que indica se a captura do histórico de alterações está ativada. Quando usada com esquemas baseados em modelo, a captura de dados de alteração depende da `_change_request_type` coluna de controle (`u` — substituir, `d` — excluir), que é avaliada durante a assimilação, mas não armazenada no esquema de destino. Esta propriedade tem suporte nas seguintes fontes de armazenamento na nuvem: <ul><li>[!DNL Azure Blob]</li><li>[!DNL Data Landing Zone]</li><li>[!DNL Google Cloud Storage]</li><li>[!DNL SFTP]</li></ul>Para obter uma visão geral desse recurso, consulte a [visão geral do Data Mirror](../../../../xdm/data-mirror/overview.md). Para obter detalhes sobre implementação, leia o guia sobre como usar a [captura de dados de alteração nas fontes](../change-data-capture.md) e a [referência técnica de esquemas baseados em modelo](../../../../xdm/schema/model-based.md). |
| `connectionSpec.id` | A ID de especificação de conexão associada à sua fonte de armazenamento em nuvem específica. Consulte o [apêndice](#appendix) para obter uma lista de IDs de especificação de conexão. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Usar expressões regulares para selecionar um conjunto específico de arquivos para assimilação {#regex}

Você pode usar expressões regulares para assimilar um conjunto específico de arquivos da origem para o Experience Platform ao criar uma conexão de origem.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

No exemplo abaixo, a expressão regular é usada no caminho do arquivo para especificar a assimilação de todos os arquivos CSV que têm `premium` no nome.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### Configurar uma conexão de origem para assimilar dados recursivamente

Ao criar uma conexão de origem, você pode usar o parâmetro `recursive` para assimilar dados de pastas profundamente aninhadas.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

No exemplo abaixo, o parâmetro `recursive: true` informa [!DNL Flow Service] para ler todas as subpastas recursivamente durante o processo de assimilação.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados no Experience Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados do Experience Platform no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](../../../../xdm/api/schemas.md).

## Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornecendo a ID do esquema de destino na carga.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../../catalog/api/create-dataset.md).

## Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação da conexão fixa associada ao Data Lake. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o Data Lake. Usando esses identificadores, você pode criar uma conexão de destino usando a API [!DNL Flow Service] para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```http
POST /targetConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.schema.id` | O `$id` do esquema XDM de destino. |
| `data.schema.version` | A versão do esquema. Este valor deve ser definido como `application/vnd.adobe.xed-full+json;version=1`, que retorna a versão secundária mais recente do esquema. |
| `params.dataSetId` | A ID do conjunto de dados de destino gerado na etapa anterior. **Observação**: você deve fornecer uma ID de conjunto de dados válida ao criar uma conexão de destino. Uma ID de conjunto de dados inválida resultará em um erro. |
| `connectionSpec.id` | A ID de especificação da conexão usada para se conectar ao data lake. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão de destino. Essa ID é necessária nas etapas posteriores.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere.

Para criar um conjunto de mapeamento, faça uma solicitação POST para o ponto de extremidade `mappingSets` da [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/) enquanto fornece o esquema XDM de destino `$id` e os detalhes dos conjuntos de mapeamento que deseja criar.

>[!TIP]
>
>Você pode mapear tipos de dados complexos, como matrizes em arquivos JSON, usando um conector de origem de armazenamento em nuvem.

**Formato da API**

```http
POST /conversion/mappingSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `xdmSchema` | A ID do esquema XDM do público-alvo. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificações de fluxo de dados {#specs}

Um fluxo de dados é responsável por coletar dados de fontes e trazê-los para o Experience Platform. Para criar um fluxo de dados, primeiro obtenha as especificações do fluxo de dados responsáveis pela coleta dos dados de armazenamento na nuvem.

**Formato da API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>A carga de resposta JSON abaixo está oculta por brevidade. Selecione &quot;carga&quot; para ver a carga de resposta.

+++ Exibir conteúdo

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação do fluxo de dados responsáveis por trazer os dados de sua origem para a Experience Platform. A resposta inclui a especificação de fluxo exclusiva `id` necessária para criar um novo fluxo de dados.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
  "permissionsInfo": {
    "view": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "optionSpec": {
    "name": "OptionSpec",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "errorDiagnosticsEnabled": {
          "title": "Error diagnostics.",
          "description": "Flag to enable detailed and sample error diagnostics summary.",
          "type": "boolean",
          "default": false
        },
        "partialIngestionPercent": {
          "title": "Partial ingestion threshold.",
          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
          "type": "number",
          "exclusiveMinimum": 0
        }
      }
    }
  },
  "scheduleSpec": {
    "name": "PeriodicSchedule",
    "type": "Periodic",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "startTime": {
          "description": "epoch time",
          "type": "integer"
        },
        "frequency": {
          "type": "string",
          "enum": [
            "once",
            "minute",
            "hour",
            "day",
            "week"
          ]
        },
        "interval": {
          "type": "integer"
        },
        "backfill": {
          "type": "boolean",
          "default": true
        }
      },
      "required": [
        "startTime",
        "frequency"
      ],
      "if": {
        "properties": {
          "frequency": {
            "const": "once"
          }
        }
      },
      "then": {
        "allOf": [
          {
            "not": {
              "required": [
                "interval"
              ]
            }
          },
          {
            "not": {
              "required": [
                "backfill"
              ]
            }
          }
        ]
      },
      "else": {
        "required": [
          "interval"
        ],
        "if": {
          "properties": {
            "frequency": {
              "const": "minute"
            }
          }
        },
        "then": {
          "properties": {
            "interval": {
              "minimum": 15
            }
          }
        },
        "else": {
          "properties": {
            "interval": {
              "minimum": 1
            }
          }
        }
      }
    }
  },
  "transformationSpec": [
    {
      "name": "Mapping",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for different mapping from source to target",
        "properties": {
          "mappingId": {
            "type": "string"
          },
          "mappingVersion": {
            "type": "string"
          }
        }
      }
    }
  ],
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## Criar um fluxo de dados

A última etapa para coletar dados de armazenamento na nuvem é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

- [ID de conexão do Source](#source)
- [ID da conexão de destino](#target)
- [ID de mapeamento](#mapping)
- [ID da especificação do fluxo de dados](#specs)

Um fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga.

>[!NOTE]
>
>Para assimilação em lote, cada fluxo de dados subsequente seleciona arquivos a serem assimilados de sua origem com base no carimbo de data/hora **última modificação**. Isso significa que os fluxos de dados em lote selecionam arquivos da origem que são novos ou que foram modificados desde a última execução do fluxo de dados.

Para agendar uma assimilação, primeiro defina o valor da hora inicial como a época em segundos. Em seguida, defina o valor de frequência para uma das cinco opções: `once`, `minute`, `hour`, `day` ou `week`. O valor do intervalo designa o período entre duas assimilações consecutivas e a criação de uma assimilação única não requer que um intervalo seja definido. Para todas as outras frequências, o valor do intervalo deve ser definido como igual ou maior que `15`.

>[!IMPORTANT]
>
>É altamente recomendável agendar seu fluxo de dados para assimilação única ao usar o [conector FTP](../../../connectors/cloud-storage/ftp.md).

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud Storage flow to Experience Platform",
        "description": "Cloud Storage flow to Experience Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | A [ID de especificação de fluxo](#specs) recuperou na etapa anterior. |
| `sourceConnectionIds` | A [ID da conexão de origem](#source) recuperou em uma etapa anterior. |
| `targetConnectionIds` | A [ID da conexão de destino](#target-connection) recuperou em uma etapa anterior. |
| `transformations.params.mappingId` | A [ID de mapeamento](#mapping) recuperou em uma etapa anterior. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções de fluxo consecutivas. O valor do intervalo deve ser um inteiro diferente de zero. O valor mínimo de intervalo aceito para cada frequência é o seguinte:<ul><li>**Uma vez**: n/d</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Dia**: 1</li><li>**Semana**: 1</li></ul> |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial sobre [monitoramento de fluxos de dados na API](../monitor.md)

## Próximas etapas

Seguindo este tutorial, você criou um conector de origem para coletar dados do armazenamento na nuvem de forma programada. Os dados de entrada agora podem ser usados por serviços downstream do Experience Platform, como [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
- [Visão geral do Espaço de trabalho de ciência de dados](../../../../data-science-workspace/home.md)

## Apêndice {#appendix}

A seção a seguir lista os diferentes conectores de origem de armazenamento na nuvem e suas especificações de conexão.

### Especificação de conexão

| Nome do conector | Especificação da conexão |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Hubs de Eventos) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
