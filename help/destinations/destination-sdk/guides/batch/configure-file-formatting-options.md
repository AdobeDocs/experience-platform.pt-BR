---
description: Configurar opções de formatação de arquivo para destinos com base em arquivo
title: Saiba como usar o Destination SDK para configurar as opções de formatação de arquivo para destinos com base em arquivo.
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 1%

---

# Configurar opções de formatação de arquivo para destinos com base em arquivo

## Visão geral {#overview}

O Destination SDK permite ajustar extensivamente as opções de formatação e compactação dos arquivos exportados para corresponder a quaisquer requisitos downstream no local de armazenamento.

Esta página descreve como usar o Destination SDK para configurar as opções de formatação de arquivo para destinos com base em arquivo.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas descritas abaixo, leia o [Introdução ao Destination SDK](../../getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O e outros pré-requisitos necessários para funcionar com as APIs do Destination SDK.

O Adobe também recomenda que você leia e familiarize-se com a seguinte documentação antes de continuar:

* Cada opção de formatação de arquivo disponível é documentada em comprimento no [configuração de formatação de arquivo](../../server-and-file-configuration.md#file-configuration) seção.
* Complete as etapas para [configurar um destino baseado em arquivo](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) usando o Destination SDK.

## Criar um servidor e uma configuração de arquivo {#create-server-file-configuration}

Comece usando o `/destination-server` endpoint para determinar quais opções de configuração de formatação de arquivo você deseja configurar para os arquivos exportados.

Veja abaixo um exemplo de uma configuração de servidor de destino para um [!DNL Amazon S3] destino, com várias opções de formatação de arquivo selecionadas.

>[!TIP]
>
>Como lembrete, todas as opções disponíveis de formatação de arquivo são documentadas na variável [configuração de formatação de arquivo](../../server-and-file-configuration.md#file-configuration) seção.

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
>**Verificar a interface do usuário do Experience Platform**. À medida que você configura as opções de formatação de arquivo com as configurações demonstradas nas seções abaixo, deve verificar a interface do usuário do Experience Platform como essas opções são renderizadas.

Depois de adicionar as opções desejadas de formatação de arquivo ao servidor de destino e à configuração de formatação de arquivo na etapa anterior, agora é possível usar o `/destinations` Ponto de extremidade da API para adicionar os campos desejados como campos de dados do cliente à configuração de destino.

>[!IMPORTANT]
>
>Essa etapa é opcional e determina apenas qual das opções de formatação de arquivo deve ser exibida para os usuários na interface do usuário do Experience Platform. Se você não configurar opções de formatação de arquivo como campos de dados do cliente, as exportações de arquivo continuarão com os valores padrão configurados na [configuração de servidor e arquivo](#create-server-file-configuration).

Nesta etapa, é possível agrupar as opções exibidas em qualquer ordem desejada, criar agrupamentos personalizados, campos suspensos e agrupamentos condicionais com base nos tipos de arquivos selecionados. Todas essas configurações são mostradas na gravação e nas seções a seguir.

![Gravação de tela mostrando várias opções de formatação de arquivo para arquivos em lote.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-options.gif)

### Ordenar as opções de formatação de arquivo {#ordering}

A ordem em que você adiciona as opções de formatação de arquivo como campos de dados do cliente na configuração de destino é refletida na interface do usuário. Por exemplo, a configuração abaixo é refletida adequadamente na interface do usuário, com as opções exibidas na ordem **[!UICONTROL Delimitador]**, **[!UICONTROL Caractere de citação]**, **[!UICONTROL Caractere de escape]**, **[!UICONTROL Valor vazio]**, **[!UICONTROL Valor nulo]**.

![Imagem que mostra a ordem das opções de formatação de arquivo na interface do usuário do Experience Platform.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-order.png)

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

### Agrupar as opções de formatação de arquivo {#grouping}

É possível agrupar várias opções de formatação de arquivos em uma seção. Ao configurar a conexão com o destino na interface do usuário, o usuário pode ver e se beneficiar de um agrupamento visual de campos semelhantes.

Para fazer isso, use `"type": "object"` para criar o grupo e coletar as opções de formatação de arquivo desejadas em uma `properties` como mostrado no exemplo abaixo, onde o agrupamento **[!UICONTROL Opções de CSV]** é realçada.

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

[...]
```

![Imagem que mostra o agrupamento de opções CSV na interface do usuário.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-grouping.png)

### Criar seletores suspensos para as opções de formatação de arquivo {#dropdown-selectors}

Para situações em que você deseja permitir que os usuários selecionem entre várias opções, por exemplo, qual caractere deve ser usado para delimitar os campos nos arquivos CSV, é possível adicionar campos suspensos à interface do usuário.

Para fazer isso, use o `namedEnum` conforme mostrado abaixo e configure um `default` para as opções que o usuário pode selecionar.

```json
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
```

![Gravação de tela mostrando um exemplo de seletores suspensos criados com a configuração mostrada acima.](/help/destinations/destination-sdk/assets/guides/batch/dropdown-options-file-formatting.gif)

### Criar opções de formatação de arquivo condicional {#conditional-options}

É possível criar opções condicionais de formatação de arquivo, que são exibidas no fluxo de trabalho de ativação somente quando o usuário seleciona um determinado tipo de arquivo para exportação. Por exemplo, a configuração abaixo cria um agrupamento condicional para opções de arquivo CSV. As opções do arquivo CSV são exibidas somente quando o usuário seleciona CSV como o tipo de arquivo desejado para exportação.

Para definir um campo como condicional, use a variável `conditional` como mostrado abaixo:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

Em um contexto mais amplo, é possível ver a variável `conditional` campo que está sendo usado na configuração de destino abaixo, junto com o `fileType` e a `csvOptions` objeto no qual está definido.

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

Abaixo, você pode ver a tela da interface do usuário resultante, com base na configuração acima. Quando o usuário seleciona o CSV do tipo de arquivo, opções adicionais de formatação de arquivo referentes ao tipo de arquivo CSV são exibidas na interface do usuário.

![Gravação de tela mostrando a opção de formatação condicional de arquivo para arquivos CSV.](/help/destinations/destination-sdk/assets/guides/batch/conditional-file-formatting.gif)

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
  "releaseNotes": "Test destination",
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

Uma determinada combinação de opções de formatação de arquivo pode levar a resultados de exportação de arquivo indesejados.
O Adobe recomenda não selecionar a seguinte combinação de opções CSV:

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Para exemplificar a limitação, considere a exportação de um arquivo com os valores abaixo:

| firstname | lastname | country | estado |
|---------|----------|---------|--------|
| Michael | Rosa | EUA | NY |
| James | Smith |  | nulo |

{style=&quot;table-layout:auto&quot;}

Isso resultaria em uma saída, como mostrado abaixo. Observe como o valor nulo da tabela é exportado incorretamente como uma cotação escaped.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Próximas etapas {#next-steps}

Ao ler este artigo, agora você sabe como configurar opções personalizadas de formatação de arquivos para seus arquivos exportados usando o Destination SDK. Em seguida, sua equipe pode usar o [fluxo de trabalho de ativação para destinos com base em arquivo](../../../ui/activate-batch-profile-destinations.md) para exportar dados para o destino.
