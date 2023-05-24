---
description: Configurar opções de formatação de arquivo para destinos baseados em arquivo
title: Saiba como usar o Destination SDK para configurar opções de formatação de arquivo para destinos baseados em arquivo.
exl-id: e61c7989-1123-4b3b-9781-a6097cd0e2b4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# Configurar opções de formatação de arquivo para destinos baseados em arquivo

## Visão geral {#overview}

O Destination SDK permite que você ajuste detalhadamente as opções de formatação e compactação dos arquivos exportados para atender a quaisquer requisitos downstream no local de armazenamento.

Esta página descreve como usar o Destination SDK para configurar opções de formatação de arquivo para destinos baseados em arquivo.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas descritas abaixo, leia o [introdução ao Destination SDK](../../getting-started.md) página para obter informações sobre como obter as credenciais de autenticação de Adobe I/O e outros pré-requisitos necessários para trabalhar com as APIs de Destination SDK.

A Adobe também recomenda que você leia e se familiarize com a seguinte documentação antes de continuar:

* Cada opção de formatação de arquivo disponível está documentada detalhadamente na [configuração da formatação de arquivo](../../functionality/destination-server/file-formatting.md) seção.
* Conclua as etapas para [configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md) usando o Destination SDK.

## Criar uma configuração de servidor e arquivo {#create-server-file-configuration}

Comece usando o `/destination-server` endpoint para determinar quais opções de configuração de formatação de arquivo você deseja definir para os arquivos exportados.

Veja abaixo um exemplo de uma configuração de servidor de destino para um [!DNL Amazon S3] destino, com várias opções de formatação de arquivo selecionadas.

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
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
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
}
}'
```

## Adicionar as opções de formatação de arquivo à configuração de destino {#create-destination-configuration}

>[!TIP]
>
>**Verifique a interface do usuário do Experience Platform**. Ao configurar as opções de formatação de arquivo com as configurações demonstradas nas seções abaixo, você deve verificar a interface do usuário do Experience Platform para saber como essas opções são renderizadas.

Depois de adicionar as opções de formatação de arquivo desejadas ao servidor de destino e a configuração de formatação de arquivo na etapa anterior, você pode usar o `/destinations` Endpoint da API para adicionar os campos desejados como campos de dados do cliente à configuração de destino.

>[!IMPORTANT]
>
>Essa etapa é opcional e determina apenas quais das opções de formatação de arquivo devem ser exibidas para os usuários na interface do usuário do Experience Platform. Se você não definir opções de formatação de arquivo como campos de dados do cliente, as exportações de arquivo continuarão com os valores padrão configurados no [configuração do servidor e do arquivo](#create-server-file-configuration).

Nesta etapa, você pode agrupar as opções exibidas em qualquer ordem, criar agrupamentos personalizados, campos suspensos e agrupamentos condicionais com base nos tipos de arquivo selecionados. Todas essas configurações são mostradas na gravação e nas seções mais abaixo.

![Gravação de tela mostrando várias opções de formatação de arquivo para arquivos de lote.](../../assets/guides/batch/file-formatting-options.gif)

### Ordenar as opções de formatação de arquivo {#ordering}

A ordem em que você adiciona as opções de formatação do arquivo como campos de dados do cliente na configuração de destino é refletida na interface. Por exemplo, a configuração abaixo é refletida de acordo na interface do usuário, com as opções exibidas na ordem **[!UICONTROL Delimitador]**, **[!UICONTROL Caractere de citação]**, **[!UICONTROL Caractere de escape]**, **[!UICONTROL Valor vazio]**, **[!UICONTROL Valor nulo]**.

![Imagem mostrando a ordem das opções de formatação de arquivo na interface do usuário do Experience Platform.](../../assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### Agrupar as opções de formatação do arquivo {#grouping}

Você pode agrupar várias opções de formatação de arquivo em uma seção. Ao configurar a conexão com o destino na interface do usuário do, o usuário pode ver e se beneficiar de um agrupamento visual de campos semelhantes.

Para fazer isso, use `"type": "object"` para criar o grupo e coletar as opções de formatação de arquivo desejadas em um `properties` como mostrado no exemplo abaixo, onde o agrupamento **[!UICONTROL Opções de CSV]** é realçado.

```json {line-numbers="true" start-number="100" highlight="106-128"}
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Imagem mostrando o agrupamento de opções de CSV na interface do usuário.](../../assets/guides/batch/file-formatting-grouping.png)

### Criar seletores suspensos para as opções de formatação de arquivo {#dropdown-selectors}

Para situações em que você deseja permitir que os usuários selecionem entre várias opções, por exemplo, qual caractere deve ser usado para delimitar os campos em arquivos CSV, é possível adicionar campos suspensos à interface do usuário.

Para fazer isso, use o `namedEnum` conforme mostrado abaixo e configure um `default` para as opções que o usuário pode selecionar.

```json {line-numbers="true" start-number="100" highlight="114-124"}
[...]
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Gravação de tela mostrando um exemplo de seletores suspensos criados com a configuração mostrada acima.](../../assets/guides/batch/dropdown-options-file-formatting.gif)

### Criar opções condicionais de formatação de arquivo {#conditional-options}

É possível criar opções condicionais de formatação de arquivo, que são exibidas no fluxo de trabalho de ativação somente quando o usuário seleciona um determinado tipo de arquivo para exportação. Por exemplo, a configuração abaixo cria um agrupamento condicional para opções de arquivo CSV. As opções do arquivo CSV são exibidas somente quando o usuário seleciona CSV como o tipo de arquivo desejado para exportação.

Para definir um campo como condicional, use o `conditional` conforme mostrado abaixo:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

Em um contexto mais amplo, você pode ver `conditional` que está sendo usado na configuração de destino abaixo, junto com o campo `fileType` e a variável `csvOptions` objeto no qual é definido.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

Abaixo, você pode ver a tela resultante da interface do usuário, com base na configuração acima. Quando o usuário seleciona o tipo de arquivo CSV, opções adicionais de formatação de arquivo referentes ao tipo de arquivo CSV são exibidas na interface.

![Gravação de tela mostrando a opção de formatação condicional de arquivo para arquivos CSV.](../../assets/guides/batch/conditional-file-formatting.gif)

### Solicitação de API completa que inclui todas as opções mostradas acima

A solicitação de API abaixo combina em uma configuração todas as opções descritas nas seções acima.

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "name": "My S3 Destination",
  "description": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
  },
  "schemaConfig": {
    "profileRequired": true,
    "segmentRequired": true,
    "identityRequired": true
  },
  "batchConfig": {
    "allowMandatoryFieldSelection": true,
    "allowDedupeKeyFieldSelection": true,
    "defaultExportMode": "DAILY_FULL_EXPORT",
    "allowedExportMode": [
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
    ],
    "allowedScheduleFrequency": [
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
    ],
    "defaultFrequency": "DAILY",
    "defaultStartTime": "00:00",
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
  },
  "destinationDelivery": [
    {
      "deliveryMatchers": [
        {
          "type": "SOURCE",
          "value": [
            "batch"
          ]
        }
      ],
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

Uma resposta bem-sucedida retorna a configuração de destino, incluindo o identificador exclusivo (`instanceId`) da configuração.

## Limitações conhecidas {#known-limitations}

Uma determinada combinação de opções de formatação de arquivo pode gerar resultados indesejados na exportação de arquivos.
O Adobe recomenda não selecionar a seguinte combinação de opções de CSV:

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Para exemplificar a limitação, considere a exportação de um arquivo com os valores abaixo:

| firstname | sobrenome | país | estado |
|---------|----------|---------|--------|
| Michael | Rosa | EUA | NY |
| James | Smith |  | nulo |

{style="table-layout:auto"}

Isso resultaria em uma saída como mostrado abaixo. Observe como o valor nulo da tabela é exportado incorretamente como uma cotação com escape.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Próximas etapas {#next-steps}

Após a leitura deste artigo, agora você sabe como configurar opções de formatação de arquivo personalizadas para seus arquivos exportados usando o Destination SDK. Em seguida, sua equipe pode usar o [fluxo de trabalho de ativação para destinos baseados em arquivo](../../../ui/activate-batch-profile-destinations.md) para exportar dados para o destino.
